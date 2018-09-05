---
title: Paket içeriğini, NuGet API'si
description: Paket temel adres, paket yakalama için basit bir arabirimdir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547160"
---
# <a name="package-content"></a><span data-ttu-id="354e9-103">Paket içeriği</span><span class="sxs-lookup"><span data-stu-id="354e9-103">Package Content</span></span>

<span data-ttu-id="354e9-104">V3 API'sini kullanarak rastgele bir paketin içerik (.nupkg dosyası) getirmek için bir URL oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="354e9-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="354e9-105">Paket içeriğini getirmek için kullanılan kaynak `PackageBaseAddress` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="354e9-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="354e9-106">Bu kaynak ayrıca listelenen, bir paketin tüm sürümlerini bulunmasını sağlar veya listeden kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="354e9-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="354e9-107">Bu kaynak genellikle ya da "Paket taban adresi" veya "düz kapsayıcı" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="354e9-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="354e9-108">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="354e9-108">Versioning</span></span>

<span data-ttu-id="354e9-109">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="354e9-109">The following `@type` value is used:</span></span>

<span data-ttu-id="354e9-110">@type Değer</span><span class="sxs-lookup"><span data-stu-id="354e9-110">@type value</span></span>              | <span data-ttu-id="354e9-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="354e9-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="354e9-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="354e9-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="354e9-113">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="354e9-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="354e9-114">Temel URL</span><span class="sxs-lookup"><span data-stu-id="354e9-114">Base URL</span></span>

<span data-ttu-id="354e9-115">Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="354e9-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="354e9-116">Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="354e9-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="354e9-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="354e9-117">HTTP methods</span></span>

<span data-ttu-id="354e9-118">Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="354e9-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="354e9-119">Paket sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="354e9-119">Enumerate package versions</span></span>

<span data-ttu-id="354e9-120">İstemci bildiği bir paket kimliği ve paket sürümleri, paketi bulmak istediği kaynak kullanılabilir olan, istemci paket sürümlerini tüm numaralandırmak için tahmin edilebilir bir URL oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="354e9-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="354e9-121">Bu liste, aşağıda belirtilen paket içeriği API için "dizin listeleme" olması için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="354e9-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="354e9-122">Bu liste, her iki listelenen ve listelenmemiş paket sürümlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="354e9-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="354e9-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="354e9-123">Request parameters</span></span>

<span data-ttu-id="354e9-124">Ad</span><span class="sxs-lookup"><span data-stu-id="354e9-124">Name</span></span>     | <span data-ttu-id="354e9-125">İçindeki</span><span class="sxs-lookup"><span data-stu-id="354e9-125">In</span></span>     | <span data-ttu-id="354e9-126">Tür</span><span class="sxs-lookup"><span data-stu-id="354e9-126">Type</span></span>    | <span data-ttu-id="354e9-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="354e9-127">Required</span></span> | <span data-ttu-id="354e9-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="354e9-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="354e9-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="354e9-129">LOWER_ID</span></span> | <span data-ttu-id="354e9-130">URL</span><span class="sxs-lookup"><span data-stu-id="354e9-130">URL</span></span>    | <span data-ttu-id="354e9-131">dize</span><span class="sxs-lookup"><span data-stu-id="354e9-131">string</span></span>  | <span data-ttu-id="354e9-132">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-132">yes</span></span>      | <span data-ttu-id="354e9-133">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="354e9-133">The package ID, lowercase</span></span>

<span data-ttu-id="354e9-134">`LOWER_ID` Tarafından uygulanan kurallar kullanarak küçük harfli istenen paket kimliği bir değerdir. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="354e9-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="354e9-135">Yanıt</span><span class="sxs-lookup"><span data-stu-id="354e9-135">Response</span></span>

