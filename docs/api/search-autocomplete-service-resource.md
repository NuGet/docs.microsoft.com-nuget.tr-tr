---
title: Otomatik Tamamlama, NuGet API'si
description: Arama otomatik tamamlama hizmeti etkileşimli olarak paket kimlikleri bulunmasını ve sürümleri destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549089"
---
# <a name="autocomplete"></a><span data-ttu-id="86dc4-103">Otomatik Tamamlama</span><span class="sxs-lookup"><span data-stu-id="86dc4-103">Autocomplete</span></span>

<span data-ttu-id="86dc4-104">V3 API'sini kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyimi oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="86dc4-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="86dc4-105">Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="86dc4-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="86dc4-106">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="86dc4-106">Versioning</span></span>

<span data-ttu-id="86dc4-107">Aşağıdaki `@type` değerleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="86dc4-107">The following `@type` values are used:</span></span>

<span data-ttu-id="86dc4-108">@type Değer</span><span class="sxs-lookup"><span data-stu-id="86dc4-108">@type value</span></span>                          | <span data-ttu-id="86dc4-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="86dc4-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="86dc4-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="86dc4-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="86dc4-111">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="86dc4-111">The initial release</span></span>
<span data-ttu-id="86dc4-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="86dc4-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="86dc4-113">Diğer adı `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="86dc4-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="86dc4-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="86dc4-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="86dc4-115">Diğer adı `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="86dc4-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="86dc4-116">Temel URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-116">Base URL</span></span>

<span data-ttu-id="86dc4-117">Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="86dc4-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="86dc4-118">Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="86dc4-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="86dc4-119">HTTP Methods</span></span>

<span data-ttu-id="86dc4-120">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="86dc4-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="86dc4-121">Paket kimlikleri için arama</span><span class="sxs-lookup"><span data-stu-id="86dc4-121">Search for package IDs</span></span>

<span data-ttu-id="86dc4-122">Bir paket kimliği dizesi bir parçası için arama ilk otomatik tamamlama API'sini destekler.</span><span class="sxs-lookup"><span data-stu-id="86dc4-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="86dc4-123">NuGet paket kaynağı ile tümleşik kullanıcı arabiriminde bir paket typeahead özelliği sağlamak istediğinizde mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="86dc4-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="86dc4-124">Yalnızca listede bulunmayan sürümler ile bir pakete sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="86dc4-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="86dc4-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="86dc4-125">Request parameters</span></span>

