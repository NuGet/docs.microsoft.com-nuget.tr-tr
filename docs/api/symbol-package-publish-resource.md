---
title: Sembol paketlerini gönderme, NuGet API | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımla hizmeti, istemcilerin yeni sembol paketleri yayımlamasına izin verir.
keywords: NuGet API gönderme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235111"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="d03b5-104">Sembol paketlerini gönder</span><span class="sxs-lookup"><span data-stu-id="d03b5-104">Push Symbol Packages</span></span>

<span data-ttu-id="d03b5-105">NuGet v3 API kullanılarak sembol paketlerinin ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) gönderimi mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d03b5-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="d03b5-106">Bu işlemler `SymbolPackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.</span><span class="sxs-lookup"><span data-stu-id="d03b5-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d03b5-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d03b5-107">Versioning</span></span>

<span data-ttu-id="d03b5-108">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d03b5-108">The following `@type` value is used:</span></span>

<span data-ttu-id="d03b5-109">@typedeeri</span><span class="sxs-lookup"><span data-stu-id="d03b5-109">@type value</span></span>                 | <span data-ttu-id="d03b5-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="d03b5-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="d03b5-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="d03b5-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="d03b5-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="d03b5-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="d03b5-113">Taban URL 'SI</span><span class="sxs-lookup"><span data-stu-id="d03b5-113">Base URL</span></span>

<span data-ttu-id="d03b5-114">Aşağıdaki API 'lerin temel URL 'si, paket kaynağının `@id` [hizmet dizinindeki](service-index.md) `SymbolPackagePublish/4.9.0` kaynak özelliğinin değeridir.</span><span class="sxs-lookup"><span data-stu-id="d03b5-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="d03b5-115">Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d03b5-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="d03b5-116">Hizmet `https://www.nuget.org/api/v2/symbolpackage` dizininde bulunan `@id` değer için bir yer tutucu olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="d03b5-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d03b5-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="d03b5-117">HTTP methods</span></span>

<span data-ttu-id="d03b5-118">`PUT` Http yöntemi bu kaynak tarafından destekleniyor.</span><span class="sxs-lookup"><span data-stu-id="d03b5-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="d03b5-119">Bir sembol paketini gönder</span><span class="sxs-lookup"><span data-stu-id="d03b5-119">Push a symbol package</span></span>

<span data-ttu-id="d03b5-120">nuget.org, aşağıdaki API 'YI kullanarak yeni sembol paketleri biçimi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) göndermeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="d03b5-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="d03b5-121">Aynı KIMLIĞE ve sürüme sahip sembol paketleri birden çok kez gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="d03b5-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="d03b5-122">Aşağıdaki durumlarda bir sembol paketi reddedilir.</span><span class="sxs-lookup"><span data-stu-id="d03b5-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="d03b5-123">Aynı KIMLIĞE ve sürüme sahip bir paket yok.</span><span class="sxs-lookup"><span data-stu-id="d03b5-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="d03b5-124">Aynı KIMLIĞE ve sürüme sahip bir sembol paketi itildi, ancak henüz yayımlanmadı.</span><span class="sxs-lookup"><span data-stu-id="d03b5-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="d03b5-125">Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz ( [sembol paketi kısıtlamalarına](../create-packages/Symbol-Packages-snupkg.md)bakın).</span><span class="sxs-lookup"><span data-stu-id="d03b5-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="d03b5-126">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="d03b5-126">Request parameters</span></span>

<span data-ttu-id="d03b5-127">Ad</span><span class="sxs-lookup"><span data-stu-id="d03b5-127">Name</span></span>           | <span data-ttu-id="d03b5-128">İçindeki</span><span class="sxs-lookup"><span data-stu-id="d03b5-128">In</span></span>     | <span data-ttu-id="d03b5-129">Tür</span><span class="sxs-lookup"><span data-stu-id="d03b5-129">Type</span></span>   | <span data-ttu-id="d03b5-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d03b5-130">Required</span></span> | <span data-ttu-id="d03b5-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="d03b5-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="d03b5-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="d03b5-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="d03b5-133">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="d03b5-133">Header</span></span> | <span data-ttu-id="d03b5-134">dize</span><span class="sxs-lookup"><span data-stu-id="d03b5-134">string</span></span> | <span data-ttu-id="d03b5-135">evet</span><span class="sxs-lookup"><span data-stu-id="d03b5-135">yes</span></span>      | <span data-ttu-id="d03b5-136">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="d03b5-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="d03b5-137">API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="d03b5-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="d03b5-138">Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d03b5-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="d03b5-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d03b5-139">Request body</span></span>

<span data-ttu-id="d03b5-140">Sembol gönderimi için istek gövdesi, bir paket gönderme isteğinin istek gövdesiyle aynı (bkz. [paket gönderme ve silme](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="d03b5-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="d03b5-141">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d03b5-141">Response</span></span>

<span data-ttu-id="d03b5-142">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="d03b5-142">Status Code</span></span> | <span data-ttu-id="d03b5-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d03b5-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="d03b5-144">201</span><span class="sxs-lookup"><span data-stu-id="d03b5-144">201</span></span>         | <span data-ttu-id="d03b5-145">Sembol paketi başarıyla gönderildi.</span><span class="sxs-lookup"><span data-stu-id="d03b5-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="d03b5-146">400</span><span class="sxs-lookup"><span data-stu-id="d03b5-146">400</span></span>         | <span data-ttu-id="d03b5-147">Belirtilen sembol paketi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="d03b5-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="d03b5-148">401</span><span class="sxs-lookup"><span data-stu-id="d03b5-148">401</span></span>         | <span data-ttu-id="d03b5-149">Kullanıcı bu eylemi gerçekleştirme yetkisine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d03b5-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="d03b5-150">404</span><span class="sxs-lookup"><span data-stu-id="d03b5-150">404</span></span>         | <span data-ttu-id="d03b5-151">Belirtilen KIMLIĞE ve sürüme sahip karşılık gelen bir paket yok.</span><span class="sxs-lookup"><span data-stu-id="d03b5-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="d03b5-152">409</span><span class="sxs-lookup"><span data-stu-id="d03b5-152">409</span></span>         | <span data-ttu-id="d03b5-153">Sağlanan KIMLIĞE ve sürüme sahip bir sembol paketi gönderildi ancak henüz kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="d03b5-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="d03b5-154">413</span><span class="sxs-lookup"><span data-stu-id="d03b5-154">413</span></span>         | <span data-ttu-id="d03b5-155">Paket çok büyük.</span><span class="sxs-lookup"><span data-stu-id="d03b5-155">The package is too large.</span></span>

