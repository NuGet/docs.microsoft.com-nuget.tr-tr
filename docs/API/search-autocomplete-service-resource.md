---
title: Otomatik Tamamlama, NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Arama otomatik tamamlama hizmeti paketi kimlikleri etkileşimli bulma ve sürümleri destekler."
keywords: "NuGet otomatik tamamlama API, NuGet arama paket kimliği, substring paket kimliği"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a>Otomatik Tamamlama

V3 API kullanarak bir paket Kimliğini ve sürümünü otomatik tamamlama deneyim oluşturmak mümkündür. Otomatik Tamamlama sorguları yapmak için kullanılan kaynak `SearchAutocompleteService` kaynak bulunan [Hizmeti dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeğer                          | Notlar
------------------------------------ | -----
SearchAutocompleteService            | İlk sürüm
SearchAutocompleteService/3.0.0-beta | Diğer adı`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Diğer adı`SearchAutocompleteService`

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri. Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.

## <a name="search-for-package-ids"></a>Paket kimlikleri için arama

Bir paket kimliği dizesi bir kısmı için arama ilk otomatik tamamlama API destekler. Bir paketi typeahead özelliği ile bir NuGet paketi kaynağı tümleşik kullanıcı arabiriminde sağlamak istediğinizde mükemmeldir.

Yalnızca listede bulunmayan sürümleri ile bir pakete sonuçlarında görünmez.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
q           | URL    | dize  | Yok       | Paket kimlikleri karşı karşılaştırmak için dize
Atla        | URL    | tamsayı | Yok       | Sayfa numaralandırma için atlamayı sonuç sayısı
Al        | URL    | tamsayı | Yok       | Sayfa numaralandırma için döndürülecek sonuç sayısı
yayın öncesi  | URL    | Boole değeri | Yok       | `true`veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | SemVer 1.0.0 sürüm dizesi 

Otomatik Tamamlama sorgu `q` sunucu uygulaması tarafından tanımlanan bir şekilde ayrıştırılır. nuget.org spliting tarafından üretilen kimliği parçalarıdır paket kimliği belirteçleri önek özgün ortası büyük harf ve sembol karakterlerinin sorgulanırken destekler.

`skip` Parametresi varsayılan ayar: 0.

`take` Parametresi, sıfırdan büyük bir tamsayı olmalıdır. Sunucu uygulaması bir maksimum değer yükleyebilir.

Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.

`semVerLevel` Sorgu parametresi için katılımı için kullanılan [SemVer 2.0.0 paketleri](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Bu sorgu parametresi dışlanırsa, yalnızca paketinin kimlikleri SemVer 1.0.0 uyumlu sürümlerini döndürülür (ile [standart NuGet sürüm](../reference/package-versioning.md) uyarılar 4 tamsayı parçalı sürüm dizeler gibi).
Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 uyumlu paketleri döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

Yanıt kadar içeren JSON belgedir `take` otomatik tamamlama sonuçları.

Kök JSON nesnesi aşağıdaki özelliklere sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
totalHits | tamsayı          | Evet      | Atlayıp eşleşirse, toplam sayısı `skip` ve`take`
veri      | Dize dizisi | Evet      | Paket kimlikleri istek tarafından eşleşti.

### <a name="sample-request"></a>Örnek istek

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

Bir paket kimliği önceki API'yi kullanarak bulununca, istemci API otomatik tamamlama sağlanan paket kimliği için paket sürümlerinin Numaralandırılacak kullanabilir

Listede bulunmayan bir paket sürümü sonuçlarında görünmez.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>İstek parametreleri

Ad        | İçindeki     | Tür    | Gerekli | Notlar
----------- | ------ | ------- | -------- | -----
kimlik          | URL    | dize  | Evet      | Sürümleri için getirmek için paket kimliği
yayın öncesi  | URL    | Boole değeri | Yok       | `true`veya `false` dahil edilip edilmeyeceğini belirlemek [yayın öncesi paketleri](../create-packages/prerelease-packages.md)
semVerLevel | URL    | dize  | Yok       | SemVer 2.0.0 sürüm dizesi 

Varsa `prerelease` olmayan ön sürüm paketlerini hariç tutulan sağlanır.

`semVerLevel` Katılımı SemVer 2.0.0 paketler için sorgu parametresi kullanılır. Bu sorgu parametresi dışlanırsa, yalnızca SemVer 1.0.0 sürümler döndürülür. Varsa `semVerLevel=2.0.0` SemVer 1.0.0 ve SemVer 2.0.0 sürümleri döndürülecek sağlanır. Bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) daha fazla bilgi için.

### <a name="response"></a>Yanıt

Yanıt, verilen sorgu parametreleri tarafından filtreleme sağlanan paket kimliği, tüm paket sürümlerini içeren JSON belgedir.

Kök JSON nesnesi aşağıdaki özelliğine sahiptir:

Ad      | Tür             | Gerekli | Notlar
--------- | ---------------- | -------- | -----
veri      | Dize dizisi | Evet      | İstek tarafından eşleşen paketi sürümleri

Paket sürümlerde `data` dizi SemVer 2.0.0 derleme meta verilerini içerebilir (örneğin `1.0.0+metadata`) varsa `semVerLevel=2.0.0` sorgu dizesinde sağlanan.

### <a name="sample-request"></a>Örnek istek

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
