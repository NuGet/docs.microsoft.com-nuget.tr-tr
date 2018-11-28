---
title: Paket meta verileri, NuGet API'si
description: Paket kayıt temel URL paketlerle ilgili meta verilerini getirmek sağlar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ba47d6fdeeaa4ee9de83ef4dd990707bd4928063
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453565"
---
# <a name="package-metadata"></a>Paket meta verileri

NuGet V3 API'sini kullanarak bir paket kaynağı üzerinde kullanılabilir paketler hakkındaki meta verileri getirmek mümkündür. Bu meta veriler kullanılarak getirilebilir `RegistrationsBaseUrl` kaynak bulunan [hizmet dizini](service-index.md).

Altında bulunan belgeleri koleksiyonunu `RegistrationsBaseUrl` genellikle "kayıtları" veya "kayıt BLOB'ları" denir. Altında tek bir belge kümesini `RegistrationsBaseUrl` "kayıt hive" adlandırılır. Bir kayıt defteri kovanı her bir paket kaynağı üzerinde kullanılabilir paketle ilgili tüm meta veriler içerir.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type Değer                     | Notlar
------------------------------- | -----
RegistrationsBaseUrl            | İlk yayın
RegistrationsBaseUrl/3.0.0-beta | Diğer adı `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Diğer adı `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzipped yanıtları
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 paketleri içerir.

