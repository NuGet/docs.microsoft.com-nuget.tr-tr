---
title: Oran sınırları, NuGet API'si
description: NuGet API'leri kötüye kullanımı önlemek üzere oran sınırları zorunlu.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508133"
---
# <a name="rate-limits"></a><span data-ttu-id="1706f-103">Oran sınırları</span><span class="sxs-lookup"><span data-stu-id="1706f-103">Rate Limits</span></span>

<span data-ttu-id="1706f-104">NuGet.org API kötüye kullanımı önlemek için hız sınırlaması zorlar.</span><span class="sxs-lookup"><span data-stu-id="1706f-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="1706f-105">Hız sınırı aşan istekleri şu hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="1706f-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="1706f-106">Oran sınırları kullanarak azaltmayı istek ek olarak, bazı API'leri ayrıca kota uygular.</span><span class="sxs-lookup"><span data-stu-id="1706f-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="1706f-107">Kotayı aştığınız isteği şu hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="1706f-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="1706f-108">Aşağıdaki tablolarda NuGet.org API için oran sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="1706f-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="1706f-109">Paket arama</span><span class="sxs-lookup"><span data-stu-id="1706f-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="1706f-110">NuGet.org kullanmanızı öneririz [V3 API'ler](https://docs.microsoft.com/nuget/api/search-query-service-resource) sınırlamak şu anda yüksek performanslı ve olmadığından arayın.</span><span class="sxs-lookup"><span data-stu-id="1706f-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="1706f-111">V1 ve V2 için arama API'leri, followins sınırlar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="1706f-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="1706f-112">API</span><span class="sxs-lookup"><span data-stu-id="1706f-112">API</span></span> | <span data-ttu-id="1706f-113">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="1706f-113">Limit Type</span></span> | <span data-ttu-id="1706f-114">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="1706f-114">Limit Value</span></span> | <span data-ttu-id="1706f-115">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="1706f-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="1706f-116">**AL** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="1706f-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="1706f-117">IP</span><span class="sxs-lookup"><span data-stu-id="1706f-117">IP</span></span> | <span data-ttu-id="1706f-118">1000 / dakika</span><span class="sxs-lookup"><span data-stu-id="1706f-118">1000 / minute</span></span> | <span data-ttu-id="1706f-119">NuGet paketi meta verilerini v1 OData aracılığıyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1706f-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="1706f-120">**AL** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="1706f-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="1706f-121">IP</span><span class="sxs-lookup"><span data-stu-id="1706f-121">IP</span></span> | <span data-ttu-id="1706f-122">3000 / dakika</span><span class="sxs-lookup"><span data-stu-id="1706f-122">3000 / minute</span></span> | <span data-ttu-id="1706f-123">V1 arama uç noktası aracılığıyla NuGet paketleri Ara</span><span class="sxs-lookup"><span data-stu-id="1706f-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="1706f-124">**AL** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="1706f-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="1706f-125">IP</span><span class="sxs-lookup"><span data-stu-id="1706f-125">IP</span></span> | <span data-ttu-id="1706f-126">20000 / dakika</span><span class="sxs-lookup"><span data-stu-id="1706f-126">20000 / minute</span></span> | <span data-ttu-id="1706f-127">NuGet paketi meta verilerini aracılığıyla v2 OData sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1706f-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="1706f-128">**AL** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="1706f-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="1706f-129">IP</span><span class="sxs-lookup"><span data-stu-id="1706f-129">IP</span></span> | <span data-ttu-id="1706f-130">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="1706f-130">100 / minute</span></span> | <span data-ttu-id="1706f-131">NuGet paket sayısı aracılığıyla v2 OData sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1706f-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="1706f-132">Paket gönderme ve listeden Kaldır</span><span class="sxs-lookup"><span data-stu-id="1706f-132">Package Push and Unlist</span></span>

| <span data-ttu-id="1706f-133">API</span><span class="sxs-lookup"><span data-stu-id="1706f-133">API</span></span> | <span data-ttu-id="1706f-134">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="1706f-134">Limit Type</span></span> | <span data-ttu-id="1706f-135">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="1706f-135">Limit Value</span></span> | <span data-ttu-id="1706f-136">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="1706f-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="1706f-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="1706f-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="1706f-138">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="1706f-138">API Key</span></span> | <span data-ttu-id="1706f-139">250 / saat</span><span class="sxs-lookup"><span data-stu-id="1706f-139">250 / hour</span></span> | <span data-ttu-id="1706f-140">V2 anında iletme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) karşıya yükleyin</span><span class="sxs-lookup"><span data-stu-id="1706f-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="1706f-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="1706f-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="1706f-142">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="1706f-142">API Key</span></span> | <span data-ttu-id="1706f-143">250 / saat</span><span class="sxs-lookup"><span data-stu-id="1706f-143">250 / hour</span></span> | <span data-ttu-id="1706f-144">V2 uç noktası aracılığıyla bir NuGet paketi (sürüm) listeden Kaldır</span><span class="sxs-lookup"><span data-stu-id="1706f-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
