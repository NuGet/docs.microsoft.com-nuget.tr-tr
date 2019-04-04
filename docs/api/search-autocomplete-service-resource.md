---
title: Otomatik Tamamlama, NuGet API'si
description: Arama otomatik tamamlama hizmeti etkileşimli olarak paket kimlikleri bulunmasını ve sürümleri destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911055"
---
# <a name="autocomplete"></a><span data-ttu-id="940bd-103">Otomatik Tamamlama</span><span class="sxs-lookup"><span data-stu-id="940bd-103">Autocomplete</span></span>

<span data-ttu-id="940bd-104">V3 API'sini kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyimi oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="940bd-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="940bd-105">Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="940bd-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="940bd-106">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="940bd-106">Versioning</span></span>

<span data-ttu-id="940bd-107">Aşağıdaki `@type` değerleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="940bd-107">The following `@type` values are used:</span></span>

<span data-ttu-id="940bd-108">@type Değer</span><span class="sxs-lookup"><span data-stu-id="940bd-108">@type value</span></span>                          | <span data-ttu-id="940bd-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="940bd-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="940bd-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="940bd-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="940bd-111">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="940bd-111">The initial release</span></span>
<span data-ttu-id="940bd-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="940bd-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="940bd-113">Diğer adı</span><span class="sxs-lookup"><span data-stu-id="940bd-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="940bd-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="940bd-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="940bd-115">Diğer adı</span><span class="sxs-lookup"><span data-stu-id="940bd-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="940bd-116">Temel URL</span><span class="sxs-lookup"><span data-stu-id="940bd-116">Base URL</span></span>

<span data-ttu-id="940bd-117">Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="940bd-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="940bd-118">Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940bd-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="940bd-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="940bd-119">HTTP Methods</span></span>

<span data-ttu-id="940bd-120">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="940bd-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="940bd-121">Paket kimlikleri için arama</span><span class="sxs-lookup"><span data-stu-id="940bd-121">Search for package IDs</span></span>

<span data-ttu-id="940bd-122">Bir paket kimliği dizesi bir parçası için arama ilk otomatik tamamlama API'sini destekler.</span><span class="sxs-lookup"><span data-stu-id="940bd-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="940bd-123">NuGet paket kaynağı ile tümleşik kullanıcı arabiriminde bir paket typeahead özelliği sağlamak istediğinizde mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="940bd-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="940bd-124">Yalnızca listede bulunmayan sürümler ile bir pakete sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="940bd-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="940bd-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="940bd-125">Request parameters</span></span>

