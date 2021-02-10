---
title: Katalog kaynağı, NuGet v3 API
description: Katalog, nuget.org üzerinde oluşturulan ve silinen tüm paketlerin bir dizinidir.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990142"
---
# <a name="catalog"></a>Katalog

**Katalog** , tüm paket işlemlerini oluşturma ve silme gibi bir paket kaynağında kaydeden bir kaynaktır. Katalog kaynağı `Catalog` [hizmet dizininde](service-index.md)türü vardır. Bu kaynağı, [yayımlanan tüm paketleri sorgulamak](../guides/api/query-for-all-published-packages.md)için kullanabilirsiniz.

> [!Note]
> Katalog resmi NuGet istemcisi tarafından kullanılmadığından, tüm paket kaynakları kataloğu uygulamaz.

> [!Note]
> Şu anda nuget.org kataloğu Çin 'de kullanılamaz. Daha ayrıntılı bilgi için bkz. [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@type deeri   | Notlar
------------- | -----
Katalog/3.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Ler için giriş noktası URL 'SI, `@id` belirtilen kaynak değerleriyle ilişkili özelliğin değeridir `@type` . Bu konu, yer tutucu URL 'sini kullanır `{@id}` .

## <a name="http-methods"></a>HTTP yöntemleri

Katalog kaynağında bulunan tüm URL 'Ler yalnızca HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="catalog-index"></a>Katalog dizini

Katalog dizini, katalog öğeleri listesi olan, kronolojik olarak sıralanmış, iyi bilinen bir konumda yer alan bir belgedir. Bu, Katalog kaynağının giriş noktasıdır.

Dizin, Katalog sayfalarından oluşur. Her Katalog sayfası Katalog öğelerini içerir. Her katalog öğesi, zaman içinde tek bir paket ile ilgili bir olayı temsil eder. Katalog öğesi, paket kaynağından oluşturulan, listelenmemiş, yeniden listelenen veya silinen bir paketi temsil edebilir. İstemci, katalog öğelerini kronolojik sırada işleyerek, V3 paket kaynağında bulunan her paketin güncel bir görünümünü oluşturabilir.

Kısaca, Katalog Blobları aşağıdaki hiyerarşik yapıya sahiptir:

- **Dizin**: Katalog için giriş noktası.
- **Sayfa**: Katalog öğelerinin gruplandırması.
- **Yaprak**: tek bir paketin durumunun anlık görüntüsü olan bir katalog öğesini temsil eden bir belge.

Her Katalog nesnesi, `commitTimeStamp` öğenin kataloğa eklendiği zaman temsil eden adında bir özelliğe sahiptir. Katalog öğeleri, işlemeler adlı toplu işlerle bir katalog sayfasına eklenir. Aynı işlemede bulunan tüm katalog öğeleri aynı COMMIT timestamp ( `commitTimeStamp` ) ve COMMıT ID () ile aynıdır `commitId` . Aynı işlemeye yerleştirilmiş katalog öğeleri, paket kaynağında aynı noktada gerçekleşen olayları temsil eder. Katalog yürütmesi içinde sıralama yoktur.

Her paket KIMLIĞI ve sürümü benzersiz olduğundan, bir yürütmede hiç bir katalog öğesi olmayacaktır. Bu, tek bir paket için Katalog öğelerinin, tamamlama zaman damgasına göre her zaman kesin bir şekilde sıralanmasını sağlar.

Her ne kadar kataloğa birden fazla kayıt yoktur `commitTimeStamp` . Diğer bir deyişle, `commitId` ile birlikte gereksizdir `commitTimeStamp` .

Paket KIMLIĞI tarafından dizin oluşturulan [paket meta verileri kaynağının](registration-base-url-resource.md)aksine, Katalog yalnızca zamana göre dizine alınır (ve sorgulanabilir).

Katalog öğeleri her zaman kataloğa tek bir artan, kronolojik sırada eklenir. Yani, Katalog yürütmesi X ' te eklenirse, hiçbir katalogda X değerinden küçük veya buna eşit bir zamana kadar hiçbir katalog yürütmesi eklenmez.

Aşağıdaki istek Katalog dizinini getirir.

```
GET {@id}
```

