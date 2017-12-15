---
title: "Anında iletme ve Delete, NuGet API | Microsoft Docs"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Yayımlama hizmeti, istemcilerin yeni paketleri yayımlama ve unlist veya var olan paketleri silmek olanak tanır."
keywords: "NuGet API itme paket NuGet API Sil paket, NuGet API unlist paketi, NuGet API karşıya yükleme paketi, NuGet API'si paketi oluşturma"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a>Anında iletme ve silin

Anında iletme ve silme (veya unlist, bağlı sunucu uygulaması) mümkündür NuGet V3 API'yi kullanarak paketler.
İki işlem kapatarak dayalı `PackagePublish` kaynak bulunan [Hizmeti dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@typedeğer          | Notlar
-------------------- | -----
PackagePublish/2.0.0 | İlk sürüm

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [Hizmeti dizini](service-index.md). Aşağıdaki belgeler için nuget.org URL'si kullanılır. Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için bir yer tutucu olarak `@id` değeri hizmet dizininde bulunamadı.

Protokol aynı olduğundan bu URL eski V2 itme bitiş noktası ile aynı konumda işaret olduğunu unutmayın.

## <a name="http-methods"></a>HTTP yöntemleri

`PUT` Ve `DELETE` HTTP yöntemleri, bu kaynak tarafından desteklenir. Hangi yöntemlerin her noktadaki desteklediği için aşağıya bakın.

## <a name="push-a-package"></a>Bir paket gönderme

nuget.org aşağıdaki API kullanarak koymadan yeni paketlerini destekler. Sağlanan Kimliğini ve sürümünü paketiyle zaten varsa, nuget.org itme reddeder. Mevcut bir paketi değiştirerek diğer paket kaynaklarını destekleyebilir.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-apikey ile yapılan | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarını paket kaynağından kullanıcı tarafından onayınızı ve istemciyi yapılandırılmış donuk bir dizedir. Hiçbir belirli dize biçimi zorunlu ancak API anahtarı uzunluğu HTTP üstbilgi değerleri için makul bir boyut aşamaz.

### <a name="request-body"></a>İstek gövdesi

İstek gövdesini şu biçimde gelmelidir:

#### <a name="multipart-form-data"></a>Çok bölümlü form verilerinin

İstek üstbilgisi `Content-Type` olan `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır. Çok bölümlü gövde sonraki öğelerde göz ardı edilir. Dosya adı veya çok parçalı öğelerinin diğer tüm üst bilgileri yoksayılır.

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
201, 202    | Paket başarıyla gönderilir
400         | Belirtilen paket geçersiz
409         | Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.

Sunucu uygulamaları bir paketi başarıyla gönderildiğinde döndürülen başarı durum kodu farklılık gösterir.

## <a name="delete-a-package"></a>Paket Sil

nuget.org yorumlar paketi silme isteği olarak "unlist" bir. Bu paketin paket varolan Tüketiciler için hala kullanılabilir olduğundan, ancak paket artık arama sonuçlarında veya web arabirimi görünür anlamına gelir. Bu uygulama hakkında daha fazla bilgi için bkz: [silinen paketler](../policies/deleting-packages.md) ilkesi. Bu sinyal sabit delete olarak yorumlama, yumuşak silin veya unlist ücretsiz diğer sunucu uygulamalarıdır. Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API destekleyen bir sunucu uygulaması) destekleyen bir unlist veya bir yapılandırma seçeneği göre sabit bir delete olarak bu isteği işleme.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | Evet      | Silmek için paket kimliği
VERSION        | URL    | dize | Evet      | Silmek için paketin sürümü
X-NuGet-apikey ile yapılan | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
204         | Paket silindi
404         | İle sağlanan bir paket yok `ID` ve `VERSION` var.
