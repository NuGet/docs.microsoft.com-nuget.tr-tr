---
title: Otomatik tamamlama, NuGet API 'SI
description: Arama otomatik tamamlama hizmeti, paket kimliklerinin ve sürümlerinin etkileşimli bulmayı destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292299"
---
# <a name="autocomplete"></a>Otomatik Tamamlama

V3 API kullanarak bir paket KIMLIĞI ve sürüm otomatik tamamlama deneyimi oluşturmak mümkündür. Otomatik tamamlama sorguları yapmak için kullanılan kaynak, `SearchAutocompleteService` [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeeri                          | Notlar
------------------------------------ | -----
SearchAutocompleteService            | İlk yayın
SearchAutocompleteService/3.0.0-Beta | Diğer adı`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Diğer adı`SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Sorgu parametresi için destek içerir `packageType`

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Bu sürüm `packageType` , sorgu parametresi için destek sunarak yazar tanımlı paket türlerine göre filtrelemeye olanak tanır. Sorgularıyla yapılan sorgularla tamamen geriye doğru uyumludur `SearchAutocompleteService` .

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Lerin temel URL 'SI, `@id` belirtilen kaynak değerlerinden biriyle ilişkili özelliğin değeridir `@type` . Aşağıdaki belgede, yer tutucu temel URL 'SI `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'Ler HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="search-for-package-ids"></a>Paket kimliklerini ara

İlk otomatik tamamlama API 'SI, bir paket KIMLIĞI dizesinin bir parçası için aramayı destekler. Bu, bir NuGet paket kaynağıyla tümleşik Kullanıcı arabirimine bir paket typeahead özelliği sağlamak istediğinizde idealdir.

Sonuçlarda yalnızca listelenmemiş sürümlerin yer aldığı bir paket görünmez.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>İstek parametreleri

Name        | İçinde     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | hayır       | Paket kimliklerine göre Karşılaştırılacak dize
Atla        | URL    | integer | hayır       | Sayfalama için atlanacak sonuç sayısı
almanız        | URL    | integer | hayır       | Sayfalama için döndürülecek sonuç sayısı
sp1'in  | URL    | boole | hayır       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | string  | hayır       | Bir SemVer 1.0.0 sürüm dizesi 
packageType | URL    | string  | hayır       | Paketleri filtrelemek için kullanılacak paket türü (eklenen `SearchAutocompleteService/3.5.0` )

AutoComplete sorgusu, `q` sunucu uygulamasıyla tanımlanan bir şekilde ayrıştırılır. nuget.org, orijinal kamel Case ve symbol karakterleri tarafından oluşturulan KIMLIğIN parçaları olan paket KIMLIĞI belirteçlerinin ön ekinin sorgulanmasını destekler.

`skip`Parametresinin varsayılan değeri 0 ' dır.

`take`Parametre sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulamasında en büyük değer uygulanabilir.

`prerelease`Sağlanmazsa, yayın öncesi paketler hariç tutulur.

`semVerLevel`Sorgu parametresi, [semver 2.0.0 paketlerini](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)kabul etmek için kullanılır.
Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 uyumlu sürümlerine sahip paket kimlikleri döndürülür (4 tamsayı parçalı sürüm dizeleri gibi [Standart NuGet sürüm oluşturma](../concepts/package-versioning.md) uyarıları ile).
`semVerLevel=2.0.0`Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 uyumlu paketler döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Bu `packageType` parametre, otomatik tamamlama sonuçlarını yalnızca paket türü adıyla eşleşen en az bir paket türüne sahip paketlere daha fazla filtrelemek için kullanılır.
Belirtilen paket türü, [paket türü belgesi](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)tarafından tanımlanan geçerli bir paket türü değilse, boş bir sonuç döndürülür.
Belirtilen paket türü boşsa, hiçbir filtre uygulanmaz. Diğer bir deyişle, parametreye hiçbir değer `packageType` geçirilmeyen gibi davranır.

### <a name="response"></a>Yanıt

Yanıt, otomatik tamamlama sonuçlarını içeren JSON belgesidir `take` .

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Name      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
Toplam Isabet sayısı | integer          | evet      | Toplam eşleşme sayısı, ile ilgili `skip` ve`take`
veri      | dize dizisi | evet      | İstekle eşleşen paket kimlikleri

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

Bir paket KIMLIĞI önceki API kullanılarak bulunduğunda, istemci, belirtilen paket KIMLIĞI için paket sürümlerini numaralandırmak üzere otomatik tamamlama API 'sini kullanabilir.

Listelenmemiş bir paket sürümü sonuçlarda görünmez.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Name        | İçinde     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
kimlik          | URL    | string  | evet      | İçin sürümlerinin getirileceği paket KIMLIĞI
sp1'in  | URL    | boole | hayır       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | string  | hayır       | Bir SemVer 2.0.0 sürüm dizesi 

`prerelease`Sağlanmazsa, yayın öncesi paketler hariç tutulur.

`semVerLevel`Sorgu parametresi, SemVer 2.0.0 paketlerini kabul etmek için kullanılır. Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 sürümleri döndürülür. `semVerLevel=2.0.0`Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 sürümleri döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Yanıt

Yanıt, sağlanan paket KIMLIĞININ tüm paket sürümlerini içeren, belirtilen Sorgu parametrelerine göre filtreleyerek JSON belgesidir.

Kök JSON nesnesi aşağıdaki özelliğe sahiptir:

Name      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
veri      | dize dizisi | evet      | İstekle eşleşen paket sürümleri

Dizideki paket sürümleri, `data` `1.0.0+metadata` sorgu dizesinde sağlanmışsa, semver 2.0.0 derleme meta verileri (ör.) içerebilir `semVerLevel=2.0.0` .

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
