---
title: Nuget.org 'e yayınlanan tüm paketler için sorgu
description: NuGet API 'sini kullanarak, nuget.org ' de yayınlanan tüm paketleri sorgulayabilir ve zaman içinde güncel kalın.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 7e611b568538e0acfcbad2e5d986a0f9382ac8fd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774117"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="49a2a-103">Nuget.org 'e yayınlanan tüm paketler için sorgu</span><span class="sxs-lookup"><span data-stu-id="49a2a-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="49a2a-104">Eski OData v2 API 'sindeki yaygın bir sorgu deseninin, paket yayımlandığında tarafından sıralanan, nuget.org 'e yayınlanan tüm paketler numaralandırıldığı için.</span><span class="sxs-lookup"><span data-stu-id="49a2a-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="49a2a-105">Nuget.org karşı bu tür bir sorgu gerektiren senaryolar farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="49a2a-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="49a2a-106">Nuget.org tamamen çoğaltılıyor</span><span class="sxs-lookup"><span data-stu-id="49a2a-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="49a2a-107">Paketlerin yeni sürümleri ne zaman yayımlanmışsa algılanıyor</span><span class="sxs-lookup"><span data-stu-id="49a2a-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="49a2a-108">Paketinize bağlı paketleri bulma</span><span class="sxs-lookup"><span data-stu-id="49a2a-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="49a2a-109">Bunu yapmanın eski yolu, genellikle OData paketi varlığının, `skip` ve `top` (sayfa boyutu) parametreleri kullanılarak oluşan büyük sonuç kümesinde bir zaman damgası ve sayfalama yoluyla sıralanarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="49a2a-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="49a2a-110">Ne yazık ki bu yaklaşımın bazı dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="49a2a-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="49a2a-111">Eksik paket olma olasılığı, çünkü sorgular sıklıkla değişen sırada olan veriler üzerinde yapılıyor</span><span class="sxs-lookup"><span data-stu-id="49a2a-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="49a2a-112">Sorgular en iyi duruma getirilmediğinden (en iyileştirilmiş sorgular resmi NuGet istemcisi için bir ana hat senaryosu destekleenler) yavaş sorgu yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="49a2a-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="49a2a-113">Kullanım dışı bırakılmış ve belgelenmemiş API 'nin kullanımı, gelecekte bu sorguların desteklenmesi garanti edilmez</span><span class="sxs-lookup"><span data-stu-id="49a2a-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="49a2a-114">Geçmişi transpired doğru sırada yeniden oynalamama</span><span class="sxs-lookup"><span data-stu-id="49a2a-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="49a2a-115">Bu nedenle, aşağıdaki kılavuzun, daha güvenilir ve gelecekte prova bir şekilde açıklanan senaryolara yönelik olarak ele alınabilir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="49a2a-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="49a2a-116">Overview</span></span>

<span data-ttu-id="49a2a-117">Bu kılavuzun merkezinde **Katalog** ADLı [NuGet API](../../api/overview.md) 'sindeki kaynak bulunur.</span><span class="sxs-lookup"><span data-stu-id="49a2a-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="49a2a-118">Katalog, çağıranın nuget.org ' de eklenen, değiştirilen ve silinen paketlerin tam geçmişini görmesini sağlayan bir yalnızca Append API 'sidir. Nuget.org ' de yayınlanan paketlerin tümünün veya hatta bir alt kümesiyle ilgileniyorsanız, katalog, zaman içinde mevcut olan paketler kümesiyle güncel kalabilmek için harika bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="49a2a-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="49a2a-119">Bu kılavuzun üst düzey bir adım adım olması amaçlanmıştır ancak kataloğun ayrıntılı ayrıntılarını almak istiyorsanız, [API başvuru belgesine](../../api/catalog-resource.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="49a2a-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="49a2a-120">Aşağıdaki adımlar, tercih ettiğiniz herhangi bir programlama dilinde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="49a2a-121">Tam çalışan bir örnek istiyorsanız aşağıda bahsedilen [C# örneğine](#c-sample-code) göz atın.</span><span class="sxs-lookup"><span data-stu-id="49a2a-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="49a2a-122">Aksi takdirde, güvenilir bir katalog okuyucusu oluşturmak için aşağıdaki kılavuzu izleyin.</span><span class="sxs-lookup"><span data-stu-id="49a2a-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="49a2a-123">İmleç başlatma</span><span class="sxs-lookup"><span data-stu-id="49a2a-123">Initialize a cursor</span></span>

<span data-ttu-id="49a2a-124">Güvenilir bir katalog okuyucusu oluşturmanın ilk adımı bir imleç uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="49a2a-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="49a2a-125">Katalog imlecinin tasarımı hakkında tam Ayrıntılar için bkz. [Katalog başvuru belgesi](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="49a2a-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="49a2a-126">Kısaca, imleç katalogda olayları işleen zaman bir noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="49a2a-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="49a2a-127">Katalogdaki olaylar paket yayımlarımı ve diğer paket değişikliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="49a2a-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="49a2a-128">NuGet 'e yayınlanan tüm paketlerle (zamandan itibaren) endişelenmeniz durumunda imlecinizi "En düşük değer" zaman damgasına (örn. `DateTime.MinValue` .net 'te) başlatmalısınız.</span><span class="sxs-lookup"><span data-stu-id="49a2a-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="49a2a-129">Yalnızca şu anda yayımlanan paketler hakkında hatırlıyorsanız, geçerli zaman damgasını ilk imleç değeri olarak kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="49a2a-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="49a2a-130">Bu kılavuzda, imlecinizi bir saat önce zaman damgasına başlatacağız.</span><span class="sxs-lookup"><span data-stu-id="49a2a-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="49a2a-131">Şimdilik bu zaman damgasını bellekte kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="49a2a-132">Katalog dizini URL 'sini belirleme</span><span class="sxs-lookup"><span data-stu-id="49a2a-132">Determine catalog index URL</span></span>

