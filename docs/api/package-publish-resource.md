---
title: Gönder ve Sil, NuGet API'si
description: Yayımlama hizmeti, yeni paket yayımlamasına ve listeden veya var olan paketleri Sil etmesine olanak tanır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426719"
---
# <a name="push-and-delete"></a><span data-ttu-id="46820-103">Gönder ve Sil</span><span class="sxs-lookup"><span data-stu-id="46820-103">Push and Delete</span></span>

<span data-ttu-id="46820-104">Anında iletme, silme (veya, bağlı sunucu uygulaması listeden da) mümkündür ve NuGet V3 API'yi kullanarak paketler yeniden listele.</span><span class="sxs-lookup"><span data-stu-id="46820-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="46820-105">Kapatarak bu işlemler temel `PackagePublish` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="46820-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="46820-106">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="46820-106">Versioning</span></span>

<span data-ttu-id="46820-107">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="46820-107">The following `@type` value is used:</span></span>

<span data-ttu-id="46820-108">@type Değer</span><span class="sxs-lookup"><span data-stu-id="46820-108">@type value</span></span>          | <span data-ttu-id="46820-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="46820-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="46820-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="46820-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="46820-111">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="46820-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="46820-112">Temel URL</span><span class="sxs-lookup"><span data-stu-id="46820-112">Base URL</span></span>

<span data-ttu-id="46820-113">Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="46820-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="46820-114">Nuget.org URL'si aşağıdaki belgeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46820-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="46820-115">Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için yer tutucu olarak `@id` değer hizmet dizinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="46820-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="46820-116">Protokol aynı olduğundan bu URL eski V2 anında iletme uç noktası ile aynı konuma işaret olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46820-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="46820-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="46820-117">HTTP methods</span></span>

<span data-ttu-id="46820-118">`PUT`, `POST` Ve `DELETE` bu kaynak tarafından desteklenen HTTP yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="46820-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="46820-119">Hangi yöntemler üzerinde her uç nokta için destekleniyor, aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="46820-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="46820-120">Bir paket gönderin</span><span class="sxs-lookup"><span data-stu-id="46820-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="46820-121">nuget.org sahip [ek gereksinimler](NuGet-Protocols.md) anında iletme uç noktası ile etkileşim kurmak için.</span><span class="sxs-lookup"><span data-stu-id="46820-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="46820-122">nuget.org aşağıdaki API'yi kullanarak koymadan yeni paketler destekler.</span><span class="sxs-lookup"><span data-stu-id="46820-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="46820-123">Paket kimliği ve sürüm sağlanan zaten varsa, anında iletme nuget.org reddeder.</span><span class="sxs-lookup"><span data-stu-id="46820-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="46820-124">Diğer paket kaynaklarını, var olan paketi değiştirerek destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="46820-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="46820-125">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="46820-125">Request parameters</span></span>

<span data-ttu-id="46820-126">Ad</span><span class="sxs-lookup"><span data-stu-id="46820-126">Name</span></span>           | <span data-ttu-id="46820-127">İçindeki</span><span class="sxs-lookup"><span data-stu-id="46820-127">In</span></span>     | <span data-ttu-id="46820-128">Tür</span><span class="sxs-lookup"><span data-stu-id="46820-128">Type</span></span>   | <span data-ttu-id="46820-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="46820-129">Required</span></span> | <span data-ttu-id="46820-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="46820-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="46820-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="46820-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="46820-132">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="46820-132">Header</span></span> | <span data-ttu-id="46820-133">dize</span><span class="sxs-lookup"><span data-stu-id="46820-133">string</span></span> | <span data-ttu-id="46820-134">evet</span><span class="sxs-lookup"><span data-stu-id="46820-134">yes</span></span>      | <span data-ttu-id="46820-135">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="46820-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="46820-136">API anahtarı kullanıcı tarafından paket kaynağından edinmiş ve istemciyi yapılandırılmış genel olmayan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="46820-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="46820-137">Hiçbir özel dize biçimi uygulanan ancak HTTP üstbilgi değerleri için makul bir boyutta API anahtarı uzunluğunu geçmemelidir.</span><span class="sxs-lookup"><span data-stu-id="46820-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="46820-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="46820-138">Request body</span></span>

<span data-ttu-id="46820-139">İstek gövdesi, aşağıdaki biçimde gelmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="46820-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="46820-140">Çok bölümlü form verilerinin</span><span class="sxs-lookup"><span data-stu-id="46820-140">Multipart form data</span></span>

