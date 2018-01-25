---
title: Otomatik Tamamlama, NuGet API | Microsoft Docs
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
description: "Arama otomatik tamamlama hizmeti paketi kimlikleri etkileşimli bulma ve sürümleri destekler."
keywords: "NuGet otomatik tamamlama API, NuGet arama paket kimliği, substring paket kimliği"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a><span data-ttu-id="d1f81-104">Otomatik Tamamlama</span><span class="sxs-lookup"><span data-stu-id="d1f81-104">Autocomplete</span></span>

<span data-ttu-id="d1f81-105">V3 API kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyim oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d1f81-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d1f81-106">Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d1f81-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d1f81-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1f81-107">Versioning</span></span>

<span data-ttu-id="d1f81-108">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d1f81-108">The following `@type` values are used:</span></span>

<span data-ttu-id="d1f81-109">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="d1f81-109">@type value</span></span>                          | <span data-ttu-id="d1f81-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="d1f81-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d1f81-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d1f81-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="d1f81-112">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="d1f81-112">The initial release</span></span>
<span data-ttu-id="d1f81-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d1f81-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d1f81-114">Diğer adı`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d1f81-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d1f81-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d1f81-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d1f81-116">Diğer adı`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d1f81-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d1f81-117">Temel URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-117">Base URL</span></span>

<span data-ttu-id="d1f81-118">Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="d1f81-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d1f81-119">Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d1f81-120">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="d1f81-120">HTTP Methods</span></span>

<span data-ttu-id="d1f81-121">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d1f81-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d1f81-122">Paket kimlikleri için arama</span><span class="sxs-lookup"><span data-stu-id="d1f81-122">Search for package IDs</span></span>

<span data-ttu-id="d1f81-123">Bir paket kimliği dizesi bir kısmı için arama ilk otomatik tamamlama API destekler.</span><span class="sxs-lookup"><span data-stu-id="d1f81-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d1f81-124">Bir paketi typeahead özelliği ile bir NuGet paketi kaynağı tümleşik kullanıcı arabiriminde sağlamak istediğinizde mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="d1f81-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d1f81-125">Yalnızca listede bulunmayan sürümleri ile bir pakete sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="d1f81-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d1f81-126">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1f81-126">Request parameters</span></span>

