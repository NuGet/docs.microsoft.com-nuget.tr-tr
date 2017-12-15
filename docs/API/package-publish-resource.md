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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="9ed33-104">Anında iletme ve silin</span><span class="sxs-lookup"><span data-stu-id="9ed33-104">Push and Delete</span></span>

<span data-ttu-id="9ed33-105">Anında iletme ve silme (veya unlist, bağlı sunucu uygulaması) mümkündür NuGet V3 API'yi kullanarak paketler.</span><span class="sxs-lookup"><span data-stu-id="9ed33-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="9ed33-106">İki işlem kapatarak dayalı `PackagePublish` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9ed33-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9ed33-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ed33-107">Versioning</span></span>

<span data-ttu-id="9ed33-108">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9ed33-108">The following `@type` value is used:</span></span>

<span data-ttu-id="9ed33-109">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="9ed33-109">@type value</span></span>          | <span data-ttu-id="9ed33-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="9ed33-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="9ed33-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="9ed33-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="9ed33-112">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="9ed33-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9ed33-113">Temel URL</span><span class="sxs-lookup"><span data-stu-id="9ed33-113">Base URL</span></span>

<span data-ttu-id="9ed33-114">Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9ed33-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="9ed33-115">Aşağıdaki belgeler için nuget.org URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ed33-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="9ed33-116">Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için bir yer tutucu olarak `@id` değeri hizmet dizininde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="9ed33-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="9ed33-117">Protokol aynı olduğundan bu URL eski V2 itme bitiş noktası ile aynı konumda işaret olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9ed33-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9ed33-118">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="9ed33-118">HTTP methods</span></span>

<span data-ttu-id="9ed33-119">`PUT` Ve `DELETE` HTTP yöntemleri, bu kaynak tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="9ed33-120">Hangi yöntemlerin her noktadaki desteklediği için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="9ed33-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="9ed33-121">Bir paket gönderme</span><span class="sxs-lookup"><span data-stu-id="9ed33-121">Push a package</span></span>

<span data-ttu-id="9ed33-122">nuget.org aşağıdaki API kullanarak koymadan yeni paketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="9ed33-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="9ed33-123">Sağlanan Kimliğini ve sürümünü paketiyle zaten varsa, nuget.org itme reddeder.</span><span class="sxs-lookup"><span data-stu-id="9ed33-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="9ed33-124">Mevcut bir paketi değiştirerek diğer paket kaynaklarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="9ed33-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="9ed33-125">Request parameters</span></span>

<span data-ttu-id="9ed33-126">Ad</span><span class="sxs-lookup"><span data-stu-id="9ed33-126">Name</span></span>           | <span data-ttu-id="9ed33-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="9ed33-127">In</span></span>     | <span data-ttu-id="9ed33-128">Tür</span><span class="sxs-lookup"><span data-stu-id="9ed33-128">Type</span></span>   | <span data-ttu-id="9ed33-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9ed33-129">Required</span></span> | <span data-ttu-id="9ed33-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="9ed33-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9ed33-131">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="9ed33-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9ed33-132">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="9ed33-132">Header</span></span> | <span data-ttu-id="9ed33-133">dize</span><span class="sxs-lookup"><span data-stu-id="9ed33-133">string</span></span> | <span data-ttu-id="9ed33-134">Evet</span><span class="sxs-lookup"><span data-stu-id="9ed33-134">yes</span></span>      | <span data-ttu-id="9ed33-135">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9ed33-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="9ed33-136">API anahtarını paket kaynağından kullanıcı tarafından onayınızı ve istemciyi yapılandırılmış donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="9ed33-137">Hiçbir belirli dize biçimi zorunlu ancak API anahtarı uzunluğu HTTP üstbilgi değerleri için makul bir boyut aşamaz.</span><span class="sxs-lookup"><span data-stu-id="9ed33-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="9ed33-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9ed33-138">Request body</span></span>

<span data-ttu-id="9ed33-139">İstek gövdesini şu biçimde gelmelidir:</span><span class="sxs-lookup"><span data-stu-id="9ed33-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="9ed33-140">Çok bölümlü form verilerinin</span><span class="sxs-lookup"><span data-stu-id="9ed33-140">Multipart form data</span></span>

