---
title: nuget.org protokolleri
description: NuGet istemcileriyle etkileşimde bulunmak için gelişen nuget.org protokolleri.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773972"
---
# <a name="nugetorg-protocols"></a>nuget.org protokolleri

Nuget.org ile etkileşim kurmak için istemcilerin belirli protokolleri izlemesi gerekir. Bu protokoller geliştiğinden, istemcilerin belirli nuget.org API 'Lerini çağırırken kullandıkları protokol sürümünü tanımlaması gerekir. Bu, nuget.org 'in eski istemciler için kırılmamış bir şekilde değişiklik almasına olanak tanır.

> [!Note]
> Bu sayfada belgelenen API 'Ler nuget.org 'e özgüdür ve diğer NuGet sunucu uygulamalarının bu API 'Leri tanıtmak için bir beklenmesi yoktur. 

NuGet ekosistemi genelinde uygulanan NuGet API 'si hakkında daha fazla bilgi için bkz. [API 'ye genel bakış](overview.md).

Bu konuda, çeşitli protokoller ve mevcut olduğunda, bu konular listelenmektedir.

## <a name="nuget-protocol-version-410"></a>NuGet protokol sürümü 4.1.0

4.1.0 protokolü, bir paketi nuget.org hesabına karşı doğrulamak için nuget.org dışındaki hizmetlerle etkileşimde bulunmak üzere Verify-Scope anahtarlarının kullanımını belirtir. `4.1.0`Sürüm numarasının donuk bir dize olduğunu, ancak bu protokolü destekleyen resmi NuGet istemcisinin ilk sürümüyle kesişeceğini unutmayın.

Doğrulama, Kullanıcı tarafından oluşturulan API anahtarlarının yalnızca nuget.org ile kullanılmasını ve üçüncü taraf bir hizmetten gelen diğer doğrulamanın veya doğrulamanın tek seferlik Use Verify-Scope anahtarları aracılığıyla işlenmesini sağlar. Bu doğrulama kapsamı anahtarları, paketin nuget.org üzerinde belirli bir kullanıcıya (hesap) ait olduğunu doğrulamak için kullanılabilir.

### <a name="client-requirement"></a>İstemci gereksinimi

İstemciler, paketleri nuget.org 'e **göndermek** için API çağrıları yaparken istemcilerin aşağıdaki üstbilgiyi geçmesi gerekir:

```
X-NuGet-Protocol-Version: 4.1.0
```

`X-NuGet-Client-Version`Üstbilginin benzer anlamolduğuna, ancak yalnızca resmi NuGet istemcisi tarafından kullanılmak üzere ayrıldığını unutmayın. Üçüncü taraf istemcileri, `X-NuGet-Protocol-Version` üstbilgiyi ve değeri kullanmalıdır.

**Gönderme** protokolünün kendisi, [ `PackagePublish` kaynağın](package-publish-resource.md)belgelerinde açıklanmıştır.

Bir istemci dış hizmetlerle etkileşime geçtiğinde ve bir paketin belirli bir kullanıcıya (hesap) ait olup olmadığını doğrulaması gerekiyorsa, aşağıdaki Protokolü kullanmalı ve nuget.org adresinden API anahtarlarını değil Verify-Scope anahtarlarını kullanmalıdır.

### <a name="api-to-request-a-verify-scope-key"></a>Verify-Scope anahtarı istemek için API

Bu API, kendisine ait bir paketi doğrulamak üzere bir nuget.org yazarı için Validate-Scope anahtarını almak için kullanılır.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | evet      | Kapsam anahtarını doğrula için istenen paket identidier
VERSION        | URL    | string | hayır       | Paket sürümü
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Yanıt

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Verify Scope anahtarını doğrulamak için API

Bu API, nuget.org yazarına ait olan paketin doğrulama kapsamı anahtarını doğrulamak için kullanılır.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>İstek parametreleri

Name           | İçinde     | Tür   | Gerekli | Notlar
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | evet      | Kapsam anahtarı doğrulaması istenen paket tanımlayıcısı
VERSION        | URL    | string | hayır       | Paket sürümü
X-NuGet-ApiKey | Üst bilgi | string | evet      | Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Bu kapsam API anahtarının süresi bir günün saati veya ilk kullanımda olduğunda, ne olursa olsun.

#### <a name="response"></a>Yanıt

Durum Kodu | Anlamı
----------- | -------
200         | API anahtarı geçerli
403         | API anahtarı geçersiz veya pakete gönderim yetkisi yok
404         | `ID`Ve `VERSION` (isteğe bağlı) tarafından başvurulan paket yok
