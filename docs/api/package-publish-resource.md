---
title: Push ve DELETE, NuGet API
description: Yayımla hizmeti, istemcilerin yeni paketleri yayımlamasına ve var olan paketleri silmesine veya silmesine izin verir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773918"
---
# <a name="push-and-delete"></a><span data-ttu-id="59a98-103">Gönder ve Sil</span><span class="sxs-lookup"><span data-stu-id="59a98-103">Push and Delete</span></span>

<span data-ttu-id="59a98-104">Bu, sunucu uygulamasına bağlı olarak bir gönderme, silme (veya listesini kaldırma) ve NuGet v3 API 'sini kullanarak paketleri yeniden listelemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="59a98-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="59a98-105">Bu işlemler `PackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.</span><span class="sxs-lookup"><span data-stu-id="59a98-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="59a98-106">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="59a98-106">Versioning</span></span>

<span data-ttu-id="59a98-107">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="59a98-107">The following `@type` value is used:</span></span>

<span data-ttu-id="59a98-108">@type deeri</span><span class="sxs-lookup"><span data-stu-id="59a98-108">@type value</span></span>          | <span data-ttu-id="59a98-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="59a98-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="59a98-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="59a98-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="59a98-111">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="59a98-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="59a98-112">Temel URL</span><span class="sxs-lookup"><span data-stu-id="59a98-112">Base URL</span></span>

<span data-ttu-id="59a98-113">Aşağıdaki API 'Lerin temel URL 'SI, `@id` `PackagePublish/2.0.0` paket kaynağının [hizmet dizinindeki](service-index.md)kaynak özelliğinin değeridir.</span><span class="sxs-lookup"><span data-stu-id="59a98-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="59a98-114">Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="59a98-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="59a98-115">`https://www.nuget.org/api/v2/package`Hizmet dizininde bulunan değer için bir yer tutucu olarak düşünün `@id` .</span><span class="sxs-lookup"><span data-stu-id="59a98-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="59a98-116">Protokol aynı olduğundan, bu URL 'nin eski v2 gönderim uç noktasıyla aynı konuma işaret ettiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="59a98-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="59a98-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="59a98-117">HTTP methods</span></span>

<span data-ttu-id="59a98-118">`PUT`, `POST` Ve `DELETE` http yöntemleri bu kaynak tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="59a98-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="59a98-119">Her uç noktada desteklenen yöntemler için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="59a98-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="59a98-120">Paket gönder</span><span class="sxs-lookup"><span data-stu-id="59a98-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="59a98-121">nuget.org, gönderim uç noktasıyla etkileşim kurmak için [ek gereksinimlere](NuGet-Protocols.md) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="59a98-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="59a98-122">nuget.org, aşağıdaki API 'YI kullanarak yeni paketleri göndermeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="59a98-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="59a98-123">Belirtilen KIMLIĞE ve sürüme sahip paket zaten mevcutsa, nuget.org itme 'yi reddeder.</span><span class="sxs-lookup"><span data-stu-id="59a98-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="59a98-124">Diğer paket kaynakları, mevcut bir paketi değiştirmeyi destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="59a98-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="59a98-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59a98-125">Request parameters</span></span>

<span data-ttu-id="59a98-126">Name</span><span class="sxs-lookup"><span data-stu-id="59a98-126">Name</span></span>           | <span data-ttu-id="59a98-127">İçinde</span><span class="sxs-lookup"><span data-stu-id="59a98-127">In</span></span>     | <span data-ttu-id="59a98-128">Tür</span><span class="sxs-lookup"><span data-stu-id="59a98-128">Type</span></span>   | <span data-ttu-id="59a98-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59a98-129">Required</span></span> | <span data-ttu-id="59a98-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="59a98-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59a98-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="59a98-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="59a98-132">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="59a98-132">Header</span></span> | <span data-ttu-id="59a98-133">string</span><span class="sxs-lookup"><span data-stu-id="59a98-133">string</span></span> | <span data-ttu-id="59a98-134">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-134">yes</span></span>      | <span data-ttu-id="59a98-135">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="59a98-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="59a98-136">API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="59a98-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="59a98-137">Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="59a98-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="59a98-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="59a98-138">Request body</span></span>

<span data-ttu-id="59a98-139">İstek gövdesinin aşağıdaki biçimde gelmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="59a98-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="59a98-140">Çok parçalı form verileri</span><span class="sxs-lookup"><span data-stu-id="59a98-140">Multipart form data</span></span>

<span data-ttu-id="59a98-141">İstek üst bilgisi `Content-Type` `multipart/form-data` ve istek gövdesindeki ilk öğe, gönderilen. nupkg 'nin ham baytlardır.</span><span class="sxs-lookup"><span data-stu-id="59a98-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="59a98-142">Çok parçalı gövdedeki sonraki öğeler yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="59a98-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="59a98-143">Dosya adı veya çok parçalı öğelerin diğer üstbilgileri yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="59a98-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="59a98-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="59a98-144">Response</span></span>

