---
title: Otomatik Tamamlama, NuGet API'si
description: Arama otomatik tamamlama hizmeti etkileşimli olarak paket kimlikleri bulunmasını ve sürümleri destekler.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324766"
---
# <a name="autocomplete"></a>Otomatik Tamamlama

V3 API'sini kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyimi oluşturmak mümkündür. Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type Değer                          | Notlar
------------------------------------ | -----
SearchAutocompleteService            | İlk yayın
SearchAutocompleteService/3.0.0-beta | Diğer adı `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Diğer adı `SearchAutocompleteService`

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri. Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="search-for-package-ids"></a>Paket kimlikleri için arama

Bir paket kimliği dizesi bir parçası için arama ilk otomatik tamamlama API'sini destekler. NuGet paket kaynağı ile tümleşik kullanıcı arabiriminde bir paket typeahead özelliği sağlamak istediğinizde mükemmeldir.

Yalnızca listede bulunmayan sürümler ile bir pakete sonuçlarında görünmez.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | Yok       | Paket kimlikleri karşı Karşılaştırılacak dize
Atla        | URL    | tamsayı | Yok       | İçin sayfalandırma atlanacak sonuç sayısı
sınav zamanı        | URL    | tamsayı | Yok       | Sayfalandırma için döndürülecek sonuç sayısı
yayın öncesi  | URL    | Boole değeri | Yok       | `true` veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | Bir SemVer 1.0.0 sürüm dizesi 

Otomatik Tamamlama sorgu `q` sunucu uygulama tarafından tanımlanan bir şekilde ayrıştırılır. nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri öneki özgün camel çalışması ve sembol karakterlerinin sorgulama destekler.

`skip` 0 varsayılan parametre değeri.

`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulaması, maksimum değer yükleyebilir.

Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.

`semVerLevel` Sorgu parametresi için katılım için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Bu sorgu parametresi dışlanırsa, yalnızca paket kimlikleri SemVer 1.0.0 uyumlu sürümler ile döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar, 4 tamsayı parçalı sürüm dizeleri gibi).
Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

En fazla içeren JSON belgesi yanıttır `take` otomatik tamamlama sonuçları.

Kök JSON nesnesinin aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
totalHits | tamsayı          | evet      | Toplam sayısı atlayıp bir eşleşme `skip` ve `take`
veri      | dize dizisi | evet      | ' % S'paketi istek tarafından eşleştirilen kimlikleri

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

Önceki API'sini kullanarak bir paket kimliği bulununca istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerini Numaralandırılacak kullanabilir

Listede bulunmayan bir paket sürümüne sonuçlarında görünmez.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
kimlik          | URL    | dize  | evet      | Sürümleri için getirmek için paket kimliği
yayın öncesi  | URL    | Boole değeri | Yok       | `true` veya `false` dahil edilip edilmeyeceğini belirleme [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | Bir SemVer 2.0.0 sürümü dizesi 

Varsa `prerelease` değil yayın öncesi paketleri dışlanmaz sağlanır.

`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır. Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür. Varsa `semVerLevel=2.0.0` SemVer 1.0.0 hem SemVer 2.0.0 sürümlerinin döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

Yanıt, filtreleme verilen sorgu parametreleri tarafından sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgesidir.

Kök JSON nesnesinin aşağıdaki özellik vardır:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
veri      | dize dizisi | evet      | İstek tarafından eşleşen paket sürümleri

Paket sürümlerinde `data` dizi SemVer 2.0.0 derleme meta verileri içeren (örn `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
