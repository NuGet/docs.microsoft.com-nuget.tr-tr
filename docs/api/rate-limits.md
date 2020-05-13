---
title: Oran limitleri, NuGet API 'SI
description: NuGet API 'Leri, kötüye kullanımı engellemek için uygulanan Hız sınırlarına sahip olur.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367940"
---
# <a name="rate-limits"></a><span data-ttu-id="96cf7-103">Oran limitleri</span><span class="sxs-lookup"><span data-stu-id="96cf7-103">Rate Limits</span></span>

<span data-ttu-id="96cf7-104">NuGet.org API 'SI, kötüye kullanımı engellemek için hız sınırlaması uygular.</span><span class="sxs-lookup"><span data-stu-id="96cf7-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="96cf7-105">Hız sınırını aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="96cf7-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="96cf7-106">Hız sınırlarını kullanarak istek azaltmasına ek olarak, bazı API 'Ler kota de uygular.</span><span class="sxs-lookup"><span data-stu-id="96cf7-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="96cf7-107">Kotayı aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="96cf7-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="96cf7-108">Aşağıdaki tablolarda NuGet.org API 'sinin hız sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="96cf7-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="96cf7-109">Paket arama</span><span class="sxs-lookup"><span data-stu-id="96cf7-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="96cf7-110">Şu anda sınırlı olmadığından NuGet. org 'ın [v3 arama API 'lerini](search-query-service-resource.md) kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="96cf7-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="96cf7-111">V1 ve v2 Search API 'Leri için aşağıdaki sınırlar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="96cf7-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="96cf7-112">API</span><span class="sxs-lookup"><span data-stu-id="96cf7-112">API</span></span> | <span data-ttu-id="96cf7-113">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="96cf7-113">Limit Type</span></span> | <span data-ttu-id="96cf7-114">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="96cf7-114">Limit Value</span></span> | <span data-ttu-id="96cf7-115">API kullanım örneği</span><span class="sxs-lookup"><span data-stu-id="96cf7-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="96cf7-116">**Al**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="96cf7-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="96cf7-117">IP</span><span class="sxs-lookup"><span data-stu-id="96cf7-117">IP</span></span> | <span data-ttu-id="96cf7-118">1000/dakika</span><span class="sxs-lookup"><span data-stu-id="96cf7-118">1000 / minute</span></span> | <span data-ttu-id="96cf7-119">NuGet paketi meta verilerini v1 OData koleksiyonu aracılığıyla sorgula `Packages`</span><span class="sxs-lookup"><span data-stu-id="96cf7-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="96cf7-120">**Al**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="96cf7-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="96cf7-121">IP</span><span class="sxs-lookup"><span data-stu-id="96cf7-121">IP</span></span> | <span data-ttu-id="96cf7-122">3000/dakika</span><span class="sxs-lookup"><span data-stu-id="96cf7-122">3000 / minute</span></span> | <span data-ttu-id="96cf7-123">V1 arama uç noktası aracılığıyla NuGet paketlerini arayın</span><span class="sxs-lookup"><span data-stu-id="96cf7-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="96cf7-124">**Al**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="96cf7-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="96cf7-125">IP</span><span class="sxs-lookup"><span data-stu-id="96cf7-125">IP</span></span> | <span data-ttu-id="96cf7-126">20000/dakika</span><span class="sxs-lookup"><span data-stu-id="96cf7-126">20000 / minute</span></span> | <span data-ttu-id="96cf7-127">NuGet paketi meta verilerini v2 OData koleksiyonu aracılığıyla sorgula `Packages`</span><span class="sxs-lookup"><span data-stu-id="96cf7-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="96cf7-128">**Al**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="96cf7-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="96cf7-129">IP</span><span class="sxs-lookup"><span data-stu-id="96cf7-129">IP</span></span> | <span data-ttu-id="96cf7-130">100/dakika</span><span class="sxs-lookup"><span data-stu-id="96cf7-130">100 / minute</span></span> | <span data-ttu-id="96cf7-131">NuGet paket sayısını v2 OData koleksiyonu aracılığıyla sorgula `Packages`</span><span class="sxs-lookup"><span data-stu-id="96cf7-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="96cf7-132">Paket gönderme ve listeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="96cf7-132">Package Push and Unlist</span></span>

| <span data-ttu-id="96cf7-133">API</span><span class="sxs-lookup"><span data-stu-id="96cf7-133">API</span></span> | <span data-ttu-id="96cf7-134">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="96cf7-134">Limit Type</span></span> | <span data-ttu-id="96cf7-135">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="96cf7-135">Limit Value</span></span> | <span data-ttu-id="96cf7-136">API kullanım örneği</span><span class="sxs-lookup"><span data-stu-id="96cf7-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="96cf7-137">**Yerleştir**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="96cf7-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="96cf7-138">API Anahtarı</span><span class="sxs-lookup"><span data-stu-id="96cf7-138">API Key</span></span> | <span data-ttu-id="96cf7-139">350/saat</span><span class="sxs-lookup"><span data-stu-id="96cf7-139">350 / hour</span></span> | <span data-ttu-id="96cf7-140">V2 Push uç noktası aracılığıyla yeni bir NuGet paketini (sürüm) karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="96cf7-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="96cf7-141">**Sil**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="96cf7-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="96cf7-142">API Anahtarı</span><span class="sxs-lookup"><span data-stu-id="96cf7-142">API Key</span></span> | <span data-ttu-id="96cf7-143">250/saat</span><span class="sxs-lookup"><span data-stu-id="96cf7-143">250 / hour</span></span> | <span data-ttu-id="96cf7-144">V2 uç noktası aracılığıyla bir NuGet paketinin (sürüm) listesini kaldırma</span><span class="sxs-lookup"><span data-stu-id="96cf7-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="96cf7-145">nuget.org web sitesi sayfası görünümleri</span><span class="sxs-lookup"><span data-stu-id="96cf7-145">nuget.org website page views</span></span>

<span data-ttu-id="96cf7-146">Nuget.org Web sayfalarına programlı bir şekilde erişiyorsanız belgelenmiş [v3 API](overview.md)'lerimizi araştırın.</span><span class="sxs-lookup"><span data-stu-id="96cf7-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="96cf7-147">Bu uç noktalar paket meta verilerine ve içeriğine daha kolay erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="96cf7-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="96cf7-148">V3 API 'sinin kullanılabilirliği daha yüksektir ve Web tarayıcısı etkileşimi için tasarlanan NuGet Galerisi Web sayfalarına erişilenden daha yüksek performansa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="96cf7-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="96cf7-149">API</span><span class="sxs-lookup"><span data-stu-id="96cf7-149">API</span></span> | <span data-ttu-id="96cf7-150">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="96cf7-150">Limit Type</span></span> | <span data-ttu-id="96cf7-151">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="96cf7-151">Limit Value</span></span> | <span data-ttu-id="96cf7-152">API kullanım örneği</span><span class="sxs-lookup"><span data-stu-id="96cf7-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="96cf7-153">**Al**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="96cf7-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="96cf7-154">IP</span><span class="sxs-lookup"><span data-stu-id="96cf7-154">IP</span></span> | <span data-ttu-id="96cf7-155">50/dakika</span><span class="sxs-lookup"><span data-stu-id="96cf7-155">50 / minute</span></span> | <span data-ttu-id="96cf7-156">Paket (sürüm) ayrıntıları sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="96cf7-156">Display package (version) details page.</span></span> 
