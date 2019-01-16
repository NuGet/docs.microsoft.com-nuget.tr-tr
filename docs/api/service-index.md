---
title: API NuGet hizmet dizini
description: Hizmet dizini NuGet HTTP API'sinin giriş noktasıdır ve sunucu yeteneklerini numaralandırır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324727"
---
# <a name="service-index"></a><span data-ttu-id="86444-103">Hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="86444-103">Service index</span></span>

<span data-ttu-id="86444-104">Hizmet dizini NuGet paket kaynağı için giriş noktası ve bir istemci uygulama paket kaynağının özelliklerini hemen bulmasına izin veren bir JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="86444-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="86444-105">Hizmet dizini iki gerekli özelliklere sahip bir JSON nesnesidir: `version` (hizmet dizini şema sürümü) ve `resources` (uç noktaları veya paket kaynağının özellikleri).</span><span class="sxs-lookup"><span data-stu-id="86444-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="86444-106">nuget.org hizmet dizini adresindedir `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="86444-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="86444-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="86444-107">Versioning</span></span>

<span data-ttu-id="86444-108">`version` Hizmet dizini şema sürümünü gösteren bir SemVer 2.0.0 parseable sürüm dizesi değeridir.</span><span class="sxs-lookup"><span data-stu-id="86444-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="86444-109">API sürüm dizesi bir ana sürüm numarasını sahip olduğunu taahhütlerin `3`.</span><span class="sxs-lookup"><span data-stu-id="86444-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="86444-110">Hizmet dizin şeması için hataya neden olmayan değişiklikler yapıldıkça, sürüm dizesinin alt sürümü artırılır.</span><span class="sxs-lookup"><span data-stu-id="86444-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="86444-111">Her hizmet dizinindeki bağımsız olarak hizmet dizin şema sürümünden tutulan bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="86444-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="86444-112">Geçerli şema sürümü `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="86444-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="86444-113">`3.0.0` Sürümüdür eski işlevsel olarak eşdeğer `3.0.0-beta.1` sürüm ancak kararlı, tanımlı bir şema daha net bir şekilde iletişim kuran olarak tercih edilen olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86444-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="86444-114">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="86444-114">HTTP methods</span></span>

<span data-ttu-id="86444-115">Hizmet dizini, HTTP yöntemleri kullanılarak erişilebilir `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="86444-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="86444-116">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="86444-116">Resources</span></span>

<span data-ttu-id="86444-117">`resources` Kaynakları bu paket kaynak tarafından desteklenen bir dizi özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="86444-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="86444-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="86444-118">Resource</span></span>

<span data-ttu-id="86444-119">Bir nesneyi bir kaynaktır `resources` dizisi.</span><span class="sxs-lookup"><span data-stu-id="86444-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="86444-120">Bu paket kaynağının tutulan bir özelliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="86444-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="86444-121">Bir kaynak, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="86444-121">A resource has the following properties:</span></span>

<span data-ttu-id="86444-122">Ad</span><span class="sxs-lookup"><span data-stu-id="86444-122">Name</span></span>          | <span data-ttu-id="86444-123">Tür</span><span class="sxs-lookup"><span data-stu-id="86444-123">Type</span></span>   | <span data-ttu-id="86444-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86444-124">Required</span></span> | <span data-ttu-id="86444-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="86444-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="86444-126">dize</span><span class="sxs-lookup"><span data-stu-id="86444-126">string</span></span> | <span data-ttu-id="86444-127">evet</span><span class="sxs-lookup"><span data-stu-id="86444-127">yes</span></span>      | <span data-ttu-id="86444-128">Kaynak URL'si</span><span class="sxs-lookup"><span data-stu-id="86444-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="86444-129">dize</span><span class="sxs-lookup"><span data-stu-id="86444-129">string</span></span> | <span data-ttu-id="86444-130">evet</span><span class="sxs-lookup"><span data-stu-id="86444-130">yes</span></span>      | <span data-ttu-id="86444-131">Kaynak türünü temsil eden bir dize sabiti</span><span class="sxs-lookup"><span data-stu-id="86444-131">A string constant representing the resource type</span></span>
<span data-ttu-id="86444-132">comment</span><span class="sxs-lookup"><span data-stu-id="86444-132">comment</span></span>       | <span data-ttu-id="86444-133">dize</span><span class="sxs-lookup"><span data-stu-id="86444-133">string</span></span> | <span data-ttu-id="86444-134">Yok</span><span class="sxs-lookup"><span data-stu-id="86444-134">no</span></span>       | <span data-ttu-id="86444-135">Kaynak insan tarafından okunabilir bir açıklaması</span><span class="sxs-lookup"><span data-stu-id="86444-135">A human readable description of the resource</span></span>

<span data-ttu-id="86444-136">`@id` Gerekir ve mutlak bir URL HTTP veya HTTPS şeması sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="86444-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="86444-137">`@type` Kaynakla etkileşim kurarken kullanacağı özel bir protokolü tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86444-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="86444-138">Kaynak türü, genel olmayan bir dizedir, ancak genellikle şu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="86444-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="86444-139">İstemciler için sabit kod beklenen `@type` anlamak ve bir paket kaynağının hizmet dizinine bakarak değerleri.</span><span class="sxs-lookup"><span data-stu-id="86444-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="86444-140">Tam `@type` numaralandırılmış değerlerinin bugün kullanımda listelenen ayrı kaynak başvuru belgelerindeki [API'sine genel bakış](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="86444-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="86444-141">Bu belge için farklı kaynaklar ile ilgili belgeler tarafından temelde gruplandırılacak `{RESOURCE_NAME}` senaryoya göre gruplandırma benzer olan hizmet dizinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="86444-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="86444-142">Her bir kaynağın benzersiz olan bir gereksinimi yoktur `@id` veya `@type`.</span><span class="sxs-lookup"><span data-stu-id="86444-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="86444-143">Bu istemci uygulamasının hangi kaynağı diğerine tercih kadar olur.</span><span class="sxs-lookup"><span data-stu-id="86444-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="86444-144">Olası bir uygulaması olan kaynaklar aynı veya uyumlu `@type` ettirirsiniz bağlantı kesintisi veya sunucu hatası olması durumunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86444-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="86444-145">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="86444-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="86444-146">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="86444-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