<span data-ttu-id="940bd-126">Ad</span><span class="sxs-lookup"><span data-stu-id="940bd-126">Name</span></span>        | <span data-ttu-id="940bd-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="940bd-127">In</span></span>     | <span data-ttu-id="940bd-128">Tür</span><span class="sxs-lookup"><span data-stu-id="940bd-128">Type</span></span>    | <span data-ttu-id="940bd-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="940bd-129">Required</span></span> | <span data-ttu-id="940bd-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="940bd-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="940bd-131">q</span><span class="sxs-lookup"><span data-stu-id="940bd-131">q</span></span>           | <span data-ttu-id="940bd-132">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-132">URL</span></span>    | <span data-ttu-id="940bd-133">dize</span><span class="sxs-lookup"><span data-stu-id="940bd-133">string</span></span>  | <span data-ttu-id="940bd-134">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-134">no</span></span>       | <span data-ttu-id="940bd-135">Paket kimlikleri karşı Karşılaştırılacak dize</span><span class="sxs-lookup"><span data-stu-id="940bd-135">The string to compare against package IDs</span></span>
<span data-ttu-id="940bd-136">Atla</span><span class="sxs-lookup"><span data-stu-id="940bd-136">skip</span></span>        | <span data-ttu-id="940bd-137">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-137">URL</span></span>    | <span data-ttu-id="940bd-138">tamsayı</span><span class="sxs-lookup"><span data-stu-id="940bd-138">integer</span></span> | <span data-ttu-id="940bd-139">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-139">no</span></span>       | <span data-ttu-id="940bd-140">İçin sayfalandırma atlanacak sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="940bd-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="940bd-141">sınav zamanı</span><span class="sxs-lookup"><span data-stu-id="940bd-141">take</span></span>        | <span data-ttu-id="940bd-142">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-142">URL</span></span>    | <span data-ttu-id="940bd-143">tamsayı</span><span class="sxs-lookup"><span data-stu-id="940bd-143">integer</span></span> | <span data-ttu-id="940bd-144">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-144">no</span></span>       | <span data-ttu-id="940bd-145">Sayfalandırma için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="940bd-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="940bd-146">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="940bd-146">prerelease</span></span>  | <span data-ttu-id="940bd-147">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-147">URL</span></span>    | <span data-ttu-id="940bd-148">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="940bd-148">boolean</span></span> | <span data-ttu-id="940bd-149">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-149">no</span></span>       | `true` <span data-ttu-id="940bd-150">veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="940bd-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="940bd-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="940bd-151">semVerLevel</span></span> | <span data-ttu-id="940bd-152">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-152">URL</span></span>    | <span data-ttu-id="940bd-153">dize</span><span class="sxs-lookup"><span data-stu-id="940bd-153">string</span></span>  | <span data-ttu-id="940bd-154">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-154">no</span></span>       | <span data-ttu-id="940bd-155">Bir SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="940bd-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="940bd-156">Otomatik Tamamlama sorgu `q` sunucu uygulama tarafından tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="940bd-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="940bd-157">nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri öneki özgün camel çalışması ve sembol karakterlerinin sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="940bd-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="940bd-158">`skip` 0 varsayılan parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="940bd-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="940bd-159">`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="940bd-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="940bd-160">Sunucu uygulaması, maksimum değer yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="940bd-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="940bd-161">Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.</span><span class="sxs-lookup"><span data-stu-id="940bd-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="940bd-162">`semVerLevel` Sorgu parametresi için katılım için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="940bd-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="940bd-163">Bu sorgu parametresi dışlanırsa, yalnızca paket kimlikleri SemVer 1.0.0 uyumlu sürümler ile döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar, 4 tamsayı parçalı sürüm dizeleri gibi).</span><span class="sxs-lookup"><span data-stu-id="940bd-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="940bd-164">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="940bd-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="940bd-165">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="940bd-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="940bd-166">Yanıt</span><span class="sxs-lookup"><span data-stu-id="940bd-166">Response</span></span>

<span data-ttu-id="940bd-167">En fazla içeren JSON belgesi yanıttır `take` otomatik tamamlama sonuçları.</span><span class="sxs-lookup"><span data-stu-id="940bd-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="940bd-168">Kök JSON nesnesinin aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="940bd-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="940bd-169">Ad</span><span class="sxs-lookup"><span data-stu-id="940bd-169">Name</span></span>      | <span data-ttu-id="940bd-170">Tür</span><span class="sxs-lookup"><span data-stu-id="940bd-170">Type</span></span>             | <span data-ttu-id="940bd-171">Gerekli</span><span class="sxs-lookup"><span data-stu-id="940bd-171">Required</span></span> | <span data-ttu-id="940bd-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="940bd-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="940bd-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="940bd-173">totalHits</span></span> | <span data-ttu-id="940bd-174">tamsayı</span><span class="sxs-lookup"><span data-stu-id="940bd-174">integer</span></span>          | <span data-ttu-id="940bd-175">evet</span><span class="sxs-lookup"><span data-stu-id="940bd-175">yes</span></span>      | <span data-ttu-id="940bd-176">Toplam sayısı atlayıp bir eşleşme `skip` ve</span><span class="sxs-lookup"><span data-stu-id="940bd-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="940bd-177">veri</span><span class="sxs-lookup"><span data-stu-id="940bd-177">data</span></span>      | <span data-ttu-id="940bd-178">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="940bd-178">array of strings</span></span> | <span data-ttu-id="940bd-179">evet</span><span class="sxs-lookup"><span data-stu-id="940bd-179">yes</span></span>      | <span data-ttu-id="940bd-180">' % S'paketi istek tarafından eşleştirilen kimlikleri</span><span class="sxs-lookup"><span data-stu-id="940bd-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="940bd-181">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="940bd-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="940bd-182">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="940bd-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="940bd-183">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="940bd-183">Enumerate package versions</span></span>

<span data-ttu-id="940bd-184">Önceki API'sini kullanarak bir paket kimliği bulununca istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerini Numaralandırılacak kullanabilir</span><span class="sxs-lookup"><span data-stu-id="940bd-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="940bd-185">Listede bulunmayan bir paket sürümüne sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="940bd-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="940bd-186">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="940bd-186">Request parameters</span></span>

<span data-ttu-id="940bd-187">Ad</span><span class="sxs-lookup"><span data-stu-id="940bd-187">Name</span></span>        | <span data-ttu-id="940bd-188">İçindeki</span><span class="sxs-lookup"><span data-stu-id="940bd-188">In</span></span>     | <span data-ttu-id="940bd-189">Tür</span><span class="sxs-lookup"><span data-stu-id="940bd-189">Type</span></span>    | <span data-ttu-id="940bd-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="940bd-190">Required</span></span> | <span data-ttu-id="940bd-191">Notlar</span><span class="sxs-lookup"><span data-stu-id="940bd-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="940bd-192">kimlik</span><span class="sxs-lookup"><span data-stu-id="940bd-192">id</span></span>          | <span data-ttu-id="940bd-193">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-193">URL</span></span>    | <span data-ttu-id="940bd-194">dize</span><span class="sxs-lookup"><span data-stu-id="940bd-194">string</span></span>  | <span data-ttu-id="940bd-195">evet</span><span class="sxs-lookup"><span data-stu-id="940bd-195">yes</span></span>      | <span data-ttu-id="940bd-196">Sürümleri için getirmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="940bd-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="940bd-197">yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="940bd-197">prerelease</span></span>  | <span data-ttu-id="940bd-198">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-198">URL</span></span>    | <span data-ttu-id="940bd-199">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="940bd-199">boolean</span></span> | <span data-ttu-id="940bd-200">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-200">no</span></span>       | `true` <span data-ttu-id="940bd-201">veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="940bd-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="940bd-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="940bd-202">semVerLevel</span></span> | <span data-ttu-id="940bd-203">URL</span><span class="sxs-lookup"><span data-stu-id="940bd-203">URL</span></span>    | <span data-ttu-id="940bd-204">dize</span><span class="sxs-lookup"><span data-stu-id="940bd-204">string</span></span>  | <span data-ttu-id="940bd-205">Yok</span><span class="sxs-lookup"><span data-stu-id="940bd-205">no</span></span>       | <span data-ttu-id="940bd-206">Bir SemVer 2.0.0 sürümü dizesi</span><span class="sxs-lookup"><span data-stu-id="940bd-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="940bd-207">Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.</span><span class="sxs-lookup"><span data-stu-id="940bd-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="940bd-208">`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="940bd-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="940bd-209">Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="940bd-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="940bd-210">Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 sürümlerinin döndürülecek sağlanır.</span><span class="sxs-lookup"><span data-stu-id="940bd-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="940bd-211">Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="940bd-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="940bd-212">Yanıt</span><span class="sxs-lookup"><span data-stu-id="940bd-212">Response</span></span>

