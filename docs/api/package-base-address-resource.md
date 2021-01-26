---
title: Paket Içeriği, NuGet API 'SI
description: Paket taban adresi, paketin kendisini getirmeye yönelik basit bir arabirimdir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773935"
---
# <a name="package-content"></a><span data-ttu-id="94c1e-103">Paket Içeriği</span><span class="sxs-lookup"><span data-stu-id="94c1e-103">Package Content</span></span>

<span data-ttu-id="94c1e-104">V3 API kullanarak rastgele bir paketin içeriğini (. nupkg dosyası) getirmek için bir URL oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="94c1e-105">Paket içeriğini getirmek için kullanılan kaynak, `PackageBaseAddress` [hizmet dizininde](service-index.md)bulunan kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="94c1e-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="94c1e-106">Bu kaynak Ayrıca, listelenen veya listelenmemiş bir paketin tüm sürümlerinin bulunmasına da izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="94c1e-107">Bu kaynak genellikle "paket temel adresi" ya da "düz kapsayıcı" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="94c1e-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="94c1e-108">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="94c1e-108">Versioning</span></span>

<span data-ttu-id="94c1e-109">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="94c1e-109">The following `@type` value is used:</span></span>

<span data-ttu-id="94c1e-110">@type deeri</span><span class="sxs-lookup"><span data-stu-id="94c1e-110">@type value</span></span>              | <span data-ttu-id="94c1e-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="94c1e-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="94c1e-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="94c1e-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="94c1e-113">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="94c1e-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="94c1e-114">Temel URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-114">Base URL</span></span>

<span data-ttu-id="94c1e-115">Aşağıdaki API 'Lerin temel URL 'SI, `@id` belirtilen kaynak değeriyle ilişkili özelliğin değeridir `@type` .</span><span class="sxs-lookup"><span data-stu-id="94c1e-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="94c1e-116">Aşağıdaki belgede, yer tutucu temel URL 'SI `{@id}` kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="94c1e-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="94c1e-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-117">HTTP methods</span></span>

<span data-ttu-id="94c1e-118">Kayıt kaynağında bulunan tüm URL 'Ler HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="94c1e-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="94c1e-119">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="94c1e-119">Enumerate package versions</span></span>

<span data-ttu-id="94c1e-120">İstemci bir paket KIMLIĞINI biliyor ve paket kaynağının hangi paket sürümlerini kullanılabilir olduğunu keşfetmesini istiyorsa, istemci tüm paket sürümlerini numaralandırmak için öngörülebilir bir URL oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="94c1e-121">Bu liste, aşağıda bahsedilen paket içeriği API 'SI için bir "Dizin listeleme" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="94c1e-122">Bu liste hem listelenmiş hem de listelenmemiş paket sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="94c1e-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-123">Request parameters</span></span>

<span data-ttu-id="94c1e-124">Name</span><span class="sxs-lookup"><span data-stu-id="94c1e-124">Name</span></span>     | <span data-ttu-id="94c1e-125">İçinde</span><span class="sxs-lookup"><span data-stu-id="94c1e-125">In</span></span>     | <span data-ttu-id="94c1e-126">Tür</span><span class="sxs-lookup"><span data-stu-id="94c1e-126">Type</span></span>    | <span data-ttu-id="94c1e-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94c1e-127">Required</span></span> | <span data-ttu-id="94c1e-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="94c1e-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="94c1e-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="94c1e-129">LOWER_ID</span></span> | <span data-ttu-id="94c1e-130">URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-130">URL</span></span>    | <span data-ttu-id="94c1e-131">string</span><span class="sxs-lookup"><span data-stu-id="94c1e-131">string</span></span>  | <span data-ttu-id="94c1e-132">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-132">yes</span></span>      | <span data-ttu-id="94c1e-133">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="94c1e-133">The package ID, lowercased</span></span>

<span data-ttu-id="94c1e-134">`LOWER_ID`Değer, tarafından uygulanan kurallar kullanılarak istenen paket kimliği küçük harf olarak belirlenir. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="94c1e-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="94c1e-135">Yanıt</span><span class="sxs-lookup"><span data-stu-id="94c1e-135">Response</span></span>

<span data-ttu-id="94c1e-136">Paket kaynağında belirtilen paket KIMLIĞI sürümü yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="94c1e-137">Paket kaynağında bir veya daha fazla sürüm varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="94c1e-138">Yanıt gövdesi, aşağıdaki özelliğe sahip bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="94c1e-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="94c1e-139">Ad</span><span class="sxs-lookup"><span data-stu-id="94c1e-139">Name</span></span>     | <span data-ttu-id="94c1e-140">Tür</span><span class="sxs-lookup"><span data-stu-id="94c1e-140">Type</span></span>             | <span data-ttu-id="94c1e-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94c1e-141">Required</span></span> | <span data-ttu-id="94c1e-142">Notlar</span><span class="sxs-lookup"><span data-stu-id="94c1e-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="94c1e-143">versions</span><span class="sxs-lookup"><span data-stu-id="94c1e-143">versions</span></span> | <span data-ttu-id="94c1e-144">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="94c1e-144">array of strings</span></span> | <span data-ttu-id="94c1e-145">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-145">yes</span></span>      | <span data-ttu-id="94c1e-146">Kullanılabilir sürümler</span><span class="sxs-lookup"><span data-stu-id="94c1e-146">The versions available</span></span>