<span data-ttu-id="d1f81-127">Ad</span><span class="sxs-lookup"><span data-stu-id="d1f81-127">Name</span></span>        | <span data-ttu-id="d1f81-128">İçindeki</span><span class="sxs-lookup"><span data-stu-id="d1f81-128">In</span></span>     | <span data-ttu-id="d1f81-129">Tür</span><span class="sxs-lookup"><span data-stu-id="d1f81-129">Type</span></span>    | <span data-ttu-id="d1f81-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d1f81-130">Required</span></span> | <span data-ttu-id="d1f81-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="d1f81-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d1f81-132">q</span><span class="sxs-lookup"><span data-stu-id="d1f81-132">q</span></span>           | <span data-ttu-id="d1f81-133">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-133">URL</span></span>    | <span data-ttu-id="d1f81-134">dize</span><span class="sxs-lookup"><span data-stu-id="d1f81-134">string</span></span>  | <span data-ttu-id="d1f81-135">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-135">no</span></span>       | <span data-ttu-id="d1f81-136">Paket kimlikleri karşı karşılaştırmak için dize</span><span class="sxs-lookup"><span data-stu-id="d1f81-136">The string to compare against package IDs</span></span>
<span data-ttu-id="d1f81-137">Atla</span><span class="sxs-lookup"><span data-stu-id="d1f81-137">skip</span></span>        | <span data-ttu-id="d1f81-138">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-138">URL</span></span>    | <span data-ttu-id="d1f81-139">tamsayı</span><span class="sxs-lookup"><span data-stu-id="d1f81-139">integer</span></span> | <span data-ttu-id="d1f81-140">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-140">no</span></span>       | <span data-ttu-id="d1f81-141">Sayfa numaralandırma için atlamayı sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="d1f81-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d1f81-142">Al</span><span class="sxs-lookup"><span data-stu-id="d1f81-142">take</span></span>        | <span data-ttu-id="d1f81-143">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-143">URL</span></span>    | <span data-ttu-id="d1f81-144">tamsayı</span><span class="sxs-lookup"><span data-stu-id="d1f81-144">integer</span></span> | <span data-ttu-id="d1f81-145">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-145">no</span></span>       | <span data-ttu-id="d1f81-146">Sayfa numaralandırma için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="d1f81-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="d1f81-147">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="d1f81-147">prerelease</span></span>  | <span data-ttu-id="d1f81-148">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-148">URL</span></span>    | <span data-ttu-id="d1f81-149">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="d1f81-149">boolean</span></span> | <span data-ttu-id="d1f81-150">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-150">no</span></span>       | <span data-ttu-id="d1f81-151">`true`veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d1f81-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d1f81-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d1f81-152">semVerLevel</span></span> | <span data-ttu-id="d1f81-153">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-153">URL</span></span>    | <span data-ttu-id="d1f81-154">dize</span><span class="sxs-lookup"><span data-stu-id="d1f81-154">string</span></span>  | <span data-ttu-id="d1f81-155">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-155">no</span></span>       | <span data-ttu-id="d1f81-156">SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="d1f81-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d1f81-157">Otomatik Tamamlama sorgu `q` sunucu uygulaması tarafından tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d1f81-158">nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri önek özgün ortası büyük harf ve sembol karakterlerinin sorgulanırken destekler.</span><span class="sxs-lookup"><span data-stu-id="d1f81-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d1f81-159">`skip` Parametresi varsayılan ayar: 0.</span><span class="sxs-lookup"><span data-stu-id="d1f81-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d1f81-160">`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d1f81-161">Sunucu uygulaması bir maksimum değer yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d1f81-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d1f81-162">Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d1f81-163">`semVerLevel` Sorgu parametresi için katılımı için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d1f81-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d1f81-164">Bu sorgu parametresi dışlanırsa, yalnızca paketinin kimlikleri SemVer 1.0.0 uyumlu sürümlerini döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar 4 tamsayı parçalı sürüm dizeler gibi).</span><span class="sxs-lookup"><span data-stu-id="d1f81-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d1f81-165">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d1f81-166">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d1f81-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d1f81-167">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d1f81-167">Response</span></span>

<span data-ttu-id="d1f81-168">Yanıt kadar içeren JSON belgedir `take` otomatik tamamlama sonuçları.</span><span class="sxs-lookup"><span data-stu-id="d1f81-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d1f81-169">Kök JSON nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d1f81-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d1f81-170">Ad</span><span class="sxs-lookup"><span data-stu-id="d1f81-170">Name</span></span>      | <span data-ttu-id="d1f81-171">Tür</span><span class="sxs-lookup"><span data-stu-id="d1f81-171">Type</span></span>             | <span data-ttu-id="d1f81-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d1f81-172">Required</span></span> | <span data-ttu-id="d1f81-173">Notlar</span><span class="sxs-lookup"><span data-stu-id="d1f81-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d1f81-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="d1f81-174">totalHits</span></span> | <span data-ttu-id="d1f81-175">tamsayı</span><span class="sxs-lookup"><span data-stu-id="d1f81-175">integer</span></span>          | <span data-ttu-id="d1f81-176">Evet</span><span class="sxs-lookup"><span data-stu-id="d1f81-176">yes</span></span>      | <span data-ttu-id="d1f81-177">Atlayıp eşleşirse, toplam sayısı `skip` ve`take`</span><span class="sxs-lookup"><span data-stu-id="d1f81-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d1f81-178">veri</span><span class="sxs-lookup"><span data-stu-id="d1f81-178">data</span></span>      | <span data-ttu-id="d1f81-179">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="d1f81-179">array of strings</span></span> | <span data-ttu-id="d1f81-180">Evet</span><span class="sxs-lookup"><span data-stu-id="d1f81-180">yes</span></span>      | <span data-ttu-id="d1f81-181">Paket kimlikleri istek tarafından eşleşti.</span><span class="sxs-lookup"><span data-stu-id="d1f81-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d1f81-182">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="d1f81-182">Sample request</span></span>

<span data-ttu-id="d1f81-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="d1f81-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="d1f81-184">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="d1f81-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d1f81-185">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="d1f81-185">Enumerate package versions</span></span>

