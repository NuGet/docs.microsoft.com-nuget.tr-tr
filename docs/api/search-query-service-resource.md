---
title: Arama, NuGet API 'SI
description: Arama hizmeti, istemcilerin paketleri anahtar sözcüğe göre sorgulamasını ve belirli paket alanlarındaki sonuçları filtrelemesine olanak tanır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b898b389ee6c962831ce789a7c304c75e6bd8774
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488210"
---
# <a name="search"></a>Ara

V3 API kullanarak bir paket kaynağında kullanılabilir olan paketleri aramak mümkündür. Arama `SearchQueryService` için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeeri                   | Notlar
----------------------------- | -----
SearchQueryService            | İlk yayın
SearchQueryService/3.0.0-Beta | Diğer adı`SearchQueryService`
SearchQueryService/3.0.0-RC   | Diğer adı`SearchQueryService`

## <a name="base-url"></a>Taban URL 'SI

Aşağıdaki API 'nin temel URL 'si, belirtilen kaynak `@id` `@type` değerlerinden biriyle ilişkili özelliğin değeridir. Aşağıdaki belgede, yer tutucu temel URL 'si `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'ler http yöntemlerini `GET` ve ' i `HEAD`destekler.

## <a name="search-for-packages"></a>Paketleri ara

Arama API 'SI, bir istemcinin belirtilen arama sorgusuyla eşleşen bir paket sayfasını sorgulamasını sağlar. Arama sorgusunun yorumu (örn. arama terimlerinin simgeleştirme) sunucu uygulamasına göre belirlenir, ancak genel beklentide arama sorgusunun, paket kimlikleri, başlıklar, açıklamalar ve Etiketler için kullanılması gerekir. Diğer paket meta verisi alanları da göz önünde bulundurulmayabilir.

Listelenmemiş bir paket, arama sonuçlarında asla görünmemelidir.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | eşleşen       | Paketleri filtrelemek için kullanılacak arama terimleri
Atla        | URL    | tamsayı | eşleşen       | Sayfalama için atlanacak sonuç sayısı
take        | URL    | tamsayı | eşleşen       | Sayfalama için döndürülecek sonuç sayısı
sp1'in  | URL    | Boole değeri | eşleşen       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | dize  | eşleşen       | Bir SemVer 1.0.0 sürüm dizesi 

Arama sorgusu `q` , sunucu uygulamasıyla tanımlanan bir şekilde ayrıştırılır. nuget.org [, çeşitli alanlarda](../consume-packages/finding-and-choosing-packages.md#search-syntax)temel filtrelemeyi destekler. Hayır `q` sağlanmazsa, atla ve Al tarafından uygulanan sınırlar dahilinde tüm paketlerin döndürülmesi gerekir. Bu, NuGet Visual Studio deneyiminde "araştır" sekmesine izin vermez.

`skip` Parametresinin varsayılan değeri 0 ' dır.

`take` Parametre sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulamasında en büyük değer uygulanabilir.

`prerelease` Sağlanmazsa, yayın öncesi paketler hariç tutulur.

Sorgu `semVerLevel` parametresi, [semver 2.0.0 paketlerini](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)kabul etmek için kullanılır.
Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 uyumlu sürümleri olan paketler döndürülür (4 tamsayı parçalı sürüm dizeleri gibi [Standart NuGet sürüm oluşturma](../concepts/package-versioning.md) uyarıları ile).
`semVerLevel=2.0.0` Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 uyumlu paketler döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Yanıt

Yanıt, `take` arama sonuçlarının bulunduğu JSON belgesidir. Arama sonuçları paket KIMLIĞINE göre gruplandırılır.

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
Toplam Isabet sayısı | tamsayı          | evet      | Toplam eşleşme sayısı, ile ilgili `skip` ve`take`
veri      | nesne dizisi | evet      | İstekle eşleşen arama sonuçları

### <a name="search-result"></a>Arama sonucu

`data` Dizideki her öğe, aynı paket kimliğini paylaşan bir paket sürümü grubundan oluşan bir JSON nesnesidir.
Nesnesi aşağıdaki özelliklere sahiptir:

Ad           | Tür                       | Gerekli | Notlar
-------------- | -------------------------- | -------- | -----
kimlik             | dize                     | evet      | Eşleşen paketin KIMLIĞI
sürüm        | dize                     | evet      | Paketin tam SemVer 2.0.0 sürüm dizesi (derleme meta verileri içerebilir)
açıklama    | dize                     | eşleşen       | 
sürümler       | nesne dizisi           | evet      | `prerelease` Parametre ile eşleşen paketin tüm sürümleri
düzenliyor        | dizelerin dizesi veya dizisi | eşleşen       | 
Iurl        | dize                     | eşleşen       | 
licenseUrl     | dize                     | eşleşen       | 
lere         | dizelerin dizesi veya dizisi | eşleşen       | 
projectUrl     | dize                     | eşleşen       | 
kayıt   | dize                     | eşleşen       | İlişkili [kayıt dizininin](registration-base-url-resource.md#registration-index) mutlak URL 'si
özet        | dize                     | eşleşen       | 
etiketler           | dizelerin dizesi veya dizisi | eşleşen       | 
title          | dize                     | eşleşen       | 
totalDownloads | tamsayı                    | eşleşen       | Bu değer `versions` dizideki indirmelerin toplamına göre çıkarsanamıyor
doğrulanamayan       | Boole değeri                    | eşleşen       | Paketin [doğrulanıp doğrulanmadığını](../nuget-org/id-prefix-reservation.md) gösteren bir JSON Boole değeri

Nuget.org üzerinde, doğrulanmış bir paket, ayrılmış bir KIMLIK önekiyle eşleşen ve ayrılmış önek sahiplerinin birine sahip olan bir paket KIMLIĞI olan bir pakettir. Daha fazla bilgi için bkz. [kimlik ön eki ayırma hakkındaki belgeler](../reference/id-prefix-reservation.md).

Arama sonucu nesnesinde bulunan meta veriler en son paket sürümünden alınmıştır. `versions` Dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
@id       | dize  | evet      | İlişkili [kayıt yaprağın](registration-base-url-resource.md#registration-leaf) mutlak URL 'si
sürüm   | dize  | evet      | Paketin tam SemVer 2.0.0 sürüm dizesi (derleme meta verileri içerebilir)
dosyaların | tamsayı | evet      | Bu belirli paket sürümü için karşıdan yüklemelerin sayısı

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [search-result.json](./_data/search-result.json)]
