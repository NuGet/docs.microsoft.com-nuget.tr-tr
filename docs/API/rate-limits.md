---
title: Oran sınırları | Microsoft Docs
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet API'ları kötüye önlemek üzere oran sınırları zorunlu.
keywords: NuGet API, oran sınırlama
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="9fb03-104">Oran sınırları</span><span class="sxs-lookup"><span data-stu-id="9fb03-104">Rate Limits</span></span>

<span data-ttu-id="9fb03-105">NuGet.org API kötüye önlemek için hız sınırlaması zorlar.</span><span class="sxs-lookup"><span data-stu-id="9fb03-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="9fb03-106">Hız sınırı aşan istekler aşağıdaki hatayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="9fb03-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="9fb03-107">Aşağıdaki tablolarda NuGet.org API'si için oran sınırları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9fb03-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="9fb03-108">Paket arama</span><span class="sxs-lookup"><span data-stu-id="9fb03-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="9fb03-109">NuGet.org kullanmanızı öneririz [V3 API'leri](https://docs.microsoft.com/nuget/api/search-query-service-resource) kullanıcı ve herhangi bir olmayan aramayı sınırla şu anda.</span><span class="sxs-lookup"><span data-stu-id="9fb03-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="9fb03-110">V1 ve V2 API'leri arama, followins sınırları Uygula:</span><span class="sxs-lookup"><span data-stu-id="9fb03-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="9fb03-111">API</span><span class="sxs-lookup"><span data-stu-id="9fb03-111">API</span></span> | <span data-ttu-id="9fb03-112">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="9fb03-112">Limit Type</span></span> | <span data-ttu-id="9fb03-113">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="9fb03-113">Limit Value</span></span> | <span data-ttu-id="9fb03-114">API kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="9fb03-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="9fb03-115">**AL** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="9fb03-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="9fb03-116">IP</span><span class="sxs-lookup"><span data-stu-id="9fb03-116">IP</span></span> | <span data-ttu-id="9fb03-117">1000 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-117">1000 / minute</span></span> | <span data-ttu-id="9fb03-118">NuGet paket meta verileri v1 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="9fb03-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="9fb03-119">**AL** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="9fb03-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="9fb03-120">IP</span><span class="sxs-lookup"><span data-stu-id="9fb03-120">IP</span></span> | <span data-ttu-id="9fb03-121">3000 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-121">3000 / minute</span></span> | <span data-ttu-id="9fb03-122">NuGet paketlerini v1 arama uç noktası aracılığıyla arayın</span><span class="sxs-lookup"><span data-stu-id="9fb03-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="9fb03-123">**AL** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="9fb03-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="9fb03-124">IP</span><span class="sxs-lookup"><span data-stu-id="9fb03-124">IP</span></span> | <span data-ttu-id="9fb03-125">20000 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-125">20000 / minute</span></span> | <span data-ttu-id="9fb03-126">NuGet paket meta verileri v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="9fb03-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="9fb03-127">**AL** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="9fb03-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="9fb03-128">IP</span><span class="sxs-lookup"><span data-stu-id="9fb03-128">IP</span></span> | <span data-ttu-id="9fb03-129">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-129">100 / minute</span></span> | <span data-ttu-id="9fb03-130">NuGet paket sayısı v2 OData yoluyla sorgu `Packages` koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="9fb03-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="9fb03-131">Paket gönderme ve Unlist</span><span class="sxs-lookup"><span data-stu-id="9fb03-131">Package Push and Unlist</span></span>

| <span data-ttu-id="9fb03-132">API</span><span class="sxs-lookup"><span data-stu-id="9fb03-132">API</span></span> | <span data-ttu-id="9fb03-133">Sınır türü</span><span class="sxs-lookup"><span data-stu-id="9fb03-133">Limit Type</span></span> | <span data-ttu-id="9fb03-134">Sınır değeri</span><span class="sxs-lookup"><span data-stu-id="9fb03-134">Limit Value</span></span> | <span data-ttu-id="9fb03-135">APU kullanım durumu</span><span class="sxs-lookup"><span data-stu-id="9fb03-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="9fb03-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="9fb03-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="9fb03-137">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="9fb03-137">API Key</span></span> | <span data-ttu-id="9fb03-138">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-138">100 / minute</span></span> | <span data-ttu-id="9fb03-139">V2 itme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) yükleme</span><span class="sxs-lookup"><span data-stu-id="9fb03-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="9fb03-140">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="9fb03-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="9fb03-141">API anahtarı</span><span class="sxs-lookup"><span data-stu-id="9fb03-141">API Key</span></span> | <span data-ttu-id="9fb03-142">100 / dakika</span><span class="sxs-lookup"><span data-stu-id="9fb03-142">100 / minute</span></span> | <span data-ttu-id="9fb03-143">NuGet paketi (sürüm) v2 uç nokta üzerinden unlist</span><span class="sxs-lookup"><span data-stu-id="9fb03-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
