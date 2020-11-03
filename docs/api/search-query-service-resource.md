---
title: Arama, NuGet API 'SI
description: Arama hizmeti, istemcilerin paketleri anahtar sözcüğe göre sorgulamasını ve belirli paket alanlarındaki sonuçları filtrelemesine olanak tanır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 86c9d07cf90b84fffd09b04847d41772dd633b98
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237880"
---
# <a name="search"></a>Arayın

V3 API kullanarak bir paket kaynağında kullanılabilir olan paketleri aramak mümkündür. Arama için kullanılan kaynak, `SearchQueryService` [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type deeri                   | Notlar
----------------------------- | -----
SearchQueryService            | İlk yayın
SearchQueryService/3.0.0-Beta | Diğer adı `SearchQueryService`
SearchQueryService/3.0.0-RC   | Diğer adı `SearchQueryService`
SearchQueryService/3.5.0      | Sorgu parametresi için destek içerir `packageType`

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Bu sürüm `packageType` , sorgu parametresi ve Response özelliği için destek sunarak `packageTypes` Yazar tanımlı paket türlerine göre filtrelemeye olanak tanır. Sorgularıyla yapılan sorgularla tamamen geriye doğru uyumludur `SearchQueryService` .

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'nin temel URL 'SI, `@id` belirtilen kaynak değerlerinden biriyle ilişkili özelliğin değeridir `@type` . Aşağıdaki belgede, yer tutucu temel URL 'SI `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'Ler HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="search-for-packages"></a>Paketleri ara

Arama API 'SI, bir istemcinin belirtilen arama sorgusuyla eşleşen bir paket sayfasını sorgulamasını sağlar. Arama sorgusunun yorumu (örn. arama terimlerinin simgeleştirme) sunucu uygulamasına göre belirlenir, ancak genel beklentide arama sorgusunun, paket kimlikleri, başlıklar, açıklamalar ve Etiketler için kullanılması gerekir. Diğer paket meta verisi alanları da göz önünde bulundurulmayabilir.

Listelenmemiş bir paket, arama sonuçlarında asla görünmemelidir.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>İstek parametreleri

Name        | İçinde     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | hayır       | Paketleri filtrelemek için kullanılacak arama terimleri
Atla        | URL    | tamsayı | hayır       | Sayfalama için atlanacak sonuç sayısı
take        | URL    | tamsayı | hayır       | Sayfalama için döndürülecek sonuç sayısı
sp1'in  | URL    | boolean | hayır       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | string  | hayır       | Bir SemVer 1.0.0 sürüm dizesi 
packageType | URL    | string  | hayır       | Paketleri filtrelemek için kullanılacak paket türü (eklenen `SearchQueryService/3.5.0` )

Arama sorgusu, `q` sunucu uygulamasıyla tanımlanan bir şekilde ayrıştırılır. nuget.org [, çeşitli alanlarda](../consume-packages/finding-and-choosing-packages.md#search-syntax)temel filtrelemeyi destekler. Hayır `q` sağlanmazsa, atla ve Al tarafından uygulanan sınırlar dahilinde tüm paketlerin döndürülmesi gerekir. Bu, NuGet Visual Studio deneyiminde "araştır" sekmesine izin vermez.

`skip`Parametresinin varsayılan değeri 0 ' dır.

`take`Parametre sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulamasında en büyük değer uygulanabilir.

`prerelease`Sağlanmazsa, yayın öncesi paketler hariç tutulur.

`semVerLevel`Sorgu parametresi, [semver 2.0.0 paketlerini](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)kabul etmek için kullanılır.
Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 uyumlu sürümleri olan paketler döndürülür (4 tamsayı parçalı sürüm dizeleri gibi [Standart NuGet sürüm oluşturma](../concepts/package-versioning.md) uyarıları ile).
`semVerLevel=2.0.0`Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 uyumlu paketler döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

`packageType`Parametresi, arama sonuçlarını yalnızca paket türü adıyla eşleşen en az bir paket türüne sahip paketlere daha fazla filtrelemek için kullanılır.
Belirtilen paket türü, [paket türü belgesi](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)tarafından tanımlanan geçerli bir paket türü değilse, boş bir sonuç döndürülür.
Belirtilen paket türü boşsa, hiçbir filtre uygulanmaz. Diğer bir deyişle, packageType parametresine hiçbir değer geçirilmesi parametre geçirilmemişse olduğu gibi davranır.

### <a name="response"></a>Yanıt

Yanıt, arama sonuçlarının bulunduğu JSON belgesidir `take` . Arama sonuçları paket KIMLIĞINE göre gruplandırılır.

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
Toplam Isabet sayısı | tamsayı          | yes      | Toplam eşleşme sayısı, ile ilgili `skip` ve `take`
veriler      | nesne dizisi | yes      | İstekle eşleşen arama sonuçları

### <a name="search-result"></a>Arama sonucu

Dizideki her öğe, `data` aynı paket kimliğini paylaşan bir paket sürümü grubundan oluşan BIR JSON nesnesidir.
Nesnesi aşağıdaki özelliklere sahiptir:

Ad           | Tür                       | Gerekli | Notlar
-------------- | -------------------------- | -------- | -----
kimlik             | string                     | yes      | Eşleşen paketin KIMLIĞI
sürüm        | string                     | yes      | Paketin tam SemVer 2.0.0 sürüm dizesi (derleme meta verileri içerebilir)
açıklama    | string                     | hayır       | 
versions       | nesne dizisi           | yes      | Parametre ile eşleşen paketin tüm sürümleri `prerelease`
düzenliyor        | dizelerin dizesi veya dizisi | hayır       | 
Iurl        | string                     | hayır       | 
licenseUrl     | string                     | hayır       | 
lere         | dizelerin dizesi veya dizisi | hayır       | 
projectUrl     | string                     | hayır       | 
kayıt   | string                     | hayır       | İlişkili [kayıt dizininin](registration-base-url-resource.md#registration-index) mutlak URL 'si
Özet        | string                     | hayır       | 
etiketler           | dizelerin dizesi veya dizisi | hayır       | 
başlık          | string                     | hayır       | 
totalDownloads | tamsayı                    | hayır       | Bu değer dizideki indirmelerin toplamına göre çıkarsanamıyor `versions`
doğrulanamayan       | boolean                    | hayır       | Paketin [doğrulanıp doğrulanmadığını](../nuget-org/id-prefix-reservation.md) gösteren bir JSON Boole değeri
packageTypes   | nesne dizisi           | yes      | Paket yazarı tarafından tanımlanan paket türleri (eklenen `SearchQueryService/3.5.0` )

Nuget.org üzerinde, doğrulanmış bir paket, ayrılmış bir KIMLIK önekiyle eşleşen ve ayrılmış önek sahiplerinin birine sahip olan bir paket KIMLIĞI olan bir pakettir. Daha fazla bilgi için bkz. [kimlik ön eki ayırma hakkındaki belgeler](../nuget-org/id-prefix-reservation.md).

Arama sonucu nesnesinde bulunan meta veriler en son paket sürümünden alınmıştır. Dizideki her öğe, `versions` aşağıdaki özelliklere sahip BIR JSON nesnesidir:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
@id       | string  | yes      | İlişkili [kayıt yaprağın](registration-base-url-resource.md#registration-leaf) mutlak URL 'si
sürüm   | string  | yes      | Paketin tam SemVer 2.0.0 sürüm dizesi (derleme meta verileri içerebilir)
indirmeler | tamsayı | yes      | Bu belirli paket sürümü için karşıdan yüklemelerin sayısı

`packageTypes`Dizi, her zaman en az bir (1) öğeden oluşur. Belirli bir paket KIMLIĞI için paket türü, diğer arama parametrelerine göre paketin en son sürümü tarafından tanımlanan paket türleri olarak kabul edilir. Dizideki her öğe, `packageTypes` aşağıdaki özelliklere sahip BIR JSON nesnesidir:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
name      | string  | yes      | Paket türünün adı.

### <a name="sample-request"></a>Örnek istek

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [search-result.json](./_data/search-result.json)]