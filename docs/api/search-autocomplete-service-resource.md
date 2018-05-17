---
title: Otomatik Tamamlama, NuGet API
description: Arama otomatik tamamlama hizmeti paketi kimlikleri etkileşimli bulma ve sürümleri destekler.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="autocomplete"></a><span data-ttu-id="03978-103">Otomatik Tamamlama</span><span class="sxs-lookup"><span data-stu-id="03978-103">Autocomplete</span></span>

<span data-ttu-id="03978-104">V3 API kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyim oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="03978-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="03978-105">Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="03978-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="03978-106">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="03978-106">Versioning</span></span>

<span data-ttu-id="03978-107">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="03978-107">The following `@type` values are used:</span></span>

<span data-ttu-id="03978-108">@type Değer</span><span class="sxs-lookup"><span data-stu-id="03978-108">@type value</span></span>                          | <span data-ttu-id="03978-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="03978-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="03978-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="03978-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="03978-111">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="03978-111">The initial release</span></span>
<span data-ttu-id="03978-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="03978-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="03978-113">Diğer adı `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="03978-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="03978-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="03978-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="03978-115">Diğer adı `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="03978-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="03978-116">Temel URL</span><span class="sxs-lookup"><span data-stu-id="03978-116">Base URL</span></span>

<span data-ttu-id="03978-117">Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="03978-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="03978-118">Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03978-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="03978-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="03978-119">HTTP Methods</span></span>

<span data-ttu-id="03978-120">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="03978-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="03978-121">Paket kimlikleri için arama</span><span class="sxs-lookup"><span data-stu-id="03978-121">Search for package IDs</span></span>

<span data-ttu-id="03978-122">Bir paket kimliği dizesi bir kısmı için arama ilk otomatik tamamlama API destekler.</span><span class="sxs-lookup"><span data-stu-id="03978-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="03978-123">Bir paketi typeahead özelliği ile bir NuGet paketi kaynağı tümleşik kullanıcı arabiriminde sağlamak istediğinizde mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="03978-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="03978-124">Yalnızca listede bulunmayan sürümleri ile bir pakete sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="03978-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="03978-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="03978-125">Request parameters</span></span>

