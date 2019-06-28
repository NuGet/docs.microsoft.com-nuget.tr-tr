---
title: Gönder ve Sil, NuGet API'si
description: Yayımlama hizmeti, yeni paket yayımlamasına ve listeden veya var olan paketleri Sil etmesine olanak tanır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426719"
---
# <a name="push-and-delete"></a>Gönder ve Sil

Anında iletme, silme (veya, bağlı sunucu uygulaması listeden da) mümkündür ve NuGet V3 API'yi kullanarak paketler yeniden listele. Kapatarak bu işlemler temel `PackagePublish` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer          | Notlar
-------------------- | -----
PackagePublish/2.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` özelliği `PackagePublish/2.0.0` paket kaynağının kaynak [hizmet dizini](service-index.md). Nuget.org URL'si aşağıdaki belgeleri için kullanılır. Göz önünde bulundurun `https://www.nuget.org/api/v2/package` için yer tutucu olarak `@id` değer hizmet dizinde bulunamadı.

Protokol aynı olduğundan bu URL eski V2 anında iletme uç noktası ile aynı konuma işaret olduğunu unutmayın.

## <a name="http-methods"></a>HTTP yöntemleri

`PUT`, `POST` Ve `DELETE` bu kaynak tarafından desteklenen HTTP yöntemleri. Hangi yöntemler üzerinde her uç nokta için destekleniyor, aşağıya bakın.

## <a name="push-a-package"></a>Bir paket gönderin

> [!Note]
> nuget.org sahip [ek gereksinimler](NuGet-Protocols.md) anında iletme uç noktası ile etkileşim kurmak için.

nuget.org aşağıdaki API'yi kullanarak koymadan yeni paketler destekler. Paket kimliği ve sürüm sağlanan zaten varsa, anında iletme nuget.org reddeder. Diğer paket kaynaklarını, var olan paketi değiştirerek destekleyebilir.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Üstbilgi | dize | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

API anahtarı kullanıcı tarafından paket kaynağından edinmiş ve istemciyi yapılandırılmış genel olmayan bir dizedir. Hiçbir özel dize biçimi uygulanan ancak HTTP üstbilgi değerleri için makul bir boyutta API anahtarı uzunluğunu geçmemelidir.

### <a name="request-body"></a>İstek gövdesi

İstek gövdesi, aşağıdaki biçimde gelmesi gerekir:

#### <a name="multipart-form-data"></a>Çok bölümlü form verilerinin

İstek üstbilgisi `Content-Type` olduğu `multipart/form-data` ve ilk öğe istek gövdesi olarak gönderilen .nupkg ham bayttır. Çok bölümlü gövde sonraki öğeleri göz ardı edilir. Dosya adı veya diğer üst bilgilerini çok bölümlü öğelerin göz ardı edilir.

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
201, 202    | Paket başarıyla gönderildi
400         | Belirtilen paket geçersiz
409         | Sağlanan Kimliğini ve sürümünü içeren bir paket zaten var.

Sunucu uygulamaları, bir paketi başarıyla gönderildiğinde döndürülen başarılı durum kodu farklılık gösterir.

## <a name="delete-a-package"></a>Paket silme

nuget.org yorumlar paket silme isteği olarak "listeden" bir. Bu paket hala paketinin mevcut kullanıcılar için kullanılabilir, ancak paket arama sonuçlarını veya web arabirimi artık görünür anlamına gelir. Bu uygulama hakkında daha fazla bilgi için bkz: [silinmiş paketleri](../nuget-org/policies/deleting-packages.md) ilkesi. Bu sinyal bir sabit silme olarak yorumlamak için geçici silme veya listeden kaldırılsın ücretsiz diğer sunucu uygulamalarıdır. Örneğin, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (yalnızca eski V2 API'si destekleyen bir sunucu uygulaması) bir listeden kaldırma veya yapılandırma seçeneğine bağlı göre silmenin olarak bu isteği işleyen destekler.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | evet      | Silmek için paket kimliği
VERSION        | URL    | dize | evet      | Silmek için Paket sürümü
X-NuGet-ApiKey | Üstbilgi | dize | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
204         | Bu paket silindi
404         | İle sağlanan paket yok `ID` ve `VERSION` var.

## <a name="relist-a-package"></a>Bir paketi yeniden listeleme

Bir paket listelenmemiş ise, bu paket "relist" uç nokta kullanarak arama sonuçlarında bir kez daha görünür hale getirmek mümkündür. Bu uç noktaya sahip aynı [Sil (listeden) uç noktası](#delete-a-package) ancak kullanır `POST` HTTP yöntemi yerine `DELETE` yöntemi.

Paket zaten listedeyse, istek yine de başarılı olur.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | evet      | Paket yeniden listelenemedi kimliği
VERSION        | URL    | dize | evet      | Paket yeniden listelenemedi sürümü
X-NuGet-ApiKey | Üstbilgi | dize | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
200         | Paket artık listelenir
404         | İle sağlanan paket yok `ID` ve `VERSION` var.
