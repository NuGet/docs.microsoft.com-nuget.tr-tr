---
title: Katalog kaynağı, NuGet V3 API
description: Bir dizin oluşturulur ve nuget.org adresinden silinen tüm paketlerin kataloğudur.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d4c13200494ed3c6fa897ce0083a52c13688b44b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547399"
---
# <a name="catalog"></a>Kataloğu

**Kataloğu** paket kaynağını, oluşturma ve silme gibi tüm paket işlemleri kaydeder bir kaynaktır. Katalog kaynağına sahip `Catalog` yazın [hizmet dizini](service-index.md).

> [!Note]
> Katalog resmi bir NuGet istemcisi tarafından kullanılmadığından, tüm paket kaynaklarını kataloğa uygulayın.

> [!Note]
> Şu anda nuget.org katalog, Çin'de kullanılamıyor. Daha fazla ayrıntı için [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer   | Notlar
------------- | -----
Catalog/3.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değerleri. Bu konu başlığı altında yer tutucu URL'yi `{@id}`.

## <a name="http-methods"></a>HTTP yöntemleri

Katalog kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="catalog-index"></a>Katalog dizini

Katalog öğeleri, tarih sırasına göre sıralı bir listesi bulunur iyi bilinen bir konumda bir belge Kataloğu dizinidir. Katalog kaynak giriş noktasıdır.

Dizin kataloğu sayfaların oluşur. Her katalog sayfa katalog öğelerini içerir. Her bir katalog öğesi, zaman içinde bir noktadaki tek bir paket ilgili bir olayı temsil eder. Katalog öğesi, paket kaynağından listelenmemiş, yeniden listelendiğinde veya silindiğinde oluşturulmuş olan bir paketi temsil edebilir. İstemci, katalog öğelerini kronolojik sırada işleyerek, V3 paket kaynağı var. her paketin güncel bir görünümü oluşturabilirsiniz.

Kısacası, katalog BLOB'ları aşağıdaki hiyerarşik yapıya sahiptir:

- **Dizin**: Katalog için giriş noktası.
- **Sayfa**: Katalog öğeleri gruplandırması.
- **Yaprak**: bir belgeyi temsil eden tek bir paketin durumunun bir anlık görüntüdür bir katalog öğesi.

Her bir katalog nesnesi adlı bir özelliğe sahiptir `commitTimeStamp` kataloğa öğesi eklendiğinde temsil eden. Katalog öğelerini, işlemeleri adlı toplu katalog sayfasına eklenir. Tüm katalog öğeleri aynı işleme içinde aynı işleme zaman damgasına sahip (`commitTimeStamp`) ve işleme kimliği (`commitId`). Katalog öğeleri aynı işlemede yerleştirilen aynı nokta çevresinde paket kaynak saat içinde gerçekleşen olayları temsil eder. Sıralama yok içinde bir katalog işleme yok.

Her bir paket kimliği ve sürüm benzersiz olduğundan, bir işlemede hiçbir zaman birden fazla katalog öğesi olacaktır. Bu, katalog öğeleri tek bir paket için her zaman kesin bir şekilde işleme zaman damgasına göre sıralanabilir sağlar.

Hiçbir zaman kataloğuna birden fazla işleme olarak yoktur `commitTimeStamp`. Diğer bir deyişle, `commitId` ile gereksiz `commitTimeStamp`.

Tersine [paket meta veri kaynağı](registration-base-url-resource.md)paket Kimliğine göre dizini, dizinlenmiş (ve sorgulanabilir) kataloğudur yalnızca zamanına göre.

Katalog öğeleri her zaman bir düz olarak artan, kronolojik sırada Kataloğu'na eklenir. Bu bir katalog işleme X anda eklenirse daha sonra Kataloğu yürütme yok hiç olmadığı kadar eklenecek anlamına gelir. bir süre daha az veya eşit x ile.

