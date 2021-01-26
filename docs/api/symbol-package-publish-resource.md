---
title: Sembol paketlerini gönderme, NuGet API | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımla hizmeti, istemcilerin yeni sembol paketleri yayımlamasına izin verir.
keywords: NuGet API gönderme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773902"
---
# <a name="push-symbol-packages"></a>Sembol paketlerini gönder

NuGet v3 API kullanılarak sembol paketlerinin ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) gönderimi mümkündür.
Bu işlemler `SymbolPackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@type deeri                 | Notlar
--------------------        | -----
SymbolPackagePublish/4.9.0  | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Lerin temel URL 'SI, `@id` `SymbolPackagePublish/4.9.0` paket kaynağının [hizmet dizinindeki](service-index.md)kaynak özelliğinin değeridir. Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır. `https://www.nuget.org/api/v2/symbolpackage`Hizmet dizininde bulunan değer için bir yer tutucu olarak düşünün `@id` .

## <a name="http-methods"></a>HTTP yöntemleri

`PUT`Http yöntemi bu kaynak tarafından destekleniyor. 

## <a name="push-a-symbol-package"></a>Bir sembol paketini gönder

nuget.org, aşağıdaki API 'YI kullanarak yeni sembol paketleri biçimi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) göndermeyi destekler. 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

Aynı KIMLIĞE ve sürüme sahip sembol paketleri birden çok kez gönderilebilir. Aşağıdaki durumlarda bir sembol paketi reddedilir.
- Aynı KIMLIĞE ve sürüme sahip bir paket yok.
- Aynı KIMLIĞE ve sürüme sahip bir sembol paketi itildi, ancak henüz yayımlanmadı.
- Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz ( [sembol paketi kısıtlamalarına](../create-packages/Symbol-Packages-snupkg.md)bakın).

### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir. Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.

### <a name="request-body"></a>İstek gövdesi

Sembol gönderimi için istek gövdesi, bir paket gönderme isteğinin istek gövdesiyle aynı (bkz. [paket gönderme ve silme](package-publish-resource.md)). 

### <a name="response"></a>Yanıt

Durum Kodu | Anlamı
----------- | -------
201         | Sembol paketi başarıyla gönderildi.
400         | Belirtilen sembol paketi geçersiz.
401         | Kullanıcı bu eylemi gerçekleştirme yetkisine sahip değil.
404         | Belirtilen KIMLIĞE ve sürüme sahip karşılık gelen bir paket yok.
409         | Sağlanan KIMLIĞE ve sürüme sahip bir sembol paketi gönderildi ancak henüz kullanılamıyor.
413         | Paket çok büyük.

