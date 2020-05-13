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

| API | Sınır türü | Sınır değeri | API kullanım örneği |
|:---|:---|:---|:---|
**Al**`/api/v1/Packages` | IP | 1000/dakika | NuGet paketi meta verilerini v1 OData koleksiyonu aracılığıyla sorgula `Packages` |
**Al**`/api/v1/Search()` | IP | 3000/dakika | V1 arama uç noktası aracılığıyla NuGet paketlerini arayın | 
**Al**`/api/v2/Packages` | IP | 20000/dakika | NuGet paketi meta verilerini v2 OData koleksiyonu aracılığıyla sorgula `Packages` | 
**Al**`/api/v2/Packages/$count` | IP | 100/dakika | NuGet paket sayısını v2 OData koleksiyonu aracılığıyla sorgula `Packages` | 

## <a name="package-push-and-unlist"></a>Paket gönderme ve listeden kaldırma

| API | Sınır türü | Sınır değeri | API kullanım örneği | 
|:---|:---|:---|:--- |
**Yerleştir**`/api/v2/package` | API Anahtarı | 350/saat | V2 Push uç noktası aracılığıyla yeni bir NuGet paketini (sürüm) karşıya yükle 
**Sil**`/api/v2/package/{id}/{version}` | API Anahtarı | 250/saat | V2 uç noktası aracılığıyla bir NuGet paketinin (sürüm) listesini kaldırma 

## <a name="nugetorg-website-page-views"></a>nuget.org web sitesi sayfası görünümleri

Nuget.org Web sayfalarına programlı bir şekilde erişiyorsanız belgelenmiş [v3 API](overview.md)'lerimizi araştırın. Bu uç noktalar paket meta verilerine ve içeriğine daha kolay erişim sağlar. V3 API 'sinin kullanılabilirliği daha yüksektir ve Web tarayıcısı etkileşimi için tasarlanan NuGet Galerisi Web sayfalarına erişilenden daha yüksek performansa sahiptir.

| API | Sınır türü | Sınır değeri | API kullanım örneği | 
|:---|:---|:---|:--- |
**Al**`/package/{id}/{version}` | IP | 50/dakika | Paket (sürüm) ayrıntıları sayfasını görüntüleyin. 
