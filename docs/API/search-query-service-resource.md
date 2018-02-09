---
title: Arama, NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Arama hizmeti istemcileri anahtar sözcüğüyle paketler için sorgu ve bazı paket alanları sonuçlarına filtre sağlar."
keywords: "NuGet arama API, NuGet paketleri, sorgu NuGet paketlerini API'sine NuGet paketlerini göz atmak için API Bul"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a><span data-ttu-id="8eb3a-104">Ara</span><span class="sxs-lookup"><span data-stu-id="8eb3a-104">Search</span></span>

<span data-ttu-id="8eb3a-105">V3 API kullanarak bir paket kaynağındaki paketleri aramak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-105">It is possible to search for packages available on a package source using the V3 API.</span></span> <span data-ttu-id="8eb3a-106">Aramak için kullanılan kaynak `SearchQueryService` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8eb3a-106">The resource used for searching is the `SearchQueryService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8eb3a-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="8eb3a-107">Versioning</span></span>

<span data-ttu-id="8eb3a-108">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8eb3a-108">The following `@type` values are used:</span></span>

<span data-ttu-id="8eb3a-109">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="8eb3a-109">@type value</span></span>                   | <span data-ttu-id="8eb3a-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="8eb3a-110">Notes</span></span>
----------------------------- | -----
<span data-ttu-id="8eb3a-111">SearchQueryService</span><span class="sxs-lookup"><span data-stu-id="8eb3a-111">SearchQueryService</span></span>            | <span data-ttu-id="8eb3a-112">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="8eb3a-112">The initial release</span></span>
<span data-ttu-id="8eb3a-113">SearchQueryService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="8eb3a-113">SearchQueryService/3.0.0-beta</span></span> | <span data-ttu-id="8eb3a-114">Diğer adı`SearchQueryService`</span><span class="sxs-lookup"><span data-stu-id="8eb3a-114">Alias of `SearchQueryService`</span></span>
<span data-ttu-id="8eb3a-115">SearchQueryService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="8eb3a-115">SearchQueryService/3.0.0-rc</span></span>   | <span data-ttu-id="8eb3a-116">Diğer adı`SearchQueryService`</span><span class="sxs-lookup"><span data-stu-id="8eb3a-116">Alias of `SearchQueryService`</span></span>

## <a name="base-url"></a><span data-ttu-id="8eb3a-117">Temel URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-117">Base URL</span></span>

<span data-ttu-id="8eb3a-118">Aşağıdaki API için temel URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-118">The base URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="8eb3a-119">Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8eb3a-120">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-120">HTTP methods</span></span>

<span data-ttu-id="8eb3a-121">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-packages"></a><span data-ttu-id="8eb3a-122">Paketler için arama</span><span class="sxs-lookup"><span data-stu-id="8eb3a-122">Search for packages</span></span>

<span data-ttu-id="8eb3a-123">API arama sorgusu istemciye belirtilen arama sorgusuyla eşleşen paketleri için bir sayfa sağlar.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-123">The search API allows a client to query for a page of packages matching a specified search query.</span></span> <span data-ttu-id="8eb3a-124">Arama sorgusu (örn. arama terimleri belirteçlere) yorumu sunucu uygulaması tarafından belirlenir. ancak genel beklentisi arama sorgusu paket kimliği, başlıklar, açıklamalar ve etiketleri eşleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-124">The interpretation of the search query (e.g. the tokenization of the search terms) is determined by the server implementation but the general expectation is that the search query is used for matching package IDs, titles, descriptions, and tags.</span></span> <span data-ttu-id="8eb3a-125">Diğer paket meta veri alanlarını da dikkate.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-125">Other package metadata fields may also be considered.</span></span>

<span data-ttu-id="8eb3a-126">Listede bulunmayan bir paket hiç arama sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-126">An unlisted package should never appear in search results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="8eb3a-127">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-127">Request parameters</span></span>

<span data-ttu-id="8eb3a-128">Ad</span><span class="sxs-lookup"><span data-stu-id="8eb3a-128">Name</span></span>        | <span data-ttu-id="8eb3a-129">İçindeki</span><span class="sxs-lookup"><span data-stu-id="8eb3a-129">In</span></span>     | <span data-ttu-id="8eb3a-130">Tür</span><span class="sxs-lookup"><span data-stu-id="8eb3a-130">Type</span></span>    | <span data-ttu-id="8eb3a-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8eb3a-131">Required</span></span> | <span data-ttu-id="8eb3a-132">Notlar</span><span class="sxs-lookup"><span data-stu-id="8eb3a-132">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="8eb3a-133">q</span><span class="sxs-lookup"><span data-stu-id="8eb3a-133">q</span></span>           | <span data-ttu-id="8eb3a-134">URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-134">URL</span></span>    | <span data-ttu-id="8eb3a-135">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-135">string</span></span>  | <span data-ttu-id="8eb3a-136">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-136">no</span></span>       | <span data-ttu-id="8eb3a-137">Filtre paketleri için kullanılan için arama terimleri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-137">The search terms to used to filter packages</span></span>
<span data-ttu-id="8eb3a-138">Atla</span><span class="sxs-lookup"><span data-stu-id="8eb3a-138">skip</span></span>        | <span data-ttu-id="8eb3a-139">URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-139">URL</span></span>    | <span data-ttu-id="8eb3a-140">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-140">integer</span></span> | <span data-ttu-id="8eb3a-141">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-141">no</span></span>       | <span data-ttu-id="8eb3a-142">Sayfa numaralandırma için atlamayı sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-142">The number of results to skip, for pagination</span></span>
<span data-ttu-id="8eb3a-143">Al</span><span class="sxs-lookup"><span data-stu-id="8eb3a-143">take</span></span>        | <span data-ttu-id="8eb3a-144">URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-144">URL</span></span>    | <span data-ttu-id="8eb3a-145">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-145">integer</span></span> | <span data-ttu-id="8eb3a-146">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-146">no</span></span>       | <span data-ttu-id="8eb3a-147">Sayfa numaralandırma için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-147">The number of results to return, for pagination</span></span>
<span data-ttu-id="8eb3a-148">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-148">prerelease</span></span>  | <span data-ttu-id="8eb3a-149">URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-149">URL</span></span>    | <span data-ttu-id="8eb3a-150">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-150">boolean</span></span> | <span data-ttu-id="8eb3a-151">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-151">no</span></span>       | <span data-ttu-id="8eb3a-152">`true`veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8eb3a-152">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="8eb3a-153">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="8eb3a-153">semVerLevel</span></span> | <span data-ttu-id="8eb3a-154">URL</span><span class="sxs-lookup"><span data-stu-id="8eb3a-154">URL</span></span>    | <span data-ttu-id="8eb3a-155">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-155">string</span></span>  | <span data-ttu-id="8eb3a-156">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-156">no</span></span>       | <span data-ttu-id="8eb3a-157">SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-157">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="8eb3a-158">Arama sorgusu `q` sunucu uygulaması tarafından tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-158">The search query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="8eb3a-159">nuget.org destekleyen temel süzme bir [çeşitli alanları](../consume-packages/finding-and-choosing-packages.md#search-syntax).</span><span class="sxs-lookup"><span data-stu-id="8eb3a-159">nuget.org supports basic filtering on a [variety of fields](../consume-packages/finding-and-choosing-packages.md#search-syntax).</span></span> <span data-ttu-id="8eb3a-160">Öyle değilse `q` tüm paketler, atlama ve alma tarafından uygulanan sınırları içinde döndürülmelidir sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-160">If no `q` is provided, all packages should be returned, within the boundaries imposed by skip and take.</span></span> <span data-ttu-id="8eb3a-161">Bu "Gözat" sekmesinde NuGet Visual Studio deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-161">This enables the "Browse" tab in the NuGet Visual Studio experience.</span></span>

<span data-ttu-id="8eb3a-162">`skip` Parametresi varsayılan ayar: 0.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-162">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="8eb3a-163">`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-163">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="8eb3a-164">Sunucu uygulaması bir maksimum değer yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-164">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="8eb3a-165">Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-165">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="8eb3a-166">`semVerLevel` Sorgu parametresi için katılımı için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="8eb3a-166">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="8eb3a-167">Bu sorgu parametresi dışlanırsa SemVer 1.0.0 uyumlu sürümlerini yalnızca paketlerle döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar 4 tamsayı parçalı sürüm dizeler gibi).</span><span class="sxs-lookup"><span data-stu-id="8eb3a-167">If this query parameter is excluded, only packages with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="8eb3a-168">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-168">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="8eb3a-169">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-169">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="8eb3a-170">Yanıt</span><span class="sxs-lookup"><span data-stu-id="8eb3a-170">Response</span></span>

