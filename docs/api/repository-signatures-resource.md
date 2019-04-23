---
title: Depo imzaları, NuGet API'si | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Depo imzaları kaynak istemcilerin kendi depo imzalama özellikleri duyurmaktan paket kaynaklarını sağlar.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931858"
---
# <a name="repository-signatures"></a>Depo imzaları

Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür. Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.

Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer                | Notlar
-------------------------- | -----
RepositorySignatures/4.7.0 | İlk yayın
RepositorySignatures/4.9.0 | NuGet v4.9 + istemcileri tarafından desteklenen
RepositorySignatures/5.0.0 | Çalışabilmelerini `allRepositorySigned`. NuGet v5.0 + istemcileri tarafından desteklenen

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri. Bu konu başlığı altında yer tutucu URL'yi `{@id}`.

Diğer kaynaklarının aksine unutmayın `{@id}` HTTPS üzerinden hizmet URL'si gereklidir.

## <a name="http-methods"></a>HTTP yöntemleri

Depo imzaları kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="repository-signatures-index"></a>Depo imzaları dizini

Depo imzaları dizin iki bilgi parçasını içerir:

1. Bu paket kaynak tarafından atılan bir depo olan alınıp alınmayacağını tüm paketleri kaynak bulunamadı.
1. Paketleri imzalamak için paket kaynağı tarafından kullanılan sertifikalar listesi.

Çoğu durumda, sertifikaların listesini her zaman sadece eklenir. Önceki imzalama sertifikasının süresi doldu ve yeni bir imzalama sertifikası kullanmaya başlamak paket kaynağı gerektiğinde yeni sertifikalar listesine eklenir. Listeden bir sertifika kaldırılırsa, kaldırılan imzalama sertifikası ile oluşturulan tüm paket imzaları artık istemci tarafından geçerli kabul edilmesi, anlamına gelir. Bu durumda, paket imzası (ancak mutlaka paket) geçersiz. Paketin imzasız olarak yüklemeden istemci ilkesini izin verebilir.

(Örneğin anahtar güvenliğinin aşılması) sertifika iptal olması durumunda, etkilenen bir sertifika tarafından imzalanmış tüm paketleri yeniden imzalamak için paket kaynağı bekleniyor. Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.

Aşağıdaki isteği, depo imzaları dizin getirir.

    GET {@id}

Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:

Ad                | Tür             | Gerekli | Notlar
------------------- | ---------------- | -------- | -----
allRepositorySigned | Boole değeri          | evet      | Olmalıdır `false` 4.7.0 ve 4.9.0 kaynaklar
signingCertificates | Nesne dizisi | evet      | 

`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır. Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.

> [!Warning]
> `allRepositorySigned` Boole 4.7.0 ve 4.9.0 kaynaklar üzerinde false olmalıdır. NuGet v4.7 v4.8 ve v4.9 istemcileri olan kaynaklardan paketleri yükleyemiyor `allRepositorySigned` true olarak ayarlanmış.

Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true. Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir. Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
contentUrl   | dize | evet      | DER ile kodlanmış bir ortak sertifika için mutlak URL
parmak izi | nesne | evet      |
Konu      | dize | evet      | Sertifikadan konu ayırt edici ad
yayınlayan       | dize | evet      | Sertifikayı verenin ayırt edici ad
notBefore    | dize | evet      | Sertifika geçerlilik döneminin başlangıç zaman damgası
notAfter     | dize | evet      | Sertifika geçerlilik bitiş zaman damgası

Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir. Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir. 

Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.
Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.

`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:

Ad                   | Tür   | Gerekli | Notlar
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | dize | evet      | SHA-256'yı parmak izi

Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.

Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