<span data-ttu-id="03978-126">Ad</span><span class="sxs-lookup"><span data-stu-id="03978-126">Name</span></span>        | <span data-ttu-id="03978-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="03978-127">In</span></span>     | <span data-ttu-id="03978-128">Tür</span><span class="sxs-lookup"><span data-stu-id="03978-128">Type</span></span>    | <span data-ttu-id="03978-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03978-129">Required</span></span> | <span data-ttu-id="03978-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="03978-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="03978-131">q</span><span class="sxs-lookup"><span data-stu-id="03978-131">q</span></span>           | <span data-ttu-id="03978-132">URL</span><span class="sxs-lookup"><span data-stu-id="03978-132">URL</span></span>    | <span data-ttu-id="03978-133">dize</span><span class="sxs-lookup"><span data-stu-id="03978-133">string</span></span>  | <span data-ttu-id="03978-134">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-134">no</span></span>       | <span data-ttu-id="03978-135">Paket kimlikleri karşı karşılaştırmak için dize</span><span class="sxs-lookup"><span data-stu-id="03978-135">The string to compare against package IDs</span></span>
<span data-ttu-id="03978-136">Atla</span><span class="sxs-lookup"><span data-stu-id="03978-136">skip</span></span>        | <span data-ttu-id="03978-137">URL</span><span class="sxs-lookup"><span data-stu-id="03978-137">URL</span></span>    | <span data-ttu-id="03978-138">tamsayı</span><span class="sxs-lookup"><span data-stu-id="03978-138">integer</span></span> | <span data-ttu-id="03978-139">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-139">no</span></span>       | <span data-ttu-id="03978-140">Sayfa numaralandırma için atlamayı sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="03978-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="03978-141">Al</span><span class="sxs-lookup"><span data-stu-id="03978-141">take</span></span>        | <span data-ttu-id="03978-142">URL</span><span class="sxs-lookup"><span data-stu-id="03978-142">URL</span></span>    | <span data-ttu-id="03978-143">tamsayı</span><span class="sxs-lookup"><span data-stu-id="03978-143">integer</span></span> | <span data-ttu-id="03978-144">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-144">no</span></span>       | <span data-ttu-id="03978-145">Sayfa numaralandırma için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="03978-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="03978-146">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="03978-146">prerelease</span></span>  | <span data-ttu-id="03978-147">URL</span><span class="sxs-lookup"><span data-stu-id="03978-147">URL</span></span>    | <span data-ttu-id="03978-148">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="03978-148">boolean</span></span> | <span data-ttu-id="03978-149">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-149">no</span></span>       | <span data-ttu-id="03978-150">`true` veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="03978-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="03978-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="03978-151">semVerLevel</span></span> | <span data-ttu-id="03978-152">URL</span><span class="sxs-lookup"><span data-stu-id="03978-152">URL</span></span>    | <span data-ttu-id="03978-153">dize</span><span class="sxs-lookup"><span data-stu-id="03978-153">string</span></span>  | <span data-ttu-id="03978-154">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-154">no</span></span>       | <span data-ttu-id="03978-155">SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="03978-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="03978-156">Otomatik Tamamlama sorgu `q` sunucu uygulaması tarafından tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="03978-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="03978-157">nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri önek özgün ortası büyük harf ve sembol karakterlerinin sorgulanırken destekler.</span><span class="sxs-lookup"><span data-stu-id="03978-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="03978-158">`skip` Parametresi varsayılan ayar: 0.</span><span class="sxs-lookup"><span data-stu-id="03978-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="03978-159">`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="03978-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="03978-160">Sunucu uygulaması bir maksimum değer yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="03978-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="03978-161">Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03978-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="03978-162">`semVerLevel` Sorgu parametresi için katılımı için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="03978-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="03978-163">Bu sorgu parametresi dışlanırsa, yalnızca paketinin kimlikleri SemVer 1.0.0 uyumlu sürümlerini döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar 4 tamsayı parçalı sürüm dizeler gibi).</span><span class="sxs-lookup"><span data-stu-id="03978-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="03978-164">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03978-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="03978-165">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="03978-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="03978-166">Yanıt</span><span class="sxs-lookup"><span data-stu-id="03978-166">Response</span></span>

<span data-ttu-id="03978-167">Yanıt kadar içeren JSON belgedir `take` otomatik tamamlama sonuçları.</span><span class="sxs-lookup"><span data-stu-id="03978-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="03978-168">Kök JSON nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="03978-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="03978-169">Ad</span><span class="sxs-lookup"><span data-stu-id="03978-169">Name</span></span>      | <span data-ttu-id="03978-170">Tür</span><span class="sxs-lookup"><span data-stu-id="03978-170">Type</span></span>             | <span data-ttu-id="03978-171">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03978-171">Required</span></span> | <span data-ttu-id="03978-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="03978-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="03978-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="03978-173">totalHits</span></span> | <span data-ttu-id="03978-174">tamsayı</span><span class="sxs-lookup"><span data-stu-id="03978-174">integer</span></span>          | <span data-ttu-id="03978-175">Evet</span><span class="sxs-lookup"><span data-stu-id="03978-175">yes</span></span>      | <span data-ttu-id="03978-176">Atlayıp eşleşirse, toplam sayısı `skip` ve `take`</span><span class="sxs-lookup"><span data-stu-id="03978-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="03978-177">veri</span><span class="sxs-lookup"><span data-stu-id="03978-177">data</span></span>      | <span data-ttu-id="03978-178">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="03978-178">array of strings</span></span> | <span data-ttu-id="03978-179">Evet</span><span class="sxs-lookup"><span data-stu-id="03978-179">yes</span></span>      | <span data-ttu-id="03978-180">Paket kimlikleri istek tarafından eşleşti.</span><span class="sxs-lookup"><span data-stu-id="03978-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="03978-181">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="03978-181">Sample request</span></span>

<span data-ttu-id="03978-182">AL https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="03978-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="03978-183">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="03978-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="03978-184">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="03978-184">Enumerate package versions</span></span>

<span data-ttu-id="03978-185">Bir paket kimliği önceki API'yi kullanarak bulununca, istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerinin Numaralandırılacak kullanabilir</span><span class="sxs-lookup"><span data-stu-id="03978-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="03978-186">Listede bulunmayan bir paket sürümü sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="03978-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="03978-187">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="03978-187">Request parameters</span></span>

<span data-ttu-id="03978-188">Ad</span><span class="sxs-lookup"><span data-stu-id="03978-188">Name</span></span>        | <span data-ttu-id="03978-189">İçindeki</span><span class="sxs-lookup"><span data-stu-id="03978-189">In</span></span>     | <span data-ttu-id="03978-190">Tür</span><span class="sxs-lookup"><span data-stu-id="03978-190">Type</span></span>    | <span data-ttu-id="03978-191">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03978-191">Required</span></span> | <span data-ttu-id="03978-192">Notlar</span><span class="sxs-lookup"><span data-stu-id="03978-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="03978-193">kimlik</span><span class="sxs-lookup"><span data-stu-id="03978-193">id</span></span>          | <span data-ttu-id="03978-194">URL</span><span class="sxs-lookup"><span data-stu-id="03978-194">URL</span></span>    | <span data-ttu-id="03978-195">dize</span><span class="sxs-lookup"><span data-stu-id="03978-195">string</span></span>  | <span data-ttu-id="03978-196">Evet</span><span class="sxs-lookup"><span data-stu-id="03978-196">yes</span></span>      | <span data-ttu-id="03978-197">Sürümleri için getirmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="03978-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="03978-198">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="03978-198">prerelease</span></span>  | <span data-ttu-id="03978-199">URL</span><span class="sxs-lookup"><span data-stu-id="03978-199">URL</span></span>    | <span data-ttu-id="03978-200">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="03978-200">boolean</span></span> | <span data-ttu-id="03978-201">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-201">no</span></span>       | <span data-ttu-id="03978-202">`true` veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="03978-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="03978-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="03978-203">semVerLevel</span></span> | <span data-ttu-id="03978-204">URL</span><span class="sxs-lookup"><span data-stu-id="03978-204">URL</span></span>    | <span data-ttu-id="03978-205">dize</span><span class="sxs-lookup"><span data-stu-id="03978-205">string</span></span>  | <span data-ttu-id="03978-206">Yok</span><span class="sxs-lookup"><span data-stu-id="03978-206">no</span></span>       | <span data-ttu-id="03978-207">SemVer 2.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="03978-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="03978-208">Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03978-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="03978-209">`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03978-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="03978-210">Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="03978-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="03978-211">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 sürümleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="03978-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="03978-212">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="03978-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="03978-213">Yanıt</span><span class="sxs-lookup"><span data-stu-id="03978-213">Response</span></span>

