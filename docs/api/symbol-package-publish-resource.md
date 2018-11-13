---
title: Sembol paketleri, NuGet API'si itme | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımlama hizmeti yeni sembol paketleri yayımlama etmesine olanak tanır.
keywords: NuGet API'si anında iletme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580454"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="c6e7d-104">Sembol paketleri gönder</span><span class="sxs-lookup"><span data-stu-id="c6e7d-104">Push Symbol Packages</span></span>

<span data-ttu-id="c6e7d-105">Anında iletme sembolleri paketlere mümkündür ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API'sini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="c6e7d-106">Kapatarak bu işlemler temel `SymbolPackagePublish` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c6e7d-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c6e7d-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6e7d-107">Versioning</span></span>

<span data-ttu-id="c6e7d-108">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c6e7d-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c6e7d-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="c6e7d-109">@type value</span></span>                 | <span data-ttu-id="c6e7d-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="c6e7d-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="c6e7d-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="c6e7d-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="c6e7d-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="c6e7d-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c6e7d-113">Temel URL</span><span class="sxs-lookup"><span data-stu-id="c6e7d-113">Base URL</span></span>

<span data-ttu-id="c6e7d-114">Aşağıdaki API'leri için temel URL değeri `@id` özelliği `SymbolPackagePublish/4.9.0` paket kaynağının kaynak [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c6e7d-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="c6e7d-115">Nuget.org URL'si aşağıdaki belgeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="c6e7d-116">Göz önünde bulundurun `https://www.nuget.org/api/v2/symbolpackage` için yer tutucu olarak `@id` değer hizmet dizinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c6e7d-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c6e7d-117">HTTP methods</span></span>

<span data-ttu-id="c6e7d-118">`PUT` HTTP yöntemi, bu kaynak tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="c6e7d-119">Bir sembol paket gönderin</span><span class="sxs-lookup"><span data-stu-id="c6e7d-119">Push a symbol package</span></span>

<span data-ttu-id="c6e7d-120">nuget.org koymadan yeni sembol paketleri biçimi destekler ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) aşağıdaki API'yi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="c6e7d-121">Sembol paketleri aynı kimliği ve sürüm birden çok kez gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="c6e7d-122">Bir sembol paketi, aşağıdaki durumlarda reddedilir.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="c6e7d-123">Bir paket ile aynı kimliği ve sürüm yok.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="c6e7d-124">Bir sembol paketi ile aynı kimliği ve sürüm gönderildiği ancak henüz yayımlanmadı.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="c6e7d-125">Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz (bkz [sembol paketi kısıtlamaları](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="c6e7d-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="c6e7d-126">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="c6e7d-126">Request parameters</span></span>

<span data-ttu-id="c6e7d-127">Ad</span><span class="sxs-lookup"><span data-stu-id="c6e7d-127">Name</span></span>           | <span data-ttu-id="c6e7d-128">İçindeki</span><span class="sxs-lookup"><span data-stu-id="c6e7d-128">In</span></span>     | <span data-ttu-id="c6e7d-129">Tür</span><span class="sxs-lookup"><span data-stu-id="c6e7d-129">Type</span></span>   | <span data-ttu-id="c6e7d-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c6e7d-130">Required</span></span> | <span data-ttu-id="c6e7d-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="c6e7d-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c6e7d-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="c6e7d-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c6e7d-133">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="c6e7d-133">Header</span></span> | <span data-ttu-id="c6e7d-134">dize</span><span class="sxs-lookup"><span data-stu-id="c6e7d-134">string</span></span> | <span data-ttu-id="c6e7d-135">Evet</span><span class="sxs-lookup"><span data-stu-id="c6e7d-135">yes</span></span>      | <span data-ttu-id="c6e7d-136">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c6e7d-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="c6e7d-137">API anahtarı kullanıcı tarafından paket kaynağından edinmiş ve istemciyi yapılandırılmış genel olmayan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="c6e7d-138">Hiçbir özel dize biçimi uygulanan ancak HTTP üstbilgi değerleri için makul bir boyutta API anahtarı uzunluğunu geçmemelidir.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="c6e7d-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c6e7d-139">Request body</span></span>

<span data-ttu-id="c6e7d-140">Sembol gönderim için istek gövdesi aynı paket gönderme isteği ile istek gövdesi (bkz [paketini anında iletme ve silme](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="c6e7d-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="c6e7d-141">Yanıt</span><span class="sxs-lookup"><span data-stu-id="c6e7d-141">Response</span></span>

<span data-ttu-id="c6e7d-142">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="c6e7d-142">Status Code</span></span> | <span data-ttu-id="c6e7d-143">Anlamı</span><span class="sxs-lookup"><span data-stu-id="c6e7d-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="c6e7d-144">201</span><span class="sxs-lookup"><span data-stu-id="c6e7d-144">201</span></span>         | <span data-ttu-id="c6e7d-145">Sembol paketi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="c6e7d-146">400</span><span class="sxs-lookup"><span data-stu-id="c6e7d-146">400</span></span>         | <span data-ttu-id="c6e7d-147">Belirtilen sembol paketi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="c6e7d-148">401</span><span class="sxs-lookup"><span data-stu-id="c6e7d-148">401</span></span>         | <span data-ttu-id="c6e7d-149">Kullanıcının bu eylemi gerçekleştirmek için yetkili değil.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="c6e7d-150">404</span><span class="sxs-lookup"><span data-stu-id="c6e7d-150">404</span></span>         | <span data-ttu-id="c6e7d-151">Sağlanan kimliği ve sürüm karşılık gelen bir paketi yok.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="c6e7d-152">409</span><span class="sxs-lookup"><span data-stu-id="c6e7d-152">409</span></span>         | <span data-ttu-id="c6e7d-153">Bir sembol paketi sağlanan kimliği ve sürüm gönderildiği ancak henüz kullanıma sunulmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="c6e7d-154">413</span><span class="sxs-lookup"><span data-stu-id="c6e7d-154">413</span></span>         | <span data-ttu-id="c6e7d-155">Paket çok büyük.</span><span class="sxs-lookup"><span data-stu-id="c6e7d-155">The package is too large.</span></span>

