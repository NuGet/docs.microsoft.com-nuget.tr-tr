---
title: Paket Içeriği, NuGet API 'SI
description: Paket taban adresi, paketin kendisini getirmeye yönelik basit bir arabirimdir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094125"
---
# <a name="package-content"></a><span data-ttu-id="59354-103">Paket Içeriği</span><span class="sxs-lookup"><span data-stu-id="59354-103">Package Content</span></span>

<span data-ttu-id="59354-104">V3 API kullanarak rastgele bir paketin içeriğini (. nupkg dosyası) getirmek için bir URL oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="59354-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="59354-105">Paket içeriğini `PackageBaseAddress` getirmek için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="59354-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="59354-106">Bu kaynak Ayrıca, listelenen veya listelenmemiş bir paketin tüm sürümlerinin bulunmasına da izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="59354-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="59354-107">Bu kaynak genellikle "paket temel adresi" ya da "düz kapsayıcı" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="59354-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="59354-108">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="59354-108">Versioning</span></span>

<span data-ttu-id="59354-109">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="59354-109">The following `@type` value is used:</span></span>

<span data-ttu-id="59354-110">@typedeeri</span><span class="sxs-lookup"><span data-stu-id="59354-110">@type value</span></span>              | <span data-ttu-id="59354-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="59354-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="59354-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="59354-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="59354-113">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="59354-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="59354-114">Taban URL 'SI</span><span class="sxs-lookup"><span data-stu-id="59354-114">Base URL</span></span>

<span data-ttu-id="59354-115">Aşağıdaki API 'lerin temel URL 'si, belirtilen kaynak `@id` `@type` değeriyle ilişkili özelliğin değeridir.</span><span class="sxs-lookup"><span data-stu-id="59354-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="59354-116">Aşağıdaki belgede, yer tutucu temel URL 'si `{@id}` kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="59354-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="59354-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="59354-117">HTTP methods</span></span>

<span data-ttu-id="59354-118">Kayıt kaynağında bulunan tüm URL 'ler http yöntemlerini `GET` ve ' i `HEAD`destekler.</span><span class="sxs-lookup"><span data-stu-id="59354-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="59354-119">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="59354-119">Enumerate package versions</span></span>

<span data-ttu-id="59354-120">İstemci bir paket KIMLIĞINI biliyor ve paket kaynağının hangi paket sürümlerini kullanılabilir olduğunu keşfetmesini istiyorsa, istemci tüm paket sürümlerini numaralandırmak için öngörülebilir bir URL oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="59354-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="59354-121">Bu liste, aşağıda bahsedilen paket içeriği API 'SI için bir "Dizin listeleme" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59354-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="59354-122">Bu liste hem listelenmiş hem de listelenmemiş paket sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="59354-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="59354-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59354-123">Request parameters</span></span>

<span data-ttu-id="59354-124">Ad</span><span class="sxs-lookup"><span data-stu-id="59354-124">Name</span></span>     | <span data-ttu-id="59354-125">İçindeki</span><span class="sxs-lookup"><span data-stu-id="59354-125">In</span></span>     | <span data-ttu-id="59354-126">Tür</span><span class="sxs-lookup"><span data-stu-id="59354-126">Type</span></span>    | <span data-ttu-id="59354-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59354-127">Required</span></span> | <span data-ttu-id="59354-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="59354-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="59354-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59354-129">LOWER_ID</span></span> | <span data-ttu-id="59354-130">URL</span><span class="sxs-lookup"><span data-stu-id="59354-130">URL</span></span>    | <span data-ttu-id="59354-131">dize</span><span class="sxs-lookup"><span data-stu-id="59354-131">string</span></span>  | <span data-ttu-id="59354-132">evet</span><span class="sxs-lookup"><span data-stu-id="59354-132">yes</span></span>      | <span data-ttu-id="59354-133">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="59354-133">The package ID, lowercased</span></span>

<span data-ttu-id="59354-134">`LOWER_ID` Değer, tarafından uygulanan kurallar kullanılarak istenen paket kimliği küçük harf olarak belirlenir. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="59354-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="59354-135">Yanıt</span><span class="sxs-lookup"><span data-stu-id="59354-135">Response</span></span>

<span data-ttu-id="59354-136">Paket kaynağında belirtilen paket KIMLIĞI sürümü yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="59354-137">Paket kaynağında bir veya daha fazla sürüm varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="59354-138">Yanıt gövdesi, aşağıdaki özelliğe sahip bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="59354-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="59354-139">Ad</span><span class="sxs-lookup"><span data-stu-id="59354-139">Name</span></span>     | <span data-ttu-id="59354-140">Tür</span><span class="sxs-lookup"><span data-stu-id="59354-140">Type</span></span>             | <span data-ttu-id="59354-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59354-141">Required</span></span> | <span data-ttu-id="59354-142">Notlar</span><span class="sxs-lookup"><span data-stu-id="59354-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="59354-143">sürümler</span><span class="sxs-lookup"><span data-stu-id="59354-143">versions</span></span> | <span data-ttu-id="59354-144">Dizeler dizisi</span><span class="sxs-lookup"><span data-stu-id="59354-144">array of strings</span></span> | <span data-ttu-id="59354-145">evet</span><span class="sxs-lookup"><span data-stu-id="59354-145">yes</span></span>      | <span data-ttu-id="59354-146">Kullanılabilir sürümler</span><span class="sxs-lookup"><span data-stu-id="59354-146">The versions available</span></span>

