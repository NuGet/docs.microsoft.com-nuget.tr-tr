---
title: Nuget.org için yayımlanan tüm paketler için sorgu
description: NuGet API'yi kullanarak nuget.org için yayımlanan tüm paketler için sorgu ve zaman içinde yeniliklerden haberdar olun.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551084"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Nuget.org için yayımlanan tüm paketler için sorgu

OData V2 API'si tüm paketleri nuget.org için yayımlanan numaralandırma eski bir yaygın sorgu düzeni sıralı olarak paketi yayımlandığında. Bu tür bir sorgu nuget.org karşı gerektiren senaryolar büyük ölçüde farklılık gösterir:

- Nuget.org tamamen çoğaltılıyor
- Yeni sürümler kullanıma paketleriniz varsa algılama
- Pakete bağlıdır paketleri bulma

Bunu yaptığınızda, eski yöntemle bu genellikle bir zaman damgası tarafından OData paket varlık sıralama ve büyük sonuç kullanarak kümesi sayfalama bağımlı `skip` ve `top` (sayfa boyutu) parametreleri. Ne yazık ki bu yaklaşımının bazı dezavantajları vardır:

- Sorgular genellikle sırasını değiştirme veriler üzerinde gerçekleştirildiğinden olasılığını paketleri eksik
- Yavaş sorgu yanıt süresi, sorguları getirilmemiş olduğundan (en iyileştirilmiş sorgular, ana hat bir senaryo için resmi bir NuGet istemcisi desteği olan)
- Destek gibi sorguların gelecekte kullanım dışı ve belgelenmemiş API, kullanımını garanti edilmez
- Bağlanamama geçmişi, ilkelerinden tam sırayla yeniden Yürüt

Bu nedenle, aşağıdaki kılavuzda daha güvenilir ve geleceğe hazır bir şekilde yukarıda sözü edilen senaryolara izlenebilir.

## <a name="overview"></a>Genel Bakış

