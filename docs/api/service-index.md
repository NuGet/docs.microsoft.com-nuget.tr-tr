---
title: Hizmet dizini, NuGet API 'SI
description: Hizmet dizini, NuGet HTTP API 'sinin giriş noktasıdır ve sunucunun yeteneklerini sıralar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775362"
---
# <a name="service-index"></a><span data-ttu-id="e43f8-103">Hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="e43f8-103">Service index</span></span>

<span data-ttu-id="e43f8-104">Hizmet dizini, bir NuGet paket kaynağı için giriş noktası olan ve istemci uygulamasının paket kaynağının yeteneklerini bulmasına izin veren bir JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e43f8-105">Hizmet dizini, iki gerekli özelliği olan bir JSON nesnesidir: `version` (hizmet dizininin şema sürümü) ve `resources`  (paket kaynağının uç noktaları veya özellikleri).</span><span class="sxs-lookup"><span data-stu-id="e43f8-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e43f8-106">NuGet. org 'ın hizmet dizini konumunda bulunur `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e43f8-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="e43f8-107">Versioning</span></span>

<span data-ttu-id="e43f8-108">`version`Değer, hizmet dizininin şema sürümünü gösteren bir SemVer 2.0.0 parseable sürümü dizesidir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="e43f8-109">Sürüm dizesinin ana sürüm numarası olan API mantarihlerinin `3` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e43f8-110">Hizmet dizini şemasında, önemli olmayan değişiklikler yapıldığından, sürüm dizesinin ikincil sürümü artar.</span><span class="sxs-lookup"><span data-stu-id="e43f8-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e43f8-111">Hizmet dizinindeki her kaynak hizmet dizini şema sürümünden bağımsız olarak sürümlüdür.</span><span class="sxs-lookup"><span data-stu-id="e43f8-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e43f8-112">Geçerli şema sürümü `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="e43f8-113">`3.0.0`Sürüm işlevsel olarak eski sürüme eşdeğerdir, `3.0.0-beta.1` ancak kararlı, tanımlı şemayı daha açık bir şekilde iletişim kurduğundan tercih edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e43f8-114">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e43f8-114">HTTP methods</span></span>

<span data-ttu-id="e43f8-115">Hizmet dizinine HTTP yöntemleri ve aracılığıyla erişilebilir `GET` `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e43f8-116">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e43f8-116">Resources</span></span>

<span data-ttu-id="e43f8-117">`resources`Özelliği, bu paket kaynağı tarafından desteklenen bir kaynak dizisi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e43f8-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e43f8-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="e43f8-118">Resource</span></span>

<span data-ttu-id="e43f8-119">Kaynak, dizideki bir nesnedir `resources` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e43f8-120">Paket kaynağının sürümlü bir özelliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e43f8-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e43f8-121">Bir kaynak aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e43f8-121">A resource has the following properties:</span></span>

<span data-ttu-id="e43f8-122">Ad</span><span class="sxs-lookup"><span data-stu-id="e43f8-122">Name</span></span>          | <span data-ttu-id="e43f8-123">Tür</span><span class="sxs-lookup"><span data-stu-id="e43f8-123">Type</span></span>   | <span data-ttu-id="e43f8-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e43f8-124">Required</span></span> | <span data-ttu-id="e43f8-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="e43f8-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e43f8-126">string</span><span class="sxs-lookup"><span data-stu-id="e43f8-126">string</span></span> | <span data-ttu-id="e43f8-127">evet</span><span class="sxs-lookup"><span data-stu-id="e43f8-127">yes</span></span>      | <span data-ttu-id="e43f8-128">Kaynağın URL 'SI</span><span class="sxs-lookup"><span data-stu-id="e43f8-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e43f8-129">string</span><span class="sxs-lookup"><span data-stu-id="e43f8-129">string</span></span> | <span data-ttu-id="e43f8-130">evet</span><span class="sxs-lookup"><span data-stu-id="e43f8-130">yes</span></span>      | <span data-ttu-id="e43f8-131">Kaynak türünü temsil eden bir dize sabiti</span><span class="sxs-lookup"><span data-stu-id="e43f8-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e43f8-132">comment</span><span class="sxs-lookup"><span data-stu-id="e43f8-132">comment</span></span>       | <span data-ttu-id="e43f8-133">string</span><span class="sxs-lookup"><span data-stu-id="e43f8-133">string</span></span> | <span data-ttu-id="e43f8-134">hayır</span><span class="sxs-lookup"><span data-stu-id="e43f8-134">no</span></span>       | <span data-ttu-id="e43f8-135">Kaynağın okunabilir bir açıklaması</span><span class="sxs-lookup"><span data-stu-id="e43f8-135">A human readable description of the resource</span></span>

<span data-ttu-id="e43f8-136">`@id`Mutlak olması gereken ve http ya da https şemasına sahip olması gereken BIR URL 'dir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e43f8-137">, `@type` Kaynakla etkileşim kurarken kullanılacak belirli Protokolü belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e43f8-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e43f8-138">Kaynağın türü donuk bir dizedir, ancak genellikle şu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="e43f8-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="e43f8-139">İstemcilerin `@type` anladıkları değerleri sabit olarak kodlamaları ve bir paket kaynağının hizmet dizininde bunları araması beklenir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e43f8-140">`@type`Günümüzde kullanımda olan değerler, [API genel](overview.md#resources-and-schema)görünümünde listelenen tek kaynak başvuru belgelerinde numaralandırılır.</span><span class="sxs-lookup"><span data-stu-id="e43f8-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e43f8-141">Bu belgelerin bir listesi için, farklı kaynaklarla ilgili belgeler temelde, `{RESOURCE_NAME}` senaryoya göre gruplandırma ile benzer hizmet dizininde bulunan tarafından gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="e43f8-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e43f8-142">Her kaynak için benzersiz bir veya olan bir gereksinim yoktur `@id` `@type` .</span><span class="sxs-lookup"><span data-stu-id="e43f8-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e43f8-143">Bu, başka bir kaynağın hangi kaynağa tercih edeceğini belirleyen istemci uygulamasına çalışır.</span><span class="sxs-lookup"><span data-stu-id="e43f8-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e43f8-144">Olası bir uygulama, `@type` bağlantı hatası veya sunucu hatası durumunda aynı veya uyumlu olan kaynakların hepsini bir kez deneme biçiminde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e43f8-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e43f8-145">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="e43f8-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e43f8-146">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="e43f8-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
