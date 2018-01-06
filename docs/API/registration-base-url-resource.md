---
title: Paket meta verileri, NuGet API | Microsoft Docs
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
ms.assetid: 96b07019-c2e1-4f40-9290-f65ad71af3b1
description: "Paket kayıt temel URL'si paketlerle ilgili meta verilerini getirmek sağlar."
keywords: "NuGet API paket meta verileri, NuGet API kayıt, NuGet API listelenmemiş paketleri"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1aabe6ae5c661e12b2639700813946e7a9a58b24
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="package-metadata"></a>Paket meta verileri

NuGet V3 API kullanarak bir paket kaynağında kullanılabilir paketler hakkında meta veri Getir mümkündür. Bu meta verileri kullanarak getirilebilir `RegistrationsBaseUrl` kaynak bulunan [Hizmeti dizini](service-index.md).

Altında bulunan belgeleri topluluğu `RegistrationsBaseUrl` genellikle "kayıtlar" veya "kayıt BLOB'lar" adı verilir. Belgeleri tek bir dizi `RegistrationsBaseUrl` "kayıt hive" adlandırılır. Bir kayıt defteri kovanı her bir paket kaynağındaki kullanılabilir paket hakkında tüm meta veriler içeriyor.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerler kullanılır:

@typedeğer                     | Notlar
------------------------------- | -----
RegistrationsBaseUrl            | İlk sürüm
RegistrationsBaseUrl/3.0.0-beta | Diğer adı`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Diğer adı`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip'li yanıtları
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 paketleri içerir

