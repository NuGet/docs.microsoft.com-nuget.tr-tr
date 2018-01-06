---
title: "Tüm paketler için sorgu nuget.org için yayımlanan | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/2/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d017cd4-3d75-4341-ba90-3c57be093b7d
description: "NuGet API'yi kullanarak nuget.org için yayımlanan tüm paketler için sorgu ve zaman içinde güncel kalın."
keywords: "NuGet API listeleme tüm paketleri, NuGet API çoğaltma paketleri nuget.org için en son paketler yayımlandı"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5559a7cd104861b1a10aa8d1513696e609c51c15
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="cedc5-104">Nuget.org için yayımlanan tüm paketler için sorgu</span><span class="sxs-lookup"><span data-stu-id="cedc5-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="cedc5-105">OData V2 API nuget.org için yayımlanan tüm paketler numaralandırma eski bir ortak sorgu desenine göre sıralayarak paketi yayımlandığında.</span><span class="sxs-lookup"><span data-stu-id="cedc5-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="cedc5-106">Bu tür bir nuget.org sorgusu gerektiren senaryolar yaygın olarak değişir:</span><span class="sxs-lookup"><span data-stu-id="cedc5-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="cedc5-107">Nuget.org tamamen çoğaltma</span><span class="sxs-lookup"><span data-stu-id="cedc5-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="cedc5-108">Paketleri yayımlanan yeni sürümleri varsa, algılama</span><span class="sxs-lookup"><span data-stu-id="cedc5-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="cedc5-109">Pakete bağlıdır paketleri bulma</span><span class="sxs-lookup"><span data-stu-id="cedc5-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="cedc5-110">Eski yol bunu yaparsanız, bu genellikle bir zaman damgası tarafından OData paket varlık sıralama ve kullanılarak büyük sonuç kümesinde disk belleği bağımlı `skip` ve `top` (sayfa boyutu) parametreleri.</span><span class="sxs-lookup"><span data-stu-id="cedc5-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="cedc5-111">Ne yazık ki, bu yaklaşımın bazı sakıncaları vardır:</span><span class="sxs-lookup"><span data-stu-id="cedc5-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="cedc5-112">Sorgular, genellikle sırasını değiştirme veriler üzerinde gerçekleştirildiğinden olasılığını paketleri eksik</span><span class="sxs-lookup"><span data-stu-id="cedc5-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="cedc5-113">Sorguları getirilmemiş nedeniyle sorgu yanıt süresi, yavaş (en iyileştirilmiş sorgular olanları mainline bir senaryo için resmi NuGet istemci desteği olan)</span><span class="sxs-lookup"><span data-stu-id="cedc5-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="cedc5-114">Bu tür sorgular destek gelecekte anlamına gelir, kullanım dışı ve belgelenmemiş API'yi garanti edilmez</span><span class="sxs-lookup"><span data-stu-id="cedc5-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="cedc5-115">Bunu ilkelerinden tam sipariş geçmişine yeniden yürütme sorunları</span><span class="sxs-lookup"><span data-stu-id="cedc5-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="cedc5-116">Bu nedenle, daha güvenilir ve gelecekteki kanıt şekilde daha önce bahsedilen senaryosu için aşağıdaki kılavuzu izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="cedc5-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="cedc5-117">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cedc5-117">Overview</span></span>

