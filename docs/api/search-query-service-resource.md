---
title: Arama, NuGet API
description: Arama hizmeti istemcileri anahtar sözcüğüyle paketler için sorgu ve bazı paket alanları sonuçlarına filtre sağlar.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 76600ee916305ee01ddfb675c83c184e980c5a42
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821089"
---
# <a name="search"></a>Ara

V3 API kullanarak bir paket kaynağındaki paketleri aramak mümkündür. Aramak için kullanılan kaynak `SearchQueryService` kaynak bulunan [Hizmeti dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type Değer                   | Notlar
----------------------------- | -----
SearchQueryService            | İlk sürüm
SearchQueryService/3.0.0-beta | Diğer adı `SearchQueryService`
SearchQueryService/3.0.0-rc   | Diğer adı `SearchQueryService`

## <a name="base-url"></a>Temel URL

Aşağıdaki API için temel URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri. Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.

## <a name="search-for-packages"></a>Paketler için arama

API arama sorgusu istemciye belirtilen arama sorgusuyla eşleşen paketleri için bir sayfa sağlar. Arama sorgusu (örn. arama terimleri belirteçlere) yorumu sunucu uygulaması tarafından belirlenir. ancak genel beklentisi arama sorgusu paket kimliği, başlıklar, açıklamalar ve etiketleri eşleştirmek için kullanılır. Diğer paket meta veri alanlarını da dikkate.

Listede bulunmayan bir paket hiç arama sonuçlarında görüntülenmesi gerekir.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | Yok       | Filtre paketleri için kullanılan için arama terimleri
Atla        | URL    | tamsayı | Yok       | Sayfa numaralandırma için atlamayı sonuç sayısı
Al        | URL    | tamsayı | Yok       | Sayfa numaralandırma için döndürülecek sonuç sayısı
yayın öncesi  | URL    | Boole değeri | Yok       | `true` veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | SemVer 1.0.0 sürüm dizesi 

Arama sorgusu `q` sunucu uygulaması tarafından tanımlanan bir şekilde ayrıştırılır. nuget.org destekleyen temel süzme bir [çeşitli alanları](../consume-packages/finding-and-choosing-packages.md#search-syntax). Öyle değilse `q` tüm paketler, atlama ve alma tarafından uygulanan sınırları içinde döndürülmelidir sağlanır. Bu "Gözat" sekmesinde NuGet Visual Studio deneyimi sağlar.

`skip` Parametresi varsayılan ayar: 0.

`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulaması bir maksimum değer yükleyebilir.

Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.

`semVerLevel` Sorgu parametresi için katılımı için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Bu sorgu parametresi dışlanırsa SemVer 1.0.0 uyumlu sürümlerini yalnızca paketlerle döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar 4 tamsayı parçalı sürüm dizeler gibi).
Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

Yanıt kadar içeren JSON belgedir `take` arama sonuçlarında. Arama sonuçları paket kimliğine göre gruplandırılır.

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
totalHits | tamsayı          | Evet      | Atlayıp eşleşirse, toplam sayısı `skip` ve `take`
veri      | Nesne dizisi | Evet      | İstek tarafından eşleşen arama sonuçları

### <a name="search-result"></a>arama sonucu

Her öğe `data` dizidir aynı paket kimliğini paylaşımı paket sürümlerinin bir grup oluşan bir JSON nesnesi
Nesne, aşağıdaki özelliklere sahiptir:

Ad           | Tür                       | Gerekli | Notlar
-------------- | -------------------------- | -------- | -----
kimlik             | dize                     | Evet      | Eşleşen paket kimliği
sürüm        | dize                     | Evet      | Tam SemVer 2.0.0 sürüm dizesi (derleme meta verilerini içerebilir) paketi
açıklama    | dize                     | Yok       | 
sürümler       | Nesne dizisi           | Evet      | Tüm paket eşleşen sürümlerinin `prerelease` parametresi
yazarları        | dize veya dize dizisi | Yok       | 
iconUrl        | dize                     | Yok       | 
licenseUrl     | dize                     | Yok       | 
Sahipleri         | dize veya dize dizisi | Yok       | 
projectUrl     | dize                     | Yok       | 
kayıt   | dize                     | Yok       | İlişkili için mutlak URL [kayıt dizini](registration-base-url-resource.md#registration-index)
özet        | dize                     | Yok       | 
etiketler           | dize veya dize dizisi | Yok       | 
Başlık          | dize                     | Yok       | 
totalDownloads | tamsayı                    | Yok       | Bu değer yüklemeler toplamına çıkarsanabileceği `versions` dizisi
Doğrulandı       | Boole değeri                    | Yok       | Paket olup olmadığını belirten bir JSON Boole [doğrulandı](../reference/id-prefix-reservation.md)

Nuget.org üzerinde bir doğrulanmış ayrılmış kimliği öneki eşleşen bir paket Kimliğine sahip ve ayrılmış ad 's sahiplerinden biri tarafından sahip olunan bir pakettir. Daha fazla bilgi için bkz: [kimliği öneki ayırma ile ilgili belgeler](../reference/id-prefix-reservation.md).

Son paket sürümünden arama sonuç nesnesinde bulunan meta veriler alınır. Her öğe `versions` dizidir aşağıdaki özelliklere sahip bir JSON nesnesi:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
@id       | dize  | Evet      | İlişkili için mutlak URL [kayıt yaprak](registration-base-url-resource.md#registration-leaf)
sürüm   | dize  | Evet      | Tam SemVer 2.0.0 sürüm dizesi (derleme meta verilerini içerebilir) paketi
Yüklemeleri | tamsayı | Evet      | Bu belirli Paket sürümü için indirme

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [search-result.json](./_data/search-result.json)]