Bu, çeşitli istemci sürümleri için kullanılabilir üç farklı kayıt kovanı temsil eder.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Bu kayıtları sıkıştırılmaz (örtük kullandıkları anlamı `Content-Encoding: identity`). SemVer 2.0.0 paketleri **dışlanan** bu hive öğesinden.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Bu kayıtları kullanarak sıkıştırılmış `Content-Encoding: gzip`. SemVer 2.0.0 paketleri **dışlanan** bu hive öğesinden.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Bu kayıtları kullanarak sıkıştırılmış `Content-Encoding: gzip`. SemVer 2.0.0 paketleri **dahil** bu kovanında.
SemVer 2.0.0 hakkında daha fazla bilgi için bkz: [nuget.org SemVer 2.0.0 desteği](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değerleri. Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="registration-index"></a>Kayıt dizini

Kayıt kaynak gruplarını meta verileri paket kimliği ile paket Aynı anda birden fazla paket kimliği hakkındaki verileri almak mümkün değildir. Bu kaynak paketi kimliklerini bulmak için hiçbir yol sağlar. Bunun yerine istemci istenen paket kimliğini zaten bildiğiniz varsayılır Sunucu uygulaması tarafından kullanılabilen meta verileri her paket sürümü hakkında değişir. Paket kayıt BLOB'ları aşağıdaki hiyerarşik yapıya sahiptir:

- **Dizin**: tüm paketleri aynı paket kimliğine sahip bir kaynak tarafından paylaşılan paket meta verileri için giriş noktası
- **Sayfa**: Paket sürümlerini gruplandırmasıdır. Paket sürümleri sayfasındaki sayısını sunucu uygulama tarafından tanımlanır.
- **Yaprak**: tek bir paket sürümüne özgü bir belge.

Kayıt dizinini URL'sini tahmin edilebilir ve paket Kimliğini ve kayıt kaynağın verilen istemci tarafından belirlenebilir `@id` hizmet dizini değeri. Kayıt dizinini inceleyerek bırakır ve kayıt sayfaları için URL'leri bulunur.

### <a name="registration-pages-and-leaves"></a>Kayıt sayfaları ve bırakır

Kayıt ayrı kayıt sayfasına belgelerde leafs gerektirmesidir depolamak bir sunucu uygulaması için zorunludur olsa da, istemci tarafı bellekten kazanacak şekilde önerilen bir yöntemdir. Yerine satır içi kullanım tüm dizin veya leaves sayfa belgelerde hemen depolama kaydı bırakır, sunucu uygulama paket sürümlerini sayısına göre iki yaklaşım arasında seçim yapmanızı bazı buluşsal tanımlamanız önerilir veya toplam boyutu, paket bırakır.

Tüm paket sürümlerini depolamak (kayıt dizin kaydeder HTTP istek sayısına getirme paket meta verileri, ancak daha büyük bir belge indirilmelidir ve daha fazla istemci bellek ayrılması gereken anlamına gelir gerekli bırakır). Öte yandan, sunucu uygulaması, kaydı bırakır hemen ayrı sayfa belgelerde depolar. istemcinin ihtiyaç duyduğu bilgileri almak için daha fazla HTTP isteklerini gerçekleştirmeniz gerekir.

Buluşsal yöntem nuget.org kullanan şu şekildedir: 128 veya daha fazla paket sürümleri varsa, boyutu 64 sayfalarına bırakır Kes. 128'den az sürümleri varsa, tüm satır içi kaydı dizine bırakır.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>İstek parametreleri

Ad     | İçindeki     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | dize  | Evet      | Küçük harfli paket kimliği

`LOWER_ID` Tarafından uygulanan kurallar kullanarak küçük harfli istenen paket kimliği bir değerdir. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Yanıt, bir kök nesnesi aşağıdaki özelliklere sahip olan bir JSON belgesi.:

Ad  | Tür             | Gerekli | Notlar
----- | ---------------- | -------- | -----
count | tamsayı          | Evet      | Kayıt sayfalarında dizin sayısı
Öğeleri | Nesne dizisi | Evet      | Kayıt sayfaları dizisi

Dizin nesnesinin her öğesini `items` dizidir kayıt sayfasını temsil eden bir JSON nesnesi.

#### <a name="registration-page-object"></a>Kayıt sayfa nesnesi

Kayıt dizinde bulunan kayıt sayfa nesnesi, aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | Evet      | Kayıt sayfası URL'si
count  | tamsayı          | Evet      | Kayıt sayısı sayfasında bırakır.
Öğeleri  | Nesne dizisi | Yok       | Kayıt bırakır ve ilişkilendirme meta verilerinin dizisi
Daha düşük  | dize           | Evet      | En düşük SemVer 2.0.0 sürümü (kapsamlı) sayfasındaki
Üst | dize           | Yok       | Kayıt dizini URL'si
üst  | dize           | Evet      | En yüksek SemVer 2.0.0 sürümü (kapsamlı) sayfasındaki

`lower` Ve `upper` sayfasında nesnenin sınırları, belirli bir sayfaya sürümü için meta verileri gerektiğinde kullanışlıdır.
Bu sınırlar, gerekli yalnızca kayıt sayfasına getirmek için kullanılabilir. Sürüm dizeleri izliyor [NuGet sürümü kurallarını](../reference/package-versioning.md). Sürüm dizeleri normalleştirilir ve derleme meta verileri içermez. NuGet ekosisteminde tüm sürümleri ile birlikte kullanarak sürüm dizeleri karşılaştırma uygulandığı şekilde [2.0.0's SemVer sürümü öncelik kuralları](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Özelliği yalnızca görünür kayıt sayfasına nesneye sahipse `items` özelliği.

Varsa `items` özelliği kayıt sayfası nesne mevcut değil, URL belirtilen `@id` tek tek Paket sürümlerini hakkındaki meta verileri getirmek için kullanılmalıdır. `items` Dizi bir iyileştirme olarak sayfa nesnesinden bazen çıkarılır. Tek bir paket kimliği sürüm sayısı çok büyük ise, kayıt dizin belge çok büyük ve yalnızca belirli bir sürüm veya küçük bir aralık sürümleri hakkında önemli bir istemci için işleme kısıp olacaktır.

Unutmayın `items` özelliği varsa `@id` özelliği kullanılamaz, tüm sayfa verileri olduğundan zaten içinde satır içine alınmış `items` özelliği.

Sayfa nesnesinin her öğesini `items` dizidir kayıt yaprak temsil eden bir JSON nesnesi ve ilişkili meta verileri.

#### <a name="registration-leaf-object-in-a-page"></a>Kayıt yaprak nesneyi sayfasındaki

Bir kayıt sayfasında bulunan kayıt yaprak nesne, aşağıdaki özelliklere sahiptir:

Ad           | Tür   | Gerekli | Notlar
-------------- | ------ | -------- | -----
@id            | dize | Evet      | Kayıt yaprak URL'si
catalogEntry   | nesne | Evet      | Paket meta verileri içeren bir katalog girişi
packageContent | dize | Evet      | Paket içeriğini (.nupkg) URL'si

Her kayıt yaprak nesnesini tek bir paket sürümü ile ilişkili verileri temsil eder.

#### <a name="catalog-entry"></a>Katalog girişi

`catalogEntry` Kayıt yaprak nesnedeki bir özellik, aşağıdaki özelliklere sahiptir:

Ad                     | Tür                       | Gerekli | Notlar
------------------------ | -------------------------- | -------- | -----
@id                      | dize                     | Evet      | Bu nesne oluşturmak için kullanılan belgesi URL'si
Yazarları                  | dize veya dize dizisi | Yok       | 
dependencyGroups         | Nesne dizisi           | Yok       | Hedef framework tarafından gruplandırılmış paket bağımlılıkları
açıklama              | dize                     | Yok       | 
IconUrl                  | dize                     | Yok       | 
kimlik                       | dize                     | Evet      | Paket kimliği
LicenseUrl               | dize                     | Yok       | 
listelenen                   | Boole değeri                    | Yok       | Listelenen çalıştırıyorsa olarak düşünülmelidir
MinClientVersion         | dize                     | Yok       | 
ProjectUrl               | dize                     | Yok       | 
Yayımlanan                | dize                     | Yok       | Paketin ne zaman yayımlandı, bir ISO 8601 zaman damgası içeren bir dize
RequireLicenseAcceptance | Boole değeri                    | Yok       | 
özet                  | dize                     | Yok       | 
etiketler                     | dize veya dize dizisi  | Yok       | 
Başlık                    | dize                     | Yok       | 
sürüm                  | dize                     | Evet      | Normalleştirme sonra tam sürüm dizesi

Paket `version` tam sürüm dizesi sonra normalleştirme özelliğidir. Bu, SemVer 2.0.0 yapılandırma verilerini buraya dahil olabileceğini anlamına gelir.

`dependencyGroups` Özelliğidir paketin hedef framework tarafından gruplandırılmış bağımlılıkları temsil eden nesneler dizisi. Paket bağımlılıkları hakkında daha fazla varsa `dependencyGroups` özelliği eksik, boş bir dizi veya `dependencies` tüm grupların özelliği boş veya eksik.

#### <a name="package-dependency-group"></a>Paket bağımlılık grubu

Her bağımlılık grup nesnesi, aşağıdaki özelliklere sahiptir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
targetFramework | dize           | Yok       | Bu bağımlılıklar için geçerli olan hedef çerçeve
bağımlılıklar    | Nesne dizisi | Yok       |

`targetFramework` NuGet'ın .NET kitaplığı tarafından uygulanan biçim dizesini kullanır [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Hayır ise `targetFramework` belirtilirse, bağımlılık grubunun tüm hedef çerçeveler için geçerlidir.

`dependencies` Her bir paket bağımlılığı geçerli paketin temsil eden bir nesne dizisi, bir özelliktir.

#### <a name="package-dependency"></a>Paket bağımlılığı

Her paket bağımlılığı aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
kimlik           | dize | Evet      | Paket bağımlılık kimliği
aralık        | nesne | Yok       | İzin verilen [sürüm aralığı](../reference/package-versioning.md#version-ranges-and-wildcards) bağımlılık
kayıt | dize | Yok       | Bu bağımlılık kaydını dizini URL'si

Varsa `range` özelliği çıkarılır ya da boş bir dize sürüm aralığı için varsayılan istemci `(, )`. Diğer bir deyişle, herhangi bir bağımlılığın sürümü izin verilir.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

Tek tek Paket sürümlerini hakkındaki meta verileri getirmek için hiçbir ek istekler gerekeceğinden bu nedenle bu durumda, satır içine alınmış kayıt sayfasına kayıt dizini içeriyor.

## <a name="registration-page"></a>Kayıt sayfası

Kayıt sayfasına kaydı bırakır içerir. Bir kayıt sayfasına getirilecek URL tarafından belirlenir `@id` özelliğinde [kayıt sayfa nesnesi](#registration-page-object) yukarıda belirtilen.

Zaman `items` dizi kayıt dizin sağlanmadıysa, HTTP GET isteği `@id` kökü olarak bir nesne içeren bir JSON belgesi değeri döndürür. Nesne, aşağıdaki özelliklere sahiptir:

Ad   | Tür             | Gerekli | Notlar
------ | ---------------- | -------- | -----
@id    | dize           | Evet      | Kayıt sayfası URL'si
count  | tamsayı          | Evet      | Kayıt sayısı sayfasında bırakır.
Öğeleri  | Nesne dizisi | Evet      | Kayıt bırakır ve ilişkilendirme meta verilerinin dizisi
Daha düşük  | dize           | Evet      | En düşük SemVer 2.0.0 sürümü (kapsamlı) sayfasındaki
Üst | dize           | Evet      | Kayıt dizini URL'si
üst  | dize           | Evet      | En yüksek SemVer 2.0.0 sürümü (kapsamlı) sayfasındaki

Kayıt yaprak nesnelerin şeklini kayıt dizini ile aynı olduğu [yukarıda](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Kayıt yaprak

Kayıt yaprak belirli bir paket kimliği ve sürüm hakkında bilgi içerir. Bu belgede belirli bir sürüm hakkındaki meta veriler kullanılamayabilir. Paket meta verileri getirilen gelen [kayıt dizin](#registration-index) veya [kayıt sayfasına](#registration-page) (hangi bulunan kayıt dizini kullanarak).

Bir kayıt yaprak getirilecek URL'yi elde edilen `@id` kayıt dizini veya kayıt sayfasına bir kayıt yaprak nesnesinin özelliği.

Kayıt, aşağıdaki özelliklere sahip bir kök nesnesi içeren bir JSON belgesi dağıtımdır:

Ad           | Tür    | Gerekli | Notlar
-------------- | ------- | -------- | -----
@id            | dize  | Evet      | Kayıt yaprak URL'si
catalogEntry   | dize  | Yok       | Üretilen bu yaprak katalog girişi URL'si
listelenen         | Boole değeri | Yok       | Listelenen çalıştırıyorsa olarak düşünülmelidir
packageContent | dize  | Yok       | Paket içeriğini (.nupkg) URL'si
Yayımlanan      | dize  | Yok       | Paketin ne zaman yayımlandı, bir ISO 8601 zaman damgası içeren bir dize
kayıt   | dize  | Yok       | Kayıt dizini URL'si

> [!Note]
> Nuget.org, `published` değeri 1900 paketi olduğunda listelenmemiş yıl için ayarlanır.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
