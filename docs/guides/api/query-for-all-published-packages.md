---
title: nuget.org için yayınlanan tüm paketler için sorgu
description: NuGet API'sini kullanarak, nuget.org için yayınlanan tüm paketleri sorgulayabilir ve zaman içinde güncel kalabilirsiniz.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498229"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>nuget.org için yayınlanan tüm paketler için sorgu

Eski OData V2 API'sindeki ortak bir sorgu deseni, paketin yayımlandığı zaman sipariş edilen nuget.org'a göre yayınlanan tüm paketleri sıralıyordu. nuget.org karşı bu tür bir sorgu gerektiren senaryolar büyük ölçüde değişir:

- nuget.org tamamen çoğaltma
- Paketlerin yeni sürümlerinin ne zaman serbest bırakıldığını algılama
- Paketinize bağlı paketleri bulma

Bunu yapmanın eski yolu genellikle OData paket varlığını bir zaman damgası ile sıralamaya ve `skip` (sayfa boyutu) parametreleri kullanılarak `top` belirlenen büyük sonuç kümesi boyunca sayfalama bağlıdır. Ne yazık ki, bu yaklaşımın bazı dezavantajları vardır:

- Sorgular genellikle sıra değiştiren veriler üzerinde yapıldığından, paketlerin eksik olma olasılığı
- Sorgular en iyi duruma getirilmediği için sorgu yanıt süresi yavaşladı (en iyi duruma getirilmiş sorgular resmi NuGet istemcisi için ana satır senaryosunu destekleyen sorgulardır)
- Amortismana ve belgesiz API'nin kullanımı, gelecekte bu tür sorguların desteklenmesi nin garanti olmadığı anlamına gelir
- Tarihin tam olarak meydana gelen sırayla tekrarlanamaması

Bu nedenle, yukarıda belirtilen senaryoları daha güvenilir ve geleceğe yönelik bir şekilde ele almak için aşağıdaki kılavuz izlenebilir.

## <a name="overview"></a>Genel Bakış

Bu kılavuzun merkezinde **NuGet** [API](../../api/overview.md) kataloğu olarak adlandırılan kaynak. Katalog, arayanın nuget.org eklenen, değiştirilen ve silinen paketlerin tam geçmişini görmesini sağlayan yalnızca ek apidir. Nuget.org için yayınlanan paketlerin tümüyle ve hatta bir alt kümesiyle ilgileniyorsanız, katalog, zaman geçtikçe mevcut paketlerkümesinden haberdar olmak için harika bir yoldur.

Bu kılavuz, üst düzey bir walk-through olması amaçlanmıştır ama kataloğun ince tane ayrıntıları ilgileniyorsanız, onun [API başvuru belgesi](../../api/catalog-resource.md)bakın.