<span data-ttu-id="940bd-213">Yanıt, filtreleme verilen sorgu parametreleri tarafından sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="940bd-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="940bd-214">Kök JSON nesnesinin aşağıdaki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="940bd-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="940bd-215">Ad</span><span class="sxs-lookup"><span data-stu-id="940bd-215">Name</span></span>      | <span data-ttu-id="940bd-216">Tür</span><span class="sxs-lookup"><span data-stu-id="940bd-216">Type</span></span>             | <span data-ttu-id="940bd-217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="940bd-217">Required</span></span> | <span data-ttu-id="940bd-218">Notlar</span><span class="sxs-lookup"><span data-stu-id="940bd-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="940bd-219">veri</span><span class="sxs-lookup"><span data-stu-id="940bd-219">data</span></span>      | <span data-ttu-id="940bd-220">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="940bd-220">array of strings</span></span> | <span data-ttu-id="940bd-221">evet</span><span class="sxs-lookup"><span data-stu-id="940bd-221">yes</span></span>      | <span data-ttu-id="940bd-222">İstek tarafından eşleşen paket sürümleri</span><span class="sxs-lookup"><span data-stu-id="940bd-222">The package versions matched by the request</span></span>

<span data-ttu-id="940bd-223">Paket sürümlerinde `data` dizi SemVer 2.0.0 derleme meta verileri içerebilir (örneğin `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.</span><span class="sxs-lookup"><span data-stu-id="940bd-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="940bd-224">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="940bd-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="940bd-225">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="940bd-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