<span data-ttu-id="d1f81-186">Bir paket kimliği önceki API'yi kullanarak bulununca, istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerinin Numaralandırılacak kullanabilir</span><span class="sxs-lookup"><span data-stu-id="d1f81-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d1f81-187">Listede bulunmayan bir paket sürümü sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="d1f81-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d1f81-188">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1f81-188">Request parameters</span></span>

<span data-ttu-id="d1f81-189">Ad</span><span class="sxs-lookup"><span data-stu-id="d1f81-189">Name</span></span>        | <span data-ttu-id="d1f81-190">İçindeki</span><span class="sxs-lookup"><span data-stu-id="d1f81-190">In</span></span>     | <span data-ttu-id="d1f81-191">Tür</span><span class="sxs-lookup"><span data-stu-id="d1f81-191">Type</span></span>    | <span data-ttu-id="d1f81-192">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d1f81-192">Required</span></span> | <span data-ttu-id="d1f81-193">Notlar</span><span class="sxs-lookup"><span data-stu-id="d1f81-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d1f81-194">kimlik</span><span class="sxs-lookup"><span data-stu-id="d1f81-194">id</span></span>          | <span data-ttu-id="d1f81-195">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-195">URL</span></span>    | <span data-ttu-id="d1f81-196">dize</span><span class="sxs-lookup"><span data-stu-id="d1f81-196">string</span></span>  | <span data-ttu-id="d1f81-197">Evet</span><span class="sxs-lookup"><span data-stu-id="d1f81-197">yes</span></span>      | <span data-ttu-id="d1f81-198">Sürümleri için getirmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="d1f81-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="d1f81-199">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="d1f81-199">prerelease</span></span>  | <span data-ttu-id="d1f81-200">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-200">URL</span></span>    | <span data-ttu-id="d1f81-201">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="d1f81-201">boolean</span></span> | <span data-ttu-id="d1f81-202">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-202">no</span></span>       | <span data-ttu-id="d1f81-203">`true`veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d1f81-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d1f81-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d1f81-204">semVerLevel</span></span> | <span data-ttu-id="d1f81-205">URL</span><span class="sxs-lookup"><span data-stu-id="d1f81-205">URL</span></span>    | <span data-ttu-id="d1f81-206">dize</span><span class="sxs-lookup"><span data-stu-id="d1f81-206">string</span></span>  | <span data-ttu-id="d1f81-207">Yok</span><span class="sxs-lookup"><span data-stu-id="d1f81-207">no</span></span>       | <span data-ttu-id="d1f81-208">SemVer 2.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="d1f81-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d1f81-209">Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d1f81-210">`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d1f81-211">Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d1f81-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d1f81-212">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 sürümleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d1f81-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d1f81-213">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d1f81-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d1f81-214">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d1f81-214">Response</span></span>

<span data-ttu-id="d1f81-215">Yanıt, verilen sorgu parametreleri tarafından filtreleme sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgedir.</span><span class="sxs-lookup"><span data-stu-id="d1f81-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d1f81-216">Kök JSON nesnesi aşağıdaki özelliğine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d1f81-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="d1f81-217">Ad</span><span class="sxs-lookup"><span data-stu-id="d1f81-217">Name</span></span>      | <span data-ttu-id="d1f81-218">Tür</span><span class="sxs-lookup"><span data-stu-id="d1f81-218">Type</span></span>             | <span data-ttu-id="d1f81-219">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d1f81-219">Required</span></span> | <span data-ttu-id="d1f81-220">Notlar</span><span class="sxs-lookup"><span data-stu-id="d1f81-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d1f81-221">veri</span><span class="sxs-lookup"><span data-stu-id="d1f81-221">data</span></span>      | <span data-ttu-id="d1f81-222">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="d1f81-222">array of strings</span></span> | <span data-ttu-id="d1f81-223">Evet</span><span class="sxs-lookup"><span data-stu-id="d1f81-223">yes</span></span>      | <span data-ttu-id="d1f81-224">İstek tarafından eşleşen paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="d1f81-224">The package versions matched by the request</span></span>

<span data-ttu-id="d1f81-225">Paket sürümlerde `data` dizi SemVer 2.0.0 derleme meta verilerini içerebilir (örneğin `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.</span><span class="sxs-lookup"><span data-stu-id="d1f81-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d1f81-226">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="d1f81-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d1f81-227">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="d1f81-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
