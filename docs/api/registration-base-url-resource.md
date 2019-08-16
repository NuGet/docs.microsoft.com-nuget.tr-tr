---
title: Paket meta verileri, NuGet API 'SI
description: Paket kayıt taban URL 'SI, paketlerle ilgili meta verilerin getirilmesi için izin verir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488310"
---
# <a name="package-metadata"></a>Paket meta verileri

NuGet v3 API kullanarak bir paket kaynağında bulunan paketlerle ilgili meta verileri getirmek mümkündür. Bu meta veriler, [hizmet dizininde](service-index.md)bulunan `RegistrationsBaseUrl` kaynak kullanılarak getirilebilir.

Altında `RegistrationsBaseUrl` bulunan belgelerin koleksiyonu, genellikle "kayıtlar" veya "kayıt Blobları" olarak adlandırılır. Tek tek `RegistrationsBaseUrl` altındaki belge kümesi, "kayıt Hive" olarak adlandırılır. Kayıt Hive bir paket kaynağında bulunan her pakete ilişkin tüm meta verileri içerir.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeeri                     | Notlar
------------------------------- | -----
RegistrationsBaseUrl            | İlk yayın
RegistrationsBaseUrl/3.0.0-Beta | Diğer adı`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Diğer adı`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gdaraltılmış yanıtlar
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 paketlerini içerir