<span data-ttu-id="86dc4-126">Ad</span><span class="sxs-lookup"><span data-stu-id="86dc4-126">Name</span></span>        | <span data-ttu-id="86dc4-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="86dc4-127">In</span></span>     | <span data-ttu-id="86dc4-128">Tür</span><span class="sxs-lookup"><span data-stu-id="86dc4-128">Type</span></span>    | <span data-ttu-id="86dc4-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86dc4-129">Required</span></span> | <span data-ttu-id="86dc4-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="86dc4-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="86dc4-131">q</span><span class="sxs-lookup"><span data-stu-id="86dc4-131">q</span></span>           | <span data-ttu-id="86dc4-132">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-132">URL</span></span>    | <span data-ttu-id="86dc4-133">dize</span><span class="sxs-lookup"><span data-stu-id="86dc4-133">string</span></span>  | <span data-ttu-id="86dc4-134">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-134">no</span></span>       | <span data-ttu-id="86dc4-135">Paket kimlikleri karşı Karşılaştırılacak dize</span><span class="sxs-lookup"><span data-stu-id="86dc4-135">The string to compare against package IDs</span></span>
<span data-ttu-id="86dc4-136">Atla</span><span class="sxs-lookup"><span data-stu-id="86dc4-136">skip</span></span>        | <span data-ttu-id="86dc4-137">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-137">URL</span></span>    | <span data-ttu-id="86dc4-138">tamsayı</span><span class="sxs-lookup"><span data-stu-id="86dc4-138">integer</span></span> | <span data-ttu-id="86dc4-139">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-139">no</span></span>       | <span data-ttu-id="86dc4-140">İçin sayfalandırma atlanacak sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="86dc4-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="86dc4-141">sınav zamanı</span><span class="sxs-lookup"><span data-stu-id="86dc4-141">take</span></span>        | <span data-ttu-id="86dc4-142">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-142">URL</span></span>    | <span data-ttu-id="86dc4-143">tamsayı</span><span class="sxs-lookup"><span data-stu-id="86dc4-143">integer</span></span> | <span data-ttu-id="86dc4-144">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-144">no</span></span>       | <span data-ttu-id="86dc4-145">Sayfalandırma için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="86dc4-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="86dc4-146">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="86dc4-146">prerelease</span></span>  | <span data-ttu-id="86dc4-147">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-147">URL</span></span>    | <span data-ttu-id="86dc4-148">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="86dc4-148">boolean</span></span> | <span data-ttu-id="86dc4-149">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-149">no</span></span>       | <span data-ttu-id="86dc4-150">`true` veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="86dc4-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="86dc4-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="86dc4-151">semVerLevel</span></span> | <span data-ttu-id="86dc4-152">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-152">URL</span></span>    | <span data-ttu-id="86dc4-153">dize</span><span class="sxs-lookup"><span data-stu-id="86dc4-153">string</span></span>  | <span data-ttu-id="86dc4-154">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-154">no</span></span>       | <span data-ttu-id="86dc4-155">Bir SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="86dc4-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="86dc4-156">Otomatik Tamamlama sorgu `q` sunucu uygulama tarafından tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="86dc4-157">nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri öneki özgün camel çalışması ve sembol karakterlerinin sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="86dc4-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="86dc4-158">`skip` 0 varsayılan parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="86dc4-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="86dc4-159">`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="86dc4-160">Sunucu uygulaması, maksimum değer yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="86dc4-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="86dc4-161">Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="86dc4-162">`semVerLevel` Sorgu parametresi için katılım için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="86dc4-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="86dc4-163">Bu sorgu parametresi dışlanırsa, yalnızca paket kimlikleri SemVer 1.0.0 uyumlu sürümler ile döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar, 4 tamsayı parçalı sürüm dizeleri gibi).</span><span class="sxs-lookup"><span data-stu-id="86dc4-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="86dc4-164">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="86dc4-165">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="86dc4-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="86dc4-166">Yanıt</span><span class="sxs-lookup"><span data-stu-id="86dc4-166">Response</span></span>

<span data-ttu-id="86dc4-167">En fazla içeren JSON belgesi yanıttır `take` otomatik tamamlama sonuçları.</span><span class="sxs-lookup"><span data-stu-id="86dc4-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="86dc4-168">Kök JSON nesnesinin aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="86dc4-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="86dc4-169">Ad</span><span class="sxs-lookup"><span data-stu-id="86dc4-169">Name</span></span>      | <span data-ttu-id="86dc4-170">Tür</span><span class="sxs-lookup"><span data-stu-id="86dc4-170">Type</span></span>             | <span data-ttu-id="86dc4-171">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86dc4-171">Required</span></span> | <span data-ttu-id="86dc4-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="86dc4-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="86dc4-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="86dc4-173">totalHits</span></span> | <span data-ttu-id="86dc4-174">tamsayı</span><span class="sxs-lookup"><span data-stu-id="86dc4-174">integer</span></span>          | <span data-ttu-id="86dc4-175">Evet</span><span class="sxs-lookup"><span data-stu-id="86dc4-175">yes</span></span>      | <span data-ttu-id="86dc4-176">Toplam sayısı atlayıp bir eşleşme `skip` ve `take`</span><span class="sxs-lookup"><span data-stu-id="86dc4-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="86dc4-177">veri</span><span class="sxs-lookup"><span data-stu-id="86dc4-177">data</span></span>      | <span data-ttu-id="86dc4-178">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="86dc4-178">array of strings</span></span> | <span data-ttu-id="86dc4-179">Evet</span><span class="sxs-lookup"><span data-stu-id="86dc4-179">yes</span></span>      | <span data-ttu-id="86dc4-180">' % S'paketi istek tarafından eşleştirilen kimlikleri</span><span class="sxs-lookup"><span data-stu-id="86dc4-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="86dc4-181">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="86dc4-181">Sample request</span></span>

<span data-ttu-id="86dc4-182">AL https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="86dc4-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="86dc4-183">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="86dc4-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="86dc4-184">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="86dc4-184">Enumerate package versions</span></span>

<span data-ttu-id="86dc4-185">Önceki API'sini kullanarak bir paket kimliği bulununca istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerini Numaralandırılacak kullanabilir</span><span class="sxs-lookup"><span data-stu-id="86dc4-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="86dc4-186">Listede bulunmayan bir paket sürümüne sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="86dc4-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="86dc4-187">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="86dc4-187">Request parameters</span></span>

