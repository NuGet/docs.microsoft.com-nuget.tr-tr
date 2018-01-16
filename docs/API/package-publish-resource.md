---
title: "Anında iletme ve Delete, NuGet API | Microsoft Docs"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Yayımlama hizmeti, istemcilerin yeni paketleri yayımlama ve unlist veya var olan paketleri silmek olanak tanır."
keywords: "NuGet API itme paket NuGet API Sil paket, NuGet API unlist paketi, NuGet API karşıya yükleme paketi, NuGet API'si paketi oluşturma"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="783c7-104">Anında iletme ve silin</span><span class="sxs-lookup"><span data-stu-id="783c7-104">Push and Delete</span></span>

<span data-ttu-id="783c7-105">Anında iletme Sil (veya unlist, bağlı sunucu uygulaması) mümkündür ve relist NuGet V3 API kullanarak paketler.</span><span class="sxs-lookup"><span data-stu-id="783c7-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="783c7-106">Bu işlemler kapatarak dayalı `PackagePublish` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="783c7-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="783c7-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="783c7-107">Versioning</span></span>

<span data-ttu-id="783c7-108">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="783c7-108">The following `@type` value is used:</span></span>

<span data-ttu-id="783c7-109">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="783c7-109">@type value</span></span>          | <span data-ttu-id="783c7-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="783c7-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="783c7-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="783c7-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="783c7-112">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="783c7-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="783c7-113">Temel URL</span><span class="sxs-lookup"><span data-stu-id="783c7-113">Base URL</span></span>

<span data-ttu-id="783c7-114">Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="783c7-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="783c7-115">Aşağıdaki belgeler için nuget.org URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="783c7-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="783c7-116">Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için bir yer tutucu olarak `@id` değeri hizmet dizininde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="783c7-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="783c7-117">Protokol aynı olduğundan bu URL eski V2 itme bitiş noktası ile aynı konumda işaret olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="783c7-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="783c7-118">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="783c7-118">HTTP methods</span></span>

<span data-ttu-id="783c7-119">`PUT`, `POST` Ve `DELETE` HTTP yöntemleri, bu kaynak tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="783c7-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="783c7-120">Hangi yöntemlerin her noktadaki desteklediği için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="783c7-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="783c7-121">Bir paket gönderme</span><span class="sxs-lookup"><span data-stu-id="783c7-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="783c7-122">nuget.org sahip [ek gereksinimler](NuGet-Protocols.md) itme uç noktasıyla etkileşim için.</span><span class="sxs-lookup"><span data-stu-id="783c7-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="783c7-123">nuget.org aşağıdaki API kullanarak koymadan yeni paketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="783c7-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="783c7-124">Sağlanan Kimliğini ve sürümünü paketiyle zaten varsa, nuget.org itme reddeder.</span><span class="sxs-lookup"><span data-stu-id="783c7-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="783c7-125">Mevcut bir paketi değiştirerek diğer paket kaynaklarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="783c7-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="783c7-126">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="783c7-126">Request parameters</span></span>

<span data-ttu-id="783c7-127">Ad</span><span class="sxs-lookup"><span data-stu-id="783c7-127">Name</span></span>           | <span data-ttu-id="783c7-128">İçindeki</span><span class="sxs-lookup"><span data-stu-id="783c7-128">In</span></span>     | <span data-ttu-id="783c7-129">Tür</span><span class="sxs-lookup"><span data-stu-id="783c7-129">Type</span></span>   | <span data-ttu-id="783c7-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="783c7-130">Required</span></span> | <span data-ttu-id="783c7-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="783c7-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="783c7-132">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="783c7-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="783c7-133">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="783c7-133">Header</span></span> | <span data-ttu-id="783c7-134">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-134">string</span></span> | <span data-ttu-id="783c7-135">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-135">yes</span></span>      | <span data-ttu-id="783c7-136">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="783c7-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="783c7-137">API anahtarını paket kaynağından kullanıcı tarafından onayınızı ve istemciyi yapılandırılmış donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="783c7-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="783c7-138">Hiçbir belirli dize biçimi zorunlu ancak API anahtarı uzunluğu HTTP üstbilgi değerleri için makul bir boyut aşamaz.</span><span class="sxs-lookup"><span data-stu-id="783c7-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="783c7-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="783c7-139">Request body</span></span>

<span data-ttu-id="783c7-140">İstek gövdesini şu biçimde gelmelidir:</span><span class="sxs-lookup"><span data-stu-id="783c7-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="783c7-141">Çok bölümlü form verilerinin</span><span class="sxs-lookup"><span data-stu-id="783c7-141">Multipart form data</span></span>