<span data-ttu-id="8eb3a-171">Yanıt kadar içeren JSON belgedir `take` arama sonuçlarında.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-171">The response is JSON document containing up to `take` search results.</span></span> <span data-ttu-id="8eb3a-172">Arama sonuçları paket kimliğine göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-172">Search results are grouped by package ID.</span></span>

<span data-ttu-id="8eb3a-173">Kök JSON nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8eb3a-173">The root JSON object has the following properties:</span></span>

<span data-ttu-id="8eb3a-174">Ad</span><span class="sxs-lookup"><span data-stu-id="8eb3a-174">Name</span></span>      | <span data-ttu-id="8eb3a-175">Tür</span><span class="sxs-lookup"><span data-stu-id="8eb3a-175">Type</span></span>             | <span data-ttu-id="8eb3a-176">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8eb3a-176">Required</span></span> | <span data-ttu-id="8eb3a-177">Notlar</span><span class="sxs-lookup"><span data-stu-id="8eb3a-177">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="8eb3a-178">totalHits</span><span class="sxs-lookup"><span data-stu-id="8eb3a-178">totalHits</span></span> | <span data-ttu-id="8eb3a-179">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-179">integer</span></span>          | <span data-ttu-id="8eb3a-180">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-180">yes</span></span>      | <span data-ttu-id="8eb3a-181">Atlayıp eşleşirse, toplam sayısı `skip` ve`take`</span><span class="sxs-lookup"><span data-stu-id="8eb3a-181">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="8eb3a-182">veri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-182">data</span></span>      | <span data-ttu-id="8eb3a-183">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-183">array of objects</span></span> | <span data-ttu-id="8eb3a-184">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-184">yes</span></span>      | <span data-ttu-id="8eb3a-185">İstek tarafından eşleşen arama sonuçları</span><span class="sxs-lookup"><span data-stu-id="8eb3a-185">The search results matched by the request</span></span>

