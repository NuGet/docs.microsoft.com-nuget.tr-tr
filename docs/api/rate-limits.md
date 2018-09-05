---
title: Oran sınırları, NuGet API'si
description: NuGet API'leri kötüye kullanımı önlemek üzere oran sınırları zorunlu.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548683"
---
# <a name="rate-limits"></a>Oran sınırları

NuGet.org API kötüye kullanımı önlemek için hız sınırlaması zorlar. Hız sınırı aşan istekleri şu hatayı döndürür: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Oran sınırları kullanarak azaltmayı istek ek olarak, bazı API'leri ayrıca kota uygular. Kotayı aştığınız isteği şu hatayı döndürür:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Aşağıdaki tablolarda NuGet.org API için oran sınırları listelenmektedir.

## <a name="package-search"></a>Paket arama

> [!Note]
> NuGet.org kullanmanızı öneririz [V3 API'ler](https://docs.microsoft.com/nuget/api/search-query-service-resource) sınırlamak şu anda yüksek performanslı ve olmadığından arayın. V1 ve V2 için arama API'leri, followins sınırlar geçerlidir:


| API | Sınır türü | Sınır değeri | API kullanım durumu |
|:---|:---|:---|:---|
**AL** `/api/v1/Packages` | IP | 1000 / dakika | NuGet paketi meta verilerini v1 OData aracılığıyla sorgu `Packages` koleksiyonu |
**AL** `/api/v1/Search()` | IP | 3000 / dakika | V1 arama uç noktası aracılığıyla NuGet paketleri Ara | 
**AL** `/api/v2/Packages` | IP | 20000 / dakika | NuGet paketi meta verilerini aracılığıyla v2 OData sorgu `Packages` koleksiyonu | 
**AL** `/api/v2/Packages/$count` | IP | 100 / dakika | NuGet paket sayısı aracılığıyla v2 OData sorgu `Packages` koleksiyonu | 

## <a name="package-push-and-unlist"></a>Paket gönderme ve listeden Kaldır

| API | Sınır türü | Sınır değeri | API kullanım durumu | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API anahtarı | 250 / saat | V2 anında iletme uç noktası aracılığıyla yeni bir NuGet paketi (sürüm) karşıya yükleyin 
**DELETE** `/api/v2/package/{id}/{version}` | API anahtarı | 250 / saat | V2 uç noktası aracılığıyla bir NuGet paketi (sürüm) listeden Kaldır 
