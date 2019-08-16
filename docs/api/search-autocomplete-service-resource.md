---
title: Otomatik tamamlama, NuGet API 'SI
description: Arama otomatik tamamlama hizmeti, paket kimliklerinin ve sürümlerinin etkileşimli bulmayı destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488299"
---
# <a name="autocomplete"></a><span data-ttu-id="34442-103">Otomatik Tamamlama</span><span class="sxs-lookup"><span data-stu-id="34442-103">Autocomplete</span></span>

<span data-ttu-id="34442-104">V3 API kullanarak bir paket KIMLIĞI ve sürüm otomatik tamamlama deneyimi oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="34442-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="34442-105">Otomatik tamamlama sorguları `SearchAutocompleteService` yapmak için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="34442-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="34442-106">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="34442-106">Versioning</span></span>

<span data-ttu-id="34442-107">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="34442-107">The following `@type` values are used:</span></span>

<span data-ttu-id="34442-108">@typedeeri</span><span class="sxs-lookup"><span data-stu-id="34442-108">@type value</span></span>                          | <span data-ttu-id="34442-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="34442-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="34442-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="34442-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="34442-111">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="34442-111">The initial release</span></span>
<span data-ttu-id="34442-112">SearchAutocompleteService/3.0.0-Beta</span><span class="sxs-lookup"><span data-stu-id="34442-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="34442-113">Diğer adı`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="34442-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="34442-114">SearchAutocompleteService/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="34442-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="34442-115">Diğer adı`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="34442-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="34442-116">Taban URL 'SI</span><span class="sxs-lookup"><span data-stu-id="34442-116">Base URL</span></span>

<span data-ttu-id="34442-117">Aşağıdaki API 'lerin temel URL 'si, belirtilen kaynak `@id` `@type` değerlerinden biriyle ilişkili özelliğin değeridir.</span><span class="sxs-lookup"><span data-stu-id="34442-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="34442-118">Aşağıdaki belgede, yer tutucu temel URL 'si `{@id}` kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="34442-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="34442-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="34442-119">HTTP Methods</span></span>

<span data-ttu-id="34442-120">Kayıt kaynağında bulunan tüm URL 'ler http yöntemlerini `GET` ve ' i `HEAD`destekler.</span><span class="sxs-lookup"><span data-stu-id="34442-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="34442-121">Paket kimliklerini ara</span><span class="sxs-lookup"><span data-stu-id="34442-121">Search for package IDs</span></span>

<span data-ttu-id="34442-122">İlk otomatik tamamlama API 'SI, bir paket KIMLIĞI dizesinin bir parçası için aramayı destekler.</span><span class="sxs-lookup"><span data-stu-id="34442-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="34442-123">Bu, bir NuGet paket kaynağıyla tümleşik Kullanıcı arabirimine bir paket typeahead özelliği sağlamak istediğinizde idealdir.</span><span class="sxs-lookup"><span data-stu-id="34442-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="34442-124">Sonuçlarda yalnızca listelenmemiş sürümlerin yer aldığı bir paket görünmez.</span><span class="sxs-lookup"><span data-stu-id="34442-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="34442-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="34442-125">Request parameters</span></span>

