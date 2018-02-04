---
title: "Paket içeriği, NuGet API | Microsoft Docs"
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
description: "Paket taban adresi paket yakalama için basit bir arabirimdir."
keywords: "NuGet düz kapsayıcı, NuGet paketi temel adres, NuGet nupkg API, NuGet API paketi sürümleri, NuGet API listelenmemiş paketleri, NuGet API indirme nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="c4076-104">Paket içeriği</span><span class="sxs-lookup"><span data-stu-id="c4076-104">Package Content</span></span>

<span data-ttu-id="c4076-105">V3 API'sini kullanarak rastgele bir paketin içerik (.nupkg dosyasını) getirmek için bir URL oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="c4076-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="c4076-106">Paket içeriğini getirmek için kullanılan kaynak `PackageBaseAddress` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c4076-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="c4076-107">Bu kaynak bulma listelenen bir paketin tüm sürümleri de etkinleştirir ya da listelenmemiş.</span><span class="sxs-lookup"><span data-stu-id="c4076-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="c4076-108">Bu kaynak genellikle ya da "paketi taban adresi" veya "düz kapsayıcı" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="c4076-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="c4076-109">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4076-109">Versioning</span></span>

<span data-ttu-id="c4076-110">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c4076-110">The following `@type` value is used:</span></span>

<span data-ttu-id="c4076-111">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="c4076-111">@type value</span></span>              | <span data-ttu-id="c4076-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4076-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="c4076-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="c4076-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="c4076-114">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="c4076-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c4076-115">Temel URL</span><span class="sxs-lookup"><span data-stu-id="c4076-115">Base URL</span></span>

<span data-ttu-id="c4076-116">Aşağıdaki API'leri için temel URL değeri `@id` özelliği daha önce bahsedilen kaynakla ilişkilendirilmiş `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="c4076-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="c4076-117">Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4076-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c4076-118">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c4076-118">HTTP methods</span></span>

<span data-ttu-id="c4076-119">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="c4076-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="c4076-120">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="c4076-120">Enumerate package versions</span></span>

<span data-ttu-id="c4076-121">İstemci bir paket kimliği bilir ve hangi sürümleri paket paketini bulmak istiyorsa kaynak kullanılabilir olan, tüm paket sürümlerini listeleme için tahmin edilebilir URL'sini istemcisi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4076-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="c4076-122">Bu liste, aşağıda belirtilen paket içeriği API için "dizin listeleme" olması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c4076-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="c4076-123">Bu liste, her iki listelenen hem de listelenmeyen paket sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="c4076-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="c4076-124">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="c4076-124">Request parameters</span></span>

<span data-ttu-id="c4076-125">Ad</span><span class="sxs-lookup"><span data-stu-id="c4076-125">Name</span></span>     | <span data-ttu-id="c4076-126">İçindeki</span><span class="sxs-lookup"><span data-stu-id="c4076-126">In</span></span>     | <span data-ttu-id="c4076-127">Tür</span><span class="sxs-lookup"><span data-stu-id="c4076-127">Type</span></span>    | <span data-ttu-id="c4076-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4076-128">Required</span></span> | <span data-ttu-id="c4076-129">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4076-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="c4076-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c4076-130">LOWER_ID</span></span> | <span data-ttu-id="c4076-131">URL</span><span class="sxs-lookup"><span data-stu-id="c4076-131">URL</span></span>    | <span data-ttu-id="c4076-132">dize</span><span class="sxs-lookup"><span data-stu-id="c4076-132">string</span></span>  | <span data-ttu-id="c4076-133">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-133">yes</span></span>      | <span data-ttu-id="c4076-134">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="c4076-134">The package ID, lowercase</span></span>

<span data-ttu-id="c4076-135">`LOWER_ID` Tarafından uygulanan kurallarını kullanarak dönüştürüldükten istenen paket kimliği bir değerdir. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4076-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="c4076-136">Yanıt</span><span class="sxs-lookup"><span data-stu-id="c4076-136">Response</span></span>

<span data-ttu-id="c4076-137">Paket kaynağı sağlanan paket Kimliğini hiçbir sürümü varsa, 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="c4076-138">Paket kaynağı bir veya birden çok sürüm varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="c4076-139">Yanıt gövdesi aşağıdaki özelliğine sahip bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="c4076-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="c4076-140">Ad</span><span class="sxs-lookup"><span data-stu-id="c4076-140">Name</span></span>     | <span data-ttu-id="c4076-141">Tür</span><span class="sxs-lookup"><span data-stu-id="c4076-141">Type</span></span>             | <span data-ttu-id="c4076-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4076-142">Required</span></span> | <span data-ttu-id="c4076-143">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4076-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="c4076-144">sürümler</span><span class="sxs-lookup"><span data-stu-id="c4076-144">versions</span></span> | <span data-ttu-id="c4076-145">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="c4076-145">array of strings</span></span> | <span data-ttu-id="c4076-146">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-146">yes</span></span>      | <span data-ttu-id="c4076-147">Paket kimlikleri kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="c4076-147">The package IDs available</span></span>