### <a name="search-result"></a><span data-ttu-id="8eb3a-186">arama sonucu</span><span class="sxs-lookup"><span data-stu-id="8eb3a-186">Search result</span></span>

<span data-ttu-id="8eb3a-187">Her öğe `data` dizidir aynı paket kimliğini paylaşımı paket sürümlerinin bir grup oluşan bir JSON nesnesi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-187">Each item in the `data` array is a JSON object comprised of a group of package versions sharing the same package ID.</span></span>
<span data-ttu-id="8eb3a-188">Nesne, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8eb3a-188">The object has the following properties:</span></span>

<span data-ttu-id="8eb3a-189">Ad</span><span class="sxs-lookup"><span data-stu-id="8eb3a-189">Name</span></span>           | <span data-ttu-id="8eb3a-190">Tür</span><span class="sxs-lookup"><span data-stu-id="8eb3a-190">Type</span></span>                       | <span data-ttu-id="8eb3a-191">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8eb3a-191">Required</span></span> | <span data-ttu-id="8eb3a-192">Notlar</span><span class="sxs-lookup"><span data-stu-id="8eb3a-192">Notes</span></span>
-------------- | -------------------------- | -------- | -----
<span data-ttu-id="8eb3a-193">kimlik</span><span class="sxs-lookup"><span data-stu-id="8eb3a-193">id</span></span>             | <span data-ttu-id="8eb3a-194">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-194">string</span></span>                     | <span data-ttu-id="8eb3a-195">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-195">yes</span></span>      | <span data-ttu-id="8eb3a-196">Eşleşen paket kimliği</span><span class="sxs-lookup"><span data-stu-id="8eb3a-196">The ID of the matched package</span></span>
<span data-ttu-id="8eb3a-197">sürüm</span><span class="sxs-lookup"><span data-stu-id="8eb3a-197">version</span></span>        | <span data-ttu-id="8eb3a-198">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-198">string</span></span>                     | <span data-ttu-id="8eb3a-199">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-199">yes</span></span>      | <span data-ttu-id="8eb3a-200">Tam SemVer 2.0.0 sürüm dizesi (derleme meta verilerini içerebilir) paketi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-200">The full SemVer 2.0.0 version string of the package (could contain build metadata)</span></span>
<span data-ttu-id="8eb3a-201">açıklama</span><span class="sxs-lookup"><span data-stu-id="8eb3a-201">description</span></span>    | <span data-ttu-id="8eb3a-202">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-202">string</span></span>                     | <span data-ttu-id="8eb3a-203">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-203">no</span></span>       | 
<span data-ttu-id="8eb3a-204">sürümler</span><span class="sxs-lookup"><span data-stu-id="8eb3a-204">versions</span></span>       | <span data-ttu-id="8eb3a-205">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-205">array of objects</span></span>           | <span data-ttu-id="8eb3a-206">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-206">yes</span></span>      | <span data-ttu-id="8eb3a-207">Tüm paket eşleşen sürümlerinin `prerelease` parametresi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-207">All of the versions of the package matching the `prerelease` parameter</span></span>
<span data-ttu-id="8eb3a-208">yazarları</span><span class="sxs-lookup"><span data-stu-id="8eb3a-208">authors</span></span>        | <span data-ttu-id="8eb3a-209">dize veya dize dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-209">string or array of strings</span></span> | <span data-ttu-id="8eb3a-210">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-210">no</span></span>       | 
<span data-ttu-id="8eb3a-211">iconUrl</span><span class="sxs-lookup"><span data-stu-id="8eb3a-211">iconUrl</span></span>        | <span data-ttu-id="8eb3a-212">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-212">string</span></span>                     | <span data-ttu-id="8eb3a-213">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-213">no</span></span>       | 
<span data-ttu-id="8eb3a-214">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="8eb3a-214">licenseUrl</span></span>     | <span data-ttu-id="8eb3a-215">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-215">string</span></span>                     | <span data-ttu-id="8eb3a-216">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-216">no</span></span>       | 
<span data-ttu-id="8eb3a-217">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-217">owners</span></span>         | <span data-ttu-id="8eb3a-218">dize veya dize dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-218">string or array of strings</span></span> | <span data-ttu-id="8eb3a-219">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-219">no</span></span>       | 
<span data-ttu-id="8eb3a-220">projectUrl</span><span class="sxs-lookup"><span data-stu-id="8eb3a-220">projectUrl</span></span>     | <span data-ttu-id="8eb3a-221">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-221">string</span></span>                     | <span data-ttu-id="8eb3a-222">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-222">no</span></span>       | 
<span data-ttu-id="8eb3a-223">kayıt</span><span class="sxs-lookup"><span data-stu-id="8eb3a-223">registration</span></span>   | <span data-ttu-id="8eb3a-224">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-224">string</span></span>                     | <span data-ttu-id="8eb3a-225">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-225">no</span></span>       | <span data-ttu-id="8eb3a-226">İlişkili için mutlak URL [kayıt dizini](registration-base-url-resource.md#registration-index)</span><span class="sxs-lookup"><span data-stu-id="8eb3a-226">The absolute URL to the associated [registration index](registration-base-url-resource.md#registration-index)</span></span>
<span data-ttu-id="8eb3a-227">özet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-227">summary</span></span>        | <span data-ttu-id="8eb3a-228">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-228">string</span></span>                     | <span data-ttu-id="8eb3a-229">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-229">no</span></span>       | 
<span data-ttu-id="8eb3a-230">etiketler</span><span class="sxs-lookup"><span data-stu-id="8eb3a-230">tags</span></span>           | <span data-ttu-id="8eb3a-231">dize veya dize dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-231">string or array of strings</span></span> | <span data-ttu-id="8eb3a-232">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-232">no</span></span>       | 
<span data-ttu-id="8eb3a-233">title</span><span class="sxs-lookup"><span data-stu-id="8eb3a-233">title</span></span>          | <span data-ttu-id="8eb3a-234">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-234">string</span></span>                     | <span data-ttu-id="8eb3a-235">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-235">no</span></span>       | 
<span data-ttu-id="8eb3a-236">totalDownloads</span><span class="sxs-lookup"><span data-stu-id="8eb3a-236">totalDownloads</span></span> | <span data-ttu-id="8eb3a-237">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-237">integer</span></span>                    | <span data-ttu-id="8eb3a-238">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-238">no</span></span>       | <span data-ttu-id="8eb3a-239">Bu değer yüklemeler toplamına çıkarsanabileceği `versions` dizisi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-239">This value can be inferred by the sum of downloads in the `versions` array</span></span>
<span data-ttu-id="8eb3a-240">Doğrulandı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-240">verified</span></span>       | <span data-ttu-id="8eb3a-241">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-241">boolean</span></span>                    | <span data-ttu-id="8eb3a-242">Yok</span><span class="sxs-lookup"><span data-stu-id="8eb3a-242">no</span></span>       | <span data-ttu-id="8eb3a-243">Paket olup olmadığını belirten bir JSON Boole [doğrulandı](../reference/id-prefix-reservation.md)</span><span class="sxs-lookup"><span data-stu-id="8eb3a-243">A JSON boolean indicating whether the package is [verified](../reference/id-prefix-reservation.md)</span></span>

<span data-ttu-id="8eb3a-244">Nuget.org üzerinde bir doğrulanmış ayrılmış kimliği öneki eşleşen bir paket Kimliğine sahip ve ayrılmış ad 's sahiplerinden biri tarafından sahip olunan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-244">On nuget.org, a verified package is one which has a package ID matching a reserved ID prefix and owned by one of the reserved namespace's owners.</span></span> <span data-ttu-id="8eb3a-245">Daha fazla bilgi için bkz: [kimliği öneki ayırma ile ilgili belgeler](../reference/id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="8eb3a-245">For more information, see the [documentation about ID prefix reservation](../reference/id-prefix-reservation.md).</span></span>

<span data-ttu-id="8eb3a-246">Son paket sürümünden arama sonuç nesnesinde bulunan meta veriler alınır.</span><span class="sxs-lookup"><span data-stu-id="8eb3a-246">The metadata contained in the search result object is taken from the latest package version.</span></span> <span data-ttu-id="8eb3a-247">Her öğe `versions` dizidir aşağıdaki özelliklere sahip bir JSON nesnesi:</span><span class="sxs-lookup"><span data-stu-id="8eb3a-247">Each item in the `versions` array is a JSON object with the following properties:</span></span>

<span data-ttu-id="8eb3a-248">Ad</span><span class="sxs-lookup"><span data-stu-id="8eb3a-248">Name</span></span>      | <span data-ttu-id="8eb3a-249">Tür</span><span class="sxs-lookup"><span data-stu-id="8eb3a-249">Type</span></span>    | <span data-ttu-id="8eb3a-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8eb3a-250">Required</span></span> | <span data-ttu-id="8eb3a-251">Notlar</span><span class="sxs-lookup"><span data-stu-id="8eb3a-251">Notes</span></span>
--------- | ------- | -------- | -----
@id       | <span data-ttu-id="8eb3a-252">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-252">string</span></span>  | <span data-ttu-id="8eb3a-253">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-253">yes</span></span>      | <span data-ttu-id="8eb3a-254">İlişkili için mutlak URL [kayıt yaprak](registration-base-url-resource.md#registration-leaf)</span><span class="sxs-lookup"><span data-stu-id="8eb3a-254">The absolute URL to the associated [registration leaf](registration-base-url-resource.md#registration-leaf)</span></span>
<span data-ttu-id="8eb3a-255">sürüm</span><span class="sxs-lookup"><span data-stu-id="8eb3a-255">version</span></span>   | <span data-ttu-id="8eb3a-256">dize</span><span class="sxs-lookup"><span data-stu-id="8eb3a-256">string</span></span>  | <span data-ttu-id="8eb3a-257">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-257">yes</span></span>      | <span data-ttu-id="8eb3a-258">Tam SemVer 2.0.0 sürüm dizesi (derleme meta verilerini içerebilir) paketi</span><span class="sxs-lookup"><span data-stu-id="8eb3a-258">The full SemVer 2.0.0 version string of the package (could contain build metadata)</span></span>
<span data-ttu-id="8eb3a-259">Yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="8eb3a-259">downloads</span></span> | <span data-ttu-id="8eb3a-260">tamsayı</span><span class="sxs-lookup"><span data-stu-id="8eb3a-260">integer</span></span> | <span data-ttu-id="8eb3a-261">Evet</span><span class="sxs-lookup"><span data-stu-id="8eb3a-261">yes</span></span>      | <span data-ttu-id="8eb3a-262">Bu belirli Paket sürümü için indirme</span><span class="sxs-lookup"><span data-stu-id="8eb3a-262">The number of downloads for this specific package version</span></span>

### <a name="sample-request"></a><span data-ttu-id="8eb3a-263">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="8eb3a-263">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a><span data-ttu-id="8eb3a-264">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="8eb3a-264">Sample response</span></span>

[!code-JSON [search-result.json](./_data/search-result.json)]