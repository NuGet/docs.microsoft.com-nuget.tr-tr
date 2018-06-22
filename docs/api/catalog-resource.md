---
title: Kaynak, NuGet V3 API katalog
description: Bir dizin oluşturulur ve üzerinde nuget.org silinen tüm paketlerin kataloğudur.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8554f9515b671dbececd94a025ec7e56037c2bd9
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2018
ms.locfileid: "34152441"
---
# <a name="catalog"></a>Katalog

**Katalog** oluşturma ve silme işlemleri gibi bir paket kaynağında tüm paket işlemleri kaydeder bir kaynaktır. Katalog kaynak `Catalog` yazın [Hizmeti dizini](service-index.md).

> [!Note]
> Katalog resmi NuGet istemcisi tarafından kullanılmadığı için tüm paket kaynaklarını katalog uygulayın.

> [!Note]
> Şu anda nuget.org katalog Çin'de kullanılamaz. Daha fazla ayrıntı için bkz: [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer   | Notlar
------------- | -----
Catalog/3.0.0 | İlk sürüm

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için giriş noktası URL değeri `@id` özelliği daha önce bahsedilen kaynakla ilişkilendirilmiş `@type` değerleri. Bu konuda yer tutucu URL'yi kullanır `{@id}`.

## <a name="http-methods"></a>HTTP yöntemleri

Katalog kaynak desteği yalnızca HTTP yöntemlerini bulunan tüm URL'leri `GET` ve `HEAD`.

## <a name="catalog-index"></a>Katalog dizini

Katalog öğeleri, kronolojik olarak sıralanan listesini içeren iyi bilinen bir konumdaki bir belge katalog dizinidir. Katalog kaynağının giriş noktasıdır.

Dizin Katalog sayfaları oluşur. Her katalog sayfa katalog öğelerini içerir. Her bir katalog öğesi zamanında bir noktada tek bir paket ilgili bir olayı temsil eder. Bir katalog öğesi, paket kaynağından listelenmemiş, relisted ya da silinmiş oluşturulmuş bir paketi temsil edebilir. Katalog öğeleri kronolojik sırada işleyerek istemci V3 paket kaynağı var. her paketin güncel bir görünümü oluşturabilirsiniz.

Kısacası, katalog BLOB'ları aşağıdaki hiyerarşik bir yapı vardır:

- **Dizin**: Katalog için giriş noktası.
- **Sayfa**: Katalog öğeleri gruplandırması.
- **Yaprak**: tek bir paketin durumunun anlık görüntüsü bir katalog öğesi temsil eden bir belge.

Her bir katalog nesne adında bir özelliğe sahiptir `commitTimeStamp` öğesi kataloğa eklendiğinde temsil eden. Katalog öğeleri işlemeleri adlı toplu katalog sayfası eklenir. Aynı yürütme tüm katalog öğeleri aynı yürütme zaman damgası vardır (`commitTimeStamp`) ve kimliği kaydedilmesi (`commitId`). Katalog öğeleri aynı uygulamada yerleştirilen aynı nokta etrafında paket kaynağında zamanında gerçekleşen olayları temsil eder. İçinde bir katalog yürütme sıralamaya yoktur.

Her bir paket kimliği ve sürümünün benzersiz olduğundan, hiçbir zaman olacaktır birden fazla katalog öğesi bir yürütme. Bu, tek bir paket için katalog öğeleri her zaman belirsizliğe yürütme zaman damgası göre sıralanabilir sağlar.

Olduğundan hiç kataloğa birden fazla yürütme olması `commitTimeStamp`. Diğer bir deyişle, `commitId` ile gereksiz `commitTimeStamp`.

Tersine için [paketini meta veri kaynağı](registration-base-url-resource.md), paket kimliği tarafından dizine, katalog Dizinli (ve sorgulanabilir) yalnızca zamana göre.

Katalog öğeleri her zaman bir düz olarak artan, kronolojik sırayla Kataloğu'na eklenir. Bir katalog yürütme zaman X eklediyseniz sonra hiçbir katalog yürütme hiç eklenecek yani bir süre daha az veya bu değere eşit x ile.

Aşağıdaki isteği katalog dizinini getirir.

    GET {@id}

Aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi katalog dizinidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
commitId        | dize           | Evet      | En son işleme ile ilişkili benzersiz bir kimliği
commitTimeStamp | dize           | Evet      | En son yürütme, zaman damgası
count           | tamsayı          | Evet      | Dizindeki sayfa sayısı
Öğeleri           | Nesne dizisi | Evet      | Bir nesne dizisi, bir sayfayı temsil eden her nesnesi

Her bir öğe `items` dizidir her sayfanın en az bazı ayrıntılarını sahip bir nesne. Bu sayfa nesneler Kataloğu bırakır (öğeleri) içermez. Bu dizisindeki öğelerin sırasını tanımlı değil. Sayfalar göre sıralayarak bellek kullanarak istemci kendi `commitTimeStamp` özelliği.

Yeni sayfa sunulduğu şekilde `count` arttırılır ve yeni nesneler görünür `items` dizi.

Öğeleri katalog için dizin eklendikçe `commitId` değiştirir ve `commitTimeStamp` artmasına neden olur. Bu iki özellik temelde özeti tüm sayfanın üstünde olan `commitId` ve `commitTimeStamp` değerler `items` dizi.

### <a name="catalog-page-object-in-the-index"></a>Dizindeki katalog sayfası nesnesi

Katalog sayfa nesneleri katalog dizinin içinde bulunan `items` özelliği aşağıdaki özellikleri vardır:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | dize  | Evet      | Fetch katalog sayfası URL'si
commitId        | dize  | Evet      | Bu sayfada en son yürütme ile ilişkili benzersiz bir kimliği
commitTimeStamp | dize  | Evet      | Bu sayfada en son yürütme, zaman damgası
count           | tamsayı | Evet      | Katalog Sayfası öğelerin sayısı

Tersine için [paketini meta veri kaynağı](registration-base-url-resource.md) Inlines, bazı durumlarda dizine bırakır, katalog bırakır hiçbir zaman dizine içermesinden ve her zaman sayfanın kullanarak getirilmesi `@id` URL.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Katalog Sayfası

Katalog Sayfası, katalog öğelerini koleksiyonudur. Aşağıdakilerden birini kullanarak alınan bir belge olduğu `@id` değerleri katalog dizininde bulunamadı. Bir katalog sayfasının URL'sini tahmin edilebilir olması amaçlanmamıştır ve yalnızca katalog dizini kullanarak bulunması gerekir.

Yeni Katalog öğelerini yalnızca zaman damgalı yüksek yürütme katalog dizin sayfası veya yeni bir sayfaya eklenen. Daha yüksek bir yürütme zaman damgası içeren bir sayfa Kataloğu'na eklendikten sonra eski sayfalar hiçbir zaman eklenecek veya değiştirildi.

Katalog sayfa belge, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
commitId        | dize           | Evet      | Bu sayfada en son yürütme ile ilişkili benzersiz bir kimliği
commitTimeStamp | dize           | Evet      | Bu sayfada en son yürütme, zaman damgası
count           | tamsayı          | Evet      | Sayfadaki öğelerin sayısı
Öğeleri           | Nesne dizisi | Evet      | Bu sayfadaki katalog öğeleri
Üst          | dize           | Evet      | Katalog dizinini URL'si

Her bir öğe `items` dizidir katalog öğesi en az bazı ayrıntılarını sahip bir nesne. Bu öğe nesneler katalog öğesi'nin veri içermez. Sayfanın öğelerin sırasını `items` dizi tanımlı değil. Öğeleri göre sıralayarak bellek kullanarak istemci kendi `commitTimeStamp` özelliği.

Katalog öğeleri sayfasında sayısı sunucu uygulaması tarafından tanımlanır. Nuget.org için en fazla 550 öğeler var. her sayfasında gerçek sayı zamandaki noktasında sonraki yürütme toplu boyutuna bağlı olarak, bazı sayfaların küçük olabilir ancak.

Yeni öğeler sunulduğu şekilde `count` artırılır ve yeni katalog öğesi nesneleri görünür olan `items` dizi.

Öğeleri sayfaya eklendikçe `commitId` değişiklikleri ve `commitTimeStamp` artırır. Bu iki özellik temelde özeti tümü `commitId` ve `commitTimeStamp` değerler `items` dizi.

### <a name="catalog-item-object-in-a-page"></a>Katalog öğesi nesnesi sayfasındaki

Katalog öğesi nesneleri bulunan katalog sayfanın `items` özelliği aşağıdaki özellikleri vardır:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | dize  | Evet      | Katalog öğesi getirmek için URL
@type           | dize  | Evet      | Katalog öğesi türü
commitId        | dize  | Evet      | Bu katalog öğesi ile ilişkili yürütme kimliği
commitTimeStamp | dize  | Evet      | Bu katalog öğesinin yürütme zaman damgası
nuget:id        | dize  | Evet      | Bu yaprak ilgili paket kimliği
nuget:version   | dize  | Evet      | Bu yaprak ilgili Paket sürümü

`@type` Değer aşağıdaki iki değerden biri olacaktır:

1. `nuget:PackageDetails`: Bu karşılık `PackageDetails` katalog yaprak belge türü.
1. `nuget:PackageDelete`: Bu karşılık `PackageDelete` katalog yaprak belge türü.

Her ne tür, göreceğiniz anlamına gelir hakkında daha fazla ayrıntı için [karşılık gelen öğe türü](#item-types) aşağıda.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog yaprak

Katalog yaprak zamanında belirli paket kimliği ve sürüm, belirli bir noktada hakkındaki meta verileri içerir. Kullanarak alınan bir belge olduğu `@id` değeri bir katalog sayfası bulundu. Bir katalog yaprak URL'sine tahmin edilebilir olması amaçlanmamıştır ve yalnızca bir katalog sayfası kullanarak bulunması gerekir.

Katalog yaprak belge, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
@type                   | dize veya dize dizisi | Evet      | Katalog öğesi türleri
catalog:commitId        | dize                     | Evet      | Bu katalog öğesi ile ilişkilendirilmiş bir yürütme kimliği
catalog:commitTimeStamp | dize                     | Evet      | Bu katalog öğesinin yürütme zaman damgası
kimlik                      | dize                     | Evet      | Katalog öğesi paket kimliği
Yayımlanan               | dize                     | Evet      | Paketin yayımlanan tarih katalog öğesi
sürüm                 | dize                     | Evet      | Katalog öğesi Paket sürümü

### <a name="item-types"></a>Öğesi türleri

`@type` Özelliği olan bir dize veya dize dizisi. Kolaylık sağlamak için `@type` değeri bir dize, herhangi bir boyutu dizisi olarak değerlendirilmelidir. İçin tüm olası değerler `@type` belgelenmiştir. Bununla birlikte, her bir katalog öğesi iki aşağıdaki dize türü değerleri tam olarak birine sahip:

1. `PackageDetails`: bir anlık görüntüsünü paket meta verileri temsil eder
1. `PackageDelete`: silinmiş bir paketi temsil eder

### <a name="package-details-catalog-items"></a>Paket ayrıntılarını katalog öğeleri

Katalog öğeleri türüyle `PackageDetails` anlık görüntüsünü (kimliği ve sürüm birleşimi) belirli bir paket için paket meta verileri içerir. Aşağıdaki senaryoların herhangi biri bir paket kaynağı karşılaştığında bir paket ayrıntılarını katalog öğesi oluşturulur:

1. Bir paketi **gönderilen**.
1. Bir paketi **listelenen**.
1. Bir paketi **listelenmemiş**.
1. Bir paketi **yeniden akıtılmaz**.

Bir paket yeniden akış temelde hiçbir değişiklik olmadan var olan bir paketi paket için bir sahte itme oluşturan bir yönetici hareketi ' dir. Nuget.org üzerinde bir yeniden akış hata katalog tüketen arka plan işleri birinde düzelttikten sonra kullanılır.

Katalog öğeleri kullanan istemciler, bu senaryolarda katalog öğesi üretilen belirlemek çalışmamalısınız. Bunun yerine, istemcinin sadece herhangi bir tutulan görünüm veya dizin katalog öğesinde bulunan meta veriler ile güncelleştirmeniz gerekir. Ayrıca, yinelenen veya yedek katalog öğeleri düzgün biçimde işleneceğini (idempotently).

Paket ayrıntılarını katalog öğeleri ek olarak aşağıdaki özelliklere sahip [tüm katalog bırakır dahil](#catalog-leaf).

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
yazarları                 | dize                     | Yok       |
Oluşturulan                 | dize                     | Yok       | Paketin ilk oluşturulduğu damgası. Geri dönüş özellik: `published`.
dependencyGroups        | Nesne dizisi           | Yok       | Aynı biçimi olarak [paketini meta veri kaynağı](registration-base-url-resource.md#package-dependency-group)
açıklama             | dize                     | Yok       |
iconUrl                 | dize                     | Yok       |
isPrerelease            | Boole değeri                    | Yok       | Olsun veya olmasın paket yayın öncesi sürümüdür. Gelen algılanan `version`.
dil                | dize                     | Yok       |
licenseUrl              | dize                     | Yok       |
listelenen                  | Boole değeri                    | Yok       | Paket listede olmayan
MinClientVersion        | dize                     | Yok       |
packageHash             | dize                     | Evet      | Kullanarak kodlama paket karmasını [standart base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | dize                     | Evet      |
packageSize             | tamsayı                    | Evet      | Paket .nupkg bayt cinsinden boyutu
projectUrl              | dize                     | Yok       |
ReleaseNotes            | dize                     | Yok       |
requireLicenseAgreement | Boole değeri                    | Yok       | Varsayın `false` dışlanan varsa
özet                 | dize                     | Yok       |
etiketler                    | Dize dizisi           | Yok       |
Başlık                   | dize                     | Yok       |
verbatimVersion         | dize                     | Yok       | Sürüm dizesi olarak başlangıçta .nuspec bulundu

Paket `version` tam, normalleştirilmiş sürüm dizesi bir özelliktir. Bu SemVer 2.0.0 yapılandırma verilerini buraya dahil olabileceği anlamına gelir.

`created` Paket ilk katalog öğesi'nin yürütme zaman damgası önce kısa bir süre genellikle olan paket kaynak tarafından alındığını zaman damgası olduğunda.

`packageHashAlgorithm` Üretmek için kullanılan karma algoritma temsil eden sunucu uygulaması tarafından tanımlanan bir dizedir `packageHash`. her zaman kullanılan nuget.org `packageHashAlgorithm` değerini `SHA512`.

`published` Zaman damgası, zaman son dosyasında listelenen paketin süre.

> [!Note]
> Nuget.org üzerinde `published` değeri paket olduğunda listelenmemiş yılına 1900 ayarlanır.

#### <a name="sample-request"></a>Örnek istek

AL https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Paket katalog öğeleri silme

Katalog öğeleri türüyle `PackageDelete` katalog istemcilere bir paketi paket kaynağından silindi ve herhangi bir paket işlemi (örneğin, geri yükleme) artık kullanılabilir olduğunu gösteren bilgiler en az bir kümesini içerir.

> [!Note]
> Silinecek paket ve aynı paketi Kimliğini ve sürümünü kullanarak, daha sonra yeniden yayımlanması için mümkündür. Bir paket kimliği ve sürüm belirli paket içeriğini kapsıyor resmi istemcinin varsayım sonları gibi nuget.org üzerinde bu çok nadir durumdur. Nuget.org paketi silme hakkında daha fazla bilgi için bkz: [ilkemize](../policies/deleting-packages.md).

Paket Sil katalog öğeleri sahip herhangi bir ek özellik listelenenlere [tüm katalog bırakır dahil](#catalog-leaf).

`version` Özelliktir özgün sürüm dizesi paketi .nuspec bulunamadı.

`published` Özelliği, genellikle olan kısa süre önce katalog öğesi'nin yürütme zaman damgası olarak ne zaman paket silindi, süre.

#### <a name="sample-request"></a>Örnek istek

AL https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>İmleç

### <a name="overview"></a>Genel Bakış

Bu bölümde, mutlaka protokolü tarafından zorunlu değildir ancak herhangi bir pratik katalog istemci uygulaması bir parçası olması gereken bir istemci kavramı açıklanmaktadır.

Katalog zamanına göre dizine yalnızca append veri yapısı olduğundan, istemci saklamalısınız bir **imleç** ne zaman içinde istemci noktası kadar temsil eden katalog öğeleri yerel olarak işledi. Bu imleç değeri hiçbir zaman istemcinin makine saatini kullanarak oluşturulsun mu olduğunu unutmayın. Bunun yerine, bir katalog nesnesinin değer gelmelidir `commitTimestamp` değeri.

İstemci paket kaynağının yeni olayları işlemek istediği her zaman, gerek yalnızca sorgu katalog bir yürütme zaman damgasına sahip tüm katalog öğeleri için saklı imleç büyüktür. İstemci başarıyla tüm yeni katalog öğeleri işledikten sonra katalog öğelerini yalnızca yeni imleç değer olarak işlenen son yürütme zaman damgasını kaydeder.

Bu yaklaşımı kullanarak, istemci hiçbir zaman paket kaynağında oluşan herhangi bir paket olayı kaçırılması emin olabilirsiniz.
Ayrıca, istemci, eski olayları imlecin kaydedilmiş yürütme zaman damgası önce yeniden işlemek hiçbir zaman vardır.

Bu güçlü kavramı imleçler, birçok nuget.org arka plan işleri için kullanılır ve V3 API güncel tutmak için kullanılır. 

### <a name="initial-value"></a>Başlangıç değeri

Katalog istemci çok ilk kez başlangıç (ve bu nedenle hiçbir imleç değerine sahip olduğunda), varsayılan imleç değerini kullanmanız gerekir. NET'in `System.DateTimeOffset.MinValue` veya bazı böyle benzer kavramı minimum gösterilebilir zaman damgası.

### <a name="iterating-over-catalog-items"></a>Katalog öğeleri yineleme yapma

Sonraki işlemek için katalog öğeleri kümesi için sorgu için istemci gerekir:

1. Kaydedilen imleci değer yerel depodan getirin.
1. Karşıdan yükle ve Katalog dizinini seri durumdan.
1. Tüm katalog yürütme zaman damgası sayfalarıyla Bul *büyük* imleci.
1. İşlem için katalog öğeleri listesi boş bildirin.
1. 3. adımda eşleşen her katalog sayfası için:
   1. Karşıdan yükle ve Katalog Sayfası seri.
   1. Tüm katalog öğeleri yürütme zaman damgası ile Bul *büyük* imleci.
   1. Tüm eşleşen katalog öğeleri 4. adımda bildirilen listesine ekleyin.
1. Katalog öğesi listesi yürütme zaman damgası göre sıralayın.
1. Her bir katalog öğesi sırayla işlemini:
   1. Karşıdan yükle ve katalog öğesi seri durumdan.
   1. Katalog öğesi'nin türüne uygun şekilde tepki.
   1. Katalog öğesi belgenin bir istemciye özgü şekilde işler.
1. Son katalog öğesi'nin yürütme zaman damgası yeni imleç değeri kaydedin.

Bu temel algoritmayla tam görünümünü kullanılabilir tüm paketler paket kaynağında yukarı istemci uygulaması oluşturabilirsiniz. İstemci, yalnızca düzenli olarak her zaman en son değişiklikleri paket kaynağına farkında olması için bu algoritma yürütme.

> [!Note]
> Bu algoritma nedir bu nuget.org Teknolojisi'ni [paket meta verileri](registration-base-url-resource.md), [paket içeriğini](package-base-address-resource.md), [arama](search-query-service-resource.md) ve [otomatik tamamlama](search-autocomplete-service-resource.md) kaynaklar güncel.

### <a name="dependent-cursors"></a>Bağımlı imleçler

Burada bir istemcinin çıkış başka bir istemcinin Çıkışta bağlıdır yapısında bir bağımlılığı olan iki katalog istemcisi vardır varsayalım. 

#### <a name="example"></a>Örnek

Örneğin, paket meta veri kaynağında görünmeden önce nuget.org üzerinde yeni yayımlanan paket arama kaynak görünmemelidir. Paket meta veri kaynağı resmi NuGet istemci tarafından gerçekleştirilen "geri yükleme" işlem kullanan olmasıdır. Bir müşteri arama hizmetini kullanarak bir paket belirlerse, paket meta veri kaynağı kullanarak, paketin başarıyla geri olmalıdır. Diğer bir deyişle, arama kaynağı üzerinde paket meta veri kaynağı bağlıdır. Her kaynak, kaynak güncelleştirme Kataloğu istemci arka plan işi var. Her bir istemci kendi imleç sahiptir.

Her iki kaynağın arama kaynak güncelleştirmeleri katalog istemci imleci katalog dışına yerleşiktir beri *ötesine geçmeyecek gerekir* paket meta veri Kataloğu istemci imleci.

#### <a name="algorithm"></a>Algoritması

Bu kısıtlamayı uygulamak için yalnızca olması için yukarıdaki algoritması değiştirin:

1. Kaydedilen imleci değer yerel depodan getirin.
1. Karşıdan yükle ve Katalog dizinini seri durumdan.
1. Tüm katalog yürütme zaman damgası sayfalarıyla Bul *büyük* imleci **bağımlılığı 's imleç küçük veya buna eşit.**
1. İşlem için katalog öğeleri listesi boş bildirin.
1. 3. adımda eşleşen her katalog sayfası için:
   1. Karşıdan yükle ve Katalog Sayfası seri.
   1. Tüm katalog öğeleri yürütme zaman damgası ile Bul *büyük* imleci **bağımlılığı 's imleç küçük veya buna eşit.**
   1. Tüm eşleşen katalog öğeleri 4. adımda bildirilen listesine ekleyin.
1. Katalog öğesi listesi yürütme zaman damgası göre sıralayın.
1. Her bir katalog öğesi sırayla işlemini:
   1. Karşıdan yükle ve katalog öğesi seri durumdan.
   1. Katalog öğesi'nin türüne uygun şekilde tepki.
   1. Katalog öğesi belgenin bir istemciye özgü şekilde işler.
1. Son katalog öğesi'nin yürütme zaman damgası yeni imleç değeri kaydedin.

Bu değiştirilen algoritması kullanılarak, tüm oluşturan kendi belirli dizinleri, yapılar, vb. bağımlı katalog istemcilerin bir sistem oluşturabilirsiniz.