<span data-ttu-id="354e9-136">Paket kaynağı, sağlanan paket kimliği hiçbir sürümü varsa, bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="354e9-137">Paket kaynağı, bir veya daha fazla sürümü varsa, bir 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="354e9-138">Yanıt gövdesi, aşağıdaki özelliklerle bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="354e9-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="354e9-139">Ad</span><span class="sxs-lookup"><span data-stu-id="354e9-139">Name</span></span>     | <span data-ttu-id="354e9-140">Tür</span><span class="sxs-lookup"><span data-stu-id="354e9-140">Type</span></span>             | <span data-ttu-id="354e9-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="354e9-141">Required</span></span> | <span data-ttu-id="354e9-142">Notlar</span><span class="sxs-lookup"><span data-stu-id="354e9-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="354e9-143">sürümler</span><span class="sxs-lookup"><span data-stu-id="354e9-143">versions</span></span> | <span data-ttu-id="354e9-144">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="354e9-144">array of strings</span></span> | <span data-ttu-id="354e9-145">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-145">yes</span></span>      | <span data-ttu-id="354e9-146">' % S'paketi kimliklerini kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="354e9-146">The package IDs available</span></span>

<span data-ttu-id="354e9-147">Dizelerde `versions` dizi tüm küçük harfli, [NuGet sürüm dizeleri normalleştirilmiş](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="354e9-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="354e9-148">Sürüm dizeleri SemVer 2.0.0 derleme meta verileri içermez.</span><span class="sxs-lookup"><span data-stu-id="354e9-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="354e9-149">Bu dizinin içinde bulunan sürüm dizeleri için verbatim kullanılabilir amacı olan `LOWER_VERSION` belirteçleri aşağıdaki uç noktaların bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="354e9-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="354e9-150">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="354e9-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="354e9-151">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="354e9-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="354e9-152">(.Nupkg) paket içeriğini indirme</span><span class="sxs-lookup"><span data-stu-id="354e9-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="354e9-153">İstemci paketi Kimliğini ve sürümünü bilir ve paket içeriğini indirme istediği, yalnızca aşağıdaki URL'yi oluşturmak için ihtiyaçları:</span><span class="sxs-lookup"><span data-stu-id="354e9-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="354e9-154">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="354e9-154">Request parameters</span></span>

<span data-ttu-id="354e9-155">Ad</span><span class="sxs-lookup"><span data-stu-id="354e9-155">Name</span></span>          | <span data-ttu-id="354e9-156">İçindeki</span><span class="sxs-lookup"><span data-stu-id="354e9-156">In</span></span>     | <span data-ttu-id="354e9-157">Tür</span><span class="sxs-lookup"><span data-stu-id="354e9-157">Type</span></span>   | <span data-ttu-id="354e9-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="354e9-158">Required</span></span> | <span data-ttu-id="354e9-159">Notlar</span><span class="sxs-lookup"><span data-stu-id="354e9-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="354e9-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="354e9-160">LOWER_ID</span></span>      | <span data-ttu-id="354e9-161">URL</span><span class="sxs-lookup"><span data-stu-id="354e9-161">URL</span></span>    | <span data-ttu-id="354e9-162">dize</span><span class="sxs-lookup"><span data-stu-id="354e9-162">string</span></span> | <span data-ttu-id="354e9-163">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-163">yes</span></span>      | <span data-ttu-id="354e9-164">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="354e9-164">The package ID, lowercase</span></span>
<span data-ttu-id="354e9-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="354e9-165">LOWER_VERSION</span></span> | <span data-ttu-id="354e9-166">URL</span><span class="sxs-lookup"><span data-stu-id="354e9-166">URL</span></span>    | <span data-ttu-id="354e9-167">dize</span><span class="sxs-lookup"><span data-stu-id="354e9-167">string</span></span> | <span data-ttu-id="354e9-168">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-168">yes</span></span>      | <span data-ttu-id="354e9-169">Normalleştirilmiş ve küçük harf yapılmış Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="354e9-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="354e9-170">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallar kullanarak küçük harf yapılmış. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="354e9-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="354e9-171">yöntem.</span><span class="sxs-lookup"><span data-stu-id="354e9-171">method.</span></span>

<span data-ttu-id="354e9-172">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kuralları](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="354e9-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="354e9-173">Başka bir deyişle, bu durumda SemVer 2.0.0 belirtimine göre izin verilen derleme meta verilerin tutulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="354e9-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="354e9-174">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="354e9-174">Response body</span></span>

<span data-ttu-id="354e9-175">Paketin paket kaynak var, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="354e9-176">Yanıt gövdesi, paket içeriğini olacaktır.</span><span class="sxs-lookup"><span data-stu-id="354e9-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="354e9-177">Paketin paket kaynak mevcut değilse bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="354e9-178">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="354e9-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="354e9-179">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="354e9-179">Sample response</span></span>

<span data-ttu-id="354e9-180">Newtonsoft.Json 9.0.1 için .nupkg ikili akışın.</span><span class="sxs-lookup"><span data-stu-id="354e9-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="354e9-181">Paket bildirimi (.nuspec) indirin</span><span class="sxs-lookup"><span data-stu-id="354e9-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="354e9-182">İstemci paketi Kimliğini ve sürümünü bilir ve paket bildirimi indirmek ister bunlar yalnızca aşağıdaki URL'yi oluşturmak gerekir:</span><span class="sxs-lookup"><span data-stu-id="354e9-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="354e9-183">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="354e9-183">Request parameters</span></span>

<span data-ttu-id="354e9-184">Ad</span><span class="sxs-lookup"><span data-stu-id="354e9-184">Name</span></span>          | <span data-ttu-id="354e9-185">İçindeki</span><span class="sxs-lookup"><span data-stu-id="354e9-185">In</span></span>     | <span data-ttu-id="354e9-186">Tür</span><span class="sxs-lookup"><span data-stu-id="354e9-186">Type</span></span>    | <span data-ttu-id="354e9-187">Gerekli</span><span class="sxs-lookup"><span data-stu-id="354e9-187">Required</span></span> | <span data-ttu-id="354e9-188">Notlar</span><span class="sxs-lookup"><span data-stu-id="354e9-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="354e9-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="354e9-189">LOWER_ID</span></span>      | <span data-ttu-id="354e9-190">URL</span><span class="sxs-lookup"><span data-stu-id="354e9-190">URL</span></span>    | <span data-ttu-id="354e9-191">dize</span><span class="sxs-lookup"><span data-stu-id="354e9-191">string</span></span>  | <span data-ttu-id="354e9-192">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-192">yes</span></span>      | <span data-ttu-id="354e9-193">Paket kimliği, küçük harf</span><span class="sxs-lookup"><span data-stu-id="354e9-193">The package ID, lowercase</span></span>
<span data-ttu-id="354e9-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="354e9-194">LOWER_VERSION</span></span> | <span data-ttu-id="354e9-195">URL</span><span class="sxs-lookup"><span data-stu-id="354e9-195">URL</span></span>    | <span data-ttu-id="354e9-196">tamsayı</span><span class="sxs-lookup"><span data-stu-id="354e9-196">integer</span></span> | <span data-ttu-id="354e9-197">Evet</span><span class="sxs-lookup"><span data-stu-id="354e9-197">yes</span></span>      | <span data-ttu-id="354e9-198">Normalleştirilmiş ve küçük harf yapılmış Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="354e9-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="354e9-199">Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallar kullanarak küçük harf yapılmış. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="354e9-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="354e9-200">`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kuralları](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="354e9-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="354e9-201">Başka bir deyişle, bu durumda SemVer 2.0.0 belirtimine göre izin verilen derleme meta verilerin tutulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="354e9-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="354e9-202">Yanıt gövdesi</span><span class="sxs-lookup"><span data-stu-id="354e9-202">Response body</span></span>

<span data-ttu-id="354e9-203">Paketin paket kaynak var, 200 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="354e9-204">Yanıt gövdesi içinde karşılık gelen .nupkg bulunan .nuspec olan paket bildirimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="354e9-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="354e9-205">.nuspec bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="354e9-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="354e9-206">Paketin paket kaynak mevcut değilse bir 404 durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="354e9-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="354e9-207">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="354e9-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="354e9-208">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="354e9-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