Aşağıdaki isteği katalog dizinini getirir.

    GET {@id}

Aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi katalog dizinidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
commitId        | dize           | Evet      | En son işlemeyle ilişkili benzersiz bir kimliği
commitTimeStamp | dize           | Evet      | En son işlemeyi bir zaman damgası
count           | tamsayı          | Evet      | Dizin içinde sayfa sayısı
Öğeleri           | Nesne dizisi | Evet      | Bir dizi her nesne bir sayfasını temsil eden nesneler

Her öğe `items` her sayfada bazı minimal ayrıntılarını içeren bir nesne dizisidir. Bu sayfa nesneler Kataloğu bırakır (öğeleri) içermez. Dizideki öğelerin sırasını tanımlı değil. Sayfalar, bellek kullanarak istemci tarafından sıralanabileceği kendi `commitTimeStamp` özelliği.

Yeni sayfa sunulan gibi `count` artırılır ve yeni nesneler görünür `items` dizisi.

Katalog için dizinin öğeleri eklendikçe `commitId` değişir ve `commitTimeStamp` artacaktır. Bu iki özellik temelde özeti tüm sayfanın üstünde olan `commitId` ve `commitTimeStamp` değerler `items` dizisi.

### <a name="catalog-page-object-in-the-index"></a>Dizindeki katalog sayfa nesnesi

Katalog sayfa nesneleri Kataloğu dizinin içinde bulunan `items` özelliği aşağıdaki özelliklere sahiptir:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | dize  | Evet      | Getirme katalog sayfası URL'si
commitId        | dize  | Evet      | Bu sayfada en son işlemeyle ilişkili benzersiz bir kimliği
commitTimeStamp | dize  | Evet      | Bu sayfada en son işlemeyi bir zaman damgası
count           | tamsayı | Evet      | Katalog sayfasındaki öğelerin sayısı

Tersine [paket meta veri kaynağı](registration-base-url-resource.md) dizine bırakır satır içleri, bazı durumlarda, katalog bırakır hiçbir zaman dizine satır içine alınmış ve sayfa kullanılarak her zaman getirilmesi gerekir `@id` URL'si.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Katalog Sayfası

Katalog Sayfası, katalog öğelerini koleksiyonudur. Biri kullanılarak bir belge olan `@id` değerleri Kataloğu dizinde bulunamadı. Katalog Sayfası URL'si tahmin edilebilir olmasını yönelik değildir ve yalnızca katalog dizinini kullanarak bulunması gerekir.

Yeni Katalog öğeleri yalnızca en yüksek işleme zaman damgasına sahip katalog dizin sayfası veya yeni bir sayfaya eklenir. Daha yüksek bir işleme zaman damgası içeren bir sayfa Kataloğu'na eklendikten sonra eski sayfa hiçbir zaman eklendikçe veya değiştirildi.

Katalog sayfa belgesi, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad            | Tür             | Gerekli | Notlar
--------------- | ---------------- | -------- | -----
commitId        | dize           | Evet      | Bu sayfada en son işlemeyle ilişkili benzersiz bir kimliği
commitTimeStamp | dize           | Evet      | Bu sayfada en son işlemeyi bir zaman damgası
count           | tamsayı          | Evet      | Sayfadaki öğelerin sayısı
Öğeleri           | Nesne dizisi | Evet      | Bu sayfada katalog öğeleri
Üst          | dize           | Evet      | Katalog dizini URL'si

Her öğe `items` bazı minimal bir katalog öğesi ayrıntılarını içeren bir nesne dizisidir. Bu öğe nesneler Kataloğu öğenin veri içermez. Sayfanın öğelerin sırasını `items` dizi tanımlı değil. Öğeleri, bellek kullanarak istemci tarafından sıralanabileceği kendi `commitTimeStamp` özelliği.