Katalog dizini, aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
CommitId        | string           | evet      | En son işlemeden ilişkili benzersiz bir KIMLIK
commitTimeStamp | string           | evet      | En son kaydetmenin zaman damgası
count           | tamsayı          | evet      | Dizindeki sayfa sayısı
öğeler           | nesne dizisi | evet      | Her nesne, bir sayfayı temsil eden nesneler dizisi

Dizideki her öğe `items` , her sayfa hakkında en az ayrıntı içeren bir nesnedir. Bu sayfa nesneleri, Katalog yaprakları (öğeler) içermez. Bu dizideki öğelerin sırası tanımlı değil. Sayfalar, özelliği kullanılarak bellekte istemci tarafından sıralanabilir `commitTimeStamp` .

Yeni sayfalar tanıtıldığında, `count` artırılır ve yeni nesneler dizi içinde görüntülenir `items` .

Kataloğa öğeler eklendikçe, Dizin `commitId` değişir ve `commitTimeStamp` artar. Bu iki özellik temelde tüm sayfa `commitId` ve dizideki değerlerin bir özetidir `commitTimeStamp` `items` .

### <a name="catalog-page-object-in-the-index"></a>Dizindeki Katalog sayfası nesnesi

Katalog dizininin özelliğinde bulunan Katalog sayfası nesneleri `items` aşağıdaki özelliklere sahiptir:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | string  | evet      | Kullanılacak Katalog sayfası URL 'SI
CommitId        | string  | evet      | Bu sayfadaki en son işlemeden ilişkili benzersiz bir KIMLIK
commitTimeStamp | string  | evet      | Bu sayfadaki en son yürütmenin zaman damgası
count           | tamsayı | evet      | Katalog sayfasındaki öğelerin sayısı

Bazı durumlarda, bazı durumlarda yer alabilen [paket meta veri kaynağının](registration-base-url-resource.md) aksine, Katalog ayrılmaları hiçbir zaman dizine alınmayacak ve sayfanın URL 'si kullanılarak her zaman alınmalıdır `@id` .

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Katalog sayfası

Katalog sayfası, Katalog öğelerinin bir koleksiyonudur. Bu, `@id` Katalog dizininde bulunan değerlerden biri kullanılarak getirilen bir belgedir. Bir katalog sayfasının URL 'SI öngörülebilir hale gelmelidir ve yalnızca katalog dizini kullanılarak keşfedilmelidir.

Yeni katalog öğeleri, Katalog dizinindeki sayfaya yalnızca en yüksek tamamlama zaman damgasıyla veya yeni bir sayfaya eklenir. Kataloğa daha yüksek bir kayıt zaman damgası eklenmiş bir sayfa eklendikten sonra, eski sayfalar hiçbir zaman eklenmez veya değiştirilmez.

Katalog sayfası belgesi, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
CommitId        | string           | evet      | Bu sayfadaki en son işlemeden ilişkili benzersiz bir KIMLIK
commitTimeStamp | string           | evet      | Bu sayfadaki en son yürütmenin zaman damgası
count           | tamsayı          | evet      | Sayfadaki öğelerin sayısı
öğeler           | nesne dizisi | evet      | Bu sayfadaki katalog öğeleri
üst          | string           | evet      | Katalog dizininin URL 'SI

Dizideki her öğe, `items` Katalog öğesiyle ilgili bazı en az ayrıntı içeren bir nesnedir. Bu öğe nesneleri tüm katalog öğesi verilerini içermez. Sayfa dizisindeki öğelerin sırası `items` tanımlı değil. Öğeler, özelliği kullanılarak bellekte istemci tarafından sıralanabilir `commitTimeStamp` .

Bir sayfadaki Katalog öğelerinin sayısı sunucu uygulamasına göre tanımlanır. Nuget.org için, her sayfada en fazla 550 öğe bulunur, ancak bir sonraki kaydetme toplu işinin boyutuna bağlı olarak bazı sayfalarda gerçek sayı daha küçük olabilir.

Yeni öğeler tanıtıldığında, `count` artırılır ve yeni katalog öğesi nesneleri `items` dizide görüntülenir.

Sayfaya öğeler eklendikçe, `commitId` değişiklikler ve `commitTimeStamp` artışlar artar. Bu iki özellik temelde `commitId` dizideki tüm ve değerlerin bir özetidir `commitTimeStamp` `items` .

