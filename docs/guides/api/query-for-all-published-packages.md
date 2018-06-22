---
title: Nuget.org için yayımlanan tüm paketler için sorgu
description: NuGet API'yi kullanarak nuget.org için yayımlanan tüm paketler için sorgu ve zaman içinde güncel kalın.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 4190cfb500127f117ea1067f0679e5c248bffb3d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821375"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Nuget.org için yayımlanan tüm paketler için sorgu

OData V2 API nuget.org için yayımlanan tüm paketler numaralandırma eski bir ortak sorgu desenine göre sıralayarak paketi yayımlandığında. Bu tür bir nuget.org sorgusu gerektiren senaryolar yaygın olarak değişir:

- Nuget.org tamamen çoğaltma
- Paketleri yayımlanan yeni sürümleri varsa, algılama
- Pakete bağlıdır paketleri bulma

Eski yol bunu yaparsanız, bu genellikle bir zaman damgası tarafından OData paket varlık sıralama ve kullanılarak büyük sonuç kümesinde disk belleği bağımlı `skip` ve `top` (sayfa boyutu) parametreleri. Ne yazık ki, bu yaklaşımın bazı sakıncaları vardır:

- Sorgular, genellikle sırasını değiştirme veriler üzerinde gerçekleştirildiğinden olasılığını paketleri eksik
- Sorguları getirilmemiş nedeniyle sorgu yanıt süresi, yavaş (en iyileştirilmiş sorgular olanları mainline bir senaryo için resmi NuGet istemci desteği olan)
- Bu tür sorgular destek gelecekte anlamına gelir, kullanım dışı ve belgelenmemiş API'yi garanti edilmez
- Bunu ilkelerinden tam sipariş geçmişine yeniden yürütme sorunları

Bu nedenle, daha güvenilir ve gelecekteki kanıt şekilde daha önce bahsedilen senaryosu için aşağıdaki kılavuzu izlenebilir.

## <a name="overview"></a>Genel Bakış

Bu kılavuzun merkezinde kaynaktır [NuGet API](../../api/overview.md) adlı **katalog**. Katalog, eklenen paketler tam geçmişini görmek arayan sağlayan bir yalnızca append API değiştirildi ve nuget.org silindi olabilir. Tüm ya da bir alt bile nuget.org için yayımlanan paket ilgileniyorsanız, katalog Zaman geçtikçe şu anda kullanılabilir paketler kümesiyle güncel kalmak için harika bir yoludur.

Bu kılavuz, bir üst düzey adım adım kılavuz olabilir ancak katalog, ayrıntılı ayrıntılarını ilgileniyorsanız görmek için hazırlanmıştır kendi [API başvuru belgesini](../../api/catalog-resource.md).

