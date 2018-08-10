---
title: Depo imzaları, NuGet API'si | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Depo imzaları kaynak istemcilerin kendi depo imzalama özellikleri duyurmaktan paket kaynaklarını sağlar.
keywords: NuGet API'si depo imzaları, sertifikaları, imzalama nuget.org nuget.org paket imzalama
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020573"
---
# <a name="repository-signatures"></a>Depo imzaları

Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür. Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.

Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).

> [!Note]
> NuGet.org Duyurusu başlayacak `RepositorySignatures` yakın gelecekte kaynak.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer                | Notlar
-------------------------- | -----
RepositorySignatures/4.7.0 | İlk yayın

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

Sertifika iptalini (örneğin anahtar güvenliğinin aşılması) söz konusu olduğunda, paket kaynağı etkilenen sertifika tarafından imzalanmış tüm paketleri çekilmeye beklenir. Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.

Aşağıdaki isteği, depo imzaları dizin getirir.

    GET {@id}

Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:

Ad                | Tür             | Gerekli
------------------- | ---------------- | --------
allRepositorySigned | Boole değeri          | Evet
signingCertificates | Nesne dizisi | Evet

`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır. Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.

Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true. Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir. Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
contentUrl   | dize | Evet      | DER ile kodlanmış bir ortak sertifika için mutlak URL
parmak izi | nesne | Evet      |
Konu      | dize | Evet      | Sertifikadan konu ayırt edici ad
yayınlayan       | dize | Evet      | Sertifikayı verenin ayırt edici ad
notBefore    | dize | Evet      | Sertifika geçerlilik döneminin başlangıç zaman damgası
notAfter     | dize | Evet      | Sertifika geçerlilik bitiş zaman damgası

Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir. Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir. 

Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.
Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.

`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:

Ad                   | Tür   | Gerekli | Notlar
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | dize | Evet      | SHA-256'yı parmak izi

Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.

Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