<span data-ttu-id="59a98-145">Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="59a98-145">Status Code</span></span> | <span data-ttu-id="59a98-146">Anlamı</span><span class="sxs-lookup"><span data-stu-id="59a98-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="59a98-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="59a98-147">201, 202</span></span>    | <span data-ttu-id="59a98-148">Paket başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="59a98-148">The package was successfully pushed</span></span>
<span data-ttu-id="59a98-149">400</span><span class="sxs-lookup"><span data-stu-id="59a98-149">400</span></span>         | <span data-ttu-id="59a98-150">Belirtilen paket geçersiz</span><span class="sxs-lookup"><span data-stu-id="59a98-150">The provided package is invalid</span></span>
<span data-ttu-id="59a98-151">409</span><span class="sxs-lookup"><span data-stu-id="59a98-151">409</span></span>         | <span data-ttu-id="59a98-152">Belirtilen KIMLIĞE ve sürüme sahip bir paket zaten var</span><span class="sxs-lookup"><span data-stu-id="59a98-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="59a98-153">Sunucu uygulamaları, bir paket başarıyla gönderildiğinde döndürülen başarı durum koduna göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="59a98-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="59a98-154">Paket silme</span><span class="sxs-lookup"><span data-stu-id="59a98-154">Delete a package</span></span>

<span data-ttu-id="59a98-155">nuget.org paket silme isteğini "listeden kaldır" olarak yorumlar.</span><span class="sxs-lookup"><span data-stu-id="59a98-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="59a98-156">Bu, paketin mevcut paketin var olan tüketicilerine hala kullanılabildiği, ancak paketin artık arama sonuçlarında veya web arabiriminde görüntülenmediği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="59a98-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="59a98-157">Bu uygulama hakkında daha fazla bilgi için, [silinen paketler](../nuget-org/policies/deleting-packages.md) ilkesine bakın.</span><span class="sxs-lookup"><span data-stu-id="59a98-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="59a98-158">Diğer sunucu uygulamaları, bu sinyali sabit silme, geçici silme veya listeden kaldırma olarak yorumlamak için ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="59a98-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="59a98-159">Örneğin, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski v2 API 'sini destekleyen bir sunucu uygulama), bu isteğin bir yapılandırma seçeneğine bağlı olarak, bir listeden kaldır veya sabit bir Delete olarak işlenmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="59a98-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="59a98-160">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59a98-160">Request parameters</span></span>

<span data-ttu-id="59a98-161">Name</span><span class="sxs-lookup"><span data-stu-id="59a98-161">Name</span></span>           | <span data-ttu-id="59a98-162">İçinde</span><span class="sxs-lookup"><span data-stu-id="59a98-162">In</span></span>     | <span data-ttu-id="59a98-163">Tür</span><span class="sxs-lookup"><span data-stu-id="59a98-163">Type</span></span>   | <span data-ttu-id="59a98-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59a98-164">Required</span></span> | <span data-ttu-id="59a98-165">Notlar</span><span class="sxs-lookup"><span data-stu-id="59a98-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59a98-166">ID</span><span class="sxs-lookup"><span data-stu-id="59a98-166">ID</span></span>             | <span data-ttu-id="59a98-167">URL</span><span class="sxs-lookup"><span data-stu-id="59a98-167">URL</span></span>    | <span data-ttu-id="59a98-168">string</span><span class="sxs-lookup"><span data-stu-id="59a98-168">string</span></span> | <span data-ttu-id="59a98-169">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-169">yes</span></span>      | <span data-ttu-id="59a98-170">Silinecek paketin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="59a98-170">The ID of the package to delete</span></span>
<span data-ttu-id="59a98-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="59a98-171">VERSION</span></span>        | <span data-ttu-id="59a98-172">URL</span><span class="sxs-lookup"><span data-stu-id="59a98-172">URL</span></span>    | <span data-ttu-id="59a98-173">string</span><span class="sxs-lookup"><span data-stu-id="59a98-173">string</span></span> | <span data-ttu-id="59a98-174">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-174">yes</span></span>      | <span data-ttu-id="59a98-175">Silinecek paketin sürümü</span><span class="sxs-lookup"><span data-stu-id="59a98-175">The version of the package to delete</span></span>
<span data-ttu-id="59a98-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="59a98-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="59a98-177">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="59a98-177">Header</span></span> | <span data-ttu-id="59a98-178">string</span><span class="sxs-lookup"><span data-stu-id="59a98-178">string</span></span> | <span data-ttu-id="59a98-179">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-179">yes</span></span>      | <span data-ttu-id="59a98-180">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="59a98-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="59a98-181">Yanıt</span><span class="sxs-lookup"><span data-stu-id="59a98-181">Response</span></span>

