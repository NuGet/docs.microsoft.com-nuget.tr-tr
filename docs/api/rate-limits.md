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
# <a name="rate-limits"></a>Oran limitleri

NuGet.org API 'SI, kötüye kullanımı engellemek için hız sınırlaması uygular. Hız sınırını aşan istekler aşağıdaki hatayı döndürür: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Hız sınırlarını kullanarak istek azaltmasına ek olarak, bazı API 'Ler kota de uygular. Kotayı aşan istekler aşağıdaki hatayı döndürür:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Aşağıdaki tablolarda NuGet.org API 'sinin hız sınırları listelenmektedir.

## <a name="package-search"></a>Paket arama

> [!Note]
> Şu anda sınırlı olmadığından NuGet. org 'ın [v3 arama API 'lerini](search-query-service-resource.md) kullanmanızı öneririz. V1 ve v2 Search API 'Leri için aşağıdaki sınırlar geçerlidir:

| API | Sınır türü | Sınır değeri | API usecase |
|:---|:---|:---|:---|
`/api/v1/Packages` **Al** | IP | 1000/dakika | NuGet paketi meta verilerini v1 OData `Packages` koleksiyonu aracılığıyla sorgula |
`/api/v1/Search()` **Al** | IP | 3000/dakika | V1 arama uç noktası aracılığıyla NuGet paketlerini arayın | 
`/api/v2/Packages` **Al** | IP | 20000/dakika | NuGet paketi meta verilerini v2 OData `Packages` koleksiyonu aracılığıyla sorgula | 
`/api/v2/Packages/$count` **Al** | IP | 100/dakika | V2 OData `Packages` koleksiyonu aracılığıyla NuGet paket sayısını sorgula | 

## <a name="package-push-and-unlist"></a>Paket gönderme ve listeden kaldırma

| API | Sınır türü | Sınır değeri | API usecase | 
|:---|:---|:---|:--- |
`/api/v2/package` **koy** | API anahtarı | 350/saat | V2 Push uç noktası aracılığıyla yeni bir NuGet paketini (sürüm) karşıya yükle 
`/api/v2/package/{id}/{version}` **Sil** | API anahtarı | 250/saat | V2 uç noktası aracılığıyla bir NuGet paketinin (sürüm) listesini kaldırma 
