---
title: Paket meta verileri, NuGet API 'SI
description: Paket kayıt taban URL 'SI, paketlerle ilgili meta verilerin getirilmesi için izin verir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237529"
---
# <a name="package-metadata"></a>Paket meta verileri

NuGet v3 API kullanarak bir paket kaynağında bulunan paketlerle ilgili meta verileri getirmek mümkündür. Bu meta veriler, `RegistrationsBaseUrl` [hizmet dizininde](service-index.md)bulunan kaynak kullanılarak getirilebilir.

Altında bulunan belgelerin koleksiyonu, `RegistrationsBaseUrl` genellikle "kayıtlar" veya "kayıt Blobları" olarak adlandırılır. Tek tek altındaki belge kümesi, `RegistrationsBaseUrl` "kayıt Hive" olarak adlandırılır. Kayıt Hive bir paket kaynağında bulunan her pakete ilişkin tüm meta verileri içerir.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type deeri                     | Notlar
------------------------------- | -----
RegistrationsBaseUrl            | İlk yayın
RegistrationsBaseUrl/3.0.0-Beta | Diğer adı `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Diğer adı `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gdaraltılmış yanıtlar
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 paketlerini içerir

Bu, çeşitli istemci sürümleri için kullanılabilen üç farklı kayıt kovanlarını temsil eder.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Bu kayıtlar sıkıştırılmaz (örtük olarak kullandıkları anlamına gelir `Content-Encoding: identity` ). SemVer 2.0.0 paketleri bu Hive **dışında tutulur** .

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Bu kayıtlar kullanılarak sıkıştırılır `Content-Encoding: gzip` . SemVer 2.0.0 paketleri bu Hive **dışında tutulur** .

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Bu kayıtlar kullanılarak sıkıştırılır `Content-Encoding: gzip` . SemVer 2.0.0 paketleri bu kovana **dahildir** .
SemVer 2.0.0 hakkında daha fazla bilgi için bkz. [NuGet.org Için semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Lerin temel URL 'SI, `@id` belirtilen kaynak değerleriyle ilişkili özelliğin değeridir `@type` . Aşağıdaki belgede, yer tutucu temel URL 'SI `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'Ler HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="registration-index"></a>Kayıt dizini

Kayıt kaynağı paket meta verilerini paket KIMLIĞIYLE gruplandırır. Aynı anda birden fazla paket KIMLIĞI hakkında veri almak mümkün değildir. Bu kaynak paket kimliklerini bulmayı sağlayan bir yol sağlar. Bunun yerine, istemcinin istenen paket KIMLIĞINI zaten öğrenmiş olduğu varsayılır. Her paket sürümü hakkında kullanılabilir meta veriler sunucu uygulamasına göre değişir. Paket kayıt Blobları aşağıdaki hiyerarşik yapıya sahiptir:

- **Dizin** : aynı paket kimliğine sahip bir kaynaktaki tüm paketler tarafından paylaşılan paket meta verileri için giriş noktası.
- **Sayfa** : paket sürümlerinin gruplandırması. Bir sayfadaki paket sürümü sayısı sunucu uygulamasına göre tanımlanır.
- **Yaprak** : tek bir paket sürümüne özgü bir belge.

Kayıt dizininin URL 'SI öngörülebilir olur ve istemci tarafından, hizmet dizininden bir paket KIMLIĞI ve kayıt kaynağının değeri verildiğinde belirlenebilir `@id` . Kayıt sayfaları ve yaprakları için URL 'Ler kayıt dizinini inceleyerek bulunur.

### <a name="registration-pages-and-leaves"></a>Kayıt sayfaları ve yaprakları

Bir sunucu uygulamasının kayıt Leafs 'i ayrı kayıt sayfası belgelerinde depolaması için kesinlikle gerekli olmasa da, istemci tarafı belleği korumak önerilen bir uygulamadır. Tüm kayıtları dizinde bırakır veya sayfa belgelerinde yaprakları hemen depolarken, sunucu uygulamasının paket sürümleri sayısına veya paketin birikmiş boyutuna bağlı olarak iki yaklaşımdan birini seçmesi önerilir.

Kayıt dizininde tüm paket sürümlerinin (yaprakları) depolanması, paket meta verilerini getirmek için gereken HTTP isteklerinin sayısına kaydedilir, ancak daha büyük bir belge indirilmeli ve daha fazla istemci belleği ayrılmalıdır. Öte yandan, sunucu uygulamasının kaydı ayrı bir sayfa belgelerinde bırakırsa, istemcinin ihtiyaç duyması gereken bilgileri almak için daha fazla HTTP isteği gerçekleştirmesi gerekir.

Nuget.org 'in kullandığı buluşsal yöntem şu şekildedir: bir paketin 128 veya daha fazla sürümü varsa, yaprakları 64 boyutundaki sayfalara bölün. 128 'den az sürüm varsa, satır içi tümü kayıt dizininde kalır. Bunun anlamı, 65 ile 127 arasındaki paketlerin dizinde iki sayfa olacağını, ancak her iki sayfanın de satır içine alınır olduğunu unutmayın.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>İstek parametreleri

Name     | İçinde     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | yes      | Paket KIMLIĞI, küçük harf

`LOWER_ID`Değer, tarafından uygulanan kurallar kullanılarak istenen paket kimliği küçük harf olarak belirlenir. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Yanıt, aşağıdaki özelliklere sahip bir kök nesnesi olan bir JSON belgesidir:

Ad  | Tür             | Gerekli | Notlar
----- | ---------------- | -------- | -----
count | tamsayı          | yes      | Dizindeki kayıt sayfası sayısı
öğeler | nesne dizisi | yes      | Kayıt sayfaları dizisi

Dizin nesnesi dizisindeki her öğe `items` , bir kayıt sayfasını temsil eden BIR JSON nesnesidir.

#### <a name="registration-page-object"></a>Kayıt sayfası nesnesi

Kayıt dizininde bulunan kayıt sayfası nesnesi aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | string           | yes      | Kayıt sayfasının URL 'SI
count  | tamsayı          | yes      | Kayıt sayısı sayfada kalır
öğeler  | nesne dizisi | hayır       | Kayıt dizisi ve onların ilişkilendirme meta verileri
düşürül  | string           | yes      | Sayfada en düşük SemVer 2.0.0 sürümü (dahil)
üst | string           | hayır       | Kayıt dizininin URL 'SI
üst  | string           | yes      | Sayfada en yüksek SemVer 2.0.0 sürümü (dahil)

`lower` `upper` Sayfa nesnesinin ve sınırları, belirli bir sayfa sürümü için meta veriler gerektiğinde faydalıdır.
Bu sınırlar, gereken tek kayıt sayfasını getirmek için kullanılabilir. Sürüm dizeleri [NuGet 'in sürüm kurallarına](../concepts/package-versioning.md)uyar. Sürüm dizeleri normalleştirilir ve derleme meta verilerini içermez. NuGet ekosistemindeki tüm sürümlerde olduğu gibi, sürüm dizelerinin karşılaştırması, [Semver 2.0.0 'in sürüm önceliği kuralları](https://semver.org/spec/v2.0.0.html#spec-item-11)kullanılarak uygulanır.

`parent`Özelliği yalnızca kayıt sayfası nesnesinin özelliği varsa görünür `items` .

Özellik, `items` kayıt sayfası nesnesinde yoksa, `@id` tek tek Paket sürümleriyle ilgili meta verileri getirmek için ÜZERINDE belirtilen URL kullanılmalıdır. `items`Dizi bazen en iyi duruma getirme olarak sayfa nesnesinden çıkarılır. Tek bir paket KIMLIĞININ sürüm sayısı çok büyükse, kayıt dizini belgesi büyük önem verir ve yalnızca belirli bir sürümü veya küçük bir sürüm aralığını gösteren bir istemci için işlem yapar.

Özellik `items` varsa, `@id` tüm sayfa verileri özelliğinde zaten satır içine alınmış olduğundan özelliğin kullanılması gerektiğini unutmayın `items` .

Sayfa nesnesi dizisindeki her öğe `items` , bir kayıt yaprağı ve onunla ilişkili meta verileri temsil eden BIR JSON nesnesidir.

#### <a name="registration-leaf-object-in-a-page"></a>Bir sayfada kayıt yaprak nesnesi

Kayıt sayfasında bulunan kayıt yaprak nesnesi aşağıdaki özelliklere sahiptir:

Ad           | Tür   | Gerekli | Notlar
-------------- | ------ | -------- | -----
@id            | string | yes      | Kayıt yaprağın URL 'SI
catalogEntry   | object | yes      | Paket meta verilerini içeren katalog girdisi
packageContent | string | yes      | Paket içeriğinin URL 'SI (. nupkg)

Her kayıt yaprak nesnesi, tek bir paket sürümüyle ilişkili verileri temsil eder.

#### <a name="catalog-entry"></a>Katalog girişi

`catalogEntry`Kayıt yaprak nesnesindeki özelliği aşağıdaki özelliklere sahiptir:

Ad                     | Tür                       | Gerekli | Notlar
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | yes      | Bu nesneyi oluşturmak için kullanılan belgenin URL 'SI
düzenliyor                  | dizelerin dizesi veya dizisi | hayır       | 
dependencyGroups         | nesne dizisi           | hayır       | Hedef çerçeveye göre gruplanmış paketin bağımlılıkları
kullanımdan kaldırma              | object                     | hayır       | Paketle ilişkili kullanımdan kaldırma
açıklama              | string                     | hayır       | 
Iurl                  | string                     | hayır       | 
kimlik                       | string                     | yes      | Paketin KIMLIĞI
licenseUrl               | string                     | hayır       |
licenseExpression        | string                     | hayır       | 
listelenen                   | boolean                    | hayır       | Yoksa listelenen olarak kabul edilmelidir
minClientVersion         | string                     | hayır       | 
projectUrl               | string                     | hayır       | 
yayımladığı                | string                     | hayır       | Paketin yayımlandığı zamana ait ISO 8601 zaman damgasını içeren bir dize
Requirelicensekabulünü | boolean                    | hayır       | 
Özet                  | string                     | hayır       | 
etiketler                     | dize veya dize dizisi  | hayır       | 
başlık                    | string                     | hayır       | 
sürüm                  | string                     | yes      | Normalleştirme sonrasında tam sürüm dizesi

Package `version` özelliği, normalleştirmenin ardından tam sürüm dizesidir. Bu, SemVer 2.0.0 derleme verilerinin buraya dahil edileceğini gösterir.

`dependencyGroups`Özelliği, hedef çerçeveye göre gruplanan, paketin bağımlılıklarını temsil eden bir nesne dizisidir. Paketin bağımlılığı yoksa, `dependencyGroups` özelliği eksik, boş bir dizi veya `dependencies` tüm grupların özelliği boş veya eksik.

`licenseExpression`Özelliğin değeri [NuGet lisans ifadesi söz dizimi](../reference/nuspec.md#license)ile uyumludur.

> [!Note]
> Nuget.org 'de, `published` paket listelenmemiş olduğunda değer 1900 olarak ayarlanır.

#### <a name="package-dependency-group"></a>Paket bağımlılığı grubu

Her bağımlılık grubu nesnesi aşağıdaki özelliklere sahiptir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
targetFramework | string           | hayır       | Bu bağımlılıkların geçerli olduğu hedef çerçeve
bağımlılıklar    | nesne dizisi | hayır       |

`targetFramework`Dize, NuGet 'in .NET Library [NuGet. çerçeveleri](https://www.nuget.org/packages/NuGet.Frameworks/)tarafından uygulanan biçimi kullanır. Hayır `targetFramework` belirtilirse, bağımlılık grubu tüm hedef çerçeveler için geçerlidir.

`dependencies`Özelliği, her biri geçerli paketin paket bağımlılığını temsil eden bir nesne dizisidir.

#### <a name="package-dependency"></a>Paket bağımlılığı

Her paket bağımlılığı aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
kimlik           | string | yes      | Paket bağımlılığının KIMLIĞI
aralık        | object | hayır       | Bağımlılığın izin verilen [Sürüm aralığı](../concepts/package-versioning.md#version-ranges)
kayıt | string | hayır       | Bu bağımlılık için kayıt dizininin URL 'SI

`range`Özellik dışlanmazsa veya boş bir dize ise, istemci varsayılan sürüm aralığı olmalıdır `(, )` . Yani, bağımlılığın herhangi bir sürümüne izin verilir. `*`Özelliği için öğesinin değerine izin verilmez `range` .

#### <a name="package-deprecation"></a>Paketi kullanımdan kaldırma

Her bir paket kullanımdan kaldırılması aşağıdaki özelliklere sahiptir:

Ad             | Tür             | Gerekli | Notlar
---------------- | ---------------- | -------- | -----
olası          | dize dizisi | yes      | Paketin kullanım dışı olma nedenleri
message          | string           | hayır       | Bu kullanımdan kaldırma ile ilgili ek ayrıntılar
alternatePackage | object           | hayır       | Bunun yerine kullanılması gereken alternatif paket

`reasons`Özelliğin en az bir dize içermesi ve yalnızca aşağıdaki tablodaki dizeleri içermesi gerekir:

Nedeni       | Açıklama             
------------ | -----------
Eski       | Paket artık korunmaz
Kritikhatalar | Pakette kullanım için uygun olmayan hatalar vardır
Diğer        | Bu listede olmayan bir nedenden dolayı paket kullanım dışı bırakıldı

`reasons`Özelliği bilinen kümeden olmayan dizeler içeriyorsa, bunlar göz ardı edilmelidir. Dizeler büyük/küçük harfe duyarlıdır, bu nedenle `legacy` aynı şekilde değerlendirilmelidir `Legacy` . Dizide herhangi bir sıralama kısıtlaması yoktur, bu nedenle dizeler herhangi bir rastgele sıraya göre düzenlenebilirler. Ayrıca, özelliği bilinen kümeden olmayan dizeler içeriyorsa, yalnızca "diğer" dizesini içermiş gibi kabul edilmelidir.

#### <a name="alternate-package"></a>Alternatif paket

Alternatif paket nesnesi aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
kimlik           | string | yes      | Alternatif paketin KIMLIĞI
aralık        | object | hayır       | İzin verilen [Sürüm aralığı](../concepts/package-versioning.md#version-ranges)veya `*` herhangi bir sürüme izin veriliyorsa

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Bu durumda, kayıt dizininde kayıt sayfası satır içine alınır ve bu nedenle tek tek paket sürümleri hakkında meta veri getirmek için fazladan istek gerekmez.

## <a name="registration-page"></a>Kayıt sayfası

Kayıt sayfası, kayıt yaprakları içerir. Kayıt sayfasını getirecek URL, `@id` yukarıda belirtilen [kayıt sayfası nesnesindeki](#registration-page-object) özelliği tarafından belirlenir. URL tahmin edilebilir değildir ve Dizin belgesi aracılığıyla her zaman keşfedilmelidir.

> [!Warning]
> Nuget.org 'de, kayıt sayfası belgesi tesadüfen URL 'SI sayfanın alt ve üst sınırını içerir. Ancak, Dizin belgesinde geçerli bir bağlantı olduğu sürece sunucu uygulamalarının URL şeklini değiştiremeyeceğinden, bu varsayım hiçbir zaman istemci tarafından yapılmamalıdır.

`items`Dizi kayıt dizininde sağlanmazsa, bu DEĞERIN http get isteği, `@id` kökü olarak bir nesnesi olan bir JSON belgesi döndürür. Nesnesi aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | string           | yes      | Kayıt sayfasının URL 'SI
count  | tamsayı          | yes      | Kayıt sayısı sayfada kalır
öğeler  | nesne dizisi | yes      | Kayıt dizisi ve onların ilişkilendirme meta verileri
düşürül  | string           | yes      | Sayfada en düşük SemVer 2.0.0 sürümü (dahil)
üst | string           | yes      | Kayıt dizininin URL 'SI
üst  | string           | yes      | Sayfada en yüksek SemVer 2.0.0 sürümü (dahil)

Kayıt yaprak nesnelerinin şekli [Yukarıdaki](#registration-leaf-object-in-a-page)kayıt diziniyle aynıdır.

## <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Kayıt yaprak

Kayıt yaprağı, belirli bir paket KIMLIĞI ve sürümü hakkında bilgi içerir. Belirli bir sürümle ilgili meta veriler bu belgede kullanılamıyor olabilir. Paket meta verileri [kayıt dizininden](#registration-index) veya kayıt [sayfasından](#registration-page) (kayıt dizini kullanılarak bulunan) alınmalıdır.

Kayıt yaprak getiren URL, kayıt `@id` dizini veya kayıt sayfasındaki bir kayıt yaprak nesnesinin özelliğinden alınır. Sayfa belgesinde olduğu gibi. URL tahmin edilebilir değil ve kayıt sayfası nesnesi aracılığıyla her zaman keşfedilmelidir.

> [!Warning]
> Nuget.org 'de, kayıt yaprak belge tesadüfen için URL paket sürümünü içerir. Ancak, ana belgenin geçerli bir bağlantısı olduğu sürece, sunucu uygulamalarının URL şeklini değiştiremeyeceğinden, bu varsayım hiçbir zaman istemci tarafından yapılmamalıdır. 

Kayıt yaprağı, aşağıdaki özelliklere sahip bir kök nesnesine sahip bir JSON belgesidir:

Ad           | Tür    | Gerekli | Notlar
-------------- | ------- | -------- | -----
@id            | string  | yes      | Kayıt yaprağın URL 'SI
catalogEntry   | string  | hayır       | Bu yaprağı üreten Katalog girişinin URL 'SI
listelenen         | boolean | hayır       | Yoksa listelenen olarak kabul edilmelidir
packageContent | string  | hayır       | Paket içeriğinin URL 'SI (. nupkg)
yayımladığı      | string  | hayır       | Paketin yayımlandığı zamana ait ISO 8601 zaman damgasını içeren bir dize
kayıt   | string  | hayır       | Kayıt dizininin URL 'SI

> [!Note]
> Nuget.org 'de, `published` paket listelenmemiş olduğunda değer 1900 olarak ayarlanır.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