<span data-ttu-id="59a98-182">Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="59a98-182">Status Code</span></span> | <span data-ttu-id="59a98-183">Anlamı</span><span class="sxs-lookup"><span data-stu-id="59a98-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="59a98-184">204</span><span class="sxs-lookup"><span data-stu-id="59a98-184">204</span></span>         | <span data-ttu-id="59a98-185">Paket silindi</span><span class="sxs-lookup"><span data-stu-id="59a98-185">The package was deleted</span></span>
<span data-ttu-id="59a98-186">404</span><span class="sxs-lookup"><span data-stu-id="59a98-186">404</span></span>         | <span data-ttu-id="59a98-187">Belirtilen `ID` ve mevcut bir paket yok `VERSION`</span><span class="sxs-lookup"><span data-stu-id="59a98-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="59a98-188">Bir paketi yeniden listeleme</span><span class="sxs-lookup"><span data-stu-id="59a98-188">Relist a package</span></span>

<span data-ttu-id="59a98-189">Bir paket listede yoksa, "relist" uç noktası kullanılarak bu paketi arama sonuçlarında bir kez daha görünür hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="59a98-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="59a98-190">Bu uç nokta, [Delete (Unlist) uç noktası](#delete-a-package) ile aynı şekle sahiptir ancak `POST` Yöntem yerine http yöntemini kullanır `DELETE` .</span><span class="sxs-lookup"><span data-stu-id="59a98-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="59a98-191">Paket zaten listeleniyorsa, istek yine de başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="59a98-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="59a98-192">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="59a98-192">Request parameters</span></span>

<span data-ttu-id="59a98-193">Name</span><span class="sxs-lookup"><span data-stu-id="59a98-193">Name</span></span>           | <span data-ttu-id="59a98-194">İçinde</span><span class="sxs-lookup"><span data-stu-id="59a98-194">In</span></span>     | <span data-ttu-id="59a98-195">Tür</span><span class="sxs-lookup"><span data-stu-id="59a98-195">Type</span></span>   | <span data-ttu-id="59a98-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59a98-196">Required</span></span> | <span data-ttu-id="59a98-197">Notlar</span><span class="sxs-lookup"><span data-stu-id="59a98-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59a98-198">ID</span><span class="sxs-lookup"><span data-stu-id="59a98-198">ID</span></span>             | <span data-ttu-id="59a98-199">URL</span><span class="sxs-lookup"><span data-stu-id="59a98-199">URL</span></span>    | <span data-ttu-id="59a98-200">string</span><span class="sxs-lookup"><span data-stu-id="59a98-200">string</span></span> | <span data-ttu-id="59a98-201">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-201">yes</span></span>      | <span data-ttu-id="59a98-202">Yeniden listelemek için paketin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="59a98-202">The ID of the package to relist</span></span>
<span data-ttu-id="59a98-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="59a98-203">VERSION</span></span>        | <span data-ttu-id="59a98-204">URL</span><span class="sxs-lookup"><span data-stu-id="59a98-204">URL</span></span>    | <span data-ttu-id="59a98-205">string</span><span class="sxs-lookup"><span data-stu-id="59a98-205">string</span></span> | <span data-ttu-id="59a98-206">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-206">yes</span></span>      | <span data-ttu-id="59a98-207">Yeniden listelemek için paketin sürümü</span><span class="sxs-lookup"><span data-stu-id="59a98-207">The version of the package to relist</span></span>
<span data-ttu-id="59a98-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="59a98-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="59a98-209">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="59a98-209">Header</span></span> | <span data-ttu-id="59a98-210">string</span><span class="sxs-lookup"><span data-stu-id="59a98-210">string</span></span> | <span data-ttu-id="59a98-211">evet</span><span class="sxs-lookup"><span data-stu-id="59a98-211">yes</span></span>      | <span data-ttu-id="59a98-212">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="59a98-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="59a98-213">Yanıt</span><span class="sxs-lookup"><span data-stu-id="59a98-213">Response</span></span>

<span data-ttu-id="59a98-214">Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="59a98-214">Status Code</span></span> | <span data-ttu-id="59a98-215">Anlamı</span><span class="sxs-lookup"><span data-stu-id="59a98-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="59a98-216">200</span><span class="sxs-lookup"><span data-stu-id="59a98-216">200</span></span>         | <span data-ttu-id="59a98-217">Paket artık listelendi</span><span class="sxs-lookup"><span data-stu-id="59a98-217">The package is now listed</span></span>
<span data-ttu-id="59a98-218">404</span><span class="sxs-lookup"><span data-stu-id="59a98-218">404</span></span>         | <span data-ttu-id="59a98-219">Belirtilen `ID` ve mevcut bir paket yok `VERSION`</span><span class="sxs-lookup"><span data-stu-id="59a98-219">No package with the provided `ID` and `VERSION` exists</span></span>