Bu, çeşitli istemci sürümleri için kullanılabilir üç ayrı kayıt kovanları temsil eder.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Bu kayıtları sıkıştırılmaz (bir kapsanan kullandıkları anlamına `Content-Encoding: identity`). SemVer 2.0.0 paketleri **dışlanan** bu hive gelen.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Bu kayıtlar kullanılarak sıkıştırılan `Content-Encoding: gzip`. SemVer 2.0.0 paketleri **dışlanan** bu hive gelen.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Bu kayıtlar kullanılarak sıkıştırılan `Content-Encoding: gzip`. SemVer 2.0.0 paketleri **dahil** bu kovanında.
SemVer 2.0.0 hakkında daha fazla bilgi için bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` özelliği daha önce bahsedilen kaynakla ilişkilendirilmiş `@type` değerleri. Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.

## <a name="registration-index"></a>Kayıt dizini

Kayıt kaynak grupları meta verileri paket kimliği ile paket Aynı anda birden fazla paket kimliği ilişkin veri almak mümkün değildir. Bu kaynak paketi kimliklerini bulmak için bir yol sağlar. Bunun yerine istemci istenen paket kimliği zaten biliyor varsayılır Her paket sürümü hakkında kullanılabilir meta veriler sunucu uygulaması tarafından değişir. Paket kaydı BLOB'ları aşağıdaki hiyerarşik bir yapı vardır:

- **Dizin**: tüm paketler aynı paket kimliğine sahip bir kaynak tarafından paylaşılan paket meta verileri için giriş noktası
- **Sayfa**: Paket sürümlerinin gruplandırmasıdır. Bir sayfasında paket sürümlerinin sayısı sunucu uygulaması tarafından tanımlanır.
- **Yaprak**: tek bir paket sürümü için belirli bir belge.

Kayıt dizin URL'sini tahmin edilebilir ve verilen bir paket kimliği ve kayıt kaynağın istemci tarafından belirlenebilir `@id` hizmet dizinden değeri. Kayıt sayfaları ve bırakır URL'leri kayıt dizin inceleyerek bulunur.

### <a name="registration-pages-and-leaves"></a>Kayıt sayfaları ve bırakır

Bunu kesinlikle olmadığında depolamak bir sunucu uygulaması için ayrı kayıt sayfası belgelerde kayıt leafs gerekli olsa da, istemci-tarafı bellekten kazanacak şekilde önerilen bir yöntemdir. Yerine satır içi kullanım tüm kayıt bırakır dizini ya da hemen bırakır sayfa belgeleri depolamak, sunucu uygulama paketi sürümleri sayısına göre iki yaklaşım arasında seçim yapma bazı buluşsal yöntem tanımlamanız önerilir veya Paket toplam boyutu bırakır.

Tüm paket sürümlerini depolamak (kayıt dizin kaydeder HTTP istek sayısı fetch paket meta verileri ancak daha büyük bir belge yüklenmelidir ve daha fazla istemci bellek tahsis edilmelidir anlamına gelir gerekli bırakır). Diğer taraftan, sunucu uygulamasına hemen kayıt bırakır ayrı sayfa belgelerde depoluyorsa, istemci, gerekli bilgileri almak için daha fazla HTTP isteklerini gerçekleştirmeniz gerekir.

Buluşsal yöntem nuget.org kullandığı aşağıdaki gibidir: bir paket 128 veya daha fazla sürümü varsa, bırakır boyutu 64 sayfalarına bölün. 128'den az sürümleri varsa, tüm satır içi kayıt dizine bırakır.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>İstek parametreleri

Ad     | İçindeki     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | dize  | Evet      | Dönüştürüldükten paket kimliği

`LOWER_ID` Tarafından uygulanan kurallarını kullanarak dönüştürüldükten istenen paket kimliği bir değerdir. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Yanıt, bir kök nesnesi aşağıdaki özelliklere sahip olan bir JSON belgesi şöyledir:

Ad  | Tür             | Gerekli | Notlar
----- | ---------------- | -------- | -----
count | tamsayı          | Evet      | Dizin kayıt sayfa sayısı
Öğeleri | Nesne dizisi | Evet      | Kayıt sayfaları dizisi

Her öğe dizini nesnenin `items` dizidir kayıt sayfası temsil eden bir JSON nesnesi.

#### <a name="registration-page-object"></a>Kayıt sayfası nesnesi

Kayıt dizininde bulundu kayıt sayfası nesnesi aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | Evet      | Kayıt sayfası URL'si
count  | tamsayı          | Evet      | Kayıt sayısı sayfasında bırakır
Öğeleri  | Nesne dizisi | Yok       | Kayıt bırakır ve bunların ilişkilendirme meta verilerini dizisi
Daha düşük  | dize           | Evet      | En düşük SemVer 2.0.0 sürüm (dahil) sayfasındaki
Üst | dize           | Yok       | Kayıt dizin URL'si
üst  | dize           | Evet      | En yüksek SemVer 2.0.0 sürüme (dahil) sayfasındaki

`lower` Ve `upper` olan sayfa nesnesine sınırları, özel sayfa sürümü için meta veriler gerektiğinde kullanışlıdır.
Bu sınırlar, gerekli yalnızca kayıt sayfası getirmek için kullanılabilir. Sürüm dizelerini uygun [NuGet sürümü kurallarını](../reference/package-versioning.md). Sürüm dizelerini normalleştirilmiş ve derleme meta verilerini içermez. NuGet ekosistemi tüm sürümlerinde ile sürüm dizelerini karşılaştırması kullanılarak gerçekleştirilir gibi [SemVer 2.0.0's sürüm öncelik kuralları](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Özelliği kayıt sayfası nesne varsa, yalnızca görünür `items` özelliği.

Varsa `items` özelliği kayıt sayfası nesne mevcut değil, URL belirtilen `@id` tek tek Paket sürümlerinin meta verilerini getirmek için kullanılması gerekir. `items` Dizi bir iyileştirme olarak sayfa nesnesinden bazen dışlandı. Tek bir paket kimliği sürümleri sayısı çok büyük ise kayıt dizini belgesinde yoğun ve yalnızca belirli bir sürüm veya küçük bir aralık sürümleri hakkında cares bir istemci için işlemini kayıp olacaktır.

Unutmayın `items` özelliği mevcutsa, `@id` özelliği kullanılamaz, tüm sayfa verileri olduğundan zaten içinde içermesinden `items` özelliği.

Her öğe sayfa nesnenin `items` dizidir kayıt yaprak temsil eden bir JSON nesnesi ve ilişkili meta verileri.

#### <a name="registration-leaf-object-in-a-page"></a>Kayıt yaprak nesne sayfasındaki

Bir kayıt sayfasında bulunan kayıt yaprak nesnesi aşağıdaki özelliklere sahiptir:

Ad           | Tür   | Gerekli | Notlar
-------------- | ------ | -------- | -----
@id            | dize | Evet      | Kayıt yaprak URL'si
catalogEntry   | nesne | Evet      | Paket meta verileri içeren bir katalog girişi
packageContent | dize | Evet      | Paket içeriğini (.nupkg) URL'si

Her kayıt yaprak nesnesi bir tek Paket sürümü ile ilişkili verileri temsil eder.

#### <a name="catalog-entry"></a>Bir katalog girişi

`catalogEntry` Özelliği kayıt yaprak nesnesindeki aşağıdaki özelliklere sahip:

Ad                     | Tür                       | Gerekli | Notlar
------------------------ | -------------------------- | -------- | -----
@id                      | dize                     | Evet      | Bu nesne üretmek için kullanılan belgesi URL'si
yazarları                  | dize veya dize dizisi | Yok       | 
dependencyGroups         | Nesne dizisi           | Yok       | Paket içeriğini (.nupkg) URL'si
açıklama              | dize                     | Yok       | 
iconUrl                  | dize                     | Yok       | 
kimlik                       | dize                     | Evet      | Paket kimliği
licenseUrl               | dize                     | Yok       | 
listelenen                   | Boole değeri                    | Yok       | Absent listelenen IF olarak kabul edilmesi
MinClientVersion         | dize                     | Yok       | 
projectUrl               | dize                     | Yok       | 
Yayımlanan                | dize                     | Yok       | Paketin ne zaman yayımlanan, bir ISO 8601 zaman damgası içeren bir dize
RequireLicenseAcceptance | Boole değeri                    | Yok       | 
özet                  | dize                     | Yok       | 
etiketler                     | dize veya dize dizisi  | Yok       | 
Başlık                    | dize                     | Yok       | 
sürüm                  | dize                     | Evet      | Paketin sürümü

`dependencyGroups` Özelliği olan bir hedef framework tarafından gruplandırılmış şekilde paketin bağımlılıklarını temsil eden nesneler dizisi. Paket hiçbir bağımlılık varsa `dependencyGroups` özelliği eksik, boş bir dizi veya `dependencies` tüm grupların özelliği boş veya eksik.

#### <a name="package-dependency-group"></a>Paket bağımlılık grubu

Her bağımlılık grup nesnesi, aşağıdaki özelliklere sahiptir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
targetFramework | dize           | Yok       | Bu bağımlılıklar için geçerli olan hedef Framework'ü
bağımlılıklar    | Nesne dizisi | Yok       |

`targetFramework` NuGet .NET kitaplığı tarafından uygulanan biçim dizesini kullanır [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Öyle değilse `targetFramework` belirtilirse, bağımlılık grubunun tüm hedef çerçeve için geçerlidir.

`dependencies` Her bir paket bağımlılığı geçerli paketi temsil eden nesneler dizisi bir özelliktir.

#### <a name="package-dependency"></a>Paket bağımlılığı

Her paket bağımlılığı aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
kimlik           | dize | Evet      | Paket bağımlılığı kimliği
aralık        | nesne | Yok       | İzin verilen [sürüm aralığı](../reference/package-versioning.md#version-ranges-and-wildcards) bağımlılığın
kayıt | dize | Yok       | Bu bağımlılığı kaydı dizini URL'si

Varsa `range` özelliği dışlandı veya boş bir dize istemci sürüm aralığı varsayılan `(, )`. Diğer bir deyişle, herhangi bir sürümünü bağımlılık izin verilir.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>Örnek yanıt 

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Bu özel durumda kayıt dizin içermesinden kayıt sayfası olduğundan, hiçbir ek istek tek tek Paket sürümlerinin meta verilerini getirmek için gerekli olması.

## <a name="registration-page"></a>Kayıt sayfası

Kayıt sayfası kayıt bırakır içerir. Bir kayıt sayfasına getirmek için URL tarafından belirlenen `@id` özelliğinde [kayıt sayfası nesne](#registration-page-object) yukarıda belirtilen.

Zaman `items` bir HTTP GET isteği dizi kayıt dizinde sağlanmaz, `@id` değer bir nesne olarak kökü olan bir JSON belgesi döndürür. Nesne, aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | Evet      | Kayıt sayfası URL'si
count  | tamsayı          | Evet      | Kayıt sayısı sayfasında bırakır
Öğeleri  | Nesne dizisi | Evet      | Kayıt bırakır ve bunların ilişkilendirme meta verilerini dizisi
Daha düşük  | dize           | Evet      | En düşük SemVer 2.0.0 sürüm (dahil) sayfasındaki
Üst | dize           | Evet      | Kayıt dizin URL'si
üst  | dize           | Evet      | En yüksek SemVer 2.0.0 sürüme (dahil) sayfasındaki

Kayıt yaprak nesnelerin şeklini kayıt dizini ile aynı olan [yukarıda](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Kayıt yaprak

Kayıt yaprak belirli paket Kimliğini ve sürümünü hakkında bilgiler içerir. Bu belgede belirli sürümü hakkındaki meta verileri kullanılamayabilir. Paket meta verileri getirilen gelen [kayıt dizin](#registration-index) veya [kayıt sayfası](#registration-page) (hangi bulunan kayıt dizini kullanarak).

Bir kayıt yaprak getirmek için URL'yi elde edilen `@id` kayıt dizin veya kayıt sayfası kayıt yaprak nesnesinin özelliği.

Aşağıdaki özelliklere sahip bir kök nesnesi içeren bir JSON belgesi kayıt dağıtımdır:

Ad           | Tür    | Gerekli | Notlar
-------------- | ------- | -------- | -----
@id            | dize  | Evet      | Kayıt yaprak URL'si
catalogEntry   | dize  | Yok       | Bu yaprak üretilen katalog girişini URL'si
listelenen         | Boole değeri | Yok       | Absent listelenen IF olarak kabul edilmesi
packageContent | dize  | Yok       | Paket içeriğini (.nupkg) URL'si
Yayımlanan      | dize  | Yok       | Paketin ne zaman yayımlanan, bir ISO 8601 zaman damgası içeren bir dize
kayıt   | dize  | Yok       | Kayıt dizin URL'si

> [!Note]
> Nuget.org üzerinde `published` değeri yıl paket olduğunda listelenmemiş 1900 ayarlanır.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
