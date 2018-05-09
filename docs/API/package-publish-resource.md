---
title: Anında iletme ve Delete, NuGet API
description: Yayımlama hizmeti, istemcilerin yeni paketleri yayımlama ve unlist veya var olan paketleri silmek olanak tanır.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="b46a2-103">Anında iletme ve silin</span><span class="sxs-lookup"><span data-stu-id="b46a2-103">Push and Delete</span></span>

<span data-ttu-id="b46a2-104">Anında iletme Sil (veya unlist, bağlı sunucu uygulaması) mümkündür ve relist NuGet V3 API kullanarak paketler.</span><span class="sxs-lookup"><span data-stu-id="b46a2-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="b46a2-105">Bu işlemler kapatarak dayalı `PackagePublish` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b46a2-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b46a2-106">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="b46a2-106">Versioning</span></span>

<span data-ttu-id="b46a2-107">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="b46a2-107">The following `@type` value is used:</span></span>

<span data-ttu-id="b46a2-108">@type Değer</span><span class="sxs-lookup"><span data-stu-id="b46a2-108">@type value</span></span>          | <span data-ttu-id="b46a2-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="b46a2-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="b46a2-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="b46a2-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="b46a2-111">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="b46a2-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b46a2-112">Temel URL</span><span class="sxs-lookup"><span data-stu-id="b46a2-112">Base URL</span></span>

<span data-ttu-id="b46a2-113">Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b46a2-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b46a2-114">Aşağıdaki belgeler için nuget.org URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b46a2-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b46a2-115">Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için bir yer tutucu olarak `@id` değeri hizmet dizininde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="b46a2-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="b46a2-116">Protokol aynı olduğundan bu URL eski V2 itme bitiş noktası ile aynı konumda işaret olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b46a2-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b46a2-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="b46a2-117">HTTP methods</span></span>

<span data-ttu-id="b46a2-118">`PUT`, `POST` Ve `DELETE` HTTP yöntemleri, bu kaynak tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="b46a2-119">Hangi yöntemlerin her noktadaki desteklediği için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="b46a2-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="b46a2-120">Bir paket gönderme</span><span class="sxs-lookup"><span data-stu-id="b46a2-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="b46a2-121">nuget.org sahip [ek gereksinimler](NuGet-Protocols.md) itme uç noktasıyla etkileşim için.</span><span class="sxs-lookup"><span data-stu-id="b46a2-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="b46a2-122">nuget.org aşağıdaki API kullanarak koymadan yeni paketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="b46a2-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="b46a2-123">Sağlanan Kimliğini ve sürümünü paketiyle zaten varsa, nuget.org itme reddeder.</span><span class="sxs-lookup"><span data-stu-id="b46a2-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="b46a2-124">Mevcut bir paketi değiştirerek diğer paket kaynaklarını destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="b46a2-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="b46a2-125">Request parameters</span></span>

<span data-ttu-id="b46a2-126">Ad</span><span class="sxs-lookup"><span data-stu-id="b46a2-126">Name</span></span>           | <span data-ttu-id="b46a2-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="b46a2-127">In</span></span>     | <span data-ttu-id="b46a2-128">Tür</span><span class="sxs-lookup"><span data-stu-id="b46a2-128">Type</span></span>   | <span data-ttu-id="b46a2-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b46a2-129">Required</span></span> | <span data-ttu-id="b46a2-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="b46a2-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b46a2-131">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="b46a2-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b46a2-132">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="b46a2-132">Header</span></span> | <span data-ttu-id="b46a2-133">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-133">string</span></span> | <span data-ttu-id="b46a2-134">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-134">yes</span></span>      | <span data-ttu-id="b46a2-135">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b46a2-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b46a2-136">API anahtarını paket kaynağından kullanıcı tarafından onayınızı ve istemciyi yapılandırılmış donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b46a2-137">Hiçbir belirli dize biçimi zorunlu ancak API anahtarı uzunluğu HTTP üstbilgi değerleri için makul bir boyut aşamaz.</span><span class="sxs-lookup"><span data-stu-id="b46a2-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b46a2-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b46a2-138">Request body</span></span>

<span data-ttu-id="b46a2-139">İstek gövdesini şu biçimde gelmelidir:</span><span class="sxs-lookup"><span data-stu-id="b46a2-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="b46a2-140">Çok bölümlü form verilerinin</span><span class="sxs-lookup"><span data-stu-id="b46a2-140">Multipart form data</span></span>

