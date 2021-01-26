---
title: Sembol paketlerini gönderme, NuGet API | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımla hizmeti, istemcilerin yeni sembol paketleri yayımlamasına izin verir.
keywords: NuGet API gönderme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773902"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="098bb-104">Sembol paketlerini gönder</span><span class="sxs-lookup"><span data-stu-id="098bb-104">Push Symbol Packages</span></span>

<span data-ttu-id="098bb-105">NuGet v3 API kullanılarak sembol paketlerinin ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) gönderimi mümkündür.</span><span class="sxs-lookup"><span data-stu-id="098bb-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="098bb-106">Bu işlemler `SymbolPackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.</span><span class="sxs-lookup"><span data-stu-id="098bb-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="098bb-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="098bb-107">Versioning</span></span>

<span data-ttu-id="098bb-108">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="098bb-108">The following `@type` value is used:</span></span>

<span data-ttu-id="098bb-109">@type deeri</span><span class="sxs-lookup"><span data-stu-id="098bb-109">@type value</span></span>                 | <span data-ttu-id="098bb-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="098bb-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="098bb-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="098bb-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="098bb-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="098bb-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="098bb-113">Temel URL</span><span class="sxs-lookup"><span data-stu-id="098bb-113">Base URL</span></span>

<span data-ttu-id="098bb-114">Aşağıdaki API 'Lerin temel URL 'SI, `@id` `SymbolPackagePublish/4.9.0` paket kaynağının [hizmet dizinindeki](service-index.md)kaynak özelliğinin değeridir.</span><span class="sxs-lookup"><span data-stu-id="098bb-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="098bb-115">Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="098bb-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="098bb-116">`https://www.nuget.org/api/v2/symbolpackage`Hizmet dizininde bulunan değer için bir yer tutucu olarak düşünün `@id` .</span><span class="sxs-lookup"><span data-stu-id="098bb-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="098bb-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="098bb-117">HTTP methods</span></span>

<span data-ttu-id="098bb-118">`PUT`Http yöntemi bu kaynak tarafından destekleniyor.</span><span class="sxs-lookup"><span data-stu-id="098bb-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="098bb-119">Bir sembol paketini gönder</span><span class="sxs-lookup"><span data-stu-id="098bb-119">Push a symbol package</span></span>

<span data-ttu-id="098bb-120">nuget.org, aşağıdaki API 'YI kullanarak yeni sembol paketleri biçimi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) göndermeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="098bb-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="098bb-121">Aynı KIMLIĞE ve sürüme sahip sembol paketleri birden çok kez gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="098bb-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="098bb-122">Aşağıdaki durumlarda bir sembol paketi reddedilir.</span><span class="sxs-lookup"><span data-stu-id="098bb-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="098bb-123">Aynı KIMLIĞE ve sürüme sahip bir paket yok.</span><span class="sxs-lookup"><span data-stu-id="098bb-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="098bb-124">Aynı KIMLIĞE ve sürüme sahip bir sembol paketi itildi, ancak henüz yayımlanmadı.</span><span class="sxs-lookup"><span data-stu-id="098bb-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="098bb-125">Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz ( [sembol paketi kısıtlamalarına](../create-packages/Symbol-Packages-snupkg.md)bakın).</span><span class="sxs-lookup"><span data-stu-id="098bb-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="098bb-126">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="098bb-126">Request parameters</span></span>

<span data-ttu-id="098bb-127">Name</span><span class="sxs-lookup"><span data-stu-id="098bb-127">Name</span></span>           | <span data-ttu-id="098bb-128">İçinde</span><span class="sxs-lookup"><span data-stu-id="098bb-128">In</span></span>     | <span data-ttu-id="098bb-129">Tür</span><span class="sxs-lookup"><span data-stu-id="098bb-129">Type</span></span>   | <span data-ttu-id="098bb-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="098bb-130">Required</span></span> | <span data-ttu-id="098bb-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="098bb-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="098bb-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="098bb-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="098bb-133">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="098bb-133">Header</span></span> | <span data-ttu-id="098bb-134">string</span><span class="sxs-lookup"><span data-stu-id="098bb-134">string</span></span> | <span data-ttu-id="098bb-135">evet</span><span class="sxs-lookup"><span data-stu-id="098bb-135">yes</span></span>      | <span data-ttu-id="098bb-136">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="098bb-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="098bb-137">API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="098bb-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="098bb-138">Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="098bb-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="098bb-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="098bb-139">Request body</span></span>

<span data-ttu-id="098bb-140">Sembol gönderimi için istek gövdesi, bir paket gönderme isteğinin istek gövdesiyle aynı (bkz. [paket gönderme ve silme](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="098bb-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="098bb-141">Yanıt</span><span class="sxs-lookup"><span data-stu-id="098bb-141">Response</span></span>

<span data-ttu-id="098bb-142">Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="098bb-142">Status Code</span></span> | <span data-ttu-id="098bb-143">Anlamı</span><span class="sxs-lookup"><span data-stu-id="098bb-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="098bb-144">201</span><span class="sxs-lookup"><span data-stu-id="098bb-144">201</span></span>         | <span data-ttu-id="098bb-145">Sembol paketi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="098bb-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="098bb-146">400</span><span class="sxs-lookup"><span data-stu-id="098bb-146">400</span></span>         | <span data-ttu-id="098bb-147">Belirtilen sembol paketi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="098bb-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="098bb-148">401</span><span class="sxs-lookup"><span data-stu-id="098bb-148">401</span></span>         | <span data-ttu-id="098bb-149">Kullanıcı bu eylemi gerçekleştirme yetkisine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="098bb-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="098bb-150">404</span><span class="sxs-lookup"><span data-stu-id="098bb-150">404</span></span>         | <span data-ttu-id="098bb-151">Belirtilen KIMLIĞE ve sürüme sahip karşılık gelen bir paket yok.</span><span class="sxs-lookup"><span data-stu-id="098bb-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="098bb-152">409</span><span class="sxs-lookup"><span data-stu-id="098bb-152">409</span></span>         | <span data-ttu-id="098bb-153">Sağlanan KIMLIĞE ve sürüme sahip bir sembol paketi gönderildi ancak henüz kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="098bb-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="098bb-154">413</span><span class="sxs-lookup"><span data-stu-id="098bb-154">413</span></span>         | <span data-ttu-id="098bb-155">Paket çok büyük.</span><span class="sxs-lookup"><span data-stu-id="098bb-155">The package is too large.</span></span>

