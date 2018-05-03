---
title: Paket içeriğini, NuGet API
description: Paket taban adresi paket yakalama için basit bir arabirimdir.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="4e0fa-103">Paket içeriği</span><span class="sxs-lookup"><span data-stu-id="4e0fa-103">Package Content</span></span>

<span data-ttu-id="4e0fa-104">V3 API'sini kullanarak rastgele bir paketin içerik (.nupkg dosyasını) getirmek için bir URL oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="4e0fa-105">Paket içeriğini getirmek için kullanılan kaynak `PackageBaseAddress` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4e0fa-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="4e0fa-106">Bu kaynak bulma listelenen bir paketin tüm sürümleri de etkinleştirir ya da listelenmemiş.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="4e0fa-107">Bu kaynak genellikle ya da "paketi taban adresi" veya "düz kapsayıcı" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="4e0fa-108">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e0fa-108">Versioning</span></span>

<span data-ttu-id="4e0fa-109">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="4e0fa-109">The following `@type` value is used:</span></span>

<span data-ttu-id="4e0fa-110">@type Değer</span><span class="sxs-lookup"><span data-stu-id="4e0fa-110">@type value</span></span>              | <span data-ttu-id="4e0fa-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e0fa-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="4e0fa-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="4e0fa-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="4e0fa-113">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="4e0fa-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="4e0fa-114">Temel URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-114">Base URL</span></span>

<span data-ttu-id="4e0fa-115">Aşağıdaki API'leri için temel URL değeri `@id` özelliği daha önce bahsedilen kaynakla ilişkilendirilmiş `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="4e0fa-116">Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4e0fa-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="4e0fa-117">HTTP methods</span></span>

<span data-ttu-id="4e0fa-118">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="4e0fa-119">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="4e0fa-119">Enumerate package versions</span></span>

<span data-ttu-id="4e0fa-120">İstemci bir paket kimliği bilir ve hangi sürümleri paket paketini bulmak istiyorsa kaynak kullanılabilir olan, tüm paket sürümlerini listeleme için tahmin edilebilir URL'sini istemcisi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="4e0fa-121">Bu liste, aşağıda belirtilen paket içeriği API için "dizin listeleme" olması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="4e0fa-122">Bu liste, her iki listelenen hem de listelenmeyen paket sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="4e0fa-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="4e0fa-123">Request parameters</span></span>

<span data-ttu-id="4e0fa-124">Ad</span><span class="sxs-lookup"><span data-stu-id="4e0fa-124">Name</span></span>     | <span data-ttu-id="4e0fa-125">İçindeki</span><span class="sxs-lookup"><span data-stu-id="4e0fa-125">In</span></span>     | <span data-ttu-id="4e0fa-126">Tür</span><span class="sxs-lookup"><span data-stu-id="4e0fa-126">Type</span></span>    | <span data-ttu-id="4e0fa-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e0fa-127">Required</span></span> | <span data-ttu-id="4e0fa-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e0fa-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e0fa-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4e0fa-129">LOWER_ID</span></span> | <span data-ttu-id="4e0fa-130">URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-130">URL</span></span>    | <span data-ttu-id="4e0fa-131">dize</span><span class="sxs-lookup"><span data-stu-id="4e0fa-131">string</span></span>  | <span data-ttu-id="4e0fa-132">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-132">yes</span></span>      | <span data-ttu-id="4e0fa-133">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="4e0fa-133">The package ID, lowercase</span></span>

<span data-ttu-id="4e0fa-134">`LOWER_ID` Tarafından uygulanan kurallarını kullanarak dönüştürüldükten istenen paket kimliği bir değerdir. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="4e0fa-135">Yanıt</span><span class="sxs-lookup"><span data-stu-id="4e0fa-135">Response</span></span>

<span data-ttu-id="4e0fa-136">Paket kaynağı sağlanan paket Kimliğini hiçbir sürümü varsa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="4e0fa-137">Paket kaynağı bir veya birden çok sürüm varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="4e0fa-138">Yanıt gövdesi aşağıdaki özelliğine sahip bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="4e0fa-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="4e0fa-139">Ad</span><span class="sxs-lookup"><span data-stu-id="4e0fa-139">Name</span></span>     | <span data-ttu-id="4e0fa-140">Tür</span><span class="sxs-lookup"><span data-stu-id="4e0fa-140">Type</span></span>             | <span data-ttu-id="4e0fa-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e0fa-141">Required</span></span> | <span data-ttu-id="4e0fa-142">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e0fa-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="4e0fa-143">sürümler</span><span class="sxs-lookup"><span data-stu-id="4e0fa-143">versions</span></span> | <span data-ttu-id="4e0fa-144">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="4e0fa-144">array of strings</span></span> | <span data-ttu-id="4e0fa-145">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-145">yes</span></span>      | <span data-ttu-id="4e0fa-146">Paket kimlikleri kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="4e0fa-146">The package IDs available</span></span>