<span data-ttu-id="46820-141">İstek üstbilgisi `Content-Type` olduğu `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır.</span><span class="sxs-lookup"><span data-stu-id="46820-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="46820-142">Çok bölümlü gövde sonraki öğeleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="46820-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="46820-143">Dosya adı veya diğer üst bilgilerini çok bölümlü öğelerin göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="46820-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="46820-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="46820-144">Response</span></span>

<span data-ttu-id="46820-145">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="46820-145">Status Code</span></span> | <span data-ttu-id="46820-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="46820-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="46820-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="46820-147">201, 202</span></span>    | <span data-ttu-id="46820-148">Paket başarıyla gönderildi</span><span class="sxs-lookup"><span data-stu-id="46820-148">The package was successfully pushed</span></span>
<span data-ttu-id="46820-149">400</span><span class="sxs-lookup"><span data-stu-id="46820-149">400</span></span>         | <span data-ttu-id="46820-150">Belirtilen paket geçersiz</span><span class="sxs-lookup"><span data-stu-id="46820-150">The provided package is invalid</span></span>
<span data-ttu-id="46820-151">409</span><span class="sxs-lookup"><span data-stu-id="46820-151">409</span></span>         | <span data-ttu-id="46820-152">Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.</span><span class="sxs-lookup"><span data-stu-id="46820-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="46820-153">Sunucu uygulamaları, bir paketi başarıyla gönderildiğinde döndürülen başarılı durum kodu farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="46820-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="46820-154">Paket silme</span><span class="sxs-lookup"><span data-stu-id="46820-154">Delete a package</span></span>

<span data-ttu-id="46820-155">nuget.org yorumlar paket silme isteği olarak "listeden" bir.</span><span class="sxs-lookup"><span data-stu-id="46820-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="46820-156">Bu paket hala paketinin mevcut kullanıcılar için kullanılabilir, ancak paket arama sonuçlarını veya web arabirimi artık görünür anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="46820-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="46820-157">Bu uygulama hakkında daha fazla bilgi için bkz: [silinmiş paketleri](../nuget-org/policies/deleting-packages.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="46820-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="46820-158">Bu sinyal bir sabit silme olarak yorumlamak için geçici silme veya listeden kaldırılsın ücretsiz diğer sunucu uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="46820-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="46820-159">Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API'si destekleyen bir sunucu uygulaması) bir listeden kaldırma veya yapılandırma seçeneğine bağlı göre silmenin olarak bu isteği işleyen destekler.</span><span class="sxs-lookup"><span data-stu-id="46820-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="46820-160">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="46820-160">Request parameters</span></span>

<span data-ttu-id="46820-161">Ad</span><span class="sxs-lookup"><span data-stu-id="46820-161">Name</span></span>           | <span data-ttu-id="46820-162">İçindeki</span><span class="sxs-lookup"><span data-stu-id="46820-162">In</span></span>     | <span data-ttu-id="46820-163">Tür</span><span class="sxs-lookup"><span data-stu-id="46820-163">Type</span></span>   | <span data-ttu-id="46820-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="46820-164">Required</span></span> | <span data-ttu-id="46820-165">Notlar</span><span class="sxs-lookup"><span data-stu-id="46820-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="46820-166">Kimlik</span><span class="sxs-lookup"><span data-stu-id="46820-166">ID</span></span>             | <span data-ttu-id="46820-167">URL</span><span class="sxs-lookup"><span data-stu-id="46820-167">URL</span></span>    | <span data-ttu-id="46820-168">dize</span><span class="sxs-lookup"><span data-stu-id="46820-168">string</span></span> | <span data-ttu-id="46820-169">evet</span><span class="sxs-lookup"><span data-stu-id="46820-169">yes</span></span>      | <span data-ttu-id="46820-170">Silmek için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="46820-170">The ID of the package to delete</span></span>
<span data-ttu-id="46820-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="46820-171">VERSION</span></span>        | <span data-ttu-id="46820-172">URL</span><span class="sxs-lookup"><span data-stu-id="46820-172">URL</span></span>    | <span data-ttu-id="46820-173">dize</span><span class="sxs-lookup"><span data-stu-id="46820-173">string</span></span> | <span data-ttu-id="46820-174">evet</span><span class="sxs-lookup"><span data-stu-id="46820-174">yes</span></span>      | <span data-ttu-id="46820-175">Silmek için Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="46820-175">The version of the package to delete</span></span>
<span data-ttu-id="46820-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="46820-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="46820-177">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="46820-177">Header</span></span> | <span data-ttu-id="46820-178">dize</span><span class="sxs-lookup"><span data-stu-id="46820-178">string</span></span> | <span data-ttu-id="46820-179">evet</span><span class="sxs-lookup"><span data-stu-id="46820-179">yes</span></span>      | <span data-ttu-id="46820-180">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="46820-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="46820-181">Yanıt</span><span class="sxs-lookup"><span data-stu-id="46820-181">Response</span></span>

<span data-ttu-id="46820-182">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="46820-182">Status Code</span></span> | <span data-ttu-id="46820-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="46820-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="46820-184">204</span><span class="sxs-lookup"><span data-stu-id="46820-184">204</span></span>         | <span data-ttu-id="46820-185">Bu paket silindi</span><span class="sxs-lookup"><span data-stu-id="46820-185">The package was deleted</span></span>
<span data-ttu-id="46820-186">404</span><span class="sxs-lookup"><span data-stu-id="46820-186">404</span></span>         | <span data-ttu-id="46820-187">İle sağlanan paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="46820-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="46820-188">Bir paketi yeniden listeleme</span><span class="sxs-lookup"><span data-stu-id="46820-188">Relist a package</span></span>

<span data-ttu-id="46820-189">Bir paket listelenmemiş ise, bu paket "relist" uç nokta kullanarak arama sonuçlarında bir kez daha görünür hale getirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="46820-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="46820-190">Bu uç noktaya sahip aynı [Sil (listeden) uç noktası](#delete-a-package) ancak kullanır `POST` HTTP yöntemi yerine `DELETE` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="46820-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="46820-191">Paket zaten listedeyse, istek yine de başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="46820-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="46820-192">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="46820-192">Request parameters</span></span>

<span data-ttu-id="46820-193">Ad</span><span class="sxs-lookup"><span data-stu-id="46820-193">Name</span></span>           | <span data-ttu-id="46820-194">İçindeki</span><span class="sxs-lookup"><span data-stu-id="46820-194">In</span></span>     | <span data-ttu-id="46820-195">Tür</span><span class="sxs-lookup"><span data-stu-id="46820-195">Type</span></span>   | <span data-ttu-id="46820-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="46820-196">Required</span></span> | <span data-ttu-id="46820-197">Notlar</span><span class="sxs-lookup"><span data-stu-id="46820-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="46820-198">Kimlik</span><span class="sxs-lookup"><span data-stu-id="46820-198">ID</span></span>             | <span data-ttu-id="46820-199">URL</span><span class="sxs-lookup"><span data-stu-id="46820-199">URL</span></span>    | <span data-ttu-id="46820-200">dize</span><span class="sxs-lookup"><span data-stu-id="46820-200">string</span></span> | <span data-ttu-id="46820-201">evet</span><span class="sxs-lookup"><span data-stu-id="46820-201">yes</span></span>      | <span data-ttu-id="46820-202">Paket yeniden listelenemedi kimliği</span><span class="sxs-lookup"><span data-stu-id="46820-202">The ID of the package to relist</span></span>
<span data-ttu-id="46820-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="46820-203">VERSION</span></span>        | <span data-ttu-id="46820-204">URL</span><span class="sxs-lookup"><span data-stu-id="46820-204">URL</span></span>    | <span data-ttu-id="46820-205">dize</span><span class="sxs-lookup"><span data-stu-id="46820-205">string</span></span> | <span data-ttu-id="46820-206">evet</span><span class="sxs-lookup"><span data-stu-id="46820-206">yes</span></span>      | <span data-ttu-id="46820-207">Paket yeniden listelenemedi sürümü</span><span class="sxs-lookup"><span data-stu-id="46820-207">The version of the package to relist</span></span>
<span data-ttu-id="46820-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="46820-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="46820-209">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="46820-209">Header</span></span> | <span data-ttu-id="46820-210">dize</span><span class="sxs-lookup"><span data-stu-id="46820-210">string</span></span> | <span data-ttu-id="46820-211">evet</span><span class="sxs-lookup"><span data-stu-id="46820-211">yes</span></span>      | <span data-ttu-id="46820-212">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="46820-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="46820-213">Yanıt</span><span class="sxs-lookup"><span data-stu-id="46820-213">Response</span></span>

<span data-ttu-id="46820-214">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="46820-214">Status Code</span></span> | <span data-ttu-id="46820-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="46820-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="46820-216">200</span><span class="sxs-lookup"><span data-stu-id="46820-216">200</span></span>         | <span data-ttu-id="46820-217">Paket artık listelenir</span><span class="sxs-lookup"><span data-stu-id="46820-217">The package is now listed</span></span>
<span data-ttu-id="46820-218">404</span><span class="sxs-lookup"><span data-stu-id="46820-218">404</span></span>         | <span data-ttu-id="46820-219">İle sağlanan paket yok `ID` ve `VERSION` var.</span><span class="sxs-lookup"><span data-stu-id="46820-219">No package with the provided `ID` and `VERSION` exists</span></span>
