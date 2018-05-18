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
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/17/2018
---
# <a name="rate-limits"></a>Oran sınırları

NuGet.org API kötüye önlemek için hız sınırlaması zorlar. Hız sınırı aşan istekler aşağıdaki hatayı döndürür: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Aşağıdaki tablolarda NuGet.org API'si için oran sınırları listelenmektedir.

## <a name="package-search"></a>Paket arama

> [!Note]
> NuGet.org kullanmanızı öneririz [V3 API'leri](https://docs.microsoft.com/nuget/api/search-query-service-resource) kullanıcı ve herhangi bir olmayan aramayı sınırla şu anda. V1 ve V2 API'leri arama, followins sınırları Uygula:


| API | Sınır türü | Sınır değeri | API kullanım durumu |
|:---|:---|:---|:---|
**AL** `/api/v1/Packages` | IP | 1000 / dakika | NuGet paket meta verileri v1 OData yoluyla sorgu `Packages` koleksiyonu |
**AL** `/api/v1/Search()` | IP | 3000 / dakika | NuGet paketlerini v1 arama uç noktası aracılığıyla arayın | 
**AL** `/api/v2/Packages` | IP | 20000 / dakika | NuGet paket meta verileri v2 OData yoluyla sorgu `Packages` koleksiyonu | 
**AL** `/api/v2/Packages/$count` | IP | 100 / dakika | NuGet paket sayısı v2 OData yoluyla sorgu `Packages` koleksiyonu | 

## <a name="package-push-and-unlist"></a>Paket gönderme ve Unlist

| API | Sınır türü | Sınır değeri | API kullanım durumu | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API anahtarı | 250 / saat | V2 itme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) yükleme 
**SİL** `/api/v2/package/{id}/{version}` | API anahtarı | 250 / saat | NuGet paketi (sürüm) v2 uç nokta üzerinden unlist 