Aşağıdaki adımlar seçtiğiniz herhangi bir programlama dilinde uygulanabilir. Tam çalışan bir örnek istiyorsanız, aşağıda belirtilen [C# örneğine](#c-sample-code) bir göz atın.

Aksi takdirde, güvenilir bir katalog okuyucu oluşturmak için aşağıdaki kılavuzu izleyin.

## <a name="initialize-a-cursor"></a>İmleci başlatma

Güvenilir bir katalog okuyucu oluşturmanın ilk adımı bir imleç uygulamaktır. Katalog imlecinin tasarımı hakkında tüm ayrıntılar için [katalog başvuru belgesine](../../api/catalog-resource.md#cursor)bakın. Kısacası, imleç, katalogdaki olayları işlediğiniz bir zaman dilimi dir. Katalogdaki olaylar paket yayınlarını ve diğer paket değişikliklerini temsil eder. NuGet'de yayınlanan tüm paketleri önemsiyorsanız (zamanın başlangıcından beri), imlecinizi "minimum değer" zaman damgasına (örn. `DateTime.MinValue` .NET'te) başlatılırsınız. Şu andan itibaren yalnızca yayınlanan paketleri önemsiyorsanız, geçerli zaman damgasını ilk imleç değeriniz olarak kullanırsınız.

Bu kılavuz için imlecimizi bir saat önce bir zaman damgasına alacağız. Şimdilik, hafızadaki zaman damgasını kaydet.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Katalog dizini URL'si belirleme

NuGet API'sindeki her kaynağın (bitiş noktası) konumu [hizmet dizini](../../api/service-index.md)kullanılarak keşfedilmelidir. Bu kılavuz nuget.org odaklandığından, nuget.org'un hizmet dizinini kullanacağız.

    GET https://api.nuget.org/v3/index.json

Hizmet belgesi, nuget.org tüm kaynakları içeren JSON belgesidir. `Catalog/3.0.0`Özellik değerine `@type` sahip kaynağı arayın. İlişkili `@id` özellik değeri, katalog dizininin URL'sidir. 

## <a name="find-new-catalog-leaves"></a>Yeni katalog yapraklarını bulma

Önceki `@id` adımda bulunan özellik değerini kullanarak katalog dizini indirin:

    GET https://api.nuget.org/v3/catalog0/index.json

[Katalog dizini](../../api/catalog-resource.md#catalog-index)deserialize. Tüm [katalog sayfa nesnelerini](../../api/catalog-resource.md#catalog-page-object-in-the-index) geçerli imleç değerinizden daha az veya eşit olacak `commitTimeStamp` şekilde filtreleyin.

Kalan her katalog sayfası için, özelliği `@id` kullanarak belgenin tamamını indirin.

    GET https://api.nuget.org/v3/catalog0/page2926.json

[Katalog sayfasını](../../api/catalog-resource.md#catalog-page)deserialize. Tüm [katalog yaprağı nesnelerini](../../api/catalog-resource.md#catalog-item-object-in-a-page) geçerli imleç değerinizden daha az veya eşit olacak `commitTimeStamp` şekilde filtreleyin.

Filtrelenmemiş tüm katalog sayfalarını indirdikten sonra, imleç zaman damganız ile şimdi arasındaki süre içinde yayınlanmış, listelenmemiş, listelenen veya silinmiş paketleri temsil eden bir katalog yaprağı nesne kümeniz vardır.

## <a name="process-catalog-leaves"></a>İşlem kataloğu yaprakları

Bu noktada, katalog öğeleri üzerinde istediğiniz herhangi bir özel işleme gerçekleştirebilirsiniz. İhtiyacınız olan tek şey paketin kimliği ve sürümüyse, sayfalarda bulunan katalog öğesi nesnelerindeki `nuget:id` ve `nuget:version` özelliklerini inceleyebilirsiniz. Katalog öğesinin varolan bir paketle mi yoksa silinmiş bir paketle mi ilgili olduğunu öğrenmek için tesise baktığınızdan `@type` emin olun.

Paketle ilgili meta verilerle ilgileniyorsanız (açıklama, bağımlılıklar, .nupkg boyutu, vb.) özelliği kullanarak `@id` katalog yaprağı [belgesini](../../api/catalog-resource.md#catalog-leaf) getirebilirsiniz.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Bu [belge, paket meta veri kaynağında](../../api/registration-base-url-resource.md)yer alan tüm meta verilere ve daha fazlana sahiptir!

Bu adım, özel mantığınızı uyguladığınız yerdir. Bu kılavuzdaki diğer adımlar katalog yaprakları ile ne yapıyor olursa olsun hemen hemen aynı şekilde uygulanır.

### <a name="downloading-the-nupkg"></a>.nupkg'ı indirme

Katalogda bulunan paketler için .nupkg'ları indirmek istiyorsanız, paket içerik [kaynağını](../../api/package-base-address-resource.md)kullanabilirsiniz. Ancak, bir paketin katalogda bulunmasıyla paket içeriği kaynağında kullanılabilir olması arasında kısa bir gecikme olduğunu unutmayın. Bu nedenle, `404 Not Found` katalogda bulduğunuz bir paket için .nupkg indirmeye çalışırken karşılaşırsanız, kısa bir süre sonra yeniden denemeniz yeterlidir. Bu gecikmegiderme GitHub sorunu [NuGet / NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455)tarafından izlenir.

## <a name="move-the-cursor-forward"></a>İmleci ileri doğru hareket ettirin

Katalog öğelerini başarıyla işledikten sonra, kaydetmek için yeni imleç değerini belirlemeniz gerekir. Bunu yapmak için, işlediğiniz tüm `commitTimeStamp` katalog öğelerinin maksimum (en son kronolojik) öğesini bulun. Bu senin yeni imleç değeriniz. Veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin. Daha fazla katalog öğesi almak istediğinizde, imleç değerinizi bu kalıcı mağazadan başlatarak [ilk adımdan](#initialize-a-cursor) başlamanız yeterlidir.

Uygulamanız bir özel durum veya hata atarsa, imleci ileri itmeyin. İmleci ileriye taşımak, imlecinizin önünde katalog öğelerini bir daha işlemeniz gerekmeyecek bir anlama gelir.

Nedense, katalog yapraklarını işleme şeklinizde bir hata varsa, imlecinizi zamanda geriye doğru taşıyabilir ve kodunuzu eski katalog öğelerini yeniden işlemesine izin verebilirsiniz.

## <a name="c-sample-code"></a>C# örnek kodu

Katalog HTTP üzerinden kullanılabilir JSON belgeleri kümesi olduğundan, bir HTTP istemcisi ve JSON deserializer olan herhangi bir programlama dili kullanılarak etkileşim olabilir.

C# örnekleri [NuGet/Numune deposunda](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)mevcuttur.

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog SDK

Kataloğu kullanmanın en kolay yolu ön sürüm .NET kataloğu SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Bu paket, NuGet paket kaynak URL'sini `nuget-build` `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`kullandığınız MyGet akışında mevcuttur.

Bu paketi (.NET Framework `netstandard1.3` 4.6 gibi) uyumlu veya daha büyük bir projeye yükleyebilirsiniz.

Bu paketi kullanan bir örnek GitHub'da [NuGet.Protocol.Catalog.Sample projesinde](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)mevcuttur.

#### <a name="sample-output"></a>Örnek çıktı

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Minimum örnek

Katalogla etkileşimi daha ayrıntılı olarak gösteren daha az bağımlılık içeren bir örnek [için, CatalogReaderExample örnek projesine](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)bakın. Proje `netcoreapp2.0` [nuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet indeksini çözmek için) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON deserialization için) hedeflerini ve bağlıdır.

Kodun ana mantığı [Program.cs dosyasında](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)görünür.

#### <a name="sample-output"></a>Örnek çıktı

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