<span data-ttu-id="34442-126">Ad</span><span class="sxs-lookup"><span data-stu-id="34442-126">Name</span></span>        | <span data-ttu-id="34442-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="34442-127">In</span></span>     | <span data-ttu-id="34442-128">Tür</span><span class="sxs-lookup"><span data-stu-id="34442-128">Type</span></span>    | <span data-ttu-id="34442-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34442-129">Required</span></span> | <span data-ttu-id="34442-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="34442-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="34442-131">q</span><span class="sxs-lookup"><span data-stu-id="34442-131">q</span></span>           | <span data-ttu-id="34442-132">URL</span><span class="sxs-lookup"><span data-stu-id="34442-132">URL</span></span>    | <span data-ttu-id="34442-133">dize</span><span class="sxs-lookup"><span data-stu-id="34442-133">string</span></span>  | <span data-ttu-id="34442-134">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-134">no</span></span>       | <span data-ttu-id="34442-135">Paket kimliklerine göre Karşılaştırılacak dize</span><span class="sxs-lookup"><span data-stu-id="34442-135">The string to compare against package IDs</span></span>
<span data-ttu-id="34442-136">Atla</span><span class="sxs-lookup"><span data-stu-id="34442-136">skip</span></span>        | <span data-ttu-id="34442-137">URL</span><span class="sxs-lookup"><span data-stu-id="34442-137">URL</span></span>    | <span data-ttu-id="34442-138">tamsayı</span><span class="sxs-lookup"><span data-stu-id="34442-138">integer</span></span> | <span data-ttu-id="34442-139">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-139">no</span></span>       | <span data-ttu-id="34442-140">Sayfalama için atlanacak sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="34442-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="34442-141">take</span><span class="sxs-lookup"><span data-stu-id="34442-141">take</span></span>        | <span data-ttu-id="34442-142">URL</span><span class="sxs-lookup"><span data-stu-id="34442-142">URL</span></span>    | <span data-ttu-id="34442-143">tamsayı</span><span class="sxs-lookup"><span data-stu-id="34442-143">integer</span></span> | <span data-ttu-id="34442-144">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-144">no</span></span>       | <span data-ttu-id="34442-145">Sayfalama için döndürülecek sonuç sayısı</span><span class="sxs-lookup"><span data-stu-id="34442-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="34442-146">sp1'in</span><span class="sxs-lookup"><span data-stu-id="34442-146">prerelease</span></span>  | <span data-ttu-id="34442-147">URL</span><span class="sxs-lookup"><span data-stu-id="34442-147">URL</span></span>    | <span data-ttu-id="34442-148">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="34442-148">boolean</span></span> | <span data-ttu-id="34442-149">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-149">no</span></span>       | <span data-ttu-id="34442-150">`true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme</span><span class="sxs-lookup"><span data-stu-id="34442-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="34442-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="34442-151">semVerLevel</span></span> | <span data-ttu-id="34442-152">URL</span><span class="sxs-lookup"><span data-stu-id="34442-152">URL</span></span>    | <span data-ttu-id="34442-153">dize</span><span class="sxs-lookup"><span data-stu-id="34442-153">string</span></span>  | <span data-ttu-id="34442-154">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-154">no</span></span>       | <span data-ttu-id="34442-155">Bir SemVer 1.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="34442-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="34442-156">AutoComplete sorgusu `q` , sunucu uygulamasıyla tanımlanan bir şekilde ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="34442-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="34442-157">nuget.org, orijinal kamel Case ve symbol karakterleri tarafından oluşturulan KIMLIğIN parçaları olan paket KIMLIĞI belirteçlerinin ön ekinin sorgulanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="34442-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="34442-158">`skip` Parametresinin varsayılan değeri 0 ' dır.</span><span class="sxs-lookup"><span data-stu-id="34442-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="34442-159">`take` Parametre sıfırdan büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="34442-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="34442-160">Sunucu uygulamasında en büyük değer uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="34442-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="34442-161">`prerelease` Sağlanmazsa, yayın öncesi paketler hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="34442-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="34442-162">Sorgu `semVerLevel` parametresi, [semver 2.0.0 paketlerini](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)kabul etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34442-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="34442-163">Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 uyumlu sürümlerine sahip paket kimlikleri döndürülür (4 tamsayı parçalı sürüm dizeleri gibi [Standart NuGet sürüm oluşturma](../concepts/package-versioning.md) uyarıları ile).</span><span class="sxs-lookup"><span data-stu-id="34442-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="34442-164">`semVerLevel=2.0.0` Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 uyumlu paketler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34442-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="34442-165">Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="34442-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="34442-166">Yanıt</span><span class="sxs-lookup"><span data-stu-id="34442-166">Response</span></span>

<span data-ttu-id="34442-167">Yanıt, `take` otomatik tamamlama sonuçlarını içeren JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="34442-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="34442-168">Kök JSON nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="34442-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="34442-169">Ad</span><span class="sxs-lookup"><span data-stu-id="34442-169">Name</span></span>      | <span data-ttu-id="34442-170">Tür</span><span class="sxs-lookup"><span data-stu-id="34442-170">Type</span></span>             | <span data-ttu-id="34442-171">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34442-171">Required</span></span> | <span data-ttu-id="34442-172">Notlar</span><span class="sxs-lookup"><span data-stu-id="34442-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="34442-173">Toplam Isabet sayısı</span><span class="sxs-lookup"><span data-stu-id="34442-173">totalHits</span></span> | <span data-ttu-id="34442-174">tamsayı</span><span class="sxs-lookup"><span data-stu-id="34442-174">integer</span></span>          | <span data-ttu-id="34442-175">evet</span><span class="sxs-lookup"><span data-stu-id="34442-175">yes</span></span>      | <span data-ttu-id="34442-176">Toplam eşleşme sayısı, ile ilgili `skip` ve`take`</span><span class="sxs-lookup"><span data-stu-id="34442-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="34442-177">veri</span><span class="sxs-lookup"><span data-stu-id="34442-177">data</span></span>      | <span data-ttu-id="34442-178">dizeler dizisi</span><span class="sxs-lookup"><span data-stu-id="34442-178">array of strings</span></span> | <span data-ttu-id="34442-179">evet</span><span class="sxs-lookup"><span data-stu-id="34442-179">yes</span></span>      | <span data-ttu-id="34442-180">İstekle eşleşen paket kimlikleri</span><span class="sxs-lookup"><span data-stu-id="34442-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="34442-181">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="34442-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="34442-182">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="34442-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="34442-183">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="34442-183">Enumerate package versions</span></span>