<span data-ttu-id="783c7-142">İstek üstbilgisi `Content-Type` olan `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır.</span><span class="sxs-lookup"><span data-stu-id="783c7-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="783c7-143">Çok bölümlü gövde sonraki öğelerde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="783c7-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="783c7-144">Dosya adı veya çok parçalı öğelerinin diğer tüm üst bilgileri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="783c7-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="783c7-145">Yanıt</span><span class="sxs-lookup"><span data-stu-id="783c7-145">Response</span></span>

<span data-ttu-id="783c7-146">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="783c7-146">Status Code</span></span> | <span data-ttu-id="783c7-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="783c7-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="783c7-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="783c7-148">201, 202</span></span>    | <span data-ttu-id="783c7-149">Paket başarıyla gönderilir</span><span class="sxs-lookup"><span data-stu-id="783c7-149">The package was successfully pushed</span></span>
<span data-ttu-id="783c7-150">400</span><span class="sxs-lookup"><span data-stu-id="783c7-150">400</span></span>         | <span data-ttu-id="783c7-151">Belirtilen paket geçersiz</span><span class="sxs-lookup"><span data-stu-id="783c7-151">The provided package is invalid</span></span>
<span data-ttu-id="783c7-152">409</span><span class="sxs-lookup"><span data-stu-id="783c7-152">409</span></span>         | <span data-ttu-id="783c7-153">Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.</span><span class="sxs-lookup"><span data-stu-id="783c7-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="783c7-154">Sunucu uygulamaları bir paketi başarıyla gönderildiğinde döndürülen başarı durum kodu farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="783c7-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="783c7-155">Paket Sil</span><span class="sxs-lookup"><span data-stu-id="783c7-155">Delete a package</span></span>

<span data-ttu-id="783c7-156">nuget.org yorumlar paketi silme isteği olarak "unlist" bir.</span><span class="sxs-lookup"><span data-stu-id="783c7-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="783c7-157">Bu paketin paket varolan Tüketiciler için hala kullanılabilir olduğundan, ancak paket artık arama sonuçlarında veya web arabirimi görünür anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="783c7-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="783c7-158">Bu uygulama hakkında daha fazla bilgi için bkz: [silinen paketler](../policies/deleting-packages.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="783c7-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="783c7-159">Bu sinyal sabit delete olarak yorumlama, yumuşak silin veya unlist ücretsiz diğer sunucu uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="783c7-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="783c7-160">Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API destekleyen bir sunucu uygulaması) destekleyen bir unlist veya bir yapılandırma seçeneği göre sabit bir delete olarak bu isteği işleme.</span><span class="sxs-lookup"><span data-stu-id="783c7-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="783c7-161">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="783c7-161">Request parameters</span></span>

<span data-ttu-id="783c7-162">Ad</span><span class="sxs-lookup"><span data-stu-id="783c7-162">Name</span></span>           | <span data-ttu-id="783c7-163">İçindeki</span><span class="sxs-lookup"><span data-stu-id="783c7-163">In</span></span>     | <span data-ttu-id="783c7-164">Tür</span><span class="sxs-lookup"><span data-stu-id="783c7-164">Type</span></span>   | <span data-ttu-id="783c7-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="783c7-165">Required</span></span> | <span data-ttu-id="783c7-166">Notlar</span><span class="sxs-lookup"><span data-stu-id="783c7-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="783c7-167">Kimlik</span><span class="sxs-lookup"><span data-stu-id="783c7-167">ID</span></span>             | <span data-ttu-id="783c7-168">URL</span><span class="sxs-lookup"><span data-stu-id="783c7-168">URL</span></span>    | <span data-ttu-id="783c7-169">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-169">string</span></span> | <span data-ttu-id="783c7-170">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-170">yes</span></span>      | <span data-ttu-id="783c7-171">Silmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="783c7-171">The ID of the package to delete</span></span>
<span data-ttu-id="783c7-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="783c7-172">VERSION</span></span>        | <span data-ttu-id="783c7-173">URL</span><span class="sxs-lookup"><span data-stu-id="783c7-173">URL</span></span>    | <span data-ttu-id="783c7-174">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-174">string</span></span> | <span data-ttu-id="783c7-175">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-175">yes</span></span>      | <span data-ttu-id="783c7-176">Silmek için paketin sürümü</span><span class="sxs-lookup"><span data-stu-id="783c7-176">The version of the package to delete</span></span>
<span data-ttu-id="783c7-177">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="783c7-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="783c7-178">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="783c7-178">Header</span></span> | <span data-ttu-id="783c7-179">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-179">string</span></span> | <span data-ttu-id="783c7-180">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-180">yes</span></span>      | <span data-ttu-id="783c7-181">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="783c7-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="783c7-182">Yanıt</span><span class="sxs-lookup"><span data-stu-id="783c7-182">Response</span></span>

<span data-ttu-id="783c7-183">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="783c7-183">Status Code</span></span> | <span data-ttu-id="783c7-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="783c7-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="783c7-185">204</span><span class="sxs-lookup"><span data-stu-id="783c7-185">204</span></span>         | <span data-ttu-id="783c7-186">Paket silindi</span><span class="sxs-lookup"><span data-stu-id="783c7-186">The package was deleted</span></span>
<span data-ttu-id="783c7-187">404</span><span class="sxs-lookup"><span data-stu-id="783c7-187">404</span></span>         | <span data-ttu-id="783c7-188">İle sağlanan bir paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="783c7-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="783c7-189">Bir paket relist</span><span class="sxs-lookup"><span data-stu-id="783c7-189">Relist a package</span></span>

<span data-ttu-id="783c7-190">Bir paket listelenmemiş ise, bu paket "relist" uç nokta kullanarak arama sonuçlarında bir kez daha görünür hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="783c7-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="783c7-191">Aynı şekilde olan bu uç noktaya sahip [Sil (unlist) uç noktası](#delete-a-package) ancak kullanır `POST` yerine HTTP yöntemini `DELETE` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="783c7-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="783c7-192">Paket zaten listeleniyorsa, istek hala başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="783c7-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="783c7-193">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="783c7-193">Request parameters</span></span>

<span data-ttu-id="783c7-194">Ad</span><span class="sxs-lookup"><span data-stu-id="783c7-194">Name</span></span>           | <span data-ttu-id="783c7-195">İçindeki</span><span class="sxs-lookup"><span data-stu-id="783c7-195">In</span></span>     | <span data-ttu-id="783c7-196">Tür</span><span class="sxs-lookup"><span data-stu-id="783c7-196">Type</span></span>   | <span data-ttu-id="783c7-197">Gerekli</span><span class="sxs-lookup"><span data-stu-id="783c7-197">Required</span></span> | <span data-ttu-id="783c7-198">Notlar</span><span class="sxs-lookup"><span data-stu-id="783c7-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="783c7-199">Kimlik</span><span class="sxs-lookup"><span data-stu-id="783c7-199">ID</span></span>             | <span data-ttu-id="783c7-200">URL</span><span class="sxs-lookup"><span data-stu-id="783c7-200">URL</span></span>    | <span data-ttu-id="783c7-201">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-201">string</span></span> | <span data-ttu-id="783c7-202">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-202">yes</span></span>      | <span data-ttu-id="783c7-203">Relist paket kimliği</span><span class="sxs-lookup"><span data-stu-id="783c7-203">The ID of the package to relist</span></span>
<span data-ttu-id="783c7-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="783c7-204">VERSION</span></span>        | <span data-ttu-id="783c7-205">URL</span><span class="sxs-lookup"><span data-stu-id="783c7-205">URL</span></span>    | <span data-ttu-id="783c7-206">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-206">string</span></span> | <span data-ttu-id="783c7-207">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-207">yes</span></span>      | <span data-ttu-id="783c7-208">Relist Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="783c7-208">The version of the package to relist</span></span>
<span data-ttu-id="783c7-209">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="783c7-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="783c7-210">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="783c7-210">Header</span></span> | <span data-ttu-id="783c7-211">dize</span><span class="sxs-lookup"><span data-stu-id="783c7-211">string</span></span> | <span data-ttu-id="783c7-212">Evet</span><span class="sxs-lookup"><span data-stu-id="783c7-212">yes</span></span>      | <span data-ttu-id="783c7-213">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="783c7-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="783c7-214">Yanıt</span><span class="sxs-lookup"><span data-stu-id="783c7-214">Response</span></span>

<span data-ttu-id="783c7-215">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="783c7-215">Status Code</span></span> | <span data-ttu-id="783c7-216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="783c7-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="783c7-217">200</span><span class="sxs-lookup"><span data-stu-id="783c7-217">200</span></span>         | <span data-ttu-id="783c7-218">Paket artık listelenir</span><span class="sxs-lookup"><span data-stu-id="783c7-218">The package is now listed</span></span>
<span data-ttu-id="783c7-219">404</span><span class="sxs-lookup"><span data-stu-id="783c7-219">404</span></span>         | <span data-ttu-id="783c7-220">İle sağlanan bir paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="783c7-220">No package with the provided `ID` and `VERSION` exists</span></span>