### <a name="catalog-item-object-in-a-page"></a>Sayfada Katalog öğesi nesnesi

Katalog sayfasının özelliğinde bulunan katalog öğesi nesneleri `items` aşağıdaki özelliklere sahiptir:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | string  | evet      | Katalog öğesini getirecek URL
@type           | string  | evet      | Katalog öğesinin türü
CommitId        | string  | evet      | Bu katalog öğesiyle ilişkili kayıt KIMLIĞI
commitTimeStamp | string  | evet      | Bu katalog öğesinin teslim zaman damgası
NuGet: kimlik        | string  | evet      | Bu yaprağın ilişkili olduğu paket KIMLIĞI
NuGet: sürüm   | string  | evet      | Bu yaprağın ilişkili olduğu paket sürümü

`@type`Değer aşağıdaki iki değerden biri olacaktır:

1. `nuget:PackageDetails`: Bu `PackageDetails` , Katalog yaprak belgesindeki türe karşılık gelir.
1. `nuget:PackageDelete`: Bu, `PackageDelete` Katalog yaprak belgesindeki türe karşılık gelir.

Her türün anlamı hakkında daha fazla ayrıntı için aşağıdaki [ilgili öğe türüne](#item-types) bakın.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog yaprağı

Katalog yaprağı, belirli bir paket KIMLIĞI ve sürümü hakkında belirli bir zamanda meta veriler içerir. Bu, `@id` bir katalog sayfasında bulunan değer kullanılarak getirilen bir belgedir. Katalog yaprağın URL 'SI öngörülebilir hale gelmelidir ve yalnızca bir katalog sayfası kullanılarak keşfedilmelidir.

Katalog yaprak belgesi, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
@type                   | dizelerin dizesi veya dizisi | evet      | Katalog öğesinin türleri
Katalog: CommitId        | string                     | evet      | Bu katalog öğesiyle ilişkili bir kayıt KIMLIĞI
Katalog: commitTimeStamp | string                     | evet      | Bu katalog öğesinin teslim zaman damgası
kimlik                      | string                     | evet      | Katalog öğesinin paket KIMLIĞI
yayımladığı               | string                     | evet      | Paket kataloğu öğesinin Yayımlanma tarihi
sürüm                 | string                     | evet      | Katalog öğesinin paket sürümü

### <a name="item-types"></a>Öğe türleri

`@type`Özelliği dize veya dizeler dizisidir. Kolaylık olması için, `@type` değer bir dize ise, tek bir boyut dizisi olarak değerlendirilmelidir. İçin olası tüm değerler `@type` açıklanmamıştır. Ancak, her bir katalog öğesi aşağıdaki iki dize türü değerinden tam olarak birine sahiptir:

1. `PackageDetails`: paket meta verilerinin anlık görüntüsünü temsil eder
1. `PackageDelete`: silinen bir paketi temsil eder

### <a name="package-details-catalog-items"></a>Paket ayrıntıları katalog öğeleri

Türüne sahip katalog öğeleri, `PackageDetails` belirli bir paket (ID ve Version birleşimi) için paket meta verilerinin anlık görüntüsünü içerir. Paket ayrıntıları Katalog öğesi, bir paket kaynağı aşağıdaki senaryolarla karşılaştığında üretilir:

1. Bir paket **gönderilir**.
1. Bir paket **listelenir**.
1. Bir paket **listelenmemiş**.
1. Bir paket yeniden **akıtılmış**.

Paket yeniden akışı, aslında paketin kendisinde değişiklik yapmadan mevcut bir paketin sahte bir şekilde gönderimi üreten bir yönetim hareketidir. Nuget.org üzerinde, Katalog kullanan arka plan işlerinin birindeki bir hata düzeltildikten sonra bir yeniden akıtma kullanılır.

Katalog öğelerini kullanan istemciler, bu senaryoların Katalog öğesi ürettiğini belirlemeyi denememelidir. Bunun yerine, istemci, Katalog öğesinde bulunan meta veriler ile yalnızca korunan görünüm veya dizini güncelleştirmelidir. Ayrıca, yinelenen veya yedekli Katalog öğelerinin düzgün şekilde işlenmesi gerekir (idempotently).

Paket ayrıntıları katalog öğeleri, [Tüm kataloglarda içerilenlere](#catalog-leaf)ek olarak aşağıdaki özelliklere sahiptir.

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
düzenliyor                 | string                     | hayır       |
yaratıl                 | string                     | hayır       | Paketin ilk oluşturulduğu zaman damgası. Geri dönüş özelliği: `published` .
dependencyGroups        | nesne dizisi           | hayır       | Hedef çerçeveye göre gruplandırılan paketin bağımlılıkları ([paket meta verileri kaynağıyla aynı biçimde](registration-base-url-resource.md#package-dependency-group))
kullanımdan kaldırma             | object                     | hayır       | Paketle ilişkili kullanımdan kaldırma ([paket meta verileri kaynağıyla aynı biçimde](registration-base-url-resource.md#package-deprecation))
açıklama             | string                     | hayır       |
Iurl                 | string                     | hayır       |
IBir ön sürüm            | boolean                    | hayır       | Paket sürümünün ön sürüm olup olmadığı. , Öğesinden algılanabilir `version` .
language                | string                     | hayır       |
licenseUrl              | string                     | hayır       |
listelenen                  | boolean                    | hayır       | Paketin listede olup olmadığı
minClientVersion        | string                     | hayır       |
packageHash             | string                     | evet      | [Standart temel 64](https://tools.ietf.org/html/rfc4648#section-4) kullanılarak kodlama, paketin karması
packageHashAlgorithm    | string                     | evet      |
packageSize             | tamsayı                    | evet      | Paketin bayt cinsinden boyutu. nupkg
packageTypes            | nesne dizisi           | hayır       | Yazar tarafından belirtilen paket türleri.
projectUrl              | string                     | hayır       |
relet 'ler            | string                     | hayır       |
requireLicenseAgreement | boolean                    | hayır       | `false`Dışlandığını varsay
Özet                 | string                     | hayır       |
etiketler                    | dize dizisi           | hayır       |
başlık                   | string                     | hayır       |
verbatimVersion         | string                     | hayır       | Özgün sürüm dizesi. nuspec içinde bulunur
'teki         | nesne dizisi           | hayır       | Paketin güvenlik açıkları

Package `version` özelliği, normalleştirmenin ardından tam sürüm dizesidir. Bu, SemVer 2.0.0 derleme verilerinin buraya dahil edileceğini gösterir.

`created`Zaman damgası, paketin paket kaynağı tarafından ilk kez alındığı, genellikle Katalog öğesinin kayıt zaman damgasından önceki kısa bir süre olan zaman damgasıdır.

, `packageHashAlgorithm` Oluşturmak için kullanılan karma algoritmasını temsil eden sunucu uygulamasıyla tanımlanan bir dizedir `packageHash` . nuget.org her zaman `packageHashAlgorithm` değerini kullandı `SHA512` .

`packageTypes`Özelliği yalnızca yazar tarafından bir paket türü belirtilmişse mevcut olacaktır. Varsa, her zaman en az bir (1) girişi olur. Dizideki her öğe, `packageTypes` aşağıdaki özelliklere sahip BIR JSON nesnesidir:

Ad      | Tür    | Gerekli | Notlar
--------- | ------- | -------- | -----
name      | string  | evet      | Paket türünün adı.
sürüm    | string  | hayır       | Paket türünün sürümü. Yalnızca yazarı nuspec içinde açıkça bir sürüm belirtmişse vardır.

`published`Zaman damgası, paketin en son listelenme zamanı olur.

> [!Note]
> Nuget.org 'de, `published` paket listelenmemiş olduğunda değer 1900 yılına ayarlanır.

#### <a name="vulnerabilities"></a>Güvenlik Açıkları

`vulnerability`Nesne dizisi. Her güvenlik açığı aşağıdaki özelliklere sahiptir:

Ad         | Tür   | Gerekli | Notlar
------------ | ------ | -------- | -----
Danışmanorrivurl 'Si  | string | evet      | Paketin Güvenlik Danışma belgesi konumu
önem derecesi     | string | evet      | Danışmanlık önem derecesi: "0" = düşük, "1" = Orta, "2" = yüksek, "3" = kritik

`severity`Özellik burada listelenenlerden farklı değerler içeriyorsa, danışmanlık 'nın önem derecesi düşük olarak değerlendirilir.

#### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Paket katalog öğelerini Sil

Türüne sahip katalog öğeleri, `PackageDelete` Katalog istemcilerinin paket kaynağından silindiğini ve hiçbir paket işlemi için (geri yükleme gibi) artık kullanılabilir olmadığını gösteren en az bir bilgi kümesi içerir.

> [!NOTE]
> Bir paketin silinmesi ve daha sonra aynı paket KIMLIĞI ve sürümü kullanılarak yeniden yayımlanması mümkündür. Nuget.org 'de, bu, resmi istemcinin bir paket KIMLIĞI ve sürümünün belirli bir paket içeriğini olduğunu varsayımını kesen çok nadir bir durumdur. Nuget.org üzerinde paket silme hakkında daha fazla bilgi için, [ilkenize](../nuget-org/policies/deleting-packages.md)bakın.

Paket silme kataloğu öğeleri, [Tüm katalogların dahil](#catalog-leaf)edilenlere ek özellikler içermez.

`version`Özelliği,. nuspec paketinde bulunan özgün sürüm dizesidir.

`published`Özelliği, paketin silindiği zaman, genellikle Katalog öğesinin kayıt zaman damgasından önceki kısa bir süredir.

#### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Oraya

### <a name="overview"></a>Genel Bakış

Bu bölümde, protokol tarafından uygulanan olmasa da hiçbir pratik Katalog istemci uygulamasının bir parçası olması gereken bir istemci kavramı açıklanmaktadır.

Katalog zamana göre dizini oluşturulmuş bir yalnızca Append veri yapısı olduğundan, istemci bir **imleci** yerel olarak depolamalıdır ve bu, istemcinin katalog öğelerini işlediği zaman noktasını temsil eder. Bu imleç değerinin, istemcinin makine saati kullanılarak hiçbir zaman oluşturulmaması gerektiğini unutmayın. Bunun yerine, değer bir katalog nesnesinin `commitTimestamp` değerinden gelmelidir.

İstemci, paket kaynağında yeni olayları her işlemek istediğinde, yalnızca saklı imleinden daha büyük bir işleme zaman damgasına sahip tüm Katalog öğelerinin kataloğunu sorgulamak gerekir. İstemci tüm yeni katalog öğelerini başarılı bir şekilde işledikten sonra, yeni imleç değeri olarak yalnızca işlenen Katalog öğelerinin en son işleme zaman damgasını kaydeder.

Bu yaklaşımı kullanarak istemci, paket kaynağında gerçekleşen paket olaylarını hiçbir şekilde kaçırmamak olabilir.
Ayrıca, istemci, imlecin kayıtlı işleme zaman damgasından önce eski olayları yeniden işlemesini istemez.

Bu güçlü işaretçiler kavramı birçok nuget.org arka plan işi için kullanılır ve v3 API 'sinin kendisini güncel tutmak için kullanılır. 

### <a name="initial-value"></a>İlk değer

Katalog istemcisi çok ilk kez başlatıldığında (ve dolayısıyla hiçbir imleç değeri yoksa) varsayılan bir imleç değeri kullanmalıdır. NET `System.DateTimeOffset.MinValue` veya bazı benzer en düşük gösterilebilir tablo zaman damgası kavramı.

### <a name="iterating-over-catalog-items"></a>Katalog öğeleri üzerinde yineleme

İşlenecek bir sonraki katalog öğeleri kümesini sorgulamak için, istemci şunları sağlamalıdır:

1. Kayıtlı imleç değerini yerel bir mağazadan getirin.
1. Katalog dizinini indirin ve serisini kaldırma.
1. Kayıt zaman *damgasından daha büyük* olan tüm katalog sayfalarını bulun.
1. İşlenecek Katalog öğelerinin boş bir listesini bildirin.
1. Adım 3 ' te eşleşen her bir katalog sayfası için:
   1. Katalog sayfasını indirin ve seri durumdan çıkarılın.
   1. Kayıt zaman *damgasından daha büyük* olan tüm katalog öğelerini bulun.
   1. Tüm eşleşen katalog öğelerini 4. adımda belirtilen listeye ekleyin.
1. Katalog öğesi listesini, COMMIT zaman damgasıyla sıralayın.
1. Her Katalog öğesini sırayla işle:
   1. Katalog öğesini indirin ve serisini kaldırma.
   1. Katalog öğesinin türüne uygun şekilde tepki verir.
   1. Katalog öğesi belgesini istemciye özgü bir biçimde işleyin.
1. Son Katalog öğesinin kaydetme zaman damgasını yeni imleç değeri olarak kaydedin.

Bu temel algoritmayla istemci uygulama, paket kaynağında bulunan tüm paketlerin tümüyle bir görünümünü oluşturabilir. İstemci yalnızca paket kaynağına yapılan en son değişiklikleri her zaman farkında olmak için bu algoritmayı düzenli aralıklarla yürütmelidir.

> [!Note]
> Bu, nuget.org 'in [paket meta verilerini](registration-base-url-resource.md), [paket içeriğini](package-base-address-resource.md), [arama](search-query-service-resource.md) [ve kaynakları](search-autocomplete-service-resource.md) güncel tutmak için kullandığı algoritmadır.

### <a name="dependent-cursors"></a>Bağımlı imleçler

Bir istemcinin çıktısının başka bir istemcinin çıkışına bağlı olduğu bir açık bağımlılığı olan iki Katalog istemcisi olduğunu varsayalım. 

#### <a name="example"></a>Örnek

Örneğin, nuget.org üzerinde yeni yayınlanan bir paket, paket meta verileri kaynağında görüntülenmeden önce arama kaynağında görünmemelidir. Bunun nedeni, resmi NuGet istemcisi tarafından gerçekleştirilen "geri yükleme" işleminin paket meta veri kaynağını kullanmamesinden kaynaklanır. Bir müşteri, arama hizmetini kullanarak bir paket saptadıysanız, paket meta verileri kaynağını kullanarak bu paketi başarıyla geri yükleyebilmelidir. Diğer bir deyişle, arama kaynağı paket meta veri kaynağına bağlıdır. Her kaynakta, bu kaynağı güncelleştiren bir katalog istemci arka plan işi vardır. Her istemcinin kendi imleci vardır.

Her iki kaynak de kataloğun yerleşik olduğundan, arama kaynağını güncelleştiren Katalog istemcisinin imleci paket meta veri kataloğu istemcisinin imlecinizin *ötesine gitmemelidir* .

#### <a name="algorithm"></a>Algoritma

Bu kısıtlamayı uygulamak için yukarıdaki algoritmayı şu şekilde değiştirmeniz yeterlidir:

1. Kayıtlı imleç değerini yerel bir mağazadan getirin.
1. Katalog dizinini indirin ve serisini kaldırma.
1. Bir tamamlama zaman damgasına sahip tüm katalog sayfalarını, **bağımlılık imlecinden küçük veya ona eşit** olan *İmleçten daha büyük* bir şekilde bulun.
1. İşlenecek Katalog öğelerinin boş bir listesini bildirin.
1. Adım 3 ' te eşleşen her bir katalog sayfası için:
   1. Katalog sayfasını indirin ve seri durumdan çıkarılın.
   1. Bir tamamlama zaman damgasına sahip tüm katalog öğelerini **, bağımlılık imlecinden küçük veya ona eşit** olan *İmleçten daha büyük* bir şekilde bulun.
   1. Tüm eşleşen katalog öğelerini 4. adımda belirtilen listeye ekleyin.
1. Katalog öğesi listesini, COMMIT zaman damgasıyla sıralayın.
1. Her Katalog öğesini sırayla işle:
   1. Katalog öğesini indirin ve serisini kaldırma.
   1. Katalog öğesinin türüne uygun şekilde tepki verir.
   1. Katalog öğesi belgesini istemciye özgü bir biçimde işleyin.
1. Son Katalog öğesinin kaydetme zaman damgasını yeni imleç değeri olarak kaydedin.

Bu değiştirilmiş algoritmayı kullanarak, kendilerine ait belirli dizinleri, yapıtları, vb. üreten bir bağımlı Katalog istemcileri sistemi oluşturabilirsiniz.
