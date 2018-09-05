---
title: Nuget.org için yayımlanan tüm paketler için sorgu
description: NuGet API'yi kullanarak nuget.org için yayımlanan tüm paketler için sorgu ve zaman içinde yeniliklerden haberdar olun.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551084"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="8f8c5-103">Nuget.org için yayımlanan tüm paketler için sorgu</span><span class="sxs-lookup"><span data-stu-id="8f8c5-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="8f8c5-104">OData V2 API'si tüm paketleri nuget.org için yayımlanan numaralandırma eski bir yaygın sorgu düzeni sıralı olarak paketi yayımlandığında.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="8f8c5-105">Bu tür bir sorgu nuget.org karşı gerektiren senaryolar büyük ölçüde farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="8f8c5-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="8f8c5-106">Nuget.org tamamen çoğaltılıyor</span><span class="sxs-lookup"><span data-stu-id="8f8c5-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="8f8c5-107">Yeni sürümler kullanıma paketleriniz varsa algılama</span><span class="sxs-lookup"><span data-stu-id="8f8c5-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="8f8c5-108">Pakete bağlıdır paketleri bulma</span><span class="sxs-lookup"><span data-stu-id="8f8c5-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="8f8c5-109">Bunu yaptığınızda, eski yöntemle bu genellikle bir zaman damgası tarafından OData paket varlık sıralama ve büyük sonuç kullanarak kümesi sayfalama bağımlı `skip` ve `top` (sayfa boyutu) parametreleri.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="8f8c5-110">Ne yazık ki bu yaklaşımının bazı dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="8f8c5-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="8f8c5-111">Sorgular genellikle sırasını değiştirme veriler üzerinde gerçekleştirildiğinden olasılığını paketleri eksik</span><span class="sxs-lookup"><span data-stu-id="8f8c5-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="8f8c5-112">Yavaş sorgu yanıt süresi, sorguları getirilmemiş olduğundan (en iyileştirilmiş sorgular, ana hat bir senaryo için resmi bir NuGet istemcisi desteği olan)</span><span class="sxs-lookup"><span data-stu-id="8f8c5-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="8f8c5-113">Destek gibi sorguların gelecekte kullanım dışı ve belgelenmemiş API, kullanımını garanti edilmez</span><span class="sxs-lookup"><span data-stu-id="8f8c5-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="8f8c5-114">Bağlanamama geçmişi, ilkelerinden tam sırayla yeniden Yürüt</span><span class="sxs-lookup"><span data-stu-id="8f8c5-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="8f8c5-115">Bu nedenle, aşağıdaki kılavuzda daha güvenilir ve geleceğe hazır bir şekilde yukarıda sözü edilen senaryolara izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="8f8c5-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8f8c5-116">Overview</span></span>

