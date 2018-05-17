---
title: Sınırları, NuGet API oranı
description: NuGet API'ları kötüye önlemek üzere oran sınırları zorunlu.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="7e297-103">Oran sınırları</span><span class="sxs-lookup"><span data-stu-id="7e297-103">Rate Limits</span></span>

<span data-ttu-id="7e297-104">NuGet.org API kötüye önlemek için hız sınırlaması zorlar.</span><span class="sxs-lookup"><span data-stu-id="7e297-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="7e297-105">Hız sınırı aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="7e297-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="7e297-106">Aşağıdaki tablolarda NuGet.org API'si için oran sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="7e297-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="7e297-107">Paket arama</span><span class="sxs-lookup"><span data-stu-id="7e297-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="7e297-108">NuGet.org kullanmanızı öneririz [V3 API'leri](https://docs.microsoft.com/nuget/api/search-query-service-resource) kullanıcı ve herhangi bir olmayan aramayı sınırla şu anda.</span><span class="sxs-lookup"><span data-stu-id="7e297-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="7e297-109">V1 ve V2 API'leri arama, followins sınırları Uygula:</span><span class="sxs-lookup"><span data-stu-id="7e297-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="7e297-110">API</span><span class="sxs-lookup"><span data-stu-id="7e297-110">API</span></span> | <span data-ttu-id="7e297-111">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="7e297-111">Limit Type</span></span> | <span data-ttu-id="7e297-112">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="7e297-112">Limit Value</span></span> | <span data-ttu-id="7e297-113">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="7e297-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="7e297-114">**AL** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="7e297-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="7e297-115">IP</span><span class="sxs-lookup"><span data-stu-id="7e297-115">IP</span></span> | <span data-ttu-id="7e297-116">1000 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-116">1000 / minute</span></span> | <span data-ttu-id="7e297-117">NuGet paket meta verileri v1 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="7e297-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="7e297-118">**AL** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="7e297-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="7e297-119">IP</span><span class="sxs-lookup"><span data-stu-id="7e297-119">IP</span></span> | <span data-ttu-id="7e297-120">3000 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-120">3000 / minute</span></span> | <span data-ttu-id="7e297-121">NuGet paketlerini v1 arama uç noktası aracılığıyla arayın</span><span class="sxs-lookup"><span data-stu-id="7e297-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="7e297-122">**AL** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="7e297-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="7e297-123">IP</span><span class="sxs-lookup"><span data-stu-id="7e297-123">IP</span></span> | <span data-ttu-id="7e297-124">20000 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-124">20000 / minute</span></span> | <span data-ttu-id="7e297-125">NuGet paket meta verileri v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="7e297-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="7e297-126">**AL** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="7e297-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="7e297-127">IP</span><span class="sxs-lookup"><span data-stu-id="7e297-127">IP</span></span> | <span data-ttu-id="7e297-128">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-128">100 / minute</span></span> | <span data-ttu-id="7e297-129">NuGet paket sayısı v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="7e297-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="7e297-130">Paket gönderme ve Unlist</span><span class="sxs-lookup"><span data-stu-id="7e297-130">Package Push and Unlist</span></span>

| <span data-ttu-id="7e297-131">API</span><span class="sxs-lookup"><span data-stu-id="7e297-131">API</span></span> | <span data-ttu-id="7e297-132">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="7e297-132">Limit Type</span></span> | <span data-ttu-id="7e297-133">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="7e297-133">Limit Value</span></span> | <span data-ttu-id="7e297-134">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="7e297-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="7e297-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="7e297-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="7e297-136">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="7e297-136">API Key</span></span> | <span data-ttu-id="7e297-137">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-137">100 / minute</span></span> | <span data-ttu-id="7e297-138">V2 itme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) yükleme</span><span class="sxs-lookup"><span data-stu-id="7e297-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="7e297-139">**SİL** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="7e297-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="7e297-140">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="7e297-140">API Key</span></span> | <span data-ttu-id="7e297-141">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="7e297-141">100 / minute</span></span> | <span data-ttu-id="7e297-142">NuGet paketi (sürüm) v2 uç nokta üzerinden unlist</span><span class="sxs-lookup"><span data-stu-id="7e297-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
