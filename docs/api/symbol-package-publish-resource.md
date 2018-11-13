---
title: Sembol paketleri, NuGet API'si itme | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Yayımlama hizmeti yeni sembol paketleri yayımlama etmesine olanak tanır.
keywords: NuGet API'si anında iletme sembol paketi
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580454"
---
# <a name="push-symbol-packages"></a>Sembol paketleri gönder

Anında iletme sembolleri paketlere mümkündür ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API'sini kullanarak.
Kapatarak bu işlemler temel `SymbolPackagePublish` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer                 | Notlar
--------------------        | -----
SymbolPackagePublish/4.9.0  | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` özelliği `SymbolPackagePublish/4.9.0` paket kaynağının kaynak [hizmet dizini](service-index.md). Nuget.org URL'si aşağıdaki belgeleri için kullanılır. Göz önünde bulundurun `https://www.nuget.org/api/v2/symbolpackage` için yer tutucu olarak `@id` değer hizmet dizinde bulunamadı.

## <a name="http-methods"></a>HTTP yöntemleri

`PUT` HTTP yöntemi, bu kaynak tarafından desteklenir. 

## <a name="push-a-symbol-package"></a>Bir sembol paket gönderin

nuget.org koymadan yeni sembol paketleri biçimi destekler ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) aşağıdaki API'yi kullanarak. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Sembol paketleri aynı kimliği ve sürüm birden çok kez gönderilebilir. Bir sembol paketi, aşağıdaki durumlarda reddedilir.
- Bir paket ile aynı kimliği ve sürüm yok.
- Bir sembol paketi ile aynı kimliği ve sürüm gönderildiği ancak henüz yayımlanmadı.
- Sembol paketi ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) geçersiz (bkz [sembol paketi kısıtlamaları](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarı kullanıcı tarafından paket kaynağından edinmiş ve istemciyi yapılandırılmış genel olmayan bir dizedir. Hiçbir özel dize biçimi uygulanan ancak HTTP üstbilgi değerleri için makul bir boyutta API anahtarı uzunluğunu geçmemelidir.

### <a name="request-body"></a>İstek gövdesi

Sembol gönderim için istek gövdesi aynı paket gönderme isteği ile istek gövdesi (bkz [paketini anında iletme ve silme](package-publish-resource.md)). 

### <a name="response"></a>Yanıt

Durum kodu | Anlamı
----------- | -------
201         | Sembol paketi başarıyla gönderildi.
400         | Belirtilen sembol paketi geçersiz.
401         | Kullanıcının bu eylemi gerçekleştirmek için yetkili değil.
404         | Sağlanan kimliği ve sürüm karşılık gelen bir paketi yok.
409         | Bir sembol paketi sağlanan kimliği ve sürüm gönderildiği ancak henüz kullanıma sunulmamıştır.
413         | Paket çok büyük.

