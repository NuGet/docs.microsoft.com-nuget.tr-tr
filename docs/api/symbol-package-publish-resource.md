---
title: Sembol paketlerini gönderme, NuGet API | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımla hizmeti, istemcilerin yeni sembol paketleri yayımlamasına izin verir.
keywords: NuGet API gönderme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235111"
---
# <a name="push-symbol-packages"></a>Sembol paketlerini gönder

NuGet v3 API kullanılarak sembol paketlerinin ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) gönderimi mümkündür.
Bu işlemler `SymbolPackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@typedeeri                 | Notlar
--------------------        | -----
SymbolPackagePublish/4.9.0  | İlk yayın

## <a name="base-url"></a>Taban URL 'SI

Aşağıdaki API 'lerin temel URL 'si, paket kaynağının `@id` [hizmet dizinindeki](service-index.md) `SymbolPackagePublish/4.9.0` kaynak özelliğinin değeridir. Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır. Hizmet `https://www.nuget.org/api/v2/symbolpackage` dizininde bulunan `@id` değer için bir yer tutucu olarak düşünün.

## <a name="http-methods"></a>HTTP yöntemleri

`PUT` Http yöntemi bu kaynak tarafından destekleniyor. 

## <a name="push-a-symbol-package"></a>Bir sembol paketini gönder

nuget.org, aşağıdaki API 'YI kullanarak yeni sembol paketleri biçimi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) göndermeyi destekler. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Aynı KIMLIĞE ve sürüme sahip sembol paketleri birden çok kez gönderilebilir. Aşağıdaki durumlarda bir sembol paketi reddedilir.
- Aynı KIMLIĞE ve sürüme sahip bir paket yok.
- Aynı KIMLIĞE ve sürüme sahip bir sembol paketi itildi, ancak henüz yayımlanmadı.
- Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz ( [sembol paketi kısıtlamalarına](../create-packages/Symbol-Packages-snupkg.md)bakın).

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Üstbilgi | dize | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir. Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.

### <a name="request-body"></a>İstek gövdesi

Sembol gönderimi için istek gövdesi, bir paket gönderme isteğinin istek gövdesiyle aynı (bkz. [paket gönderme ve silme](package-publish-resource.md)). 

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
201         | Sembol paketi başarıyla gönderildi.
400         | Belirtilen sembol paketi geçersiz.
401         | Kullanıcı bu eylemi gerçekleştirme yetkisine sahip değil.
404         | Belirtilen KIMLIĞE ve sürüme sahip karşılık gelen bir paket yok.
409         | Sağlanan KIMLIĞE ve sürüme sahip bir sembol paketi gönderildi ancak henüz kullanılamıyor.
413         | Paket çok büyük.