Katalog öğeleri sayfasındaki sayısı, sunucu uygulama tarafından tanımlanır. Nuget.org için en fazla 550 öğe yok her sayfada gerçek sayı zaman noktasında ileri işleme batch boyutuna bağlı olarak bazı sayfalar için daha küçük olabilir.

Yeni öğeler sunulan gibi `count` artırılmasına ya da yeni katalog öğesi nesneleri görünür olan `items` dizi.

Öğeleri sayfaya eklendikçe `commitId` değişiklikleri ve `commitTimeStamp` artırır. Bu iki özellik temelde özeti tümü `commitId` ve `commitTimeStamp` değerler `items` dizisi.

### <a name="catalog-item-object-in-a-page"></a>Katalog öğesi nesneyi sayfasındaki

Katalog öğesi nesneleri, katalog sayfa bulunamadı `items` özelliği aşağıdaki özelliklere sahiptir:

Ad            | Tür    | Gerekli | Notlar
--------------- | ------- | -------- | -----
@id             | dize  | Evet      | Katalog öğesi getirilecek URL'si
@type           | dize  | Evet      | Katalog öğesi türü
commitId        | dize  | Evet      | Bu katalog öğesi ile ilişkili işleme kimliği
commitTimeStamp | dize  | Evet      | Bu katalog öğesi işleme zaman damgası
nuget:id        | dize  | Evet      | Bu yaprak ilgili paket kimliği
nuget:version   | dize  | Evet      | Bu yaprak ilgili Paket sürümü

`@type` Değeri, şu iki değerden birini olacaktır:

1. `nuget:PackageDetails`: Bu karşılık gelir `PackageDetails` Kataloğu yaprak belge türü.
1. `nuget:PackageDelete`: Bu karşılık gelir `PackageDelete` Kataloğu yaprak belge türü.

