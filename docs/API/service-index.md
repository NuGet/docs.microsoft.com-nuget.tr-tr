---
title: Hizmet dizini, NuGet API | Microsoft Docs
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
description: "Hizmet dizini NuGet HTTP API giriş noktasıdır ve sunucu özelliklerini numaralandırır."
keywords: "NuGet API giriş noktası, NuGetA PI uç nokta bulma"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="90532-104">Hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="90532-104">Service index</span></span>

<span data-ttu-id="90532-105">NuGet paket kaynağı için giriş noktasıdır ve paket kaynağının özellikleri bulmak bir istemci uygulaması izin veren bir JSON belgesi hizmet dizinidir.</span><span class="sxs-lookup"><span data-stu-id="90532-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="90532-106">İki gerekli özellikleri olan bir JSON nesnesi hizmet dizinidir: `version` (hizmeti dizini şema sürümü) ve `resources` (uç noktaları veya paket kaynağının özelliklerini).</span><span class="sxs-lookup"><span data-stu-id="90532-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="90532-107">nuget.org Hizmeti dizini adresindedir `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="90532-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="90532-108">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="90532-108">Versioning</span></span>

<span data-ttu-id="90532-109">`version` Hizmeti dizini şema sürümü gösteren bir SemVer 2.0.0 parseable sürüm dizesi değeridir.</span><span class="sxs-lookup"><span data-stu-id="90532-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="90532-110">Sürüm dizesi bir ana sürüm numarası olan API olması zorunlu tutulmuştur `3`.</span><span class="sxs-lookup"><span data-stu-id="90532-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="90532-111">Hizmet dizin şemasına yapılan bölünemez değişiklikler gibi sürüm dizesinin alt sürümü artırılır.</span><span class="sxs-lookup"><span data-stu-id="90532-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="90532-112">Her hizmet dizindeki bağımsız olarak hizmet dizin şeması sürümünden sürümlü kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="90532-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="90532-113">Geçerli şema sürümü `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="90532-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="90532-114">`3.0.0` Sürümü eski işlevsel olarak eşdeğer `3.0.0-beta.1` sürüm ancak kararlı, tanımlı şemanın daha net bir şekilde iletişim kurar tercih edilen olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="90532-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="90532-115">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="90532-115">HTTP methods</span></span>

<span data-ttu-id="90532-116">Hizmet dizini HTTP yöntemleri kullanılarak erişilebilir olduğundan `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="90532-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="90532-117">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="90532-117">Resources</span></span>

<span data-ttu-id="90532-118">`resources` Özelliği, bu paket kaynak tarafından desteklenen kaynakları dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="90532-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="90532-119">Kaynak</span><span class="sxs-lookup"><span data-stu-id="90532-119">Resource</span></span>

<span data-ttu-id="90532-120">Bir nesne bir kaynaktır `resources` dizi.</span><span class="sxs-lookup"><span data-stu-id="90532-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="90532-121">Paket kaynağının sürümlü bir özelliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="90532-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="90532-122">Bir kaynak aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="90532-122">A resource has the following properties:</span></span>

<span data-ttu-id="90532-123">Ad</span><span class="sxs-lookup"><span data-stu-id="90532-123">Name</span></span>          | <span data-ttu-id="90532-124">Tür</span><span class="sxs-lookup"><span data-stu-id="90532-124">Type</span></span>   | <span data-ttu-id="90532-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="90532-125">Required</span></span> | <span data-ttu-id="90532-126">Notlar</span><span class="sxs-lookup"><span data-stu-id="90532-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="90532-127">dize</span><span class="sxs-lookup"><span data-stu-id="90532-127">string</span></span> | <span data-ttu-id="90532-128">Evet</span><span class="sxs-lookup"><span data-stu-id="90532-128">yes</span></span>      | <span data-ttu-id="90532-129">Kaynak URL</span><span class="sxs-lookup"><span data-stu-id="90532-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="90532-130">dize</span><span class="sxs-lookup"><span data-stu-id="90532-130">string</span></span> | <span data-ttu-id="90532-131">Evet</span><span class="sxs-lookup"><span data-stu-id="90532-131">yes</span></span>      | <span data-ttu-id="90532-132">Kaynak türü temsil eden bir dize sabiti</span><span class="sxs-lookup"><span data-stu-id="90532-132">A string constant representing the resource type</span></span>
<span data-ttu-id="90532-133">comment</span><span class="sxs-lookup"><span data-stu-id="90532-133">comment</span></span>       | <span data-ttu-id="90532-134">dize</span><span class="sxs-lookup"><span data-stu-id="90532-134">string</span></span> | <span data-ttu-id="90532-135">Yok</span><span class="sxs-lookup"><span data-stu-id="90532-135">no</span></span>       | <span data-ttu-id="90532-136">Kaynak İnsan okunabilir açıklaması</span><span class="sxs-lookup"><span data-stu-id="90532-136">A human readable description of the resource</span></span>

<span data-ttu-id="90532-137">`@id` Mutlak olmalı ve ya da gereken bir URL HTTP veya HTTPS şeması sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="90532-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="90532-138">`@type` Kaynakla kullanılırken kullanılacak belirli Protokolü tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90532-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="90532-139">Kaynak türü donuk bir dizedir ancak genellikle biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="90532-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="90532-140">İstemciler için sabit kod beklenen `@type` anlamak ve bir paket kaynağının hizmet dizinde aramak değerleri.</span><span class="sxs-lookup"><span data-stu-id="90532-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="90532-141">Tam `@type` Günümüzde kullanılan değerleri numaralandırılan listelenen tek tek kaynak başvuru belgelerinde [API genel bakış](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="90532-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="90532-142">Bu belge amacıyla, farklı kaynaklarının ilgili belgelere tarafından temelde gruplandırılacak `{RESOURCE_NAME}` senaryo gruplandırarak paraleldir hizmet dizininde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="90532-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="90532-143">Her kaynak benzersiz olduğunu gereksinimi yoktur ve `@id` veya `@type`.</span><span class="sxs-lookup"><span data-stu-id="90532-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="90532-144">Hangi kaynak üzerinde başka bir tercih belirlemek için istemci uygulaması kadar olur.</span><span class="sxs-lookup"><span data-stu-id="90532-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="90532-145">Bir olası uygulama işlemidir aynı veya uyumlu kaynakları `@type` bağlantı hatası veya sunucu hatası durumunda hepsini şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="90532-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="90532-146">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="90532-146">Sample request</span></span>

<span data-ttu-id="90532-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="90532-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="90532-148">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="90532-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
