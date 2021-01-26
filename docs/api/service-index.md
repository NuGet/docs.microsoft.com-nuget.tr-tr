---
title: Hizmet dizini, NuGet API 'SI
description: Hizmet dizini, NuGet HTTP API 'sinin giriş noktasıdır ve sunucunun yeteneklerini sıralar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775362"
---
# <a name="service-index"></a>Hizmet dizini

Hizmet dizini, bir NuGet paket kaynağı için giriş noktası olan ve istemci uygulamasının paket kaynağının yeteneklerini bulmasına izin veren bir JSON belgesidir. Hizmet dizini, iki gerekli özelliği olan bir JSON nesnesidir: `version` (hizmet dizininin şema sürümü) ve `resources`  (paket kaynağının uç noktaları veya özellikleri).

NuGet. org 'ın hizmet dizini konumunda bulunur `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Sürüm Oluşturma

`version`Değer, hizmet dizininin şema sürümünü gösteren bir SemVer 2.0.0 parseable sürümü dizesidir. Sürüm dizesinin ana sürüm numarası olan API mantarihlerinin `3` . Hizmet dizini şemasında, önemli olmayan değişiklikler yapıldığından, sürüm dizesinin ikincil sürümü artar.

Hizmet dizinindeki her kaynak hizmet dizini şema sürümünden bağımsız olarak sürümlüdür.

Geçerli şema sürümü `3.0.0` . `3.0.0`Sürüm işlevsel olarak eski sürüme eşdeğerdir, `3.0.0-beta.1` ancak kararlı, tanımlı şemayı daha açık bir şekilde iletişim kurduğundan tercih edilmelidir.

## <a name="http-methods"></a>HTTP yöntemleri

Hizmet dizinine HTTP yöntemleri ve aracılığıyla erişilebilir `GET` `HEAD` .

## <a name="resources"></a>Kaynaklar

`resources`Özelliği, bu paket kaynağı tarafından desteklenen bir kaynak dizisi içeriyor.

### <a name="resource"></a>Kaynak

Kaynak, dizideki bir nesnedir `resources` . Paket kaynağının sürümlü bir özelliğini temsil eder. Bir kaynak aşağıdaki özelliklere sahiptir:

Ad          | Tür   | Gerekli | Notlar
------------- | ------ | -------- | -----
@id           | string | evet      | Kaynağın URL 'SI
@type         | string | evet      | Kaynak türünü temsil eden bir dize sabiti
comment       | string | hayır       | Kaynağın okunabilir bir açıklaması

`@id`Mutlak olması gereken ve http ya da https şemasına sahip olması gereken BIR URL 'dir.

, `@type` Kaynakla etkileşim kurarken kullanılacak belirli Protokolü belirlemek için kullanılır. Kaynağın türü donuk bir dizedir, ancak genellikle şu biçimdedir:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

İstemcilerin `@type` anladıkları değerleri sabit olarak kodlamaları ve bir paket kaynağının hizmet dizininde bunları araması beklenir. `@type`Günümüzde kullanımda olan değerler, [API genel](overview.md#resources-and-schema)görünümünde listelenen tek kaynak başvuru belgelerinde numaralandırılır.

Bu belgelerin bir listesi için, farklı kaynaklarla ilgili belgeler temelde, `{RESOURCE_NAME}` senaryoya göre gruplandırma ile benzer hizmet dizininde bulunan tarafından gruplandırılır. 

Her kaynak için benzersiz bir veya olan bir gereksinim yoktur `@id` `@type` . Bu, başka bir kaynağın hangi kaynağa tercih edeceğini belirleyen istemci uygulamasına çalışır. Olası bir uygulama, `@type` bağlantı hatası veya sunucu hatası durumunda aynı veya uyumlu olan kaynakların hepsini bir kez deneme biçiminde kullanılabilir.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [service-index.json](./_data/service-index.json)]