<span data-ttu-id="94c1e-147">`versions`Dizideki dizeler, tüm küçük harf, [normalleştirilmiş NuGet sürüm dizeleridir](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="94c1e-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="94c1e-148">Sürüm dizeleri herhangi bir SemVer 2.0.0 derleme meta verisi içermiyor.</span><span class="sxs-lookup"><span data-stu-id="94c1e-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="94c1e-149">Amaç, bu dizide bulunan sürüm dizelerinin `LOWER_VERSION` aşağıdaki uç noktalarında bulunan belirteçler için tam olarak kullanılabileceği şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="94c1e-150">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="94c1e-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="94c1e-151">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="94c1e-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="94c1e-152">Paket içeriğini indir (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="94c1e-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="94c1e-153">İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket içeriğini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:</span><span class="sxs-lookup"><span data-stu-id="94c1e-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="94c1e-154">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-154">Request parameters</span></span>

<span data-ttu-id="94c1e-155">Name</span><span class="sxs-lookup"><span data-stu-id="94c1e-155">Name</span></span>          | <span data-ttu-id="94c1e-156">İçinde</span><span class="sxs-lookup"><span data-stu-id="94c1e-156">In</span></span>     | <span data-ttu-id="94c1e-157">Tür</span><span class="sxs-lookup"><span data-stu-id="94c1e-157">Type</span></span>   | <span data-ttu-id="94c1e-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94c1e-158">Required</span></span> | <span data-ttu-id="94c1e-159">Notlar</span><span class="sxs-lookup"><span data-stu-id="94c1e-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="94c1e-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="94c1e-160">LOWER_ID</span></span>      | <span data-ttu-id="94c1e-161">URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-161">URL</span></span>    | <span data-ttu-id="94c1e-162">string</span><span class="sxs-lookup"><span data-stu-id="94c1e-162">string</span></span> | <span data-ttu-id="94c1e-163">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-163">yes</span></span>      | <span data-ttu-id="94c1e-164">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="94c1e-164">The package ID, lowercase</span></span>
<span data-ttu-id="94c1e-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="94c1e-165">LOWER_VERSION</span></span> | <span data-ttu-id="94c1e-166">URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-166">URL</span></span>    | <span data-ttu-id="94c1e-167">string</span><span class="sxs-lookup"><span data-stu-id="94c1e-167">string</span></span> | <span data-ttu-id="94c1e-168">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-168">yes</span></span>      | <span data-ttu-id="94c1e-169">Paket sürümü, normalleştirilmiş ve küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="94c1e-170">Her ikisi de `LOWER_ID` `LOWER_VERSION` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="94c1e-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="94c1e-171">yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-171">method.</span></span>

<span data-ttu-id="94c1e-172">, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="94c1e-173">Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="94c1e-174">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="94c1e-174">Response body</span></span>

<span data-ttu-id="94c1e-175">Paket, paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="94c1e-176">Yanıt gövdesi, paket içeriğinin kendisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="94c1e-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="94c1e-177">Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="94c1e-178">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="94c1e-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="94c1e-179">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="94c1e-179">Sample response</span></span>

<span data-ttu-id="94c1e-180">9.0.1 üzerinde Newtonsoft.Jsiçin. nupkg olan ikili akış.</span><span class="sxs-lookup"><span data-stu-id="94c1e-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="94c1e-181">Paket bildirimini indir (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="94c1e-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="94c1e-182">İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket bildirimini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:</span><span class="sxs-lookup"><span data-stu-id="94c1e-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="94c1e-183">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-183">Request parameters</span></span>

<span data-ttu-id="94c1e-184">Name</span><span class="sxs-lookup"><span data-stu-id="94c1e-184">Name</span></span>          | <span data-ttu-id="94c1e-185">İçinde</span><span class="sxs-lookup"><span data-stu-id="94c1e-185">In</span></span>     | <span data-ttu-id="94c1e-186">Tür</span><span class="sxs-lookup"><span data-stu-id="94c1e-186">Type</span></span>   | <span data-ttu-id="94c1e-187">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94c1e-187">Required</span></span> | <span data-ttu-id="94c1e-188">Notlar</span><span class="sxs-lookup"><span data-stu-id="94c1e-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="94c1e-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="94c1e-189">LOWER_ID</span></span>      | <span data-ttu-id="94c1e-190">URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-190">URL</span></span>    | <span data-ttu-id="94c1e-191">string</span><span class="sxs-lookup"><span data-stu-id="94c1e-191">string</span></span> | <span data-ttu-id="94c1e-192">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-192">yes</span></span>      | <span data-ttu-id="94c1e-193">Paket KIMLIĞI, küçük harf</span><span class="sxs-lookup"><span data-stu-id="94c1e-193">The package ID, lowercase</span></span>
<span data-ttu-id="94c1e-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="94c1e-194">LOWER_VERSION</span></span> | <span data-ttu-id="94c1e-195">URL</span><span class="sxs-lookup"><span data-stu-id="94c1e-195">URL</span></span>    | <span data-ttu-id="94c1e-196">string</span><span class="sxs-lookup"><span data-stu-id="94c1e-196">string</span></span> | <span data-ttu-id="94c1e-197">evet</span><span class="sxs-lookup"><span data-stu-id="94c1e-197">yes</span></span>      | <span data-ttu-id="94c1e-198">Paket sürümü, normalleştirilmiş ve küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="94c1e-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="94c1e-199">Her ikisi de `LOWER_ID` `LOWER_VERSION` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="94c1e-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="94c1e-200">, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="94c1e-201">Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="94c1e-202">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="94c1e-202">Response body</span></span>

<span data-ttu-id="94c1e-203">Paket, paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="94c1e-204">Yanıt gövdesi, karşılık gelen. nupkg 'da bulunan. nuspec olan paket bildirimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="94c1e-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="94c1e-205">. Nuspec bir XML belgesidir.</span><span class="sxs-lookup"><span data-stu-id="94c1e-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="94c1e-206">Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="94c1e-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="94c1e-207">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="94c1e-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="94c1e-208">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="94c1e-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