Bu kılavuzun merkezinde kaynaktır [NuGet API'si](../../api/overview.md) adlı **Kataloğu**. Katalog, eklenen paketler tam geçmişini görmek çağıranın izin veren bir yalnızca ekleme yapılabilen API değiştirilebilir ve nuget.org adresinden silinmiş olabilir. Tüm veya hatta nuget.org için yayımlanmış paketleri kümesini ilgileniyorsanız, katalog Zaman geçtikçe şu anda kullanılabilir paketler kümesiyle güncel kalmak için harika bir yoludur.

Bu kılavuz, üst düzey bir gözden geçirme ancak katalog detaylı ayrıntılarını ilgileniyorsanız bkz yöneliktir, [API başvuru belgesini](../../api/catalog-resource.md).

Aşağıdaki adımlar, tercih ettiğiniz programlama diliyle uygulanabilir. Tam bir çalışan örnek istiyorsanız göz atın [C# örneği](#c-sample-code) aşağıda belirtilen.

Aksi takdirde, bir güvenilir Kataloğu okuyucu oluşturmak için aşağıdaki kılavuzu izleyin.

## <a name="initialize-a-cursor"></a>Bir imleç Başlat

Bir güvenilir Kataloğu okuyucu oluşturmanın ilk adımı bir imleç uygular. Katalog imleci tasarımı hakkında tam Ayrıntılar için bkz [Kataloğu başvuru belgesini](../../api/catalog-resource.md#cursor). Kısacası, imleç bir zamanda kadar olay Kataloğu işledikten noktasıdır. Katalog temsil paketini olayları yayımlar ve başka bir paketin değiştirir. Şimdiye kadar (başlangıçtan itibaren) için NuGet yayımlanan tüm paketleri verdiğiniz "sınırın" zaman damgası için imlecinizi başlatmak (örneğin `DateTime.MinValue` .NET içinde). Şimdi başlangıç yayımlanan yalnızca paketleri hakkında dikkatli olun, ilk imleç değeriniz geçerli zaman damgasını kullanmanız gerekir.

Bu kılavuz için biz bir saat önce bir zaman damgası bizim imleç başlatmak. Şimdilik, zaman damgası bellekte yalnızca kaydedin.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Katalog dizini URL'si belirlenemedi

Kullanarak NuGet API'sindeki her kaynağın (uç nokta) yerini keşfedilmesini [hizmet dizini](../../api/service-index.md). Bu kılavuz nuget.org üzerinde odaklanır çünkü nuget.org hizmet dizini kullanacağız.

    GET https://api.nuget.org/v3/index.json

Hizmet belgesini tüm kaynakları nuget.org içeren JSON belgesidir. Sahip kaynak için konum `@type` özelliği değerinin `Catalog/3.0.0`. İlişkili `@id` özellik değeri, katalog dizini URL'si. 

## <a name="find-new-catalog-leaves"></a>Yeni Katalog leaves bulun

Kullanarak `@id` özellik değerini önceki adımda bulduğunuz katalog dizinini indirin:

    GET https://api.nuget.org/v3/catalog0/index.json

Seri durumdan [Kataloğu dizin](../../api/catalog-resource.md#catalog-index). Tüm filtre [sayfa nesneleri katalog](../../api/catalog-resource.md#catalog-page-object-in-the-index) ile `commitTimeStamp` geçerli imleç değerinizi küçüktür veya eşittir.

Kullanarak tüm belgenin geri kalan her katalog sayfası için indirme `@id` özelliği.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Seri durumdan [katalog sayfası](../../api/catalog-resource.md#catalog-page). Tüm filtre [yaprak nesneleri katalog](../../api/catalog-resource.md#catalog-item-object-in-a-page) ile `commitTimeStamp` geçerli imleç değerinizi küçüktür veya eşittir.

Tüm katalog sayfalar filtrelendi değil indirdikten sonra yayımlanmış, listede bulunmayan, listelenen veya silinen, imleç zaman damgası arasında bir süre silinmiş paketleri temsil eden bir katalog yaprak nesne olan ve artık.

## <a name="process-catalog-leaves"></a>İşlem Kataloğu bırakır

Bu noktada, katalog öğeleri üzerinde istediğiniz herhangi bir özel işlem gerçekleştirebilirsiniz. Tüm yapmanız gereken ise kimliği ve Paket sürümü inceleyebilirsiniz `nuget:id` ve `nuget:version` özellikleri katalog öğesi sayfalarında bulunan nesneler. Bakmak emin `@type` katalog öğesi var olan bir paket veya silinen paket ilgiliyse bilmek özelliği.

(Açıklama, bağımlılıkları, .nupkg boyutu, vb. gibi) paket hakkında meta verilerinde ilgileniyorsanız getirebilirsiniz [Kataloğu yaprak belge](../../api/catalog-resource.md#catalog-leaf) kullanarak `@id` özelliği.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Bu belgede bulunan meta verileri tümünün [paket meta veri kaynağı](../../api/registration-base-url-resource.md)ve daha fazlası!

Bu adım, özel mantığı uygulamak burada ' dir. Bu kılavuzdaki diğer adımlar uygulanır pretty içinde çok aynı katalog leaves ile neler yaptığına önemli yolu değil.

### <a name="downloading-the-nupkg"></a>.nupkg indiriliyor

İndirilirken ilgileniyorsanız .nupkg ait paketler için bulunan Kataloğu'nda kullanabileceğiniz [paket içerik kaynağı](../../api/package-base-address-resource.md). Ancak, bir paket kataloğunda bulunduğunda ve paket içerik kaynağı kullanılabilir olduğunda arasında kısa bir gecikme olduğunu unutmayın. Bu nedenle, karşılaşırsanız `404 Not Found` katalogda bulunan bir paket için bir .nupkg indirmeye çalışırken, yalnızca kısa bir süre daha sonra yeniden deneyin. Bu gecikme düzeltme GitHub sorunu tarafından izlenir [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>İmleci ileriye taşıyın

Katalog öğeleri başarıyla işledikten sonra kaydetmek için yeni imleç değeri belirlemek gerekir. Bunu yapmak için en fazla bulma (en son tarih sırasına göre) `commitTimeStamp` , işlenen tüm katalog öğeleri. Bu, yeni bir imleç değerdir. Bir veritabanı, dosya sistemi veya blob depolama gibi bazı kalıcı depoya kaydedin. Daha fazla katalog öğelerini almak istediğinizde, sadece başlangıç [ilk adım](#initialize-a-cursor) tarafından bu kalıcı depolama alanından, imleç değeri başlatılıyor.

Uygulamanızı bir özel durum ya da hatalar oluşturursa, imleç ileri taşıma. İmleç ilerletme hiçbir zaman yeniden imlecinizi önce katalog öğelerini işlemek için gereken bir anlamı vardır.

Bazı nedenlerden dolayı varsa, katalog işleminin nasıl içinde bir hata bırakır, yalnızca zaman içinde geriye dönük imlecinizi hareket ettirin ve eski katalog öğeleri yeniden işlemek kodunuzu izin.

## <a name="c-sample-code"></a>C# örnek kod

Katalog HTTP üzerinden bir dizi JSON belgeleri kullanılabilir olduğundan, istemci HTTP ve JSON seri durumdan çıkarıcının içeren herhangi bir programlama dilini kullanarak kurulabilen.

C# örnekleri kullanılabilir [NuGet/Samples deposuna](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK'sı katalog

Katalog kullanmak için en kolay yolu, yayın öncesi .NET Kataloğu SDK paketini kullanmaktır: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Bu paket üzerinde kullanılabilir `nuget-build` akışına MyGet NuGet paket kaynağı URL'si kullandığınız `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Bu paket ile uyumlu bir projeye yükleyebileceğiniz `netstandard1.3` veya üzeri (örneğin, .NET Framework 4. 6'da).

Bu paket kullanılarak bir örnek github'da kullanılabilir [NuGet.Protocol.Catalog.Sample proje](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

Daha ayrıntılı katalog etkileşimi gösteren bir örnek için daha az bağımlılıklar, bkz [CatalogReaderExample kodunuzla](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Projenizin hedeflediği `netcoreapp2.0` ve bağımlı [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet dizini çözme için) ve [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (için JSON seri durumundan çıkarma).

Kod ana mantığını görülebilir [Program.cs dosyasının](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