<span data-ttu-id="b46a2-141">İstek üstbilgisi `Content-Type` olan `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır.</span><span class="sxs-lookup"><span data-stu-id="b46a2-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="b46a2-142">Çok bölümlü gövde sonraki öğelerde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="b46a2-143">Dosya adı veya çok parçalı öğelerinin diğer tüm üst bilgileri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="b46a2-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="b46a2-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b46a2-144">Response</span></span>

<span data-ttu-id="b46a2-145">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="b46a2-145">Status Code</span></span> | <span data-ttu-id="b46a2-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b46a2-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="b46a2-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="b46a2-147">201, 202</span></span>    | <span data-ttu-id="b46a2-148">Paket başarıyla gönderilir</span><span class="sxs-lookup"><span data-stu-id="b46a2-148">The package was successfully pushed</span></span>
<span data-ttu-id="b46a2-149">400</span><span class="sxs-lookup"><span data-stu-id="b46a2-149">400</span></span>         | <span data-ttu-id="b46a2-150">Belirtilen paket geçersiz</span><span class="sxs-lookup"><span data-stu-id="b46a2-150">The provided package is invalid</span></span>
<span data-ttu-id="b46a2-151">409</span><span class="sxs-lookup"><span data-stu-id="b46a2-151">409</span></span>         | <span data-ttu-id="b46a2-152">Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.</span><span class="sxs-lookup"><span data-stu-id="b46a2-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="b46a2-153">Sunucu uygulamaları bir paketi başarıyla gönderildiğinde döndürülen başarı durum kodu farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="b46a2-154">Paket Sil</span><span class="sxs-lookup"><span data-stu-id="b46a2-154">Delete a package</span></span>

<span data-ttu-id="b46a2-155">nuget.org yorumlar paketi silme isteği olarak "unlist" bir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="b46a2-156">Bu paketin paket varolan Tüketiciler için hala kullanılabilir olduğundan, ancak paket artık arama sonuçlarında veya web arabirimi görünür anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b46a2-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="b46a2-157">Bu uygulama hakkında daha fazla bilgi için bkz: [silinen paketler](../policies/deleting-packages.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="b46a2-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="b46a2-158">Bu sinyal sabit delete olarak yorumlama, yumuşak silin veya unlist ücretsiz diğer sunucu uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="b46a2-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="b46a2-159">Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API destekleyen bir sunucu uygulaması) destekleyen bir unlist veya bir yapılandırma seçeneği göre sabit bir delete olarak bu isteği işleme.</span><span class="sxs-lookup"><span data-stu-id="b46a2-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b46a2-160">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="b46a2-160">Request parameters</span></span>

<span data-ttu-id="b46a2-161">Ad</span><span class="sxs-lookup"><span data-stu-id="b46a2-161">Name</span></span>           | <span data-ttu-id="b46a2-162">İçindeki</span><span class="sxs-lookup"><span data-stu-id="b46a2-162">In</span></span>     | <span data-ttu-id="b46a2-163">Tür</span><span class="sxs-lookup"><span data-stu-id="b46a2-163">Type</span></span>   | <span data-ttu-id="b46a2-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b46a2-164">Required</span></span> | <span data-ttu-id="b46a2-165">Notlar</span><span class="sxs-lookup"><span data-stu-id="b46a2-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b46a2-166">Kimlik</span><span class="sxs-lookup"><span data-stu-id="b46a2-166">ID</span></span>             | <span data-ttu-id="b46a2-167">URL</span><span class="sxs-lookup"><span data-stu-id="b46a2-167">URL</span></span>    | <span data-ttu-id="b46a2-168">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-168">string</span></span> | <span data-ttu-id="b46a2-169">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-169">yes</span></span>      | <span data-ttu-id="b46a2-170">Silmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="b46a2-170">The ID of the package to delete</span></span>
<span data-ttu-id="b46a2-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="b46a2-171">VERSION</span></span>        | <span data-ttu-id="b46a2-172">URL</span><span class="sxs-lookup"><span data-stu-id="b46a2-172">URL</span></span>    | <span data-ttu-id="b46a2-173">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-173">string</span></span> | <span data-ttu-id="b46a2-174">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-174">yes</span></span>      | <span data-ttu-id="b46a2-175">Silmek için paketin sürümü</span><span class="sxs-lookup"><span data-stu-id="b46a2-175">The version of the package to delete</span></span>
<span data-ttu-id="b46a2-176">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="b46a2-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b46a2-177">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="b46a2-177">Header</span></span> | <span data-ttu-id="b46a2-178">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-178">string</span></span> | <span data-ttu-id="b46a2-179">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-179">yes</span></span>      | <span data-ttu-id="b46a2-180">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b46a2-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b46a2-181">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b46a2-181">Response</span></span>

<span data-ttu-id="b46a2-182">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="b46a2-182">Status Code</span></span> | <span data-ttu-id="b46a2-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b46a2-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="b46a2-184">204</span><span class="sxs-lookup"><span data-stu-id="b46a2-184">204</span></span>         | <span data-ttu-id="b46a2-185">Paket silindi</span><span class="sxs-lookup"><span data-stu-id="b46a2-185">The package was deleted</span></span>
<span data-ttu-id="b46a2-186">404</span><span class="sxs-lookup"><span data-stu-id="b46a2-186">404</span></span>         | <span data-ttu-id="b46a2-187">İle sağlanan bir paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="b46a2-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="b46a2-188">Bir paket relist</span><span class="sxs-lookup"><span data-stu-id="b46a2-188">Relist a package</span></span>

<span data-ttu-id="b46a2-189">Bir paket listelenmemiş ise, bu paket "relist" uç nokta kullanarak arama sonuçlarında bir kez daha görünür hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b46a2-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="b46a2-190">Aynı şekilde olan bu uç noktaya sahip [Sil (unlist) uç noktası](#delete-a-package) ancak kullanır `POST` yerine HTTP yöntemini `DELETE` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b46a2-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="b46a2-191">Paket zaten listeleniyorsa, istek hala başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="b46a2-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b46a2-192">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="b46a2-192">Request parameters</span></span>

<span data-ttu-id="b46a2-193">Ad</span><span class="sxs-lookup"><span data-stu-id="b46a2-193">Name</span></span>           | <span data-ttu-id="b46a2-194">İçindeki</span><span class="sxs-lookup"><span data-stu-id="b46a2-194">In</span></span>     | <span data-ttu-id="b46a2-195">Tür</span><span class="sxs-lookup"><span data-stu-id="b46a2-195">Type</span></span>   | <span data-ttu-id="b46a2-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b46a2-196">Required</span></span> | <span data-ttu-id="b46a2-197">Notlar</span><span class="sxs-lookup"><span data-stu-id="b46a2-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b46a2-198">Kimlik</span><span class="sxs-lookup"><span data-stu-id="b46a2-198">ID</span></span>             | <span data-ttu-id="b46a2-199">URL</span><span class="sxs-lookup"><span data-stu-id="b46a2-199">URL</span></span>    | <span data-ttu-id="b46a2-200">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-200">string</span></span> | <span data-ttu-id="b46a2-201">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-201">yes</span></span>      | <span data-ttu-id="b46a2-202">Relist paket kimliği</span><span class="sxs-lookup"><span data-stu-id="b46a2-202">The ID of the package to relist</span></span>
<span data-ttu-id="b46a2-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="b46a2-203">VERSION</span></span>        | <span data-ttu-id="b46a2-204">URL</span><span class="sxs-lookup"><span data-stu-id="b46a2-204">URL</span></span>    | <span data-ttu-id="b46a2-205">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-205">string</span></span> | <span data-ttu-id="b46a2-206">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-206">yes</span></span>      | <span data-ttu-id="b46a2-207">Relist Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="b46a2-207">The version of the package to relist</span></span>
<span data-ttu-id="b46a2-208">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="b46a2-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b46a2-209">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="b46a2-209">Header</span></span> | <span data-ttu-id="b46a2-210">dize</span><span class="sxs-lookup"><span data-stu-id="b46a2-210">string</span></span> | <span data-ttu-id="b46a2-211">Evet</span><span class="sxs-lookup"><span data-stu-id="b46a2-211">yes</span></span>      | <span data-ttu-id="b46a2-212">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b46a2-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b46a2-213">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b46a2-213">Response</span></span>

<span data-ttu-id="b46a2-214">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="b46a2-214">Status Code</span></span> | <span data-ttu-id="b46a2-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b46a2-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="b46a2-216">200</span><span class="sxs-lookup"><span data-stu-id="b46a2-216">200</span></span>         | <span data-ttu-id="b46a2-217">Paket artık listelenir</span><span class="sxs-lookup"><span data-stu-id="b46a2-217">The package is now listed</span></span>
<span data-ttu-id="b46a2-218">404</span><span class="sxs-lookup"><span data-stu-id="b46a2-218">404</span></span>         | <span data-ttu-id="b46a2-219">İle sağlanan bir paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="b46a2-219">No package with the provided `ID` and `VERSION` exists</span></span>