<span data-ttu-id="03978-214">Yanıt, verilen sorgu parametreleri tarafından filtreleme sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgedir.</span><span class="sxs-lookup"><span data-stu-id="03978-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="03978-215">Kök JSON nesnesi aşağıdaki özelliğine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="03978-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="03978-216">Ad</span><span class="sxs-lookup"><span data-stu-id="03978-216">Name</span></span>      | <span data-ttu-id="03978-217">Tür</span><span class="sxs-lookup"><span data-stu-id="03978-217">Type</span></span>             | <span data-ttu-id="03978-218">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03978-218">Required</span></span> | <span data-ttu-id="03978-219">Notlar</span><span class="sxs-lookup"><span data-stu-id="03978-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="03978-220">veri</span><span class="sxs-lookup"><span data-stu-id="03978-220">data</span></span>      | <span data-ttu-id="03978-221">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="03978-221">array of strings</span></span> | <span data-ttu-id="03978-222">Evet</span><span class="sxs-lookup"><span data-stu-id="03978-222">yes</span></span>      | <span data-ttu-id="03978-223">İstek tarafından eşleşen paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="03978-223">The package versions matched by the request</span></span>

<span data-ttu-id="03978-224">Paket sürümlerde `data` dizi SemVer 2.0.0 derleme meta verilerini içerebilir (örneğin `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.</span><span class="sxs-lookup"><span data-stu-id="03978-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="03978-225">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="03978-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="03978-226">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="03978-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
