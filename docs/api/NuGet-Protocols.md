---
title: nuget.org protokolleri
description: NuGet istemcileri ile etkileşim kurmak için gelişen nuget.org protokoller.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822584"
---
# <a name="nugetorg-protocols"></a>nuget.org protokolleri

Nuget.org ile etkileşim kurmak için istemcileri belirli protokoller izlemeleri gerekir. Bu protokollerin gelişen tutmak için istemcileri belirli nuget.org API'leri çağrılırken kullandıkları Protokolü sürüm tanımlamanız gerekir. Bu değişiklikleri eski istemcileri için bir satır sonu olmayan biçimde tanıtmak nuget.org sağlar.

> [!Note]
> Bu sayfada belgelenen API'leri nuget.org için özeldir ve bu API'leri tanıtmak diğer NuGet sunucu uygulamaları için hiçbir Beklenti yoktur. 

Kapsamlı NuGet ekosistemi uygulanan NuGet API'si hakkında daha fazla bilgi için bkz: [API genel bakış](overview.md).

Bu konu, çeşitli protokoller olarak ve varlığı için ne zaman geldikleri listeler.

## <a name="nuget-protocol-version-410"></a>NuGet Protokolü sürüm 4.1.0'da

4.1.0'da Protokolü paketi nuget.org hesabı karşı doğrulama için nuget.org dışında Hizmetleri ile etkileşim kurmak için doğrulayın kapsam anahtarları kullanımını belirtir. Unutmayın `4.1.0` sürüm numarası donuk bir dizedir ancak bu protokolü desteklenen resmi NuGet istemci ilk sürümü ile çakıştığı için gerçekleşir.

Doğrulama işlemi kullanıcı tarafından oluşturulan API anahtarlar yalnızca nuget.org ile kullanılır ve bu bir doğrulama veya bir üçüncü taraf hizmetinden doğrulama bir kerelik kullanım doğrulayın kapsam anahtarlarıyla gerçekleştirilir sağlar. Bu doğrulama kapsam anahtarları paket nuget.org ağdaki belirli bir kullanıcı (hesap) ait olduğunu doğrulamak için kullanılabilir.

### <a name="client-requirement"></a>İstemci gereksinimi

İstemciler için API çağrıları yaptığınızda aşağıdaki üstbilgi geçirmek için gerekli **itme** nuget.org paketler:

    X-NuGet-Protocol-Version: 4.1.0

Unutmayın `X-NuGet-Client-Version` üstbilgi benzer bir semantik vardır, ancak yalnızca resmi NuGet istemci tarafından kullanılmak üzere ayrılmıştır. Üçüncü taraf istemcileri kullanması gereken `X-NuGet-Protocol-Version` üstbilgiyi ve değeri.

**İtme** protokolün kendini belgelerine açıklanan [ `PackagePublish` kaynak](package-publish-resource.md).

Bir istemci dış hizmetler ve belirli bir kullanıcıya (hesap) bir pakete ait olup olmadığını doğrulamak için gereksinimleri ile etkileşime giren, bunu aşağıdaki protokolünü kullanan ve doğrulama kapsam anahtarları ve nuget.org değil API anahtarlarından kullanmanız gerekir.

### <a name="api-to-request-a-verify-scope-key"></a>Doğrulama kapsam anahtarı istemek için API

Bu API him/her tarafından sahip olunan bir paket doğrulamak bir nuget.org yazar için bir doğrulama kapsam anahtarı almak için kullanılır.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | Evet      | Doğrulama kapsam anahtarı istenen paket identidier
VERSION        | URL    | dize | Yok       | Paket sürümü
X-NuGet-apikey ile yapılan | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Yanıt

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API doğrula kapsam anahtarını doğrulayın

Bu API, nuget.org yazar tarafından sahip olunan paket için bir doğrulama kapsam anahtar doğrulamak için kullanılır.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------  | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | Evet      | Doğrulama kapsam anahtarı istenen paket tanımlayıcısı
VERSION        | URL    | dize | Yok       | Paket sürümü
X-NuGet-apikey ile yapılan | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Bu doğrulama kapsam API anahtarı bir günün süresi dolduğunda veya ilk kullanımda, hangisi daha önce gerçekleşir.

#### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
200         | API anahtarını geçerlidir
403         | API anahtarı geçersiz veya paket karşı göndermek için yetkili değil
404         | Paket başvurduğu `ID` ve `VERSION` (isteğe bağlı) mevcut değil
