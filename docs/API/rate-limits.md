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

| API | Sınır türü | Sınır değeri | APU kullanım durumu | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API anahtarı | 100 / dakika | V2 itme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) yükleme 
**SİL** `/api/v2/package/{id}/{version}` | API anahtarı | 100 / dakika | NuGet paketi (sürüm) v2 uç nokta üzerinden unlist 
