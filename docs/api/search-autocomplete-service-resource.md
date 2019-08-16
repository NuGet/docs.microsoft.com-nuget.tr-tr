---
title: Otomatik tamamlama, NuGet API 'SI
description: Arama otomatik tamamlama hizmeti, paket kimliklerinin ve sürümlerinin etkileşimli bulmayı destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488299"
---
# <a name="autocomplete"></a>Otomatik Tamamlama

V3 API kullanarak bir paket KIMLIĞI ve sürüm otomatik tamamlama deneyimi oluşturmak mümkündür. Otomatik tamamlama sorguları `SearchAutocompleteService` yapmak için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeeri                          | Notlar
------------------------------------ | -----
SearchAutocompleteService            | İlk yayın
SearchAutocompleteService/3.0.0-Beta | Diğer adı`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Diğer adı`SearchAutocompleteService`

## <a name="base-url"></a>Taban URL 'SI

Aşağıdaki API 'lerin temel URL 'si, belirtilen kaynak `@id` `@type` değerlerinden biriyle ilişkili özelliğin değeridir. Aşağıdaki belgede, yer tutucu temel URL 'si `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'ler http yöntemlerini `GET` ve ' i `HEAD`destekler.

## <a name="search-for-package-ids"></a>Paket kimliklerini ara

İlk otomatik tamamlama API 'SI, bir paket KIMLIĞI dizesinin bir parçası için aramayı destekler. Bu, bir NuGet paket kaynağıyla tümleşik Kullanıcı arabirimine bir paket typeahead özelliği sağlamak istediğinizde idealdir.

Sonuçlarda yalnızca listelenmemiş sürümlerin yer aldığı bir paket görünmez.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | eşleşen       | Paket kimliklerine göre Karşılaştırılacak dize
Atla        | URL    | tamsayı | eşleşen       | Sayfalama için atlanacak sonuç sayısı
take        | URL    | tamsayı | eşleşen       | Sayfalama için döndürülecek sonuç sayısı
sp1'in  | URL    | Boole değeri | eşleşen       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | dize  | eşleşen       | Bir SemVer 1.0.0 sürüm dizesi 

AutoComplete sorgusu `q` , sunucu uygulamasıyla tanımlanan bir şekilde ayrıştırılır. nuget.org, orijinal kamel Case ve symbol karakterleri tarafından oluşturulan KIMLIğIN parçaları olan paket KIMLIĞI belirteçlerinin ön ekinin sorgulanmasını destekler.

`skip` Parametresinin varsayılan değeri 0 ' dır.

`take` Parametre sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulamasında en büyük değer uygulanabilir.

`prerelease` Sağlanmazsa, yayın öncesi paketler hariç tutulur.

Sorgu `semVerLevel` parametresi, [semver 2.0.0 paketlerini](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)kabul etmek için kullanılır.
Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 uyumlu sürümlerine sahip paket kimlikleri döndürülür (4 tamsayı parçalı sürüm dizeleri gibi [Standart NuGet sürüm oluşturma](../concepts/package-versioning.md) uyarıları ile).
`semVerLevel=2.0.0` Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 uyumlu paketler döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Yanıt

Yanıt, `take` otomatik tamamlama sonuçlarını içeren JSON belgesidir.

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
Toplam Isabet sayısı | tamsayı          | evet      | Toplam eşleşme sayısı, ile ilgili `skip` ve`take`
veri      | dizeler dizisi | evet      | İstekle eşleşen paket kimlikleri

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

Bir paket KIMLIĞI önceki API kullanılarak bulunduğunda, istemci, belirtilen paket KIMLIĞI için paket sürümlerini numaralandırmak üzere otomatik tamamlama API 'sini kullanabilir.

Listelenmemiş bir paket sürümü sonuçlarda görünmez.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
kimlik          | URL    | dize  | evet      | İçin sürümlerinin getirileceği paket KIMLIĞI
sp1'in  | URL    | Boole değeri | eşleşen       | `true`veya `false` [yayın öncesi paketlerin](../create-packages/prerelease-packages.md) eklenip eklenmeyeceğini belirleme
semVerLevel | URL    | dize  | eşleşen       | Bir SemVer 2.0.0 sürüm dizesi 

`prerelease` Sağlanmazsa, yayın öncesi paketler hariç tutulur.

Sorgu `semVerLevel` parametresi, semver 2.0.0 paketlerini kabul etmek için kullanılır. Bu sorgu parametresi dışlanmazsa, yalnızca SemVer 1.0.0 sürümleri döndürülür. `semVerLevel=2.0.0` Sağlanmışsa, hem semver 1.0.0 hem de semver 2.0.0 sürümleri döndürülür. Daha fazla bilgi için bkz. [NuGet.org Için Semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Yanıt

Yanıt, sağlanan paket KIMLIĞININ tüm paket sürümlerini içeren, belirtilen Sorgu parametrelerine göre filtreleyerek JSON belgesidir.

Kök JSON nesnesi aşağıdaki özelliğe sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
veri      | dizeler dizisi | evet      | İstekle eşleşen paket sürümleri

`data` Dizideki paket sürümleri, sorgu dizesinde sağlanmışsa, `semVerLevel=2.0.0` semver 2.0.0 derleme meta verileri (ör `1.0.0+metadata`.) içerebilir.

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
