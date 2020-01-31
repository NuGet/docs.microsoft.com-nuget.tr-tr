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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813201"
---
# <a name="rate-limits"></a><span data-ttu-id="09503-103">Oran limitleri</span><span class="sxs-lookup"><span data-stu-id="09503-103">Rate Limits</span></span>

<span data-ttu-id="09503-104">NuGet.org API 'SI, kötüye kullanımı engellemek için hız sınırlaması uygular.</span><span class="sxs-lookup"><span data-stu-id="09503-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="09503-105">Hız sınırını aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="09503-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="09503-106">Hız sınırlarını kullanarak istek azaltmasına ek olarak, bazı API 'Ler kota de uygular.</span><span class="sxs-lookup"><span data-stu-id="09503-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="09503-107">Kotayı aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="09503-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="09503-108">Aşağıdaki tablolarda NuGet.org API 'sinin hız sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="09503-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="09503-109">Paket arama</span><span class="sxs-lookup"><span data-stu-id="09503-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="09503-110">Şu anda sınırlı olmadığından NuGet. org 'ın [v3 arama API 'lerini](search-query-service-resource.md) kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="09503-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="09503-111">V1 ve v2 Search API 'Leri için aşağıdaki sınırlar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="09503-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="09503-112">API</span><span class="sxs-lookup"><span data-stu-id="09503-112">API</span></span> | <span data-ttu-id="09503-113">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="09503-113">Limit Type</span></span> | <span data-ttu-id="09503-114">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="09503-114">Limit Value</span></span> | <span data-ttu-id="09503-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="09503-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="09503-116">`/api/v1/Packages` **Al**</span><span class="sxs-lookup"><span data-stu-id="09503-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="09503-117">IP</span><span class="sxs-lookup"><span data-stu-id="09503-117">IP</span></span> | <span data-ttu-id="09503-118">1000/dakika</span><span class="sxs-lookup"><span data-stu-id="09503-118">1000 / minute</span></span> | <span data-ttu-id="09503-119">NuGet paketi meta verilerini v1 OData `Packages` koleksiyonu aracılığıyla sorgula</span><span class="sxs-lookup"><span data-stu-id="09503-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="09503-120">`/api/v1/Search()` **Al**</span><span class="sxs-lookup"><span data-stu-id="09503-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="09503-121">IP</span><span class="sxs-lookup"><span data-stu-id="09503-121">IP</span></span> | <span data-ttu-id="09503-122">3000/dakika</span><span class="sxs-lookup"><span data-stu-id="09503-122">3000 / minute</span></span> | <span data-ttu-id="09503-123">V1 arama uç noktası aracılığıyla NuGet paketlerini arayın</span><span class="sxs-lookup"><span data-stu-id="09503-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="09503-124">`/api/v2/Packages` **Al**</span><span class="sxs-lookup"><span data-stu-id="09503-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="09503-125">IP</span><span class="sxs-lookup"><span data-stu-id="09503-125">IP</span></span> | <span data-ttu-id="09503-126">20000/dakika</span><span class="sxs-lookup"><span data-stu-id="09503-126">20000 / minute</span></span> | <span data-ttu-id="09503-127">NuGet paketi meta verilerini v2 OData `Packages` koleksiyonu aracılığıyla sorgula</span><span class="sxs-lookup"><span data-stu-id="09503-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="09503-128">`/api/v2/Packages/$count` **Al**</span><span class="sxs-lookup"><span data-stu-id="09503-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="09503-129">IP</span><span class="sxs-lookup"><span data-stu-id="09503-129">IP</span></span> | <span data-ttu-id="09503-130">100/dakika</span><span class="sxs-lookup"><span data-stu-id="09503-130">100 / minute</span></span> | <span data-ttu-id="09503-131">V2 OData `Packages` koleksiyonu aracılığıyla NuGet paket sayısını sorgula</span><span class="sxs-lookup"><span data-stu-id="09503-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="09503-132">Paket gönderme ve listeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="09503-132">Package Push and Unlist</span></span>

| <span data-ttu-id="09503-133">API</span><span class="sxs-lookup"><span data-stu-id="09503-133">API</span></span> | <span data-ttu-id="09503-134">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="09503-134">Limit Type</span></span> | <span data-ttu-id="09503-135">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="09503-135">Limit Value</span></span> | <span data-ttu-id="09503-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="09503-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="09503-137">`/api/v2/package` **koy**</span><span class="sxs-lookup"><span data-stu-id="09503-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="09503-138">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="09503-138">API Key</span></span> | <span data-ttu-id="09503-139">350/saat</span><span class="sxs-lookup"><span data-stu-id="09503-139">350 / hour</span></span> | <span data-ttu-id="09503-140">V2 Push uç noktası aracılığıyla yeni bir NuGet paketini (sürüm) karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="09503-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="09503-141">`/api/v2/package/{id}/{version}` **Sil**</span><span class="sxs-lookup"><span data-stu-id="09503-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="09503-142">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="09503-142">API Key</span></span> | <span data-ttu-id="09503-143">250/saat</span><span class="sxs-lookup"><span data-stu-id="09503-143">250 / hour</span></span> | <span data-ttu-id="09503-144">V2 uç noktası aracılığıyla bir NuGet paketinin (sürüm) listesini kaldırma</span><span class="sxs-lookup"><span data-stu-id="09503-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