<span data-ttu-id="c4076-148">Dizelerde `versions` dizi tüm dönüştürüldükten, [NuGet sürümü dizeleri normalleştirilmiş](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c4076-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c4076-149">Sürüm dizelerini SemVer 2.0.0 Yapı meta verileri içermez.</span><span class="sxs-lookup"><span data-stu-id="c4076-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="c4076-150">Bu dizide bulunan sürüm dizelerini için aynen kullanılabilir amacı olan `LOWER_VERSION` belirteçleri aşağıdaki uç noktalardan bulundu.</span><span class="sxs-lookup"><span data-stu-id="c4076-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c4076-151">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="c4076-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="c4076-152">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="c4076-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="c4076-153">(.Nupkg) paket içeriğini indirme</span><span class="sxs-lookup"><span data-stu-id="c4076-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="c4076-154">İstemci paketi Kimliğini ve sürümünü bilir ve paket içeriğini indirme istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:</span><span class="sxs-lookup"><span data-stu-id="c4076-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="c4076-155">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="c4076-155">Request parameters</span></span>

<span data-ttu-id="c4076-156">Ad</span><span class="sxs-lookup"><span data-stu-id="c4076-156">Name</span></span>          | <span data-ttu-id="c4076-157">İçindeki</span><span class="sxs-lookup"><span data-stu-id="c4076-157">In</span></span>     | <span data-ttu-id="c4076-158">Tür</span><span class="sxs-lookup"><span data-stu-id="c4076-158">Type</span></span>   | <span data-ttu-id="c4076-159">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4076-159">Required</span></span> | <span data-ttu-id="c4076-160">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4076-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c4076-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c4076-161">LOWER_ID</span></span>      | <span data-ttu-id="c4076-162">URL</span><span class="sxs-lookup"><span data-stu-id="c4076-162">URL</span></span>    | <span data-ttu-id="c4076-163">dize</span><span class="sxs-lookup"><span data-stu-id="c4076-163">string</span></span> | <span data-ttu-id="c4076-164">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-164">yes</span></span>      | <span data-ttu-id="c4076-165">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="c4076-165">The package ID, lowercase</span></span>
<span data-ttu-id="c4076-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="c4076-166">LOWER_VERSION</span></span> | <span data-ttu-id="c4076-167">URL</span><span class="sxs-lookup"><span data-stu-id="c4076-167">URL</span></span>    | <span data-ttu-id="c4076-168">dize</span><span class="sxs-lookup"><span data-stu-id="c4076-168">string</span></span> | <span data-ttu-id="c4076-169">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-169">yes</span></span>      | <span data-ttu-id="c4076-170">Normalleştirilmiş ve dönüştürüldükten Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="c4076-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="c4076-171">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4076-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="c4076-172">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c4076-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c4076-173">Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4076-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="c4076-174">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="c4076-174">Response body</span></span>

<span data-ttu-id="c4076-175">Paketi paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="c4076-176">Yanıt gövdesi paket içeriğini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4076-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="c4076-177">Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c4076-178">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="c4076-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="c4076-179">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="c4076-179">Sample response</span></span>

<span data-ttu-id="c4076-180">Newtonsoft.Json 9.0.1 .nupkg ikili akışın.</span><span class="sxs-lookup"><span data-stu-id="c4076-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="c4076-181">Paket bildirimi (.nuspec) yükle</span><span class="sxs-lookup"><span data-stu-id="c4076-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="c4076-182">İstemci paketi Kimliğini ve sürümünü bilir ve paket bildirimi karşıdan istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:</span><span class="sxs-lookup"><span data-stu-id="c4076-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="c4076-183">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="c4076-183">Request parameters</span></span>

<span data-ttu-id="c4076-184">Ad</span><span class="sxs-lookup"><span data-stu-id="c4076-184">Name</span></span>          | <span data-ttu-id="c4076-185">İçindeki</span><span class="sxs-lookup"><span data-stu-id="c4076-185">In</span></span>     | <span data-ttu-id="c4076-186">Tür</span><span class="sxs-lookup"><span data-stu-id="c4076-186">Type</span></span>    | <span data-ttu-id="c4076-187">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4076-187">Required</span></span> | <span data-ttu-id="c4076-188">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4076-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="c4076-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="c4076-189">LOWER_ID</span></span>      | <span data-ttu-id="c4076-190">URL</span><span class="sxs-lookup"><span data-stu-id="c4076-190">URL</span></span>    | <span data-ttu-id="c4076-191">dize</span><span class="sxs-lookup"><span data-stu-id="c4076-191">string</span></span>  | <span data-ttu-id="c4076-192">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-192">yes</span></span>      | <span data-ttu-id="c4076-193">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="c4076-193">The package ID, lowercase</span></span>
<span data-ttu-id="c4076-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="c4076-194">LOWER_VERSION</span></span> | <span data-ttu-id="c4076-195">URL</span><span class="sxs-lookup"><span data-stu-id="c4076-195">URL</span></span>    | <span data-ttu-id="c4076-196">tamsayı</span><span class="sxs-lookup"><span data-stu-id="c4076-196">integer</span></span> | <span data-ttu-id="c4076-197">Evet</span><span class="sxs-lookup"><span data-stu-id="c4076-197">yes</span></span>      | <span data-ttu-id="c4076-198">Normalleştirilmiş ve dönüştürüldükten Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="c4076-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="c4076-199">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c4076-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="c4076-200">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c4076-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="c4076-201">Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4076-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="c4076-202">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="c4076-202">Response body</span></span>

<span data-ttu-id="c4076-203">Paketi paket kaynağında varsa, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="c4076-204">Yanıt gövdesi içinde karşılık gelen .nupkg bulunan .nuspec olduğundan paket bildirimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4076-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="c4076-205">.nuspec bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c4076-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="c4076-206">Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c4076-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c4076-207">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="c4076-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="c4076-208">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="c4076-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
