---
title: nuget.org için yayınlanan tüm paketler için sorgu
description: NuGet API'sini kullanarak, nuget.org için yayınlanan tüm paketleri sorgulayabilir ve zaman içinde güncel kalabilirsiniz.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498229"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="33758-103">nuget.org için yayınlanan tüm paketler için sorgu</span><span class="sxs-lookup"><span data-stu-id="33758-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="33758-104">Eski OData V2 API'sindeki ortak bir sorgu deseni, paketin yayımlandığı zaman sipariş edilen nuget.org'a göre yayınlanan tüm paketleri sıralıyordu.</span><span class="sxs-lookup"><span data-stu-id="33758-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="33758-105">nuget.org karşı bu tür bir sorgu gerektiren senaryolar büyük ölçüde değişir:</span><span class="sxs-lookup"><span data-stu-id="33758-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="33758-106">nuget.org tamamen çoğaltma</span><span class="sxs-lookup"><span data-stu-id="33758-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="33758-107">Paketlerin yeni sürümlerinin ne zaman serbest bırakıldığını algılama</span><span class="sxs-lookup"><span data-stu-id="33758-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="33758-108">Paketinize bağlı paketleri bulma</span><span class="sxs-lookup"><span data-stu-id="33758-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="33758-109">Bunu yapmanın eski yolu genellikle OData paket varlığını bir zaman damgası ile sıralamaya ve `skip` (sayfa boyutu) parametreleri kullanılarak `top` belirlenen büyük sonuç kümesi boyunca sayfalama bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="33758-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="33758-110">Ne yazık ki, bu yaklaşımın bazı dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="33758-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="33758-111">Sorgular genellikle sıra değiştiren veriler üzerinde yapıldığından, paketlerin eksik olma olasılığı</span><span class="sxs-lookup"><span data-stu-id="33758-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="33758-112">Sorgular en iyi duruma getirilmediği için sorgu yanıt süresi yavaşladı (en iyi duruma getirilmiş sorgular resmi NuGet istemcisi için ana satır senaryosunu destekleyen sorgulardır)</span><span class="sxs-lookup"><span data-stu-id="33758-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="33758-113">Amortismana ve belgesiz API'nin kullanımı, gelecekte bu tür sorguların desteklenmesi nin garanti olmadığı anlamına gelir</span><span class="sxs-lookup"><span data-stu-id="33758-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="33758-114">Tarihin tam olarak meydana gelen sırayla tekrarlanamaması</span><span class="sxs-lookup"><span data-stu-id="33758-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="33758-115">Bu nedenle, yukarıda belirtilen senaryoları daha güvenilir ve geleceğe yönelik bir şekilde ele almak için aşağıdaki kılavuz izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="33758-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="33758-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="33758-116">Overview</span></span>

