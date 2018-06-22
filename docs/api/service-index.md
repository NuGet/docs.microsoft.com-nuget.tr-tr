---
title: Hizmet dizini, NuGet API
description: Hizmet dizini NuGet HTTP API giriş noktasıdır ve sunucu özelliklerini numaralandırır.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822100"
---
# <a name="service-index"></a><span data-ttu-id="a14b0-103">Hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="a14b0-103">Service index</span></span>

<span data-ttu-id="a14b0-104">NuGet paket kaynağı için giriş noktasıdır ve paket kaynağının özellikleri bulmak bir istemci uygulaması izin veren bir JSON belgesi hizmet dizinidir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="a14b0-105">İki gerekli özellikleri olan bir JSON nesnesi hizmet dizinidir: `version` (hizmeti dizini şema sürümü) ve `resources` (uç noktaları veya paket kaynağının özelliklerini).</span><span class="sxs-lookup"><span data-stu-id="a14b0-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="a14b0-106">nuget.org Hizmeti dizini adresindedir `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a14b0-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="a14b0-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="a14b0-107">Versioning</span></span>

<span data-ttu-id="a14b0-108">`version` Hizmeti dizini şema sürümü gösteren bir SemVer 2.0.0 parseable sürüm dizesi değeridir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="a14b0-109">Sürüm dizesi bir ana sürüm numarası olan API olması zorunlu tutulmuştur `3`.</span><span class="sxs-lookup"><span data-stu-id="a14b0-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="a14b0-110">Hizmet dizin şemasına yapılan bölünemez değişiklikler gibi sürüm dizesinin alt sürümü artırılır.</span><span class="sxs-lookup"><span data-stu-id="a14b0-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="a14b0-111">Her hizmet dizindeki bağımsız olarak hizmet dizin şeması sürümünden sürümlü kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="a14b0-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="a14b0-112">Geçerli şema sürümü `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a14b0-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="a14b0-113">`3.0.0` Sürümü eski işlevsel olarak eşdeğer `3.0.0-beta.1` sürüm ancak kararlı, tanımlı şemanın daha net bir şekilde iletişim kurar tercih edilen olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a14b0-114">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="a14b0-114">HTTP methods</span></span>

<span data-ttu-id="a14b0-115">Hizmet dizini HTTP yöntemleri kullanılarak erişilebilir olduğundan `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a14b0-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="a14b0-116">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a14b0-116">Resources</span></span>

<span data-ttu-id="a14b0-117">`resources` Özelliği, bu paket kaynak tarafından desteklenen kaynakları dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="a14b0-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a14b0-118">Resource</span></span>

<span data-ttu-id="a14b0-119">Bir nesne bir kaynaktır `resources` dizi.</span><span class="sxs-lookup"><span data-stu-id="a14b0-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="a14b0-120">Paket kaynağının sürümlü bir özelliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a14b0-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="a14b0-121">Bir kaynak aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a14b0-121">A resource has the following properties:</span></span>

<span data-ttu-id="a14b0-122">Ad</span><span class="sxs-lookup"><span data-stu-id="a14b0-122">Name</span></span>          | <span data-ttu-id="a14b0-123">Tür</span><span class="sxs-lookup"><span data-stu-id="a14b0-123">Type</span></span>   | <span data-ttu-id="a14b0-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a14b0-124">Required</span></span> | <span data-ttu-id="a14b0-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="a14b0-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="a14b0-126">dize</span><span class="sxs-lookup"><span data-stu-id="a14b0-126">string</span></span> | <span data-ttu-id="a14b0-127">Evet</span><span class="sxs-lookup"><span data-stu-id="a14b0-127">yes</span></span>      | <span data-ttu-id="a14b0-128">Kaynak URL</span><span class="sxs-lookup"><span data-stu-id="a14b0-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="a14b0-129">dize</span><span class="sxs-lookup"><span data-stu-id="a14b0-129">string</span></span> | <span data-ttu-id="a14b0-130">Evet</span><span class="sxs-lookup"><span data-stu-id="a14b0-130">yes</span></span>      | <span data-ttu-id="a14b0-131">Kaynak türü temsil eden bir dize sabiti</span><span class="sxs-lookup"><span data-stu-id="a14b0-131">A string constant representing the resource type</span></span>
<span data-ttu-id="a14b0-132">comment</span><span class="sxs-lookup"><span data-stu-id="a14b0-132">comment</span></span>       | <span data-ttu-id="a14b0-133">dize</span><span class="sxs-lookup"><span data-stu-id="a14b0-133">string</span></span> | <span data-ttu-id="a14b0-134">Yok</span><span class="sxs-lookup"><span data-stu-id="a14b0-134">no</span></span>       | <span data-ttu-id="a14b0-135">Kaynak İnsan okunabilir açıklaması</span><span class="sxs-lookup"><span data-stu-id="a14b0-135">A human readable description of the resource</span></span>

<span data-ttu-id="a14b0-136">`@id` Mutlak olmalı ve ya da gereken bir URL HTTP veya HTTPS şeması sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="a14b0-137">`@type` Kaynakla kullanılırken kullanılacak belirli Protokolü tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a14b0-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="a14b0-138">Kaynak türü donuk bir dizedir ancak genellikle biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a14b0-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="a14b0-139">İstemciler için sabit kod beklenen `@type` anlamak ve bir paket kaynağının hizmet dizinde aramak değerleri.</span><span class="sxs-lookup"><span data-stu-id="a14b0-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="a14b0-140">Tam `@type` Günümüzde kullanılan değerleri numaralandırılan listelenen tek tek kaynak başvuru belgelerinde [API genel bakış](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="a14b0-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="a14b0-141">Bu belge amacıyla, farklı kaynaklarının ilgili belgelere tarafından temelde gruplandırılacak `{RESOURCE_NAME}` senaryo gruplandırarak paraleldir hizmet dizininde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a14b0-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="a14b0-142">Her kaynak benzersiz olduğunu gereksinimi yoktur ve `@id` veya `@type`.</span><span class="sxs-lookup"><span data-stu-id="a14b0-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="a14b0-143">Hangi kaynak üzerinde başka bir tercih belirlemek için istemci uygulaması kadar olur.</span><span class="sxs-lookup"><span data-stu-id="a14b0-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="a14b0-144">Bir olası uygulama işlemidir aynı veya uyumlu kaynakları `@type` bağlantı hatası veya sunucu hatası durumunda hepsini şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a14b0-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a14b0-145">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="a14b0-145">Sample request</span></span>

<span data-ttu-id="a14b0-146">AL https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="a14b0-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="a14b0-147">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="a14b0-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