<span data-ttu-id="49a2a-133">NuGet API 'sindeki her kaynağın (uç nokta) konumu, [hizmet dizini](../../api/service-index.md)kullanılarak keşfedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="49a2a-134">Bu kılavuz nuget.org 'e odaklandığından NuGet. org 'ın hizmet dizinini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="49a2a-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="49a2a-135">Hizmet belgesi, nuget.org üzerindeki tüm kaynakları içeren JSON belgesidir. Özellik değerine sahip kaynağı arayın `@type` `Catalog/3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="49a2a-136">İlişkili `@id` özellik değeri, Katalog dizininin URL 'sidir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="49a2a-137">Yeni Katalog bul yaprakları</span><span class="sxs-lookup"><span data-stu-id="49a2a-137">Find new catalog leaves</span></span>

<span data-ttu-id="49a2a-138">`@id`Önceki adımda bulunan özellik değerini kullanarak, Katalog dizinini indirin:</span><span class="sxs-lookup"><span data-stu-id="49a2a-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="49a2a-139">[Katalog dizininin](../../api/catalog-resource.md#catalog-index)serisini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="49a2a-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="49a2a-140">Geçerli imlecinizin değerine eşit veya daha küçük olan tüm [Katalog sayfası nesnelerini](../../api/catalog-resource.md#catalog-page-object-in-the-index) filtreleyin `commitTimeStamp` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="49a2a-141">Kalan her bir katalog sayfası için, özelliğini kullanarak tam belgeyi indirin `@id` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="49a2a-142">[Katalog sayfasının](../../api/catalog-resource.md#catalog-page)serisini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="49a2a-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="49a2a-143">Geçerli imlecinizin değerine eşit veya daha küçük olan tüm [Katalog yaprak nesnelerini](../../api/catalog-resource.md#catalog-item-object-in-a-page) filtreleyin `commitTimeStamp` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="49a2a-144">Filtrelenmeyen tüm katalog sayfalarını indirdikten sonra, imlecinizin zaman damgası ve hemen sonrasında yayımlanmış, listelenmemiş, listelenen veya silinen paketleri temsil eden bir katalog yaprak nesneleri kümesine sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="49a2a-145">İşlem kataloğu yaprakları</span><span class="sxs-lookup"><span data-stu-id="49a2a-145">Process catalog leaves</span></span>

<span data-ttu-id="49a2a-146">Bu noktada, Katalog öğelerinde istediğiniz özel işlemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="49a2a-147">Tüm ihtiyacınız olan paketin KIMLIĞI ve sürümü ise, `nuget:id` `nuget:version` sayfada bulunan katalog öğesi nesnelerinde ve özelliklerini inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="49a2a-148">`@type`Katalog öğesinin mevcut bir paket veya silinen bir paket ile ilgilenmediğini görmek için özelliğine baktığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="49a2a-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="49a2a-149">Paketle ilgili meta veriler (örneğin, açıklama, bağımlılıklar,. nupkg boyutu vb.) ile ilgileniyorsanız, özelliğini kullanarak [Katalog yaprak belgesini](../../api/catalog-resource.md#catalog-leaf) getirebilirsiniz `@id` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="49a2a-150">Bu belge, [paket meta verileri kaynağında](../../api/registration-base-url-resource.md)bulunan tüm meta verilere sahiptir ve daha fazla!</span><span class="sxs-lookup"><span data-stu-id="49a2a-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="49a2a-151">Bu adım, özel mantığınızı uyguladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="49a2a-152">Bu kılavuzdaki diğer adımlar, Katalog yaprakları ile yaptığınız bağımsız şekilde oldukça benzer şekilde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="49a2a-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="49a2a-153">. Nupkg indiriliyor</span><span class="sxs-lookup"><span data-stu-id="49a2a-153">Downloading the .nupkg</span></span>

<span data-ttu-id="49a2a-154">Kataloğunda bulunan paketler için. nupkg 'yı indirmek istiyorsanız [paket içerik kaynağını](../../api/package-base-address-resource.md)kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="49a2a-155">Ancak, katalogda bir paketin bulunduğu ve paket içerik kaynağında kullanılabildiği zaman arasında kısa bir gecikme olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49a2a-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="49a2a-156">Bu nedenle, `404 Not Found` katalogda bulduğunuz bir paket için. nupkg 'yı indirmeye çalışırken karşılaşırsanız, daha sonra kısa bir süre sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="49a2a-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="49a2a-157">Bu gecikmeyi düzeltmek, GitHub sorunu [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455)tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="49a2a-158">İmleci öne taşı</span><span class="sxs-lookup"><span data-stu-id="49a2a-158">Move the cursor forward</span></span>

<span data-ttu-id="49a2a-159">Katalog öğelerini başarıyla işledikten sonra kaydedilecek yeni imleç değerini belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="49a2a-160">Bunu yapmak için, istediğiniz tüm Katalog öğelerinin en yüksek (en son kronolojik) `commitTimeStamp` sayısını bulun.</span><span class="sxs-lookup"><span data-stu-id="49a2a-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="49a2a-161">Bu, yeni imlecinizin değeridir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-161">This is your new cursor value.</span></span> <span data-ttu-id="49a2a-162">Veritabanı, dosya sistemi veya blob depolama gibi bir kalıcı depoya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="49a2a-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="49a2a-163">Daha fazla katalog öğesi almak istediğinizde, bu kalıcı mağazadan imlecinizin değerini başlatarak [ilk adımdan](#initialize-a-cursor) başlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="49a2a-164">Uygulamanız bir özel durum veya hatalar oluşturursa, imleci öne taşımayın.</span><span class="sxs-lookup"><span data-stu-id="49a2a-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="49a2a-165">İmleci ileriye doğru taşımak, imlecinizin öncesinde katalog öğelerini işlemek için hiçbir değişiklik yapmanıza gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="49a2a-166">Bazı nedenlerle, Katalog yaprakları sırasında bir hata varsa imlecinizi geri doğru bir şekilde hareket ettirmeniz ve kodunuzun eski katalog öğelerini yeniden işlemesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="49a2a-167">C# örnek kodu</span><span class="sxs-lookup"><span data-stu-id="49a2a-167">C# sample code</span></span>

<span data-ttu-id="49a2a-168">Katalog, HTTP üzerinden kullanılabilen bir JSON belgeleri kümesi olduğundan, HTTP istemcisi ve JSON seri hale getiricisi olan herhangi bir programlama dili kullanılarak ile etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="49a2a-169">C# örnekleri [NuGet/Samples deposunda](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="49a2a-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="49a2a-170">Katalog SDK 'Sı</span><span class="sxs-lookup"><span data-stu-id="49a2a-170">Catalog SDK</span></span>

<span data-ttu-id="49a2a-171">Kataloğu kullanmanın en kolay yolu `NuGet.Protocol.Catalog` , aşağıdaki NuGet paketi kaynak URL 'si kullanılarak Azure Artifacts sağlanan yayın öncesi .net Catalog SDK paketini kullanmaktır: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="49a2a-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package `NuGet.Protocol.Catalog`, which is available on Azure Artifacts using the following NuGet package source URL: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span></span>

<span data-ttu-id="49a2a-172">Bu paketi, `netstandard1.3` veya daha büyük (.NET Framework 4,6 gibi) uyumlu bir projeye yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49a2a-172">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="49a2a-173">Bu paketi kullanan bir örnek, [NuGet. Protocol. Catalog. Sample projesinde](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)GitHub 'da bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="49a2a-173">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="49a2a-174">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="49a2a-174">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="49a2a-175">Minimum örnek</span><span class="sxs-lookup"><span data-stu-id="49a2a-175">Minimal sample</span></span>

<span data-ttu-id="49a2a-176">Daha ayrıntılı olarak katalogla etkileşimi gösteren daha az bağımlılıklara sahip bir örnek için bkz. [Catalogreadersample örnek projesi](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="49a2a-176">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="49a2a-177">Proje, `netcoreapp2.0` [NuGet. Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet dizinini çözümlemek için) ve [ 9.0.1 üzerindeNewtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON serisini kaldırma için) öğesine bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="49a2a-177">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="49a2a-178">Kodun ana mantığı [program.cs dosyasında](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)görünür.</span><span class="sxs-lookup"><span data-stu-id="49a2a-178">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="49a2a-179">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="49a2a-179">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
