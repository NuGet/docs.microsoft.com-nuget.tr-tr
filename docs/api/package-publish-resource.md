---
title: Push ve DELETE, NuGet API
description: Yayımla hizmeti, istemcilerin yeni paketleri yayımlamasına ve var olan paketleri silmesine veya silmesine izin verir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773918"
---
# <a name="push-and-delete"></a>Gönder ve Sil

Bu, sunucu uygulamasına bağlı olarak bir gönderme, silme (veya listesini kaldırma) ve NuGet v3 API 'sini kullanarak paketleri yeniden listelemek mümkündür. Bu işlemler `PackagePublish` [hizmet dizininde](service-index.md)bulunan kaynağı temel alınır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@type deeri          | Notlar
-------------------- | -----
PackagePublish/2.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Lerin temel URL 'SI, `@id` `PackagePublish/2.0.0` paket kaynağının [hizmet dizinindeki](service-index.md)kaynak özelliğinin değeridir. Aşağıdaki belgeler için NuGet. org 'ın URL 'SI kullanılır. `https://www.nuget.org/api/v2/package`Hizmet dizininde bulunan değer için bir yer tutucu olarak düşünün `@id` .

Protokol aynı olduğundan, bu URL 'nin eski v2 gönderim uç noktasıyla aynı konuma işaret ettiğini unutmayın.

## <a name="http-methods"></a>HTTP yöntemleri

`PUT`, `POST` Ve `DELETE` http yöntemleri bu kaynak tarafından desteklenir. Her uç noktada desteklenen yöntemler için aşağıya bakın.

## <a name="push-a-package"></a>Paket gönder

> [!Note]
> nuget.org, gönderim uç noktasıyla etkileşim kurmak için [ek gereksinimlere](NuGet-Protocols.md) sahiptir.

nuget.org, aşağıdaki API 'YI kullanarak yeni paketleri göndermeyi destekler. Belirtilen KIMLIĞE ve sürüme sahip paket zaten mevcutsa, nuget.org itme 'yi reddeder. Diğer paket kaynakları, mevcut bir paketi değiştirmeyi destekleyebilir.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarı, Kullanıcı tarafından paket kaynağından alınan ve istemciye yapılandırılan donuk bir dizedir. Belirli bir dize biçimi uygulanan değildir ancak API anahtarının uzunluğu, HTTP üst bilgisi değerleri için makul bir boyutu aşmamalıdır.

### <a name="request-body"></a>İstek gövdesi

İstek gövdesinin aşağıdaki biçimde gelmesi gerekir:

#### <a name="multipart-form-data"></a>Çok parçalı form verileri

İstek üst bilgisi `Content-Type` `multipart/form-data` ve istek gövdesindeki ilk öğe, gönderilen. nupkg 'nin ham baytlardır. Çok parçalı gövdedeki sonraki öğeler yok sayılır. Dosya adı veya çok parçalı öğelerin diğer üstbilgileri yok sayılır.

### <a name="response"></a>Yanıt

Durum Kodu | Anlamı
----------- | -------
201, 202    | Paket başarıyla gönderildi
400         | Belirtilen paket geçersiz
409         | Belirtilen KIMLIĞE ve sürüme sahip bir paket zaten var

Sunucu uygulamaları, bir paket başarıyla gönderildiğinde döndürülen başarı durum koduna göre farklılık gösterir.

## <a name="delete-a-package"></a>Paket silme

nuget.org paket silme isteğini "listeden kaldır" olarak yorumlar. Bu, paketin mevcut paketin var olan tüketicilerine hala kullanılabildiği, ancak paketin artık arama sonuçlarında veya web arabiriminde görüntülenmediği anlamına gelir. Bu uygulama hakkında daha fazla bilgi için, [silinen paketler](../nuget-org/policies/deleting-packages.md) ilkesine bakın. Diğer sunucu uygulamaları, bu sinyali sabit silme, geçici silme veya listeden kaldırma olarak yorumlamak için ücretsizdir. Örneğin, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski v2 API 'sini destekleyen bir sunucu uygulama), bu isteğin bir yapılandırma seçeneğine bağlı olarak, bir listeden kaldır veya sabit bir Delete olarak işlenmesini destekler.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | evet      | Silinecek paketin KIMLIĞI
VERSION        | URL    | string | evet      | Silinecek paketin sürümü
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Yanıt

Durum Kodu | Anlamı
----------- | -------
204         | Paket silindi
404         | Belirtilen `ID` ve mevcut bir paket yok `VERSION`

## <a name="relist-a-package"></a>Bir paketi yeniden listeleme

Bir paket listede yoksa, "relist" uç noktası kullanılarak bu paketi arama sonuçlarında bir kez daha görünür hale getirmek mümkündür. Bu uç nokta, [Delete (Unlist) uç noktası](#delete-a-package) ile aynı şekle sahiptir ancak `POST` Yöntem yerine http yöntemini kullanır `DELETE` .

Paket zaten listeleniyorsa, istek yine de başarılı olur.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | evet      | Yeniden listelemek için paketin KIMLIĞI
VERSION        | URL    | string | evet      | Yeniden listelemek için paketin sürümü
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Yanıt

Durum Kodu | Anlamı
----------- | -------
200         | Paket artık listelendi
404         | Belirtilen `ID` ve mevcut bir paket yok `VERSION`