<span data-ttu-id="cedc5-118">Bu kılavuzun merkezinde kaynaktır [NuGet API](../../api/overview.md) adlı **katalog**.</span><span class="sxs-lookup"><span data-stu-id="cedc5-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="cedc5-119">Katalog, eklenen paketler tam geçmişini görmek arayan sağlayan bir yalnızca append API değiştirildi ve nuget.org silindi olabilir. Tüm ya da bir alt bile nuget.org için yayımlanan paket ilgileniyorsanız, katalog Zaman geçtikçe şu anda kullanılabilir paketler kümesiyle güncel kalmak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="cedc5-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="cedc5-120">Bu kılavuz, bir üst düzey adım adım kılavuz olabilir ancak katalog, ayrıntılı ayrıntılarını ilgileniyorsanız görmek için hazırlanmıştır kendi [API başvuru belgesini](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="cedc5-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="cedc5-121">Aşağıdaki adımlar, tercih ettiğiniz herhangi programlama dilinde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="cedc5-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="cedc5-122">Tam bir çalışan örnek istiyorsanız, bir göz atalım [C# örnek](#c-sample-code) aşağıda belirtilen.</span><span class="sxs-lookup"><span data-stu-id="cedc5-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="cedc5-123">Aksi takdirde, bir güvenilir katalog okuyucu oluşturmak için aşağıdaki kılavuzu uygulayın.</span><span class="sxs-lookup"><span data-stu-id="cedc5-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="cedc5-124">Bir imleç başlatma</span><span class="sxs-lookup"><span data-stu-id="cedc5-124">Initialize a cursor</span></span>

<span data-ttu-id="cedc5-125">Bir güvenilir katalog okuyucu oluşturmanın ilk adımı bir imleç uygular.</span><span class="sxs-lookup"><span data-stu-id="cedc5-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="cedc5-126">Katalog imleci tasarımı ile ilgili tam Ayrıntılar için bkz [katalog başvuru belgesini](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="cedc5-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="cedc5-127">Kısacası, imleç bir kadar kataloğunda olayları işlenmiş zaman noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="cedc5-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="cedc5-128">Olay Kataloğu temsil paketindeki yayımlar ve başka bir paketi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="cedc5-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="cedc5-129">Şimdiye kadar Nuget'e (sürenin başlangıcından bu yana) yayımlanan tüm paketler önem verdiğiniz, imlecinizi bir "en düşük değer" zaman damgası başlatmak (örneğin `DateTime.MinValue` .NET içinde).</span><span class="sxs-lookup"><span data-stu-id="cedc5-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="cedc5-130">Şimdi başlatılıyor yayımlanan yalnızca paketleri hakkında verdiğiniz, geçerli zaman damgası ilk imleci değeri olarak kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="cedc5-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="cedc5-131">Bu kılavuz, biz bir saatten önce bir zaman damgası için bizim imleç başlatması.</span><span class="sxs-lookup"><span data-stu-id="cedc5-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="cedc5-132">Şimdilik, zaman damgası bellekte yalnızca kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cedc5-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="cedc5-133">Katalog dizin URL belirleme</span><span class="sxs-lookup"><span data-stu-id="cedc5-133">Determine catalog index URL</span></span>

<span data-ttu-id="cedc5-134">Kullanarak her kaynağın (Bitiş) NuGet API'sindeki konumu bulunmasına [Hizmeti dizini](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cedc5-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="cedc5-135">Bu kılavuz nuget.org üzerinde odaklanmıştır olduğundan, biz nuget.org Hizmeti dizini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="cedc5-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="cedc5-136">Hizmet belgesini nuget.org üzerinde kaynakların tümünü içeren JSON belgedir. Kaynak sahip Ara `@type` özellik değerinin `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="cedc5-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="cedc5-137">İlişkili `@id` özellik değeri olan katalog dizinini URL'si.</span><span class="sxs-lookup"><span data-stu-id="cedc5-137">The associated `@id` property value is the URL to the catalog index itself.</span></span>

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="cedc5-138">Yeni Katalog bırakır Bul</span><span class="sxs-lookup"><span data-stu-id="cedc5-138">Find new catalog leaves</span></span>

<span data-ttu-id="cedc5-139">Kullanarak `@id` özellik değeri önceki adımda bulundu indirmek katalog dizini:</span><span class="sxs-lookup"><span data-stu-id="cedc5-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="cedc5-140">Seri durumdan [katalog dizinini](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="cedc5-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="cedc5-141">Tüm filtre [sayfa nesneleri katalog](../../api/catalog-resource.md#catalog-page-object-in-the-index) ile `commitTimeStamp` değerinden küçük veya eşit, geçerli imleç.</span><span class="sxs-lookup"><span data-stu-id="cedc5-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="cedc5-142">Kullanarak tam belgenin geri kalan her katalog sayfası karşıdan `@id` özelliği.</span><span class="sxs-lookup"><span data-stu-id="cedc5-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="cedc5-143">Seri durumdan [katalog sayfası](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="cedc5-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="cedc5-144">Tüm filtre [yaprak nesneleri katalog](../../api/catalog-resource.md#catalog-item-object-in-a-page) ile `commitTimeStamp` değerinden küçük veya eşit, geçerli imleç.</span><span class="sxs-lookup"><span data-stu-id="cedc5-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="cedc5-145">Tüm filtrelenmelidir değil Katalog sayfaları indirdikten sonra yayımlanan, listede, listelenen veya silinen, imleç zaman damgası arasında bir süre paketleri temsil eden bir katalog yaprak nesne sahip olur ve artık.</span><span class="sxs-lookup"><span data-stu-id="cedc5-145">After you have downloaded all of the catalog pages not filtered out, you will have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="cedc5-146">İşlem katalog bırakır</span><span class="sxs-lookup"><span data-stu-id="cedc5-146">Process catalog leaves</span></span>

<span data-ttu-id="cedc5-147">Bu noktada, katalog öğeleri istediğiniz herhangi bir özel işlem gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cedc5-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="cedc5-148">İhtiyacınız olan tek şey, Paket sürümü ve kimliği inceleyebilirsiniz `nuget:id` ve `nuget:version` özellikleri katalog öğesi sayfalarında bulunan nesneler.</span><span class="sxs-lookup"><span data-stu-id="cedc5-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="cedc5-149">Bakmak emin olun `@type` katalog öğesi var olan bir paket veya silinmiş bir paket ilgiliyse bilmeniz özelliği.</span><span class="sxs-lookup"><span data-stu-id="cedc5-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="cedc5-150">Meta verileri (Açıklama, bağımlılıkları, .nupkg boyutu, vb. gibi) paket hakkında ilgileniyorsanız getirebilirsiniz [katalog yaprak belge](../../api/catalog-resource.md#catalog-leaf) kullanarak `@id` özelliği.</span><span class="sxs-lookup"><span data-stu-id="cedc5-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="cedc5-151">Bu belgede bulunan meta verileri tümünün [paketini meta veri kaynağı](../../api/registration-base-url-resource.md)ve daha fazlası!</span><span class="sxs-lookup"><span data-stu-id="cedc5-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="cedc5-152">Bu adım, burada özel mantığınızı uygulamak bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cedc5-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="cedc5-153">Bu kılavuzdaki diğer adımları uygulanan pretty içinde çok aynı ile katalog bırakır yapmakta olduğunuz önemli yolu değil.</span><span class="sxs-lookup"><span data-stu-id="cedc5-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="cedc5-154">.nupkg yükleniyor</span><span class="sxs-lookup"><span data-stu-id="cedc5-154">Downloading the .nupkg</span></span>

<span data-ttu-id="cedc5-155">İndirme içinde ilgileniyorsanız .nupkg ait paketler için bulunan Kataloğu'nda kullanabileceğiniz [paket içerik kaynağı](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="cedc5-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="cedc5-156">Ancak, bir paketi kataloğunda bulunduğunda ve paket içerik kaynağı kullanılabilir olduğunda arasına kısa bir gecikme olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cedc5-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="cedc5-157">Bu nedenle, karşılaşırsanız `404 Not Found` .nupkg Kataloğu'nda bulunan bir paket için indirme girişiminde bulunulduğunda yalnızca kısa bir süre daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="cedc5-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="cedc5-158">Bu gecikme düzelttikten GitHub sorunu tarafından izlenir [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="cedc5-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="cedc5-159">İmleç ilerlemek</span><span class="sxs-lookup"><span data-stu-id="cedc5-159">Move the cursor forward</span></span>

<span data-ttu-id="cedc5-160">Katalog öğeleri başarıyla işledikten sonra kaydetmek için yeni imleç değeri belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cedc5-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="cedc5-161">Bunu yapmak için en fazla bulun (son tarih sırasına göre) `commitTimeStamp` , işlenen tüm katalog öğelerinin.</span><span class="sxs-lookup"><span data-stu-id="cedc5-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="cedc5-162">Bu, yeni bir imleç değerdir.</span><span class="sxs-lookup"><span data-stu-id="cedc5-162">This is your new cursor value.</span></span> <span data-ttu-id="cedc5-163">Bu veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cedc5-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="cedc5-164">Daha fazla katalog öğeleri almak istediğinizde, sadece başlangıcı [ilk adım](#initialize-a-cursor) imleç değeriniz bu kalıcı deposundan başlatma tarafından.</span><span class="sxs-lookup"><span data-stu-id="cedc5-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="cedc5-165">Uygulamanızı bir özel durum ya da hatalar oluşturursa, imleci İleri taşımayın.</span><span class="sxs-lookup"><span data-stu-id="cedc5-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="cedc5-166">İmleç ilerleyen hiçbir zaman yeniden imlecinizi önce katalog öğelerini işlemek için gereken bir anlamı yoktur.</span><span class="sxs-lookup"><span data-stu-id="cedc5-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="cedc5-167">Herhangi bir nedenle varsa, katalog işleminin nasıl içinde bir hata bırakır, sadece imlecinizi sürede geri taşımak ve eski katalog öğeleri yeniden işlemek kodunuzu izin.</span><span class="sxs-lookup"><span data-stu-id="cedc5-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="cedc5-168">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="cedc5-168">C# sample code</span></span>

<span data-ttu-id="cedc5-169">Katalog HTTP üzerinden bir dizi JSON belgeleri kullanılabilir olduğundan, bir HTTP istemcisi ve JSON seri durumdan çıkarıcının sahip herhangi bir programlama dili kullanarak kurduğunda.</span><span class="sxs-lookup"><span data-stu-id="cedc5-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="cedc5-170">C# örnekleri kullanılabilir [NuGet/Samples depo](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="cedc5-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="cedc5-171">SDK katalog</span><span class="sxs-lookup"><span data-stu-id="cedc5-171">Catalog SDK</span></span>

<span data-ttu-id="cedc5-172">Katalog kullanmak için en kolay yolu, yayın öncesi .NET katalog SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="cedc5-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span>
<span data-ttu-id="cedc5-173">Bu paket edinilebilir `nuget-build` akış, MyGet NuGet paket kaynağı URL'sini kullandığınız `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="cedc5-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="cedc5-174">İle uyumlu bir proje için bu paketi yükleyebilirsiniz `netstandard1.3` ya da (örneğin, .NET Framework 4.6) büyük.</span><span class="sxs-lookup"><span data-stu-id="cedc5-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="cedc5-175">Bu paketi kullanan bir örnek github'da kullanılabilir [NuGet.Protocol.Catalog.Sample proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="cedc5-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="cedc5-176">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="cedc5-176">Sample output</span></span>

```
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

### <a name="minimal-sample"></a><span data-ttu-id="cedc5-177">En az örnek</span><span class="sxs-lookup"><span data-stu-id="cedc5-177">Minimal sample</span></span>

<span data-ttu-id="cedc5-178">Daha fazla ayrıntı kataloğunda etkileşim gösteren bir örnek için daha az bağımlılıkları, bkz: [CatalogReaderExample örnek proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="cedc5-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span>
<span data-ttu-id="cedc5-179">Proje hedefleri `netcoreapp2.0` ve bağımlı [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (için hizmeti dizini çözme) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (için JSON seri durumundan çıkarma).</span><span class="sxs-lookup"><span data-stu-id="cedc5-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="cedc5-180">Kod ana mantığı görünür [Program.cs dosyasının](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="cedc5-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="cedc5-181">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="cedc5-181">Sample output</span></span>

```
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