Aşağıdaki adımlar, tercih ettiğiniz herhangi programlama dilinde uygulanabilir. Tam bir çalışan örnek istiyorsanız, bir göz atalım [C# örnek](#c-sample-code) aşağıda belirtilen.

Aksi takdirde, bir güvenilir katalog okuyucu oluşturmak için aşağıdaki kılavuzu uygulayın.

## <a name="initialize-a-cursor"></a>Bir imleç başlatma

Bir güvenilir katalog okuyucu oluşturmanın ilk adımı bir imleç uygular. Katalog imleci tasarımı ile ilgili tam Ayrıntılar için bkz [katalog başvuru belgesini](../../api/catalog-resource.md#cursor). Kısacası, imleç bir kadar kataloğunda olayları işlenmiş zaman noktasıdır. Olay Kataloğu temsil paketindeki yayımlar ve başka bir paketi değiştirir. Şimdiye kadar Nuget'e (sürenin başlangıcından bu yana) yayımlanan tüm paketler önem verdiğiniz, imlecinizi bir "en düşük değer" zaman damgası başlatmak (örneğin `DateTime.MinValue` .NET içinde). Şimdi başlatılıyor yayımlanan yalnızca paketleri hakkında verdiğiniz, geçerli zaman damgası ilk imleci değeri olarak kullanırsınız.

Bu kılavuz, biz bir saatten önce bir zaman damgası için bizim imleç başlatması. Şimdilik, zaman damgası bellekte yalnızca kaydedin.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Katalog dizin URL belirleme

Kullanarak her kaynağın (Bitiş) NuGet API'sindeki konumu bulunmasına [Hizmeti dizini](../../api/service-index.md). Bu kılavuz nuget.org üzerinde odaklanmıştır olduğundan, biz nuget.org Hizmeti dizini kullanırsınız.

    GET https://api.nuget.org/v3/index.json

Hizmet belgesini nuget.org üzerinde kaynakların tümünü içeren JSON belgedir. Kaynak sahip Ara `@type` özellik değerinin `Catalog/3.0.0`. İlişkili `@id` özellik değeri olan katalog dizinini URL'si. 

## <a name="find-new-catalog-leaves"></a>Yeni Katalog bırakır Bul

Kullanarak `@id` özellik değeri önceki adımda bulundu indirmek katalog dizini:

    GET https://api.nuget.org/v3/catalog0/index.json

Seri durumdan [katalog dizinini](../../api/catalog-resource.md#catalog-index). Tüm filtre [sayfa nesneleri katalog](../../api/catalog-resource.md#catalog-page-object-in-the-index) ile `commitTimeStamp` değerinden küçük veya eşit, geçerli imleç.

Kullanarak tam belgenin geri kalan her katalog sayfası karşıdan `@id` özelliği.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Seri durumdan [katalog sayfası](../../api/catalog-resource.md#catalog-page). Tüm filtre [yaprak nesneleri katalog](../../api/catalog-resource.md#catalog-item-object-in-a-page) ile `commitTimeStamp` değerinden küçük veya eşit, geçerli imleç.

Tüm filtrelenmelidir değil Katalog sayfaları indirdikten sonra yayımlanan, listede, listelenen veya silinen, imleç zaman damgası arasında bir süre paketleri temsil eden bir katalog yaprak nesneleri kümesine sahiptir ve şimdi.

## <a name="process-catalog-leaves"></a>İşlem katalog bırakır

Bu noktada, katalog öğeleri istediğiniz herhangi bir özel işlem gerçekleştirebilirsiniz. İhtiyacınız olan tek şey, Paket sürümü ve kimliği inceleyebilirsiniz `nuget:id` ve `nuget:version` özellikleri katalog öğesi sayfalarında bulunan nesneler. Bakmak emin olun `@type` katalog öğesi var olan bir paket veya silinmiş bir paket ilgiliyse bilmeniz özelliği.

Meta verileri (Açıklama, bağımlılıkları, .nupkg boyutu, vb. gibi) paket hakkında ilgileniyorsanız getirebilirsiniz [katalog yaprak belge](../../api/catalog-resource.md#catalog-leaf) kullanarak `@id` özelliği.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Bu belgede bulunan meta verileri tümünün [paketini meta veri kaynağı](../../api/registration-base-url-resource.md)ve daha fazlası!

Bu adım, burada özel mantığınızı uygulamak bağlıdır. Bu kılavuzdaki diğer adımları uygulanan pretty içinde çok aynı ile katalog bırakır yapmakta olduğunuz önemli yolu değil.

### <a name="downloading-the-nupkg"></a>.nupkg yükleniyor

İndirme içinde ilgileniyorsanız .nupkg ait paketler için bulunan Kataloğu'nda kullanabileceğiniz [paket içerik kaynağı](../../api/package-base-address-resource.md). Ancak, bir paketi kataloğunda bulunduğunda ve paket içerik kaynağı kullanılabilir olduğunda arasına kısa bir gecikme olduğunu unutmayın. Bu nedenle, karşılaşırsanız `404 Not Found` .nupkg Kataloğu'nda bulunan bir paket için indirme girişiminde bulunulduğunda yalnızca kısa bir süre daha sonra yeniden deneyin. Bu gecikme düzelttikten GitHub sorunu tarafından izlenir [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>İmleç ilerlemek

Katalog öğeleri başarıyla işledikten sonra kaydetmek için yeni imleç değeri belirlemeniz gerekir. Bunu yapmak için en fazla bulun (son tarih sırasına göre) `commitTimeStamp` , işlenen tüm katalog öğelerinin. Bu, yeni bir imleç değerdir. Bu veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin. Daha fazla katalog öğeleri almak istediğinizde, sadece başlangıcı [ilk adım](#initialize-a-cursor) imleç değeriniz bu kalıcı deposundan başlatma tarafından.

Uygulamanızı bir özel durum ya da hatalar oluşturursa, imleci İleri taşımayın. İmleç ilerleyen hiçbir zaman yeniden imlecinizi önce katalog öğelerini işlemek için gereken bir anlamı yoktur.

Herhangi bir nedenle varsa, katalog işleminin nasıl içinde bir hata bırakır, sadece imlecinizi sürede geri taşımak ve eski katalog öğeleri yeniden işlemek kodunuzu izin.

## <a name="c-sample-code"></a>C# örnek kod

Katalog HTTP üzerinden bir dizi JSON belgeleri kullanılabilir olduğundan, bir HTTP istemcisi ve JSON seri durumdan çıkarıcının sahip herhangi bir programlama dili kullanarak kurduğunda.

C# örnekleri kullanılabilir [NuGet/Samples depo](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK katalog

Katalog kullanmak için en kolay yolu, yayın öncesi .NET katalog SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Bu paket edinilebilir `nuget-build` akış, MyGet NuGet paket kaynağı URL'sini kullandığınız `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

İle uyumlu bir proje için bu paketi yükleyebilirsiniz `netstandard1.3` ya da (örneğin, .NET Framework 4.6) büyük.

Bu paketi kullanan bir örnek github'da kullanılabilir [NuGet.Protocol.Catalog.Sample proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

### <a name="minimal-sample"></a>En az örnek

Daha fazla ayrıntı kataloğunda etkileşim gösteren bir örnek için daha az bağımlılıkları, bkz: [CatalogReaderExample örnek proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Proje hedefleri `netcoreapp2.0` ve bağımlı [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (için hizmeti dizini çözme) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (için JSON seri durumundan çıkarma).

Kod ana mantığı görünür [Program.cs dosyasının](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