<span data-ttu-id="8f8c5-117">Bu kılavuzun merkezinde kaynaktır [NuGet API'si](../../api/overview.md) adlı **Kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="8f8c5-118">Katalog, eklenen paketler tam geçmişini görmek çağıranın izin veren bir yalnızca ekleme yapılabilen API değiştirilebilir ve nuget.org adresinden silinmiş olabilir. Tüm veya hatta nuget.org için yayımlanmış paketleri kümesini ilgileniyorsanız, katalog Zaman geçtikçe şu anda kullanılabilir paketler kümesiyle güncel kalmak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="8f8c5-119">Bu kılavuz, üst düzey bir gözden geçirme ancak katalog detaylı ayrıntılarını ilgileniyorsanız bkz yöneliktir, [API başvuru belgesini](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="8f8c5-120">Aşağıdaki adımlar, tercih ettiğiniz programlama diliyle uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="8f8c5-121">Tam bir çalışan örnek istiyorsanız göz atın [C# örneği](#c-sample-code) aşağıda belirtilen.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="8f8c5-122">Aksi takdirde, bir güvenilir Kataloğu okuyucu oluşturmak için aşağıdaki kılavuzu izleyin.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="8f8c5-123">Bir imleç Başlat</span><span class="sxs-lookup"><span data-stu-id="8f8c5-123">Initialize a cursor</span></span>

<span data-ttu-id="8f8c5-124">Bir güvenilir Kataloğu okuyucu oluşturmanın ilk adımı bir imleç uygular.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="8f8c5-125">Katalog imleci tasarımı hakkında tam Ayrıntılar için bkz [Kataloğu başvuru belgesini](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="8f8c5-126">Kısacası, imleç bir zamanda kadar olay Kataloğu işledikten noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="8f8c5-127">Katalog temsil paketini olayları yayımlar ve başka bir paketin değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="8f8c5-128">Şimdiye kadar (başlangıçtan itibaren) için NuGet yayımlanan tüm paketleri verdiğiniz "sınırın" zaman damgası için imlecinizi başlatmak (örneğin `DateTime.MinValue` .NET içinde).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="8f8c5-129">Şimdi başlangıç yayımlanan yalnızca paketleri hakkında dikkatli olun, ilk imleç değeriniz geçerli zaman damgasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="8f8c5-130">Bu kılavuz için biz bir saat önce bir zaman damgası bizim imleç başlatmak.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="8f8c5-131">Şimdilik, zaman damgası bellekte yalnızca kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="8f8c5-132">Katalog dizini URL'si belirlenemedi</span><span class="sxs-lookup"><span data-stu-id="8f8c5-132">Determine catalog index URL</span></span>

<span data-ttu-id="8f8c5-133">Kullanarak NuGet API'sindeki her kaynağın (uç nokta) yerini keşfedilmesini [hizmet dizini](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="8f8c5-134">Bu kılavuz nuget.org üzerinde odaklanır çünkü nuget.org hizmet dizini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="8f8c5-135">Hizmet belgesini tüm kaynakları nuget.org içeren JSON belgesidir. Sahip kaynak için konum `@type` özelliği değerinin `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="8f8c5-136">İlişkili `@id` özellik değeri, katalog dizini URL'si.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="8f8c5-137">Yeni Katalog leaves bulun</span><span class="sxs-lookup"><span data-stu-id="8f8c5-137">Find new catalog leaves</span></span>

<span data-ttu-id="8f8c5-138">Kullanarak `@id` özellik değerini önceki adımda bulduğunuz katalog dizinini indirin:</span><span class="sxs-lookup"><span data-stu-id="8f8c5-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="8f8c5-139">Seri durumdan [Kataloğu dizin](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="8f8c5-140">Tüm filtre [sayfa nesneleri katalog](../../api/catalog-resource.md#catalog-page-object-in-the-index) ile `commitTimeStamp` geçerli imleç değerinizi küçüktür veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="8f8c5-141">Kullanarak tüm belgenin geri kalan her katalog sayfası için indirme `@id` özelliği.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="8f8c5-142">Seri durumdan [katalog sayfası](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="8f8c5-143">Tüm filtre [yaprak nesneleri katalog](../../api/catalog-resource.md#catalog-item-object-in-a-page) ile `commitTimeStamp` geçerli imleç değerinizi küçüktür veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="8f8c5-144">Tüm katalog sayfalar filtrelendi değil indirdikten sonra yayımlanmış, listede bulunmayan, listelenen veya silinen, imleç zaman damgası arasında bir süre silinmiş paketleri temsil eden bir katalog yaprak nesne olan ve artık.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="8f8c5-145">İşlem Kataloğu bırakır</span><span class="sxs-lookup"><span data-stu-id="8f8c5-145">Process catalog leaves</span></span>

<span data-ttu-id="8f8c5-146">Bu noktada, katalog öğeleri üzerinde istediğiniz herhangi bir özel işlem gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="8f8c5-147">Tüm yapmanız gereken ise kimliği ve Paket sürümü inceleyebilirsiniz `nuget:id` ve `nuget:version` özellikleri katalog öğesi sayfalarında bulunan nesneler.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="8f8c5-148">Bakmak emin `@type` katalog öğesi var olan bir paket veya silinen paket ilgiliyse bilmek özelliği.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="8f8c5-149">(Açıklama, bağımlılıkları, .nupkg boyutu, vb. gibi) paket hakkında meta verilerinde ilgileniyorsanız getirebilirsiniz [Kataloğu yaprak belge](../../api/catalog-resource.md#catalog-leaf) kullanarak `@id` özelliği.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="8f8c5-150">Bu belgede bulunan meta verileri tümünün [paket meta veri kaynağı](../../api/registration-base-url-resource.md)ve daha fazlası!</span><span class="sxs-lookup"><span data-stu-id="8f8c5-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="8f8c5-151">Bu adım, özel mantığı uygulamak burada ' dir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="8f8c5-152">Bu kılavuzdaki diğer adımlar uygulanır pretty içinde çok aynı katalog leaves ile neler yaptığına önemli yolu değil.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="8f8c5-153">.nupkg indiriliyor</span><span class="sxs-lookup"><span data-stu-id="8f8c5-153">Downloading the .nupkg</span></span>

<span data-ttu-id="8f8c5-154">İndirilirken ilgileniyorsanız .nupkg ait paketler için bulunan Kataloğu'nda kullanabileceğiniz [paket içerik kaynağı](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="8f8c5-155">Ancak, bir paket kataloğunda bulunduğunda ve paket içerik kaynağı kullanılabilir olduğunda arasında kısa bir gecikme olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="8f8c5-156">Bu nedenle, karşılaşırsanız `404 Not Found` katalogda bulunan bir paket için bir .nupkg indirmeye çalışırken, yalnızca kısa bir süre daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="8f8c5-157">Bu gecikme düzeltme GitHub sorunu tarafından izlenir [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="8f8c5-158">İmleci ileriye taşıyın</span><span class="sxs-lookup"><span data-stu-id="8f8c5-158">Move the cursor forward</span></span>

<span data-ttu-id="8f8c5-159">Katalog öğeleri başarıyla işledikten sonra kaydetmek için yeni imleç değeri belirlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="8f8c5-160">Bunu yapmak için en fazla bulma (en son tarih sırasına göre) `commitTimeStamp` , işlenen tüm katalog öğeleri.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="8f8c5-161">Bu, yeni bir imleç değerdir.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-161">This is your new cursor value.</span></span> <span data-ttu-id="8f8c5-162">Bir veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="8f8c5-163">Daha fazla katalog öğelerini almak istediğinizde, sadece başlangıç [ilk adım](#initialize-a-cursor) tarafından bu kalıcı depolama alanından, imleç değeri başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="8f8c5-164">Uygulamanızı bir özel durum ya da hatalar oluşturursa, imleç ileri taşıma.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="8f8c5-165">İmleç ilerletme hiçbir zaman yeniden imlecinizi önce katalog öğelerini işlemek için gereken bir anlamı vardır.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="8f8c5-166">Bazı nedenlerden dolayı varsa, katalog işleminin nasıl içinde bir hata bırakır, yalnızca zaman içinde geriye dönük imlecinizi hareket ettirin ve eski katalog öğeleri yeniden işlemek kodunuzu izin.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="8f8c5-167">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="8f8c5-167">C# sample code</span></span>

<span data-ttu-id="8f8c5-168">Katalog HTTP üzerinden bir dizi JSON belgeleri kullanılabilir olduğundan, istemci HTTP ve JSON seri durumdan çıkarıcının içeren herhangi bir programlama dilini kullanarak kurulabilen.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="8f8c5-169">C# örnekleri kullanılabilir [NuGet/Samples deposuna](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="8f8c5-170">SDK'sı katalog</span><span class="sxs-lookup"><span data-stu-id="8f8c5-170">Catalog SDK</span></span>

<span data-ttu-id="8f8c5-171">Katalog kullanmak için en kolay yolu, yayın öncesi .NET Kataloğu SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="8f8c5-172">Bu paket üzerinde kullanılabilir `nuget-build` akışına MyGet NuGet paket kaynağı URL'si kullandığınız `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8f8c5-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="8f8c5-173">Bu paket ile uyumlu bir projeye yükleyebileceğiniz `netstandard1.3` veya üzeri (örneğin, .NET Framework 4. 6'da).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="8f8c5-174">Bu paket kullanılarak bir örnek github'da kullanılabilir [NuGet.Protocol.Catalog.Sample proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="8f8c5-175">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="8f8c5-175">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="8f8c5-176">En az örnek</span><span class="sxs-lookup"><span data-stu-id="8f8c5-176">Minimal sample</span></span>

<span data-ttu-id="8f8c5-177">Daha ayrıntılı katalog etkileşimi gösteren bir örnek için daha az bağımlılıklar, bkz [CatalogReaderExample kodunuzla](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="8f8c5-178">Projenizin hedeflediği `netcoreapp2.0` ve bağımlı [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet dizini çözme için) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (için JSON seri durumundan çıkarma).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="8f8c5-179">Kod ana mantığını görülebilir [Program.cs dosyasının](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="8f8c5-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="8f8c5-180">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="8f8c5-180">Sample output</span></span>

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
