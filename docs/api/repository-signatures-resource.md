---
title: Depo Imzaları, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Depo imzaları kaynağı, istemci paket kaynaklarının depo imzalama yeteneklerini duyurmasını sağlar.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775329"
---
# <a name="repository-signatures"></a>Depo imzaları

Bir paket kaynağı yayımlanan paketlere depo imzaları eklemeyi destekliyorsa, istemci, paket kaynağı tarafından kullanılan imzalama sertifikalarını tespit etmek mümkündür. Bu kaynak, istemcilerin depo imzalı bir paketin değiştirilmediğini veya beklenmedik bir imzalama sertifikasına sahip olup olmadığını algılamasını sağlar.

Bu depo imza bilgilerini getirmek için kullanılan kaynak, `RepositorySignatures` [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@type deeri                | Notlar
-------------------------- | -----
Imza/4.7.0 | İlk yayın
Imza/4.9.0 | NuGet v 4.9 + istemcileri tarafından desteklenir
Imza/5.0.0 | Etkinleştirmeye izin verir `allRepositorySigned` . NuGet v 5.0 + istemcileri tarafından desteklenir

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Ler için giriş noktası URL 'SI, `@id` belirtilen kaynak değeriyle ilişkili özelliğin değeridir `@type` . Bu konu, yer tutucu URL 'sini kullanır `{@id}` .

Diğer kaynakların aksine, `{@id}` URL 'nın https üzerinden sunulması gerektiğini unutmayın.

## <a name="http-methods"></a>HTTP yöntemleri

Depo imzaları kaynağında bulunan tüm URL 'Ler yalnızca HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="repository-signatures-index"></a>Depo imzaları dizini

Depo imzaları dizini iki parça bilgi içerir:

1. Kaynakta bulunan tüm paketlerin, bu paket kaynağı tarafından imzalanmış depo olup olmadığı.
1. Paket kaynağı tarafından paketleri imzalamak için kullanılan sertifikaların listesi.

Çoğu durumda, sertifika listesi yalnızca öğesine eklenir. Önceki imza sertifikasının süresi dolduğunda ve paket kaynağının yeni bir imzalama sertifikası kullanmaya başlaması gerektiğinde listeye yeni sertifikalar eklenecektir. Bir sertifika listeden kaldırılırsa, bu, kaldırılan imzalama sertifikasıyla oluşturulan tüm paket imzalarının artık istemci tarafından geçerli kabul edilmeyeceği anlamına gelir. Bu durumda, paket imzası (ancak paket olması gerekmez) geçersiz olur. İstemci ilkesi, paketin imzasız olarak yüklenmesine izin verebilir.

Sertifika iptali durumunda (örn. Anahtar Uzlaşması), paket kaynağının etkilenen sertifika tarafından imzalanan tüm paketlerin yeniden imzalanması beklenir. Ayrıca, paket kaynağının etkilenen sertifikayı imzalama sertifikası listesinden kaldırması gerekir.

Aşağıdaki istek depo imzaları dizinini getirir.

```
GET {@id}
```

Depo imza dizini, aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesidir:

Ad                | Tür             | Gerekli | Notlar
------------------- | ---------------- | -------- | -----
Alldepotorsigned | boolean          | evet      | `false`4.7.0 ve 4.9.0 kaynaklarında olmalıdır
signingCertificates | nesne dizisi | evet      | 

`allRepositorySigned`Paket kaynağında depo imzası olmayan bazı paketler varsa, Boole değeri false olarak ayarlanır. Boole değeri true olarak ayarlanırsa, kaynakta bulunan tüm paketlerin, içinde bahsedilen imzalama sertifikalarından biri tarafından üretilmiş bir depo imzası olması gerekir `signingCertificates` .

> [!Warning]
> `allRepositorySigned`4.7.0 ve 4.9.0 kaynaklarında Boole değeri false olmalıdır. NuGet v 4.7, v 4.8 ve v 4.9 istemcileri, `allRepositorySigned` doğru olarak ayarlanmış kaynaklardan paket yükleyemez.

`signingCertificates`Boole değeri true olarak ayarlandıysa dizide bir veya daha fazla imzalama sertifikası olması gerekir `allRepositorySigned` . Dizi boşsa ve `allRepositorySigned` true olarak ayarlanırsa, bir istemci ilkesi paketlerin tüketimine izin verebilir olmasına rağmen kaynaktaki tüm paketlerin geçersiz kabul edilmesi gerekir. Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
contentUrl   | string | evet      | DER kodlu ortak sertifikaya yönelik mutlak URL
parmak izlerini | object | evet      |
subject      | string | evet      | Sertifikadan konu ayırt edici adı
yayınlayan       | string | evet      | Sertifikanın verenin ayırt edici adı
notBefore    | string | evet      | Sertifikanın geçerlilik döneminin başlangıç zaman damgası
notAfter     | string | evet      | Sertifikanın geçerlilik döneminin bitiş zaman damgası

`contentUrl`Https üzerinden sunulması gerektiğini unutmayın. Bu URL 'nin belirli bir URL kalıbı yok ve bu depo imzaları Dizin belgesi kullanılarak dinamik olarak bulunması gerekir. 

Bu nesnedeki tüm özelliklerin (bir kenara `contentUrl` ), konumunda bulunan sertifikadan alınabilir olması gerekir `contentUrl` .
Bu derikaydedilebilir özellikler, gidiş dönüşlerin en aza indirilmesine yönelik kolaylık olarak sağlanır.

`fingerprints`Nesnesi aşağıdaki özelliklere sahiptir:

Ad                   | Tür   | Gerekli | Notlar
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | evet      | SHA-256 parmak izi

Anahtar adı, `2.16.840.1.101.3.4.2.1` SHA-256 karma ALGORITMASıNıN OID 'dir.

Tüm karma değerleri, karma özetinin küçük, onaltılı kodlanmış dize temsilleri olmalıdır.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
