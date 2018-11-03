---
title: Arama, NuGet API'si
description: İstemciler, anahtar sözcüğe göre paketler için sorgu ve belirli bir paket alanlara sonuçları filtrelemek için arama hizmeti sağlar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: cfcb52ba7689f1b392c782b4ad42ba820a76c8bf
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981138"
---
# <a name="search"></a>Ara

Bir paket kaynağı V3 API'sini kullanarak kullanılabilir paketleri aramak mümkündür. Aramak için kullanılan kaynak `SearchQueryService` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type Değer                   | Notlar
----------------------------- | -----
SearchQueryService            | İlk yayın
SearchQueryService/3.0.0-beta | Diğer adı `SearchQueryService`
SearchQueryService/3.0.0-rc   | Diğer adı `SearchQueryService`

## <a name="base-url"></a>Temel URL

Aşağıdaki API için temel URL değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri. Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="search-for-packages"></a>Paketleri Ara

Arama API'si, sorgu için bir istemci için paketlerin belirli bir arama sorgusuyla eşleşen bir sayfa sağlar. Arama sorgusu (örneğin arama terimlerini simgeleştirme) yorumu sunucu uygulaması tarafından belirlenir, ancak genel beklenir arama sorgusu paket kimlikleri, başlıklarını, açıklamaları ve etiketleri eşleştirmek için kullanılır. Diğer paket meta veri alanlarını da olarak kabul edilebilir.

Listede bulunmayan bir paket, hiçbir zaman arama sonuçlarında görüntülenmesi gerekir.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | Yok       | Filtre paketleri için kullanılan arama koşulları
Atla        | URL    | tamsayı | Yok       | İçin sayfalandırma atlanacak sonuç sayısı
sınav zamanı        | URL    | tamsayı | Yok       | Sayfalandırma için döndürülecek sonuç sayısı
yayın öncesi  | URL    | Boole değeri | Yok       | `true` veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | Bir SemVer 1.0.0 sürüm dizesi 

Arama sorgusu `q` sunucu uygulama tarafından tanımlanan bir şekilde ayrıştırılır. nuget.org üzerindeki temel filtreleme destekleyen bir [çeşitli alanları](../consume-packages/finding-and-choosing-packages.md#search-syntax). Hayır ise `q` tüm paketleri skip ve take tarafından uygulanan sınırları içinde döndürülmelidir sağlanır. Bu "Gözatma türü" sekmesinde NuGet Visual Studio deneyimi sağlar.

`skip` 0 varsayılan parametre değeri.

`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulaması, maksimum değer yükleyebilir.

Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.

`semVerLevel` Sorgu parametresi için katılım için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Bu sorgu parametresi dışlanırsa SemVer 1.0.0 uyumlu sürümler yalnızca paketlerle döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar, 4 tamsayı parçalı sürüm dizeleri gibi).
Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

En fazla içeren JSON belgesi yanıttır `take` arama sonuçları. Arama sonuçları paket kimliğine göre gruplandırılır.

Kök JSON nesnesinin aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
totalHits | tamsayı          | Evet      | Toplam sayısı atlayıp bir eşleşme `skip` ve `take`
veri      | Nesne dizisi | Evet      | İstek tarafından eşleştirilen arama sonuçları

### <a name="search-result"></a>Arama sonucu

Her öğe `data` dizidir paket sürümleri aynı paket kimliğini paylaşımı birtakım oluşan bir JSON nesnesi
Nesne, aşağıdaki özelliklere sahiptir:

Ad           | Tür                       | Gerekli | Notlar
-------------- | -------------------------- | -------- | -----
kimlik             | dize                     | Evet      | Eşleşen bir paket kimliği
sürüm        | dize                     | Evet      | (Derleme meta verilerini içerebilir) paketin tam SemVer 2.0.0 sürümü dizesi
açıklama    | dize                     | Yok       | 
sürümler       | Nesne dizisi           | Evet      | Eşleşen paket sürümlerini tüm `prerelease` parametresi
Yazarları        | dize veya dize dizisi | Yok       | 
IconUrl        | dize                     | Yok       | 
LicenseUrl     | dize                     | Yok       | 
Sahipleri         | dize veya dize dizisi | Yok       | 
ProjectUrl     | dize                     | Yok       | 
kayıt   | dize                     | Yok       | İlişkili için mutlak URL [kayıt dizini](registration-base-url-resource.md#registration-index)
özet        | dize                     | Yok       | 
etiketler           | dize veya dize dizisi | Yok       | 
Başlık          | dize                     | Yok       | 
totalDownloads | tamsayı                    | Yok       | Bu değer yüklemeler toplamına göre çıkarılan `versions` dizi
doğrulandı       | Boole değeri                    | Yok       | Paket olup olmadığını belirten bir JSON boolean [doğrulandı](../reference/id-prefix-reservation.md)

Nuget.org bir doğrulanmış ayrılmış bir kimliği öneki eşleşen bir paket Kimliğine sahip ve ayrılmış önek 's sahiplerinden biri tarafından sahip olunan bir pakettir. Daha fazla bilgi için [kimlik ön eki ayırma hakkında belgeler](../reference/id-prefix-reservation.md).

Arama sonuç nesnesinde bulunan meta veriler en son Paket sürümü alınır. Her öğe `versions` aşağıdaki özelliklere sahip bir JSON nesnesi dizisidir:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
@id       | dize  | Evet      | İlişkili için mutlak URL [kayıt yaprak](registration-base-url-resource.md#registration-leaf)
sürüm   | dize  | Evet      | (Derleme meta verilerini içerebilir) paketin tam SemVer 2.0.0 sürümü dizesi
İndirmeler | tamsayı | Evet      | Bu belirli bir paket sürümü için indirme sayısı

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [search-result.json](./_data/search-result.json)]