<span data-ttu-id="34442-184">Bir paket KIMLIĞI önceki API kullanılarak bulunduğunda, istemci, belirtilen paket KIMLIĞI için paket sürümlerini numaralandırmak üzere otomatik tamamlama API 'sini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="34442-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="34442-185">Listelenmemiş bir paket sürümü sonuçlarda görünmez.</span><span class="sxs-lookup"><span data-stu-id="34442-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="34442-186">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="34442-186">Request parameters</span></span>

<span data-ttu-id="34442-187">Ad</span><span class="sxs-lookup"><span data-stu-id="34442-187">Name</span></span>        | <span data-ttu-id="34442-188">İçindeki</span><span class="sxs-lookup"><span data-stu-id="34442-188">In</span></span>     | <span data-ttu-id="34442-189">Tür</span><span class="sxs-lookup"><span data-stu-id="34442-189">Type</span></span>    | <span data-ttu-id="34442-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34442-190">Required</span></span> | <span data-ttu-id="34442-191">Notlar</span><span class="sxs-lookup"><span data-stu-id="34442-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="34442-192">kimlik</span><span class="sxs-lookup"><span data-stu-id="34442-192">id</span></span>          | <span data-ttu-id="34442-193">URL</span><span class="sxs-lookup"><span data-stu-id="34442-193">URL</span></span>    | <span data-ttu-id="34442-194">dize</span><span class="sxs-lookup"><span data-stu-id="34442-194">string</span></span>  | <span data-ttu-id="34442-195">evet</span><span class="sxs-lookup"><span data-stu-id="34442-195">yes</span></span>      | <span data-ttu-id="34442-196">İçin sürümlerinin getirileceği paket KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="34442-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="34442-197">sp1'in</span><span class="sxs-lookup"><span data-stu-id="34442-197">prerelease</span></span>  | <span data-ttu-id="34442-198">URL</span><span class="sxs-lookup"><span data-stu-id="34442-198">URL</span></span>    | <span data-ttu-id="34442-199">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="34442-199">boolean</span></span> | <span data-ttu-id="34442-200">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-200">no</span></span>       | <span data-ttu-id="34442-201">`true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme</span><span class="sxs-lookup"><span data-stu-id="34442-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="34442-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="34442-202">semVerLevel</span></span> | <span data-ttu-id="34442-203">URL</span><span class="sxs-lookup"><span data-stu-id="34442-203">URL</span></span>    | <span data-ttu-id="34442-204">dize</span><span class="sxs-lookup"><span data-stu-id="34442-204">string</span></span>  | <span data-ttu-id="34442-205">eşleşen</span><span class="sxs-lookup"><span data-stu-id="34442-205">no</span></span>       | <span data-ttu-id="34442-206">Bir SemVer 2.0.0 sürüm dizesi</span><span class="sxs-lookup"><span data-stu-id="34442-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="34442-207">`prerelease` Sağlanmazsa, yayın öncesi paketler hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="34442-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="34442-208">Sorgu `semVerLevel` parametresi, semver 2.0.0 paketlerini kabul etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34442-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="34442-209">Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 sürümleri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34442-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="34442-210">`semVerLevel=2.0.0` Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 sürümleri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="34442-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="34442-211">Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="34442-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="34442-212">Yanıt</span><span class="sxs-lookup"><span data-stu-id="34442-212">Response</span></span>

<span data-ttu-id="34442-213">Yanıt, sağlanan paket KIMLIĞININ tüm paket sürümlerini içeren, belirtilen Sorgu parametrelerine göre filtreleyerek JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="34442-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="34442-214">Kök JSON nesnesi aşağıdaki özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="34442-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="34442-215">Ad</span><span class="sxs-lookup"><span data-stu-id="34442-215">Name</span></span>      | <span data-ttu-id="34442-216">Tür</span><span class="sxs-lookup"><span data-stu-id="34442-216">Type</span></span>             | <span data-ttu-id="34442-217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34442-217">Required</span></span> | <span data-ttu-id="34442-218">Notlar</span><span class="sxs-lookup"><span data-stu-id="34442-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="34442-219">veri</span><span class="sxs-lookup"><span data-stu-id="34442-219">data</span></span>      | <span data-ttu-id="34442-220">dizeler dizisi</span><span class="sxs-lookup"><span data-stu-id="34442-220">array of strings</span></span> | <span data-ttu-id="34442-221">evet</span><span class="sxs-lookup"><span data-stu-id="34442-221">yes</span></span>      | <span data-ttu-id="34442-222">İstekle eşleşen paket sürümleri</span><span class="sxs-lookup"><span data-stu-id="34442-222">The package versions matched by the request</span></span>

<span data-ttu-id="34442-223">`data` Dizideki paket sürümleri, sorgu dizesinde sağlanmışsa, `semVerLevel=2.0.0` semver 2.0.0 derleme meta verileri (ör `1.0.0+metadata`.) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="34442-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="34442-224">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="34442-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="34442-225">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="34442-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