<span data-ttu-id="59354-147">`versions` Dizideki dizeler, tüm küçük harf, [normalleştirilmiş NuGet sürüm dizeleridir](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="59354-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59354-148">Sürüm dizeleri herhangi bir SemVer 2.0.0 derleme meta verisi içermiyor.</span><span class="sxs-lookup"><span data-stu-id="59354-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="59354-149">Amaç, bu dizide bulunan sürüm dizelerinin aşağıdaki uç noktalarında bulunan `LOWER_VERSION` belirteçler için tam olarak kullanılabileceği şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59354-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59354-150">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="59354-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="59354-151">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="59354-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="59354-152">Paket içeriğini indir (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="59354-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="59354-153">İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket içeriğini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:</span><span class="sxs-lookup"><span data-stu-id="59354-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="59354-154">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59354-154">Request parameters</span></span>

<span data-ttu-id="59354-155">Ad</span><span class="sxs-lookup"><span data-stu-id="59354-155">Name</span></span>          | <span data-ttu-id="59354-156">İçindeki</span><span class="sxs-lookup"><span data-stu-id="59354-156">In</span></span>     | <span data-ttu-id="59354-157">Tür</span><span class="sxs-lookup"><span data-stu-id="59354-157">Type</span></span>   | <span data-ttu-id="59354-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59354-158">Required</span></span> | <span data-ttu-id="59354-159">Notlar</span><span class="sxs-lookup"><span data-stu-id="59354-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59354-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59354-160">LOWER_ID</span></span>      | <span data-ttu-id="59354-161">URL</span><span class="sxs-lookup"><span data-stu-id="59354-161">URL</span></span>    | <span data-ttu-id="59354-162">dize</span><span class="sxs-lookup"><span data-stu-id="59354-162">string</span></span> | <span data-ttu-id="59354-163">evet</span><span class="sxs-lookup"><span data-stu-id="59354-163">yes</span></span>      | <span data-ttu-id="59354-164">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="59354-164">The package ID, lowercase</span></span>
<span data-ttu-id="59354-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="59354-165">LOWER_VERSION</span></span> | <span data-ttu-id="59354-166">URL</span><span class="sxs-lookup"><span data-stu-id="59354-166">URL</span></span>    | <span data-ttu-id="59354-167">dize</span><span class="sxs-lookup"><span data-stu-id="59354-167">string</span></span> | <span data-ttu-id="59354-168">evet</span><span class="sxs-lookup"><span data-stu-id="59354-168">yes</span></span>      | <span data-ttu-id="59354-169">Paket sürümü, normalleştirilmiş ve küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="59354-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="59354-170">Her ikisi de `LOWER_ID` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür.`LOWER_VERSION` NET 'in[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="59354-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="59354-171">yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="59354-171">method.</span></span>

<span data-ttu-id="59354-172">, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir.</span><span class="sxs-lookup"><span data-stu-id="59354-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59354-173">Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59354-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="59354-174">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="59354-174">Response body</span></span>

<span data-ttu-id="59354-175">Paket, paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="59354-176">Yanıt gövdesi, paket içeriğinin kendisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="59354-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="59354-177">Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59354-178">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="59354-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="59354-179">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="59354-179">Sample response</span></span>

<span data-ttu-id="59354-180">Newtonsoft. JSON 9.0.1 için. nupkg olan ikili akış.</span><span class="sxs-lookup"><span data-stu-id="59354-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="59354-181">Paket bildirimini indir (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="59354-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="59354-182">İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket bildirimini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:</span><span class="sxs-lookup"><span data-stu-id="59354-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="59354-183">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59354-183">Request parameters</span></span>

<span data-ttu-id="59354-184">Ad</span><span class="sxs-lookup"><span data-stu-id="59354-184">Name</span></span>          | <span data-ttu-id="59354-185">İçindeki</span><span class="sxs-lookup"><span data-stu-id="59354-185">In</span></span>     | <span data-ttu-id="59354-186">Tür</span><span class="sxs-lookup"><span data-stu-id="59354-186">Type</span></span>   | <span data-ttu-id="59354-187">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59354-187">Required</span></span> | <span data-ttu-id="59354-188">Notlar</span><span class="sxs-lookup"><span data-stu-id="59354-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59354-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59354-189">LOWER_ID</span></span>      | <span data-ttu-id="59354-190">URL</span><span class="sxs-lookup"><span data-stu-id="59354-190">URL</span></span>    | <span data-ttu-id="59354-191">dize</span><span class="sxs-lookup"><span data-stu-id="59354-191">string</span></span> | <span data-ttu-id="59354-192">evet</span><span class="sxs-lookup"><span data-stu-id="59354-192">yes</span></span>      | <span data-ttu-id="59354-193">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="59354-193">The package ID, lowercase</span></span>
<span data-ttu-id="59354-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="59354-194">LOWER_VERSION</span></span> | <span data-ttu-id="59354-195">URL</span><span class="sxs-lookup"><span data-stu-id="59354-195">URL</span></span>    | <span data-ttu-id="59354-196">dize</span><span class="sxs-lookup"><span data-stu-id="59354-196">string</span></span> | <span data-ttu-id="59354-197">evet</span><span class="sxs-lookup"><span data-stu-id="59354-197">yes</span></span>      | <span data-ttu-id="59354-198">Paket sürümü, normalleştirilmiş ve küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="59354-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="59354-199">Her ikisi de `LOWER_ID` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür.`LOWER_VERSION` NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="59354-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="59354-200">, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir.</span><span class="sxs-lookup"><span data-stu-id="59354-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59354-201">Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59354-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="59354-202">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="59354-202">Response body</span></span>

<span data-ttu-id="59354-203">Paket, paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="59354-204">Yanıt gövdesi, karşılık gelen. nupkg 'da bulunan. nuspec olan paket bildirimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="59354-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="59354-205">. Nuspec bir XML belgesidir.</span><span class="sxs-lookup"><span data-stu-id="59354-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="59354-206">Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59354-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59354-207">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="59354-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="59354-208">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="59354-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