Her hangi bir türü, göreceğiniz anlamına gelir hakkında daha fazla ayrıntı için [karşılık gelen öğe türü](#item-types) aşağıda.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Yaprak katalog

Katalog yaprak zaman içinde belirli bir paket kimliği ve sürüm belirli bir noktada hakkındaki meta verileri içerir. Kullanılarak bir belge olan `@id` değeri bir katalog sayfa bulunamadı. Katalog yaprak URL'sine tahmin edilebilir olmasını yönelik değildir ve yalnızca bir katalog sayfası kullanılarak bulunması gerekir.

Katalog yaprak belge, aşağıdaki özelliklere sahip bir JSON nesnesidir:

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
@type                   | dize veya dize dizisi | Evet      | Katalog öğesi türlerinin
catalog:commitId        | dize                     | Evet      | Bu katalog öğesi ile ilişkili bir işleme kimliği
catalog:commitTimeStamp | dize                     | Evet      | Bu katalog öğesi işleme zaman damgası
kimlik                      | dize                     | Evet      | Katalog öğesi, paket kimliği
Yayımlanan               | dize                     | Evet      | Paket yayımlanma tarihi katalog öğesi
sürüm                 | dize                     | Evet      | Katalog öğesi, Paket sürümü

### <a name="item-types"></a>Öğe türleri

`@type` Özelliği olan bir dize veya dize dizisi. Kolaylık sağlamak için `@type` değeri bir dize ise, herhangi bir boyut dizisi olarak değerlendirilmelidir. Tüm olası değerleri `@type` belgelenmiştir. Ancak, her bir katalog öğesi, aşağıdaki iki dize türü değerleri tam olarak birine sahiptir:

1. `PackageDetails`: bir anlık görüntüsünü paket meta verileri temsil eder
1. `PackageDelete`: silinen bir paketi temsil eder

### <a name="package-details-catalog-items"></a>Paket Ayrıntıları katalog öğeleri

Katalog öğeleri türüyle `PackageDetails` (kimliği ve sürüm birleşimi) belirli bir paket için paket meta verilerin anlık görüntüsünü içerir. Paket Ayrıntıları katalog öğesi, aşağıdaki senaryolardan herhangi bir paket kaynağı karşılaştığında üretilir:

1. Bir paketi **gönderilen**.
1. Bir paketi **listelenen**.
1. Bir paketi **listelenmemiş**.
1. Bir paketi **yeniden akıtılmaz**.

Paket yeniden akış aslında bir sahte gönderme değişikliğine gerek olmadan var olan bir paketi paket oluşturan bir yönetici harekettir. Nuget.org bir hata, katalog tükettikleri arka plan işleri birinde düzelttikten sonra bir yeniden akış kullanılır.

Katalog öğeleri kullanan istemciler, bu senaryolarda katalog öğesi üretilen belirlemek çalışmamalıdır. Bunun yerine, istemci basitçe herhangi bir işlenen görünümü veya dizin katalog öğesi içinde bulunan meta veriler ile güncelleştirmeniz gerekir. Ayrıca, yinelenen veya gereksiz katalog öğeleri düzgün bir şekilde yapılması gerekir (idempotently).

Paket Ayrıntıları katalog öğelerini ek olarak aşağıdaki özelliklere sahip [tüm Kataloğu leaves dahil](#catalog-leaf).

Ad                    | Tür                       | Gerekli | Notlar
----------------------- | -------------------------- | -------- | -----
Yazarları                 | dize                     | Yok       |
Oluşturulan                 | dize                     | Yok       | Paketin ilk oluşturulduğu zaman damgası. Geri dönüş özelliği: `published`.
dependencyGroups        | Nesne dizisi           | Yok       | Aynı biçimi olarak [paket meta veri kaynağı](registration-base-url-resource.md#package-dependency-group)
açıklama             | dize                     | Yok       |
IconUrl                 | dize                     | Yok       |
isPrerelease            | Boole değeri                    | Yok       | Olup olmadığı paket yayın öncesi sürümüdür. Gelen algılanabilir `version`.
dil                | dize                     | Yok       |
LicenseUrl              | dize                     | Yok       |
listelenen                  | Boole değeri                    | Yok       | Paket listede değil
MinClientVersion        | dize                     | Yok       |
packageHash             | dize                     | Evet      | Kullanarak kodlama paket karmasını [standart taban 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | dize                     | Evet      |
packageSize             | tamsayı                    | Evet      | Paket .nupkg bayt cinsinden boyutu
ProjectUrl              | dize                     | Yok       |
ReleaseNotes            | dize                     | Yok       |
requireLicenseAgreement | Boole değeri                    | Yok       | Varsayar `false` dışlanırsa
özet                 | dize                     | Yok       |
etiketler                    | dize dizisi           | Yok       |
Başlık                   | dize                     | Yok       |
verbatimVersion         | dize                     | Yok       | Sürüm dizesi olarak başlangıçta .nuspec içinde bulunamadı

Paket `version` tam, normalleştirilmiş sürüm dizesi bir özelliktir. Bu, SemVer 2.0.0 yapılandırma verilerini buraya dahil olabileceğini anlamına gelir.

`created` Paket varsayılan, genellikle kısa bir süre önce Kataloğu öğenin yürütme zaman damgası olan paket kaynak tarafından alındığını zaman damgası olduğunda.

`packageHashAlgorithm` Üretmek için kullanılan karma algoritması temsil eden sunucu uygulama tarafından tanımlanan bir dizedir `packageHash`. her zaman kullanılan nuget.org `packageHashAlgorithm` değerini `SHA512`.

`published` Zaman damgası olan zaman zaman paketin son listeleniyordu.

> [!Note]
> Nuget.org, `published` değeri paketi olduğunda listelenmemiş yıla 1900 ayarlanır.

#### <a name="sample-request"></a>Örnek istek

AL https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Paket Kataloğu öğeleri silme

Katalog öğeleri türüyle `PackageDelete` Kataloğu istemcilere bir paketi paket kaynağından silinir ve herhangi bir paket işlemi (örneğin, geri yükleme) için artık kullanılamıyor gösteren bilgileri en az bir kümesini içerir.

> [!Note]
> Bir paket silinecek ve daha sonra yeniden yayımlamışsa belki aynı paket Kimliğini ve sürümünü kullanarak için mümkündür. Nuget.org bir paket kimliği ve sürüm belirli paket içeriğini yaptığından emin resmi istemcinin varsayım durdurduğundan çok nadir bir durum budur. Nuget.org paket silme hakkında daha fazla bilgi için bkz. [ilkemizi](../policies/deleting-packages.md).

Paket Kataloğu öğeleri silme sahip herhangi bir ek özellik listelenenlere [tüm Kataloğu leaves dahil](#catalog-leaf).

`version` Özgün sürüm dizesi paket .nuspec içinde bulunan bir özelliktir.

`published` Genellikle kısa süre önce Kataloğu öğenin yürütme zaman damgası olarak ne zaman paket silindi, saati bir özelliktir.

#### <a name="sample-request"></a>Örnek istek

AL https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>İmleç

### <a name="overview"></a>Genel Bakış

Bu bölümde, mutlaka protokolü tarafından zorunlu değildir ancak herhangi bir pratik Kataloğu istemci uygulaması bir parçası olmalıdır, bir istemci kavramı açıklanmaktadır.

Katalog zamanına göre dizini oluşturulmuş bir yalnızca ekleme yapılabilen bir veri yapısı olduğundan, istemci depolamanız gerekir bir **imleç** ne istemcinin belirli bir noktaya kadar temsil eden katalog öğeleri yerel olarak işledi. Bu imleç değeri hiçbir zaman istemci makine düzende oluşturulacağını unutmayın. Bunun yerine, değeri bir katalog nesnenin gelmesi gerektiğini `commitTimestamp` değeri.

İstemci paket kaynağı yeni olayları işlemek istediği her durumda ihtiyaç yalnızca katalog sorgu yürütme zaman damgasına sahip tüm katalog öğeleri için kendi saklı imleç büyüktür. İstemci başarıyla tüm yeni katalog öğelerini işledikten sonra katalog öğelerini yalnızca yeni imleç değer olarak işlenen en son işleme zaman damgası kaydeder.

Bu yaklaşımı kullanarak, istemci hiçbir paket kaynağında oluşan herhangi bir paket olayı kaçırmayın emin olabilirsiniz.
Ayrıca, istemci, imlecin kayıtlı işleme zaman damgası önce eski olayları yeniden işlemek hiçbir zaman vardır.

Bu güçlü kavramı imleçler, birçok nuget.org arka plan işleri için kullanılır ve V3 API güncel tutmak için kullanılır. 

### <a name="initial-value"></a>Başlangıç değeri

Katalog istemci çok ilk kez başlattığında (ve bu nedenle imleci değere sahip olduğunda), varsayılan imleç değerini kullanmanız gerekir. NET `System.DateTimeOffset.MinValue` ya gösterilebilir en düşük zaman damgası bazı benzer tür biçimi.

### <a name="iterating-over-catalog-items"></a>Katalog öğeleri üzerinde yineleme

Sonraki kümesini işlemek için katalog öğeleri için sorgu için istemci gerekir:

1. Kaydedilen imleç değeri yerel depodan getirilemedi.
1. İndirin ve Katalog dizinini seri durumdan.
1. Tüm sayfa işleme zaman damgasına sahip katalog Bul *büyüktür* imleç.
1. Katalog öğelerini işlemek için boş bir listesini bildirir.
1. Adım 3'te eşleşen her katalog sayfası için:
   1. İndirin ve Katalog Sayfası seri durumdan.
   1. Tüm öğeleri işleme zaman damgasına sahip katalog Bul *büyüktür* imleç.
   1. Tüm eşleşen katalog öğelerini 4. adımda bildirilen listesine ekleyin.
1. Katalog öğesi listesini işleme zaman sıralar.
1. Her bir katalog öğesi, sırada İşle:
   1. İndirin ve katalog öğesi seri durumdan.
   1. Katalog öğenin türü için uygun şekilde tepki.
   1. Katalog öğesi belgenin istemciye özgü bir şekilde işleyin.
1. Son kataloğu öğenin yürütme zaman damgası, yeni işaretçi değeri olarak kaydedin.

Bu temel algoritma ile kullanılabilir tüm paketleri eksiksiz bir görünümünü paket kaynağında'kurmak istemci uygulama oluşturabilirsiniz. İstemci, yalnızca bu algoritma, düzenli aralıklarla her zaman en son değişiklikleri paket kaynağına dikkat edilmesi gereken yürütme.

> [!Note]
> Bu algoritma, o nuget.org Teknolojisi'ni [paket meta verileri](registration-base-url-resource.md), [paket içeriğini](package-base-address-resource.md), [arama](search-query-service-resource.md) ve [otomatik tamamlama](search-autocomplete-service-resource.md) kaynakların en güncel.

### <a name="dependent-cursors"></a>Bağımlı imleçler

Burada başka bir istemcinin çıktıda bir istemcinin çıkış bağlıdır devralınmış bir bağımlılığı olan iki Kataloğu istemciler vardır varsayalım. 

#### <a name="example"></a>Örnek

Örneğin, paket meta veri kaynağında görünmeden önce nuget.org adresinden yeni yayımlanan paket arama kaynak görünmemelidir. Paket meta veri kaynağı resmi bir NuGet istemcisi tarafından gerçekleştirilen "geri" işlemi kullanıyor olmasıdır. Bir müşteri Arama Hizmeti'ni kullanarak bir paket belirlerse, başarılı bir şekilde, paketin paket meta veri kaynağı kullanarak geri yükleme olanağınız olmalıdır. Diğer bir deyişle, paket meta veri kaynağında arama kaynağına bağlıdır. Her kaynak, kaynak güncelleştirme Kataloğu istemci arka plan işi var. Her istemci kendi imleç yok.

İki kaynağın bir arama kaynağı Kataloğu istemci imleci Kataloğu dışına yerleşik olduğundan *ötesine geçip gerekir değil* paket meta veri Kataloğu istemci imleci.

#### <a name="algorithm"></a>Algoritması

Bu kısıtlama uygulamak için basitçe olması için yukarıdaki algoritmasını değiştirin:

1. Kaydedilen imleç değeri yerel depodan getirilemedi.
1. İndirin ve Katalog dizinini seri durumdan.
1. Tüm sayfa işleme zaman damgasına sahip katalog Bul *büyüktür* imleç **bağımlılık'ın imleç küçüktür veya eşittir.**
1. Katalog öğelerini işlemek için boş bir listesini bildirir.
1. Adım 3'te eşleşen her katalog sayfası için:
   1. İndirin ve Katalog Sayfası seri durumdan.
   1. Tüm öğeleri işleme zaman damgasına sahip katalog Bul *büyüktür* imleç **bağımlılık'ın imleç küçüktür veya eşittir.**
   1. Tüm eşleşen katalog öğelerini 4. adımda bildirilen listesine ekleyin.
1. Katalog öğesi listesini işleme zaman sıralar.
1. Her bir katalog öğesi, sırada İşle:
   1. İndirin ve katalog öğesi seri durumdan.
   1. Katalog öğenin türü için uygun şekilde tepki.
   1. Katalog öğesi belgenin istemciye özgü bir şekilde işleyin.
1. Son kataloğu öğenin yürütme zaman damgası, yeni işaretçi değeri olarak kaydedin.

Bu değiştirilmiş bir algoritma kullanarak, bir sistem bağımlı Kataloğu istemcilerin tüm üretme kendi belirli dizinleri, yapılar, vb. oluşturabilirsiniz.
