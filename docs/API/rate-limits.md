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
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="81935-103">Oran sınırları</span><span class="sxs-lookup"><span data-stu-id="81935-103">Rate Limits</span></span>

<span data-ttu-id="81935-104">NuGet.org API kötüye önlemek için hız sınırlaması zorlar.</span><span class="sxs-lookup"><span data-stu-id="81935-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="81935-105">Hız sınırı aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="81935-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="81935-106">Aşağıdaki tablolarda NuGet.org API'si için oran sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="81935-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="81935-107">Paket arama</span><span class="sxs-lookup"><span data-stu-id="81935-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="81935-108">NuGet.org kullanmanızı öneririz [V3 API'leri](https://docs.microsoft.com/nuget/api/search-query-service-resource) kullanıcı ve herhangi bir olmayan aramayı sınırla şu anda.</span><span class="sxs-lookup"><span data-stu-id="81935-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="81935-109">V1 ve V2 API'leri arama, followins sınırları Uygula:</span><span class="sxs-lookup"><span data-stu-id="81935-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="81935-110">API</span><span class="sxs-lookup"><span data-stu-id="81935-110">API</span></span> | <span data-ttu-id="81935-111">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="81935-111">Limit Type</span></span> | <span data-ttu-id="81935-112">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="81935-112">Limit Value</span></span> | <span data-ttu-id="81935-113">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="81935-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="81935-114">**AL** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="81935-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="81935-115">IP</span><span class="sxs-lookup"><span data-stu-id="81935-115">IP</span></span> | <span data-ttu-id="81935-116">1000 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-116">1000 / minute</span></span> | <span data-ttu-id="81935-117">NuGet paket meta verileri v1 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="81935-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="81935-118">**AL** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="81935-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="81935-119">IP</span><span class="sxs-lookup"><span data-stu-id="81935-119">IP</span></span> | <span data-ttu-id="81935-120">3000 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-120">3000 / minute</span></span> | <span data-ttu-id="81935-121">NuGet paketlerini v1 arama uç noktası aracılığıyla arayın</span><span class="sxs-lookup"><span data-stu-id="81935-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="81935-122">**AL** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="81935-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="81935-123">IP</span><span class="sxs-lookup"><span data-stu-id="81935-123">IP</span></span> | <span data-ttu-id="81935-124">20000 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-124">20000 / minute</span></span> | <span data-ttu-id="81935-125">NuGet paket meta verileri v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="81935-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="81935-126">**AL** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="81935-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="81935-127">IP</span><span class="sxs-lookup"><span data-stu-id="81935-127">IP</span></span> | <span data-ttu-id="81935-128">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-128">100 / minute</span></span> | <span data-ttu-id="81935-129">NuGet paket sayısı v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="81935-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="81935-130">Paket gönderme ve Unlist</span><span class="sxs-lookup"><span data-stu-id="81935-130">Package Push and Unlist</span></span>

| <span data-ttu-id="81935-131">API</span><span class="sxs-lookup"><span data-stu-id="81935-131">API</span></span> | <span data-ttu-id="81935-132">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="81935-132">Limit Type</span></span> | <span data-ttu-id="81935-133">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="81935-133">Limit Value</span></span> | <span data-ttu-id="81935-134">APU kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="81935-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="81935-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="81935-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="81935-136">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="81935-136">API Key</span></span> | <span data-ttu-id="81935-137">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-137">100 / minute</span></span> | <span data-ttu-id="81935-138">V2 itme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) yükleme</span><span class="sxs-lookup"><span data-stu-id="81935-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="81935-139">**SİL** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="81935-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="81935-140">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="81935-140">API Key</span></span> | <span data-ttu-id="81935-141">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="81935-141">100 / minute</span></span> | <span data-ttu-id="81935-142">NuGet paketi (sürüm) v2 uç nokta üzerinden unlist</span><span class="sxs-lookup"><span data-stu-id="81935-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