<span data-ttu-id="9ed33-141">İstek üstbilgisi `Content-Type` olan `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır.</span><span class="sxs-lookup"><span data-stu-id="9ed33-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="9ed33-142">Çok bölümlü gövde sonraki öğelerde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="9ed33-143">Dosya adı veya çok parçalı öğelerinin diğer tüm üst bilgileri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="9ed33-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="9ed33-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="9ed33-144">Response</span></span>

<span data-ttu-id="9ed33-145">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="9ed33-145">Status Code</span></span> | <span data-ttu-id="9ed33-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9ed33-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="9ed33-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="9ed33-147">201, 202</span></span>    | <span data-ttu-id="9ed33-148">Paket başarıyla gönderilir</span><span class="sxs-lookup"><span data-stu-id="9ed33-148">The package was successfully pushed</span></span>
<span data-ttu-id="9ed33-149">400</span><span class="sxs-lookup"><span data-stu-id="9ed33-149">400</span></span>         | <span data-ttu-id="9ed33-150">Belirtilen paket geçersiz</span><span class="sxs-lookup"><span data-stu-id="9ed33-150">The provided package is invalid</span></span>
<span data-ttu-id="9ed33-151">409</span><span class="sxs-lookup"><span data-stu-id="9ed33-151">409</span></span>         | <span data-ttu-id="9ed33-152">Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.</span><span class="sxs-lookup"><span data-stu-id="9ed33-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="9ed33-153">Sunucu uygulamaları bir paketi başarıyla gönderildiğinde döndürülen başarı durum kodu farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="9ed33-154">Paket Sil</span><span class="sxs-lookup"><span data-stu-id="9ed33-154">Delete a package</span></span>

<span data-ttu-id="9ed33-155">nuget.org yorumlar paketi silme isteği olarak "unlist" bir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="9ed33-156">Bu paketin paket varolan Tüketiciler için hala kullanılabilir olduğundan, ancak paket artık arama sonuçlarında veya web arabirimi görünür anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9ed33-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="9ed33-157">Bu uygulama hakkında daha fazla bilgi için bkz: [silinen paketler](../policies/deleting-packages.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="9ed33-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="9ed33-158">Bu sinyal sabit delete olarak yorumlama, yumuşak silin veya unlist ücretsiz diğer sunucu uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="9ed33-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="9ed33-159">Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API destekleyen bir sunucu uygulaması) destekleyen bir unlist veya bir yapılandırma seçeneği göre sabit bir delete olarak bu isteği işleme.</span><span class="sxs-lookup"><span data-stu-id="9ed33-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9ed33-160">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="9ed33-160">Request parameters</span></span>

<span data-ttu-id="9ed33-161">Ad</span><span class="sxs-lookup"><span data-stu-id="9ed33-161">Name</span></span>           | <span data-ttu-id="9ed33-162">İçindeki</span><span class="sxs-lookup"><span data-stu-id="9ed33-162">In</span></span>     | <span data-ttu-id="9ed33-163">Tür</span><span class="sxs-lookup"><span data-stu-id="9ed33-163">Type</span></span>   | <span data-ttu-id="9ed33-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9ed33-164">Required</span></span> | <span data-ttu-id="9ed33-165">Notlar</span><span class="sxs-lookup"><span data-stu-id="9ed33-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9ed33-166">Kimlik</span><span class="sxs-lookup"><span data-stu-id="9ed33-166">ID</span></span>             | <span data-ttu-id="9ed33-167">URL</span><span class="sxs-lookup"><span data-stu-id="9ed33-167">URL</span></span>    | <span data-ttu-id="9ed33-168">dize</span><span class="sxs-lookup"><span data-stu-id="9ed33-168">string</span></span> | <span data-ttu-id="9ed33-169">Evet</span><span class="sxs-lookup"><span data-stu-id="9ed33-169">yes</span></span>      | <span data-ttu-id="9ed33-170">Silmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="9ed33-170">The ID of the package to delete</span></span>
<span data-ttu-id="9ed33-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="9ed33-171">VERSION</span></span>        | <span data-ttu-id="9ed33-172">URL</span><span class="sxs-lookup"><span data-stu-id="9ed33-172">URL</span></span>    | <span data-ttu-id="9ed33-173">dize</span><span class="sxs-lookup"><span data-stu-id="9ed33-173">string</span></span> | <span data-ttu-id="9ed33-174">Evet</span><span class="sxs-lookup"><span data-stu-id="9ed33-174">yes</span></span>      | <span data-ttu-id="9ed33-175">Silmek için paketin sürümü</span><span class="sxs-lookup"><span data-stu-id="9ed33-175">The version of the package to delete</span></span>
<span data-ttu-id="9ed33-176">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="9ed33-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9ed33-177">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="9ed33-177">Header</span></span> | <span data-ttu-id="9ed33-178">dize</span><span class="sxs-lookup"><span data-stu-id="9ed33-178">string</span></span> | <span data-ttu-id="9ed33-179">Evet</span><span class="sxs-lookup"><span data-stu-id="9ed33-179">yes</span></span>      | <span data-ttu-id="9ed33-180">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9ed33-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9ed33-181">Yanıt</span><span class="sxs-lookup"><span data-stu-id="9ed33-181">Response</span></span>

<span data-ttu-id="9ed33-182">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="9ed33-182">Status Code</span></span> | <span data-ttu-id="9ed33-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9ed33-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="9ed33-184">204</span><span class="sxs-lookup"><span data-stu-id="9ed33-184">204</span></span>         | <span data-ttu-id="9ed33-185">Paket silindi</span><span class="sxs-lookup"><span data-stu-id="9ed33-185">The package was deleted</span></span>
<span data-ttu-id="9ed33-186">404</span><span class="sxs-lookup"><span data-stu-id="9ed33-186">404</span></span>         | <span data-ttu-id="9ed33-187">İle sağlanan bir paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="9ed33-187">No package with the provided `ID` and `VERSION` exists</span></span>