<span data-ttu-id="86dc4-188">Ad</span><span class="sxs-lookup"><span data-stu-id="86dc4-188">Name</span></span>        | <span data-ttu-id="86dc4-189">İçindeki</span><span class="sxs-lookup"><span data-stu-id="86dc4-189">In</span></span>     | <span data-ttu-id="86dc4-190">Tür</span><span class="sxs-lookup"><span data-stu-id="86dc4-190">Type</span></span>    | <span data-ttu-id="86dc4-191">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86dc4-191">Required</span></span> | <span data-ttu-id="86dc4-192">Notlar</span><span class="sxs-lookup"><span data-stu-id="86dc4-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="86dc4-193">kimlik</span><span class="sxs-lookup"><span data-stu-id="86dc4-193">id</span></span>          | <span data-ttu-id="86dc4-194">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-194">URL</span></span>    | <span data-ttu-id="86dc4-195">dize</span><span class="sxs-lookup"><span data-stu-id="86dc4-195">string</span></span>  | <span data-ttu-id="86dc4-196">Evet</span><span class="sxs-lookup"><span data-stu-id="86dc4-196">yes</span></span>      | <span data-ttu-id="86dc4-197">Sürümleri için getirmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="86dc4-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="86dc4-198">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="86dc4-198">prerelease</span></span>  | <span data-ttu-id="86dc4-199">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-199">URL</span></span>    | <span data-ttu-id="86dc4-200">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="86dc4-200">boolean</span></span> | <span data-ttu-id="86dc4-201">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-201">no</span></span>       | <span data-ttu-id="86dc4-202">`true` veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="86dc4-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="86dc4-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="86dc4-203">semVerLevel</span></span> | <span data-ttu-id="86dc4-204">URL</span><span class="sxs-lookup"><span data-stu-id="86dc4-204">URL</span></span>    | <span data-ttu-id="86dc4-205">dize</span><span class="sxs-lookup"><span data-stu-id="86dc4-205">string</span></span>  | <span data-ttu-id="86dc4-206">Yok</span><span class="sxs-lookup"><span data-stu-id="86dc4-206">no</span></span>       | <span data-ttu-id="86dc4-207">Bir SemVer 2.0.0 sürümü dizesi</span><span class="sxs-lookup"><span data-stu-id="86dc4-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="86dc4-208">Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="86dc4-209">`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="86dc4-210">Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="86dc4-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="86dc4-211">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 sürümlerinin döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86dc4-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="86dc4-212">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="86dc4-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="86dc4-213">Yanıt</span><span class="sxs-lookup"><span data-stu-id="86dc4-213">Response</span></span>

<span data-ttu-id="86dc4-214">Yanıt, filtreleme verilen sorgu parametreleri tarafından sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="86dc4-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="86dc4-215">Kök JSON nesnesinin aşağıdaki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="86dc4-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="86dc4-216">Ad</span><span class="sxs-lookup"><span data-stu-id="86dc4-216">Name</span></span>      | <span data-ttu-id="86dc4-217">Tür</span><span class="sxs-lookup"><span data-stu-id="86dc4-217">Type</span></span>             | <span data-ttu-id="86dc4-218">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86dc4-218">Required</span></span> | <span data-ttu-id="86dc4-219">Notlar</span><span class="sxs-lookup"><span data-stu-id="86dc4-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="86dc4-220">veri</span><span class="sxs-lookup"><span data-stu-id="86dc4-220">data</span></span>      | <span data-ttu-id="86dc4-221">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="86dc4-221">array of strings</span></span> | <span data-ttu-id="86dc4-222">Evet</span><span class="sxs-lookup"><span data-stu-id="86dc4-222">yes</span></span>      | <span data-ttu-id="86dc4-223">İstek tarafından eşleşen paket sürümleri</span><span class="sxs-lookup"><span data-stu-id="86dc4-223">The package versions matched by the request</span></span>

<span data-ttu-id="86dc4-224">Paket sürümlerinde `data` dizi SemVer 2.0.0 derleme meta verileri içeren (örn `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.</span><span class="sxs-lookup"><span data-stu-id="86dc4-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="86dc4-225">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="86dc4-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="86dc4-226">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="86dc4-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