<span data-ttu-id="33758-117">Bu kılavuzun merkezinde **NuGet** [API](../../api/overview.md) kataloğu olarak adlandırılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="33758-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="33758-118">Katalog, arayanın nuget.org eklenen, değiştirilen ve silinen paketlerin tam geçmişini görmesini sağlayan yalnızca ek apidir. Nuget.org için yayınlanan paketlerin tümüyle ve hatta bir alt kümesiyle ilgileniyorsanız, katalog, zaman geçtikçe mevcut paketlerkümesinden haberdar olmak için harika bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="33758-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="33758-119">Bu kılavuz, üst düzey bir walk-through olması amaçlanmıştır ama kataloğun ince tane ayrıntıları ilgileniyorsanız, onun [API başvuru belgesi](../../api/catalog-resource.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="33758-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="33758-120">Aşağıdaki adımlar seçtiğiniz herhangi bir programlama dilinde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="33758-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="33758-121">Tam çalışan bir örnek istiyorsanız, aşağıda belirtilen [C# örneğine](#c-sample-code) bir göz atın.</span><span class="sxs-lookup"><span data-stu-id="33758-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="33758-122">Aksi takdirde, güvenilir bir katalog okuyucu oluşturmak için aşağıdaki kılavuzu izleyin.</span><span class="sxs-lookup"><span data-stu-id="33758-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="33758-123">İmleci başlatma</span><span class="sxs-lookup"><span data-stu-id="33758-123">Initialize a cursor</span></span>

<span data-ttu-id="33758-124">Güvenilir bir katalog okuyucu oluşturmanın ilk adımı bir imleç uygulamaktır.</span><span class="sxs-lookup"><span data-stu-id="33758-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="33758-125">Katalog imlecinin tasarımı hakkında tüm ayrıntılar için [katalog başvuru belgesine](../../api/catalog-resource.md#cursor)bakın.</span><span class="sxs-lookup"><span data-stu-id="33758-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="33758-126">Kısacası, imleç, katalogdaki olayları işlediğiniz bir zaman dilimi dir.</span><span class="sxs-lookup"><span data-stu-id="33758-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="33758-127">Katalogdaki olaylar paket yayınlarını ve diğer paket değişikliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="33758-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="33758-128">NuGet'de yayınlanan tüm paketleri önemsiyorsanız (zamanın başlangıcından beri), imlecinizi "minimum değer" zaman damgasına (örn. `DateTime.MinValue` .NET'te) başlatılırsınız.</span><span class="sxs-lookup"><span data-stu-id="33758-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="33758-129">Şu andan itibaren yalnızca yayınlanan paketleri önemsiyorsanız, geçerli zaman damgasını ilk imleç değeriniz olarak kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="33758-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="33758-130">Bu kılavuz için imlecimizi bir saat önce bir zaman damgasına alacağız.</span><span class="sxs-lookup"><span data-stu-id="33758-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="33758-131">Şimdilik, hafızadaki zaman damgasını kaydet.</span><span class="sxs-lookup"><span data-stu-id="33758-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="33758-132">Katalog dizini URL'si belirleme</span><span class="sxs-lookup"><span data-stu-id="33758-132">Determine catalog index URL</span></span>

<span data-ttu-id="33758-133">NuGet API'sindeki her kaynağın (bitiş noktası) konumu [hizmet dizini](../../api/service-index.md)kullanılarak keşfedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="33758-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="33758-134">Bu kılavuz nuget.org odaklandığından, nuget.org'un hizmet dizinini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="33758-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="33758-135">Hizmet belgesi, nuget.org tüm kaynakları içeren JSON belgesidir. `Catalog/3.0.0`Özellik değerine `@type` sahip kaynağı arayın.</span><span class="sxs-lookup"><span data-stu-id="33758-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="33758-136">İlişkili `@id` özellik değeri, katalog dizininin URL'sidir.</span><span class="sxs-lookup"><span data-stu-id="33758-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="33758-137">Yeni katalog yapraklarını bulma</span><span class="sxs-lookup"><span data-stu-id="33758-137">Find new catalog leaves</span></span>

<span data-ttu-id="33758-138">Önceki `@id` adımda bulunan özellik değerini kullanarak katalog dizini indirin:</span><span class="sxs-lookup"><span data-stu-id="33758-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="33758-139">[Katalog dizini](../../api/catalog-resource.md#catalog-index)deserialize.</span><span class="sxs-lookup"><span data-stu-id="33758-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="33758-140">Tüm [katalog sayfa nesnelerini](../../api/catalog-resource.md#catalog-page-object-in-the-index) geçerli imleç değerinizden daha az veya eşit olacak `commitTimeStamp` şekilde filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="33758-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="33758-141">Kalan her katalog sayfası için, özelliği `@id` kullanarak belgenin tamamını indirin.</span><span class="sxs-lookup"><span data-stu-id="33758-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="33758-142">[Katalog sayfasını](../../api/catalog-resource.md#catalog-page)deserialize.</span><span class="sxs-lookup"><span data-stu-id="33758-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="33758-143">Tüm [katalog yaprağı nesnelerini](../../api/catalog-resource.md#catalog-item-object-in-a-page) geçerli imleç değerinizden daha az veya eşit olacak `commitTimeStamp` şekilde filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="33758-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="33758-144">Filtrelenmemiş tüm katalog sayfalarını indirdikten sonra, imleç zaman damganız ile şimdi arasındaki süre içinde yayınlanmış, listelenmemiş, listelenen veya silinmiş paketleri temsil eden bir katalog yaprağı nesne kümeniz vardır.</span><span class="sxs-lookup"><span data-stu-id="33758-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="33758-145">İşlem kataloğu yaprakları</span><span class="sxs-lookup"><span data-stu-id="33758-145">Process catalog leaves</span></span>

<span data-ttu-id="33758-146">Bu noktada, katalog öğeleri üzerinde istediğiniz herhangi bir özel işleme gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="33758-147">İhtiyacınız olan tek şey paketin kimliği ve sürümüyse, sayfalarda bulunan katalog öğesi nesnelerindeki `nuget:id` ve `nuget:version` özelliklerini inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="33758-148">Katalog öğesinin varolan bir paketle mi yoksa silinmiş bir paketle mi ilgili olduğunu öğrenmek için tesise baktığınızdan `@type` emin olun.</span><span class="sxs-lookup"><span data-stu-id="33758-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="33758-149">Paketle ilgili meta verilerle ilgileniyorsanız (açıklama, bağımlılıklar, .nupkg boyutu, vb.) özelliği kullanarak `@id` katalog yaprağı [belgesini](../../api/catalog-resource.md#catalog-leaf) getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="33758-150">Bu [belge, paket meta veri kaynağında](../../api/registration-base-url-resource.md)yer alan tüm meta verilere ve daha fazlana sahiptir!</span><span class="sxs-lookup"><span data-stu-id="33758-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="33758-151">Bu adım, özel mantığınızı uyguladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="33758-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="33758-152">Bu kılavuzdaki diğer adımlar katalog yaprakları ile ne yapıyor olursa olsun hemen hemen aynı şekilde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="33758-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="33758-153">.nupkg'ı indirme</span><span class="sxs-lookup"><span data-stu-id="33758-153">Downloading the .nupkg</span></span>

<span data-ttu-id="33758-154">Katalogda bulunan paketler için .nupkg'ları indirmek istiyorsanız, paket içerik [kaynağını](../../api/package-base-address-resource.md)kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="33758-155">Ancak, bir paketin katalogda bulunmasıyla paket içeriği kaynağında kullanılabilir olması arasında kısa bir gecikme olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="33758-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="33758-156">Bu nedenle, `404 Not Found` katalogda bulduğunuz bir paket için .nupkg indirmeye çalışırken karşılaşırsanız, kısa bir süre sonra yeniden denemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="33758-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="33758-157">Bu gecikmegiderme GitHub sorunu [NuGet / NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455)tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="33758-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="33758-158">İmleci ileri doğru hareket ettirin</span><span class="sxs-lookup"><span data-stu-id="33758-158">Move the cursor forward</span></span>

<span data-ttu-id="33758-159">Katalog öğelerini başarıyla işledikten sonra, kaydetmek için yeni imleç değerini belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="33758-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="33758-160">Bunu yapmak için, işlediğiniz tüm `commitTimeStamp` katalog öğelerinin maksimum (en son kronolojik) öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="33758-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="33758-161">Bu senin yeni imleç değeriniz.</span><span class="sxs-lookup"><span data-stu-id="33758-161">This is your new cursor value.</span></span> <span data-ttu-id="33758-162">Veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="33758-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="33758-163">Daha fazla katalog öğesi almak istediğinizde, imleç değerinizi bu kalıcı mağazadan başlatarak [ilk adımdan](#initialize-a-cursor) başlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="33758-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="33758-164">Uygulamanız bir özel durum veya hata atarsa, imleci ileri itmeyin.</span><span class="sxs-lookup"><span data-stu-id="33758-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="33758-165">İmleci ileriye taşımak, imlecinizin önünde katalog öğelerini bir daha işlemeniz gerekmeyecek bir anlama gelir.</span><span class="sxs-lookup"><span data-stu-id="33758-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="33758-166">Nedense, katalog yapraklarını işleme şeklinizde bir hata varsa, imlecinizi zamanda geriye doğru taşıyabilir ve kodunuzu eski katalog öğelerini yeniden işlemesine izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="33758-167">C# örnek kodu</span><span class="sxs-lookup"><span data-stu-id="33758-167">C# sample code</span></span>

<span data-ttu-id="33758-168">Katalog HTTP üzerinden kullanılabilir JSON belgeleri kümesi olduğundan, bir HTTP istemcisi ve JSON deserializer olan herhangi bir programlama dili kullanılarak etkileşim olabilir.</span><span class="sxs-lookup"><span data-stu-id="33758-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="33758-169">C# örnekleri [NuGet/Numune deposunda](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="33758-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="33758-170">Katalog SDK</span><span class="sxs-lookup"><span data-stu-id="33758-170">Catalog SDK</span></span>

<span data-ttu-id="33758-171">Kataloğu kullanmanın en kolay yolu ön sürüm .NET kataloğu SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="33758-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="33758-172">Bu paket, NuGet paket kaynak URL'sini `nuget-build` `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`kullandığınız MyGet akışında mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="33758-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="33758-173">Bu paketi (.NET Framework `netstandard1.3` 4.6 gibi) uyumlu veya daha büyük bir projeye yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33758-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="33758-174">Bu paketi kullanan bir örnek GitHub'da [NuGet.Protocol.Catalog.Sample projesinde](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="33758-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="33758-175">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="33758-175">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="33758-176">Minimum örnek</span><span class="sxs-lookup"><span data-stu-id="33758-176">Minimal sample</span></span>

<span data-ttu-id="33758-177">Katalogla etkileşimi daha ayrıntılı olarak gösteren daha az bağımlılık içeren bir örnek [için, CatalogReaderExample örnek projesine](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)bakın.</span><span class="sxs-lookup"><span data-stu-id="33758-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="33758-178">Proje `netcoreapp2.0` [nuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet indeksini çözmek için) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON deserialization için) hedeflerini ve bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="33758-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="33758-179">Kodun ana mantığı [Program.cs dosyasında](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)görünür.</span><span class="sxs-lookup"><span data-stu-id="33758-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="33758-180">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="33758-180">Sample output</span></span>

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
