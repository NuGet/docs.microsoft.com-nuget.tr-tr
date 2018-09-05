---
title: nuget.org protokolleri
description: NuGet istemcileri ile etkileşim kurmak için gelişen nuget.org protokolleri.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547279"
---
# <a name="nugetorg-protocols"></a>nuget.org protokolleri

Nuget.org ile etkileşim kurmak için istemcileri belirli protokoller izlemeniz gerekir. Bu protokollerin gelişen tutmak olduğundan, istemcileri belirli nuget.org API'leri çağırırken kullandıkları protokol sürümü tanımlamanız gerekir. Bu değişiklikler, eski istemciler için bir hataya neden olmayan şekilde tanıtmak nuget.org sağlar.

> [!Note]
> Bu sayfada belgelenen API'leri nuget.org için özeldir ve bu API'leri tanıtmak diğer NuGet sunucu uygulamaları için hiçbir beklentisi yoktur. 

Genel olarak NuGet ekosisteminde uygulanan NuGet API'si hakkında daha fazla bilgi için bkz [API'sine genel bakış](overview.md).

Bu konu, çeşitli protokoller olarak ve varlığı için ne zaman geldikleri listeler.

## <a name="nuget-protocol-version-410"></a>NuGet Protokolü sürüm 4.1.0

4.1.0 protokolü paketi nuget.org hesabına karşı doğrulamak için nuget.org dışındaki hizmetlerle etkileşim için doğrulama kapsamı anahtarları kullanımını belirtir. Unutmayın `4.1.0` sürüm numarası genel olmayan bir dizedir, ancak ilk sürümü bu protokolü desteklenen resmi bir NuGet istemcisi ile çakıştığı için gerçekleşir.

Nuget.org ile yalnızca kullanıcı tarafından oluşturulan API anahtarları kullanılır ve bu bir doğrulama veya bir üçüncü taraf hizmetinden doğrulama tek seferlik kullanım doğrulama kapsamı anahtarlar aracılığıyla işlenir doğrulama sağlar. Bu doğrulama kapsamı anahtarları paket nuget.org üzerindeki belirli bir kullanıcı (hesap) ait olduğunu doğrulamak için kullanılabilir.

### <a name="client-requirement"></a>İstemci gereksinimi

İstemciler bir API çağrısına zaman aşağıdaki üst bilgi geçirmek için gerekli **anında iletme** nuget.org paketler:

    X-NuGet-Protocol-Version: 4.1.0

Unutmayın `X-NuGet-Client-Version` üstbilgisi, benzer semantiğe sahip ancak yalnızca resmi bir NuGet istemcisi tarafından kullanılmak üzere ayrılmıştır. Üçüncü taraf istemcileri kullanması gereken `X-NuGet-Protocol-Version` üstbilgiyi ve değeri.

**Anında iletme** protokolün kendisini belgelerinde açıklanmıştır [ `PackagePublish` kaynak](package-publish-resource.md).

Dış hizmetler ve gereksinimlerini bir paket (hesap) belirli bir kullanıcıya ait olup olmadığını doğrulamak için bir istemci etkileşimde gerekirse, aşağıdaki protokolünü kullanan ve doğrulama kapsamı anahtarları ve nuget.org değil API anahtarlarını kullanın.

### <a name="api-to-request-a-verify-scope-key"></a>API doğrulama kapsamı anahtar istemek için

Bu API, bir nuget.org Yazar him/her tarafından sahip olunan bir paket doğrulamak için bir kapsam doğrulama anahtarını almak için kullanılır.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | Evet      | Doğrulama kapsamı anahtar istendiği paket identidier
VERSION        | URL    | dize | Yok       | Paket sürümü
X-NuGet-ApiKey | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Yanıt

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API doğrulama kapsamı anahtar doğrulamak için

Bu API, nuget.org yazarı tarafından sahip olunan bir paket için bir doğrulama kapsamı anahtar doğrulamak için kullanılır.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>İstek parametreleri

Ad           | İçindeki     | Tür   | Gerekli | Notlar
-------------  | ------ | ------ | -------- | -----
Kimlik             | URL    | dize | Evet      | Doğrulama kapsamı anahtar istendiği paket tanımlayıcısı
VERSION        | URL    | dize | Yok       | Paket sürümü
X-NuGet-ApiKey | Üstbilgi | dize | Evet      | Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Bu doğrulama kapsamı API anahtarı bir günün süresi veya ilk kez kullanıldığında, hangisi önce gerçekleşirse.

#### <a name="response"></a>Yanıt

Durum kodu | Açıklama
----------- | -------
200         | API anahtarı geçerlidir
403         | API anahtarı geçersiz veya karşı paket göndermek için yetkili değil
404         | Tarafından paket adlandırılan `ID` ve `VERSION` (isteğe bağlı) yok
