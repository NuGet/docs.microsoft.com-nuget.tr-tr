---
title: API NuGet hizmet dizini
description: Hizmet dizini NuGet HTTP API'sinin giriş noktasıdır ve sunucu yeteneklerini numaralandırır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324727"
---
# <a name="service-index"></a>Hizmet dizini

Hizmet dizini NuGet paket kaynağı için giriş noktası ve bir istemci uygulama paket kaynağının özelliklerini hemen bulmasına izin veren bir JSON belgesidir. Hizmet dizini iki gerekli özelliklere sahip bir JSON nesnesidir: `version` (hizmet dizini şema sürümü) ve `resources` (uç noktaları veya paket kaynağının özellikleri).

nuget.org hizmet dizini adresindedir `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Sürüm oluşturma

`version` Hizmet dizini şema sürümünü gösteren bir SemVer 2.0.0 parseable sürüm dizesi değeridir. API sürüm dizesi bir ana sürüm numarasını sahip olduğunu taahhütlerin `3`. Hizmet dizin şeması için hataya neden olmayan değişiklikler yapıldıkça, sürüm dizesinin alt sürümü artırılır.

Her hizmet dizinindeki bağımsız olarak hizmet dizin şema sürümünden tutulan bir kaynaktır.

Geçerli şema sürümü `3.0.0`. `3.0.0` Sürümüdür eski işlevsel olarak eşdeğer `3.0.0-beta.1` sürüm ancak kararlı, tanımlı bir şema daha net bir şekilde iletişim kuran olarak tercih edilen olmalıdır.

## <a name="http-methods"></a>HTTP yöntemleri

Hizmet dizini, HTTP yöntemleri kullanılarak erişilebilir `GET` ve `HEAD`.

## <a name="resources"></a>Kaynaklar

`resources` Kaynakları bu paket kaynak tarafından desteklenen bir dizi özelliği içerir.

### <a name="resource"></a>Kaynak

Bir nesneyi bir kaynaktır `resources` dizisi. Bu paket kaynağının tutulan bir özelliği temsil eder. Bir kaynak, aşağıdaki özelliklere sahiptir:

Ad          | Tür   | Gerekli | Notlar
------------- | ------ | -------- | -----
@id           | dize | evet      | Kaynak URL'si
@type         | dize | evet      | Kaynak türünü temsil eden bir dize sabiti
comment       | dize | Yok       | Kaynak insan tarafından okunabilir bir açıklaması

`@id` Gerekir ve mutlak bir URL HTTP veya HTTPS şeması sahip olabilir.

`@type` Kaynakla etkileşim kurarken kullanacağı özel bir protokolü tanımlamak için kullanılır. Kaynak türü, genel olmayan bir dizedir, ancak genellikle şu biçimdedir:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

İstemciler için sabit kod beklenen `@type` anlamak ve bir paket kaynağının hizmet dizinine bakarak değerleri. Tam `@type` numaralandırılmış değerlerinin bugün kullanımda listelenen ayrı kaynak başvuru belgelerindeki [API'sine genel bakış](overview.md#resources-and-schema).

Bu belge için farklı kaynaklar ile ilgili belgeler tarafından temelde gruplandırılacak `{RESOURCE_NAME}` senaryoya göre gruplandırma benzer olan hizmet dizinde bulunamadı. 

Her bir kaynağın benzersiz olan bir gereksinimi yoktur `@id` veya `@type`. Bu istemci uygulamasının hangi kaynağı diğerine tercih kadar olur. Olası bir uygulaması olan kaynaklar aynı veya uyumlu `@type` ettirirsiniz bağlantı kesintisi veya sunucu hatası olması durumunda kullanılabilir.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [service-index.json](./_data/service-index.json)]
