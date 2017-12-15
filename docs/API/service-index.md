---
title: Hizmet dizini, NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 2f6d6cf2-53fb-417a-b1d8-e0ac591c1699
description: "Hizmet dizini NuGet HTTP API giriş noktasıdır ve sunucu özelliklerini numaralandırır."
keywords: "NuGet API giriş noktası, NuGetA PI uç nokta bulma"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 0c43a09d8564964bd0140b9ac5deb9d3063e4dc5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="service-index"></a>Hizmet dizini

NuGet paket kaynağı için giriş noktasıdır ve paket kaynağının özellikleri bulmak bir istemci uygulaması izin veren bir JSON belgesi hizmet dizinidir. İki gerekli özellikleri olan bir JSON nesnesi hizmet dizinidir: `version` (hizmeti dizini şema sürümü) ve `resources` (uç noktaları veya paket kaynağının özelliklerini).

nuget.org Hizmeti dizini burada bulunur:
```
https://api.nuget.org/v3/index.json
```

## <a name="versioning"></a>Sürüm oluşturma

`version` Hizmeti dizini şema sürümü gösteren bir SemVer 2.0.0 parseable sürüm dizesi değeridir.
Sürüm dizesi bir ana sürüm numarası olan API olması zorunlu tutulmuştur `3`. Hizmet dizin şemasına yapılan bölünemez değişiklikler gibi sürüm dizesinin alt sürümü artırılır.

Her hizmet dizindeki bağımsız olarak hizmet dizin şeması sürümünden sürümlü kaynaktır.

Geçerli şema sürümü `3.0.0-beta.1`.

## <a name="http-methods"></a>HTTP yöntemleri

Hizmet dizini HTTP yöntemleri kullanılarak erişilebilir olduğundan `GET` ve `HEAD`.

## <a name="resources"></a>Kaynaklar

`resources` Özelliği, bu paket kaynak tarafından desteklenen kaynakları dizisi içerir.

### <a name="resource"></a>Kaynak

Bir nesne bir kaynaktır `resources` dizi. Paket kaynağının sürümlü bir özelliği temsil eder. Bir kaynak aşağıdaki özelliklere sahiptir:

Ad          | Tür   | Gerekli | Notlar
------------- | ------ | -------- | -----
@id           | dize | Evet      | Kaynak URL
@type         | dize | Evet      | Kaynak türü temsil eden bir dize sabiti
comment       | dize | Yok       | Kaynak İnsan okunabilir açıklaması

`@id` Mutlak olmalı ve ya da gereken bir URL HTTP veya HTTPS şeması sahip olabilir.

`@type` Kaynakla kullanılırken kullanılacak belirli Protokolü tanımlamak için kullanılır. Kaynak türü donuk bir dizedir ancak genellikle biçime sahiptir:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

İstemciler için sabit kod beklenen `@type` anlamak ve bir paket kaynağının hizmet dizinde aramak değerleri. Tam `@type` Günümüzde kullanılan değerleri numaralandırılan listelenen tek tek kaynak başvuru belgelerinde [API genel bakış](overview.md#resources-and-schema).

Bu belge amacıyla, farklı kaynaklarının ilgili belgelere tarafından temelde gruplandırılacak `{RESOURCE_NAME}` senaryo gruplandırarak paraleldir hizmet dizininde bulunamadı. 

Her kaynak benzersiz olduğunu gereksinimi yoktur ve `@id` veya `@type`. Hangi kaynak üzerinde başka bir tercih belirlemek için istemci uygulaması kadar olur. Bir olası uygulama işlemidir aynı veya uyumlu kaynakları `@type` bağlantı hatası veya sunucu hatası durumunda hepsini şekilde kullanılabilir.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [service-index.json](./_data/service-index.json)]