Bu, çeşitli istemci sürümleri için kullanılabilen üç farklı kayıt kovanlarını temsil eder.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Bu kayıtlar sıkıştırılmaz (örtük `Content-Encoding: identity`olarak kullandıkları anlamına gelir). SemVer 2.0.0 paketleri bu Hive **dışında tutulur** .

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Bu kayıtlar kullanılarak `Content-Encoding: gzip`sıkıştırılır. SemVer 2.0.0 paketleri bu Hive **dışında tutulur** .

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Bu kayıtlar kullanılarak `Content-Encoding: gzip`sıkıştırılır. SemVer 2.0.0 paketleri bu kovana **dahildir** .
SemVer 2.0.0 hakkında daha fazla bilgi için bkz. [NuGet.org Için semver 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Taban URL 'SI

Aşağıdaki API 'lerin temel URL 'si, belirtilen kaynak `@id` `@type` değerleriyle ilişkili özelliğin değeridir. Aşağıdaki belgede, yer tutucu temel URL 'si `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'ler http yöntemlerini `GET` ve ' i `HEAD`destekler.

## <a name="registration-index"></a>Kayıt dizini

Kayıt kaynağı paket meta verilerini paket KIMLIĞIYLE gruplandırır. Aynı anda birden fazla paket KIMLIĞI hakkında veri almak mümkün değildir. Bu kaynak paket kimliklerini bulmayı sağlayan bir yol sağlar. Bunun yerine, istemcinin istenen paket KIMLIĞINI zaten öğrenmiş olduğu varsayılır. Her paket sürümü hakkında kullanılabilir meta veriler sunucu uygulamasına göre değişir. Paket kayıt Blobları aşağıdaki hiyerarşik yapıya sahiptir:

- **Dizin**: aynı paket kimliğine sahip bir kaynaktaki tüm paketler tarafından paylaşılan paket meta verileri için giriş noktası.
- **Sayfa**: paket sürümlerinin gruplandırması. Bir sayfadaki paket sürümü sayısı sunucu uygulamasına göre tanımlanır.
- **Yaprak**: tek bir paket sürümüne özgü bir belge.

Kayıt dizininin URL 'si öngörülebilir olur ve istemci tarafından, hizmet dizininden bir paket kimliği ve kayıt kaynağının `@id` değeri verildiğinde belirlenebilir. Kayıt sayfaları ve yaprakları için URL 'Ler kayıt dizinini inceleyerek bulunur.

### <a name="registration-pages-and-leaves"></a>Kayıt sayfaları ve yaprakları

Bir sunucu uygulamasının kayıt Leafs 'i ayrı kayıt sayfası belgelerinde depolaması için kesinlikle gerekli olmasa da, istemci tarafı belleği korumak önerilen bir uygulamadır. Tüm kayıt, dizinde bırakılır veya sayfa belgelerinde yaprakları hemen depolarken, sunucu uygulamasının paket sürümü sayısına göre iki yaklaşım arasından seçim yapmak için bazı buluşsal yöntemleri tanımlamasına önerilir veya paketin birikmiş boyutu bırakılır.

Kayıt dizininde tüm paket sürümlerinin (yaprakları) depolanması, paket meta verilerini getirmek için gereken HTTP isteklerinin sayısına kaydedilir, ancak daha büyük bir belge indirilmeli ve daha fazla istemci belleği ayrılmalıdır. Öte yandan, sunucu uygulamasının kaydı ayrı bir sayfa belgelerinde bırakırsa, istemcinin ihtiyaç duyması gereken bilgileri almak için daha fazla HTTP isteği gerçekleştirmesi gerekir.

Nuget.org 'in kullandığı buluşsal yöntem şu şekildedir: bir paketin 128 veya daha fazla sürümü varsa, yaprakları 64 boyutundaki sayfalara bölün. 128 'den az sürüm varsa, satır içi tümü kayıt dizininde kalır.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>İstek parametreleri

Ad     | İçindeki     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | dize  | evet      | Paket KIMLIĞI, küçük harf

`LOWER_ID` Değer, tarafından uygulanan kurallar kullanılarak istenen paket kimliği küçük harf olarak belirlenir. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Yanıt, aşağıdaki özelliklere sahip bir kök nesnesi olan bir JSON belgesidir:

Ad  | Tür             | Gerekli | Notlar
----- | ---------------- | -------- | -----
count | tamsayı          | evet      | Dizindeki kayıt sayfası sayısı
items | nesne dizisi | evet      | Kayıt sayfaları dizisi

Dizin nesnesi `items` dizisindeki her öğe, bir kayıt sayfasını temsil eden bir JSON nesnesidir.

#### <a name="registration-page-object"></a>Kayıt sayfası nesnesi

Kayıt dizininde bulunan kayıt sayfası nesnesi aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | evet      | Kayıt sayfasının URL 'SI
count  | tamsayı          | evet      | Kayıt sayısı sayfada kalır
items  | nesne dizisi | eşleşen       | Kayıt dizisi ve onların ilişkilendirme meta verileri
düşürül  | dize           | evet      | Sayfada en düşük SemVer 2.0.0 sürümü (dahil)
üst | dize           | eşleşen       | Kayıt dizininin URL 'SI
üst  | dize           | evet      | Sayfada en yüksek SemVer 2.0.0 sürümü (dahil)

Sayfa nesnesinin `upper` ve sınırları, belirli bir sayfa sürümü için meta veriler gerektiğinde faydalıdır. `lower`
Bu sınırlar, gereken tek kayıt sayfasını getirmek için kullanılabilir. Sürüm dizeleri [NuGet 'in sürüm kurallarına](../concepts/package-versioning.md)uyar. Sürüm dizeleri normalleştirilir ve derleme meta verilerini içermez. NuGet ekosistemindeki tüm sürümlerde olduğu gibi, sürüm dizelerinin karşılaştırması, [Semver 2.0.0 'in sürüm önceliği kuralları](http://semver.org/spec/v2.0.0.html#spec-item-11)kullanılarak uygulanır.

Özelliği yalnızca kayıt sayfası nesnesinin `items` özelliği varsa görünür. `parent`

Özellik, kayıt sayfası nesnesinde yoksa, tek tek Paket sürümleriyle ilgili meta verileri getirmek için `@id` üzerinde belirtilen URL kullanılmalıdır. `items` `items` Dizi bazen en iyi duruma getirme olarak sayfa nesnesinden çıkarılır. Tek bir paket KIMLIĞININ sürüm sayısı çok büyükse, kayıt dizini belgesi büyük önem verir ve yalnızca belirli bir sürümü veya küçük bir sürüm aralığını gösteren bir istemci için işlem yapar.

Özellik varsa, tüm sayfa verileri `items` özelliğinde zaten satır içine alınmış olduğundan özelliğin kullanılması gerektiğini unutmayın. `@id` `items`

Sayfa nesnesi `items` dizisindeki her öğe, bir kayıt yaprağı ve onunla ilişkili meta verileri temsil eden bir JSON nesnesidir.

#### <a name="registration-leaf-object-in-a-page"></a>Bir sayfada kayıt yaprak nesnesi

Kayıt sayfasında bulunan kayıt yaprak nesnesi aşağıdaki özelliklere sahiptir:

Ad           | Tür   | Gerekli | Notlar
-------------- | ------ | -------- | -----
@id            | dize | evet      | Kayıt yaprağın URL 'SI
catalogEntry   | nesne | evet      | Paket meta verilerini içeren katalog girdisi
packageContent | dize | evet      | Paket içeriğinin URL 'SI (. nupkg)

Her kayıt yaprak nesnesi, tek bir paket sürümüyle ilişkili verileri temsil eder.

#### <a name="catalog-entry"></a>Katalog girişi

Kayıt yaprak nesnesindeki özelliği aşağıdaki özelliklere sahiptir: `catalogEntry`

Ad                     | Tür                       | Gerekli | Notlar
------------------------ | -------------------------- | -------- | -----
@id                      | dize                     | evet      | Bu nesneyi oluşturmak için kullanılan belgenin URL 'SI
düzenliyor                  | dizelerin dizesi veya dizisi | eşleşen       | 
dependencyGroups         | nesne dizisi           | eşleşen       | Hedef çerçeveye göre gruplanmış paketin bağımlılıkları
kullanımdan kaldırma              | nesne                     | eşleşen       | Paketle ilişkili kullanımdan kaldırma
açıklama              | dize                     | eşleşen       | 
Iurl                  | dize                     | eşleşen       | 
kimlik                       | dize                     | evet      | Paketin KIMLIĞI
licenseUrl               | dize                     | eşleşen       |
licenseExpression        | dize                     | eşleşen       | 
listelenen                   | Boole değeri                    | eşleşen       | Yoksa listelenen olarak kabul edilmelidir
minClientVersion         | dize                     | eşleşen       | 
projectUrl               | dize                     | eşleşen       | 
yayımladığı                | dize                     | eşleşen       | Paketin yayımlandığı zamana ait ISO 8601 zaman damgasını içeren bir dize
Requirelicensekabulünü | Boole değeri                    | eşleşen       | 
özet                  | dize                     | eşleşen       | 
etiketler                     | dize veya dize dizisi  | eşleşen       | 
title                    | dize                     | eşleşen       | 
sürüm                  | dize                     | evet      | Normalleştirme sonrasında tam sürüm dizesi

Package `version` özelliği, normalleştirmenin ardından tam sürüm dizesidir. Bu, SemVer 2.0.0 derleme verilerinin buraya dahil edileceğini gösterir.

`dependencyGroups` Özelliği, hedef çerçeveye göre gruplanan, paketin bağımlılıklarını temsil eden bir nesne dizisidir. Paketin bağımlılığı yoksa, `dependencyGroups` özelliği eksik, boş bir dizi `dependencies` veya tüm grupların özelliği boş veya eksik.

`licenseExpression` Özelliğin değeri [NuGet lisans ifadesi söz dizimi](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)ile uyumludur.

#### <a name="package-dependency-group"></a>Paket bağımlılığı grubu

Her bağımlılık grubu nesnesi aşağıdaki özelliklere sahiptir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
targetFramework | dize           | eşleşen       | Bu bağımlılıkların geçerli olduğu hedef çerçeve
bağımlılıklar    | nesne dizisi | eşleşen       |

Dize `targetFramework` , NuGet 'in .NET Library [NuGet. çerçeveleri](https://www.nuget.org/packages/NuGet.Frameworks/)tarafından uygulanan biçimi kullanır. Hayır `targetFramework` belirtilirse, bağımlılık grubu tüm hedef çerçeveler için geçerlidir.

`dependencies` Özelliği, her biri geçerli paketin paket bağımlılığını temsil eden bir nesne dizisidir.

#### <a name="package-dependency"></a>Paket bağımlılığı

Her paket bağımlılığı aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
kimlik           | dize | evet      | Paket bağımlılığının KIMLIĞI
aralık        | nesne | eşleşen       | Bağımlılığın izin verilen [Sürüm aralığı](../concepts/package-versioning.md#version-ranges-and-wildcards)
kayıt | dize | eşleşen       | Bu bağımlılık için kayıt dizininin URL 'SI

Özellik dışlanmazsa veya boş bir dize ise, istemci varsayılan sürüm aralığı `(, )`olmalıdır. `range` Yani, bağımlılığın herhangi bir sürümüne izin verilir.

#### <a name="package-deprecation"></a>Paketin kullanımdan kaldırılması

Her bir paket kullanımdan kaldırılması aşağıdaki özelliklere sahiptir:

Ad             | Tür             | Gerekli | Notlar
---------------- | ---------------- | -------- | -----
olası          | dizeler dizisi | evet      | Paketin kullanım dışı olma nedenleri
iletisi          | dize           | eşleşen       | Bu kullanımdan kaldırma ile ilgili ek ayrıntılar
alternatePackage | nesne           | eşleşen       | Bunun yerine kullanılması gereken paket bağımlılığı

`reasons` Özelliğin en az bir dize içermesi ve yalnızca aşağıdaki tablodaki dizeleri içermesi gerekir:

Neden       | Açıklama             
------------ | -----------
Eski       | Paket artık korunmaz
Kritikhatalar | Pakette kullanım için uygun olmayan hatalar vardır
Diğer        | Bu listede olmayan bir nedenden dolayı paket kullanım dışı bırakıldı

`reasons` Özelliği bilinen kümeden olmayan dizeler içeriyorsa, bunlar göz ardı edilmelidir. Dizeler büyük/küçük harfe duyarlıdır, bu `legacy` nedenle `Legacy`aynı şekilde değerlendirilmelidir. Dizide herhangi bir sıralama kısıtlaması yoktur, bu nedenle dizeler herhangi bir rastgele sıraya göre düzenlenebilirler. Ayrıca, özelliği bilinen kümeden olmayan dizeler içeriyorsa, yalnızca "diğer" dizesini içermiş gibi kabul edilmelidir.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Bu durumda, kayıt dizininde kayıt sayfası satır içine alınır ve bu nedenle tek tek paket sürümleri hakkında meta veri getirmek için fazladan istek gerekmez.

## <a name="registration-page"></a>Kayıt sayfası

Kayıt sayfası, kayıt yaprakları içerir. Kayıt sayfasını getirecek URL, yukarıda belirtilen `@id` [kayıt sayfası nesnesindeki](#registration-page-object) özelliği tarafından belirlenir.

Dizi kayıt dizininde sağlanmazsa, bu `@id` değerin http get isteği, kökü olarak bir nesnesi olan bir JSON belgesi döndürür. `items` Nesnesi aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | evet      | Kayıt sayfasının URL 'SI
count  | tamsayı          | evet      | Kayıt sayısı sayfada kalır
items  | nesne dizisi | evet      | Kayıt dizisi ve onların ilişkilendirme meta verileri
düşürül  | dize           | evet      | Sayfada en düşük SemVer 2.0.0 sürümü (dahil)
üst | dize           | evet      | Kayıt dizininin URL 'SI
üst  | dize           | evet      | Sayfada en yüksek SemVer 2.0.0 sürümü (dahil)

Kayıt yaprak nesnelerinin şekli [Yukarıdaki](#registration-leaf-object-in-a-page)kayıt diziniyle aynıdır.

## <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Kayıt yaprak

Kayıt yaprağı, belirli bir paket KIMLIĞI ve sürümü hakkında bilgi içerir. Belirli bir sürümle ilgili meta veriler bu belgede kullanılamıyor olabilir. Paket meta verileri [kayıt dizininden](#registration-index) veya kayıt [sayfasından](#registration-page) (kayıt dizini kullanılarak bulunan) alınmalıdır.

Kayıt yaprak getiren URL, kayıt dizini veya kayıt sayfasındaki bir `@id` kayıt yaprak nesnesinin özelliğinden alınır.

Kayıt yaprağı, aşağıdaki özelliklere sahip bir kök nesnesine sahip bir JSON belgesidir:

Ad           | Tür    | Gerekli | Notlar
-------------- | ------- | -------- | -----
@id            | dize  | evet      | Kayıt yaprağın URL 'SI
catalogEntry   | dize  | eşleşen       | Bu yaprağı üreten Katalog girişinin URL 'SI
listelenen         | Boole değeri | eşleşen       | Yoksa listelenen olarak kabul edilmelidir
packageContent | dize  | eşleşen       | Paket içeriğinin URL 'SI (. nupkg)
yayımladığı      | dize  | eşleşen       | Paketin yayımlandığı zamana ait ISO 8601 zaman damgasını içeren bir dize
kayıt   | dize  | eşleşen       | Kayıt dizininin URL 'SI

> [!Note]
> NuGet.org 'de, `published` paket listelenmemiş olduğunda değer 1900 olarak ayarlanır.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