<span data-ttu-id="4e0fa-147">Dizelerde `versions` dizi tüm dönüştürüldükten, [NuGet sürümü dizeleri normalleştirilmiş](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4e0fa-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4e0fa-148">Sürüm dizelerini SemVer 2.0.0 Yapı meta verileri içermez.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="4e0fa-149">Bu dizide bulunan sürüm dizelerini için aynen kullanılabilir amacı olan `LOWER_VERSION` belirteçleri aşağıdaki uç noktalardan bulundu.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e0fa-150">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="4e0fa-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="4e0fa-151">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="4e0fa-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="4e0fa-152">(.Nupkg) paket içeriğini indirme</span><span class="sxs-lookup"><span data-stu-id="4e0fa-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="4e0fa-153">İstemci paketi Kimliğini ve sürümünü bilir ve paket içeriğini indirme istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:</span><span class="sxs-lookup"><span data-stu-id="4e0fa-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="4e0fa-154">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="4e0fa-154">Request parameters</span></span>

<span data-ttu-id="4e0fa-155">Ad</span><span class="sxs-lookup"><span data-stu-id="4e0fa-155">Name</span></span>          | <span data-ttu-id="4e0fa-156">İçindeki</span><span class="sxs-lookup"><span data-stu-id="4e0fa-156">In</span></span>     | <span data-ttu-id="4e0fa-157">Tür</span><span class="sxs-lookup"><span data-stu-id="4e0fa-157">Type</span></span>   | <span data-ttu-id="4e0fa-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e0fa-158">Required</span></span> | <span data-ttu-id="4e0fa-159">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e0fa-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4e0fa-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4e0fa-160">LOWER_ID</span></span>      | <span data-ttu-id="4e0fa-161">URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-161">URL</span></span>    | <span data-ttu-id="4e0fa-162">dize</span><span class="sxs-lookup"><span data-stu-id="4e0fa-162">string</span></span> | <span data-ttu-id="4e0fa-163">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-163">yes</span></span>      | <span data-ttu-id="4e0fa-164">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="4e0fa-164">The package ID, lowercase</span></span>
<span data-ttu-id="4e0fa-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="4e0fa-165">LOWER_VERSION</span></span> | <span data-ttu-id="4e0fa-166">URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-166">URL</span></span>    | <span data-ttu-id="4e0fa-167">dize</span><span class="sxs-lookup"><span data-stu-id="4e0fa-167">string</span></span> | <span data-ttu-id="4e0fa-168">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-168">yes</span></span>      | <span data-ttu-id="4e0fa-169">Normalleştirilmiş ve dönüştürüldükten Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="4e0fa-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="4e0fa-170">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="4e0fa-171">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4e0fa-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4e0fa-172">Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="4e0fa-173">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="4e0fa-173">Response body</span></span>

<span data-ttu-id="4e0fa-174">Paketi paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="4e0fa-175">Yanıt gövdesi paket içeriğini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="4e0fa-176">Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e0fa-177">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="4e0fa-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="4e0fa-178">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="4e0fa-178">Sample response</span></span>

<span data-ttu-id="4e0fa-179">Newtonsoft.Json 9.0.1 .nupkg ikili akışın.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="4e0fa-180">Paket bildirimi (.nuspec) yükle</span><span class="sxs-lookup"><span data-stu-id="4e0fa-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="4e0fa-181">İstemci paketi Kimliğini ve sürümünü bilir ve paket bildirimi karşıdan istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:</span><span class="sxs-lookup"><span data-stu-id="4e0fa-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="4e0fa-182">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="4e0fa-182">Request parameters</span></span>

<span data-ttu-id="4e0fa-183">Ad</span><span class="sxs-lookup"><span data-stu-id="4e0fa-183">Name</span></span>          | <span data-ttu-id="4e0fa-184">İçindeki</span><span class="sxs-lookup"><span data-stu-id="4e0fa-184">In</span></span>     | <span data-ttu-id="4e0fa-185">Tür</span><span class="sxs-lookup"><span data-stu-id="4e0fa-185">Type</span></span>    | <span data-ttu-id="4e0fa-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e0fa-186">Required</span></span> | <span data-ttu-id="4e0fa-187">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e0fa-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e0fa-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="4e0fa-188">LOWER_ID</span></span>      | <span data-ttu-id="4e0fa-189">URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-189">URL</span></span>    | <span data-ttu-id="4e0fa-190">dize</span><span class="sxs-lookup"><span data-stu-id="4e0fa-190">string</span></span>  | <span data-ttu-id="4e0fa-191">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-191">yes</span></span>      | <span data-ttu-id="4e0fa-192">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="4e0fa-192">The package ID, lowercase</span></span>
<span data-ttu-id="4e0fa-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="4e0fa-193">LOWER_VERSION</span></span> | <span data-ttu-id="4e0fa-194">URL</span><span class="sxs-lookup"><span data-stu-id="4e0fa-194">URL</span></span>    | <span data-ttu-id="4e0fa-195">tamsayı</span><span class="sxs-lookup"><span data-stu-id="4e0fa-195">integer</span></span> | <span data-ttu-id="4e0fa-196">Evet</span><span class="sxs-lookup"><span data-stu-id="4e0fa-196">yes</span></span>      | <span data-ttu-id="4e0fa-197">Normalleştirilmiş ve dönüştürüldükten Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="4e0fa-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="4e0fa-198">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="4e0fa-199">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4e0fa-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="4e0fa-200">Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="4e0fa-201">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="4e0fa-201">Response body</span></span>

<span data-ttu-id="4e0fa-202">Paketi paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="4e0fa-203">Yanıt gövdesi içinde karşılık gelen .nupkg bulunan .nuspec olduğundan paket bildirimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="4e0fa-204">.nuspec bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="4e0fa-205">Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4e0fa-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e0fa-206">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="4e0fa-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="4e0fa-207">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="4e0fa-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
