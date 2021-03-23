---
title: Nuget.org 'e yayınlanan tüm paketler için sorgu
description: NuGet API 'sini kullanarak, nuget.org ' de yayınlanan tüm paketleri sorgulayabilir ve zaman içinde güncel kalın.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 8f21aad93eb952035683314c10cd964f265ec4fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859349"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Nuget.org 'e yayınlanan tüm paketler için sorgu

Eski OData v2 API 'sindeki yaygın bir sorgu deseninin, paket yayımlandığında tarafından sıralanan, nuget.org 'e yayınlanan tüm paketler numaralandırıldığı için. Nuget.org karşı bu tür bir sorgu gerektiren senaryolar farklılık gösterir:

- Nuget.org tamamen çoğaltılıyor
- Paketlerin yeni sürümleri ne zaman yayımlanmışsa algılanıyor
- Paketinize bağlı paketleri bulma

Bunu yapmanın eski yolu, genellikle OData paketi varlığının, `skip` ve `top` (sayfa boyutu) parametreleri kullanılarak oluşan büyük sonuç kümesinde bir zaman damgası ve sayfalama yoluyla sıralanarak yapılır. Ne yazık ki bu yaklaşımın bazı dezavantajları vardır:

- Eksik paket olma olasılığı, çünkü sorgular sıklıkla değişen sırada olan veriler üzerinde yapılıyor
- Sorgular en iyi duruma getirilmediğinden (en iyileştirilmiş sorgular resmi NuGet istemcisi için bir ana hat senaryosu destekleenler) yavaş sorgu yanıt süresi
- Kullanım dışı bırakılmış ve belgelenmemiş API 'nin kullanımı, gelecekte bu sorguların desteklenmesi garanti edilmez
- Geçmişi transpired doğru sırada yeniden oynalamama

Bu nedenle, aşağıdaki kılavuzun, daha güvenilir ve gelecekte prova bir şekilde açıklanan senaryolara yönelik olarak ele alınabilir.

## <a name="overview"></a>Genel Bakış

Bu kılavuzun merkezinde **Katalog** ADLı [NuGet API](../../api/overview.md) 'sindeki kaynak bulunur. Katalog, çağıranın nuget.org ' de eklenen, değiştirilen ve silinen paketlerin tam geçmişini görmesini sağlayan bir yalnızca Append API 'sidir. Nuget.org ' de yayınlanan paketlerin tümünün veya hatta bir alt kümesiyle ilgileniyorsanız, katalog, zaman içinde mevcut olan paketler kümesiyle güncel kalabilmek için harika bir yoldur.

Bu kılavuzun üst düzey bir adım adım olması amaçlanmıştır ancak kataloğun ayrıntılı ayrıntılarını almak istiyorsanız, [API başvuru belgesine](../../api/catalog-resource.md)bakın.

Aşağıdaki adımlar, tercih ettiğiniz herhangi bir programlama dilinde uygulanabilir. Tam çalışan bir örnek istiyorsanız aşağıda bahsedilen [C# örneğine](#c-sample-code) göz atın.

Aksi takdirde, güvenilir bir katalog okuyucusu oluşturmak için aşağıdaki kılavuzu izleyin.

## <a name="initialize-a-cursor"></a>İmleç başlatma

Güvenilir bir katalog okuyucusu oluşturmanın ilk adımı bir imleç uygulamalarıdır. Katalog imlecinin tasarımı hakkında tam Ayrıntılar için bkz. [Katalog başvuru belgesi](../../api/catalog-resource.md#cursor). Kısaca, imleç katalogda olayları işleen zaman bir noktasıdır. Katalogdaki olaylar paket yayımlarımı ve diğer paket değişikliklerini temsil eder. NuGet 'e yayınlanan tüm paketlerle (zamandan itibaren) endişelenmeniz durumunda imlecinizi "En düşük değer" zaman damgasına (örn. `DateTime.MinValue` .net 'te) başlatmalısınız. Yalnızca şu anda yayımlanan paketler hakkında hatırlıyorsanız, geçerli zaman damgasını ilk imleç değeri olarak kullanacaksınız.

Bu kılavuzda, imlecinizi bir saat önce zaman damgasına başlatacağız. Şimdilik bu zaman damgasını bellekte kaydetmelisiniz.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Katalog dizini URL 'sini belirleme

NuGet API 'sindeki her kaynağın (uç nokta) konumu, [hizmet dizini](../../api/service-index.md)kullanılarak keşfedilmelidir. Bu kılavuz nuget.org 'e odaklandığından NuGet. org 'ın hizmet dizinini kullanacağız.

```
GET https://api.nuget.org/v3/index.json
```

Hizmet belgesi, nuget.org üzerindeki tüm kaynakları içeren JSON belgesidir. Özellik değerine sahip kaynağı arayın `@type` `Catalog/3.0.0` . İlişkili `@id` özellik değeri, Katalog dizininin URL 'sidir. 

## <a name="find-new-catalog-leaves"></a>Yeni Katalog bul yaprakları

`@id`Önceki adımda bulunan özellik değerini kullanarak, Katalog dizinini indirin:

```
GET https://api.nuget.org/v3/catalog0/index.json
```

[Katalog dizininin](../../api/catalog-resource.md#catalog-index)serisini kaldırma. Geçerli imlecinizin değerine eşit veya daha küçük olan tüm [Katalog sayfası nesnelerini](../../api/catalog-resource.md#catalog-page-object-in-the-index) filtreleyin `commitTimeStamp` .

Kalan her bir katalog sayfası için, özelliğini kullanarak tam belgeyi indirin `@id` .

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

[Katalog sayfasının](../../api/catalog-resource.md#catalog-page)serisini kaldırma. Geçerli imlecinizin değerine eşit veya daha küçük olan tüm [Katalog yaprak nesnelerini](../../api/catalog-resource.md#catalog-item-object-in-a-page) filtreleyin `commitTimeStamp` .

Filtrelenmeyen tüm katalog sayfalarını indirdikten sonra, imlecinizin zaman damgası ve hemen sonrasında yayımlanmış, listelenmemiş, listelenen veya silinen paketleri temsil eden bir katalog yaprak nesneleri kümesine sahip olursunuz.

## <a name="process-catalog-leaves"></a>İşlem kataloğu yaprakları

Bu noktada, Katalog öğelerinde istediğiniz özel işlemleri gerçekleştirebilirsiniz. Tüm ihtiyacınız olan paketin KIMLIĞI ve sürümü ise, `nuget:id` `nuget:version` sayfada bulunan katalog öğesi nesnelerinde ve özelliklerini inceleyebilirsiniz. `@type`Katalog öğesinin mevcut bir paket veya silinen bir paket ile ilgilenmediğini görmek için özelliğine baktığınızdan emin olun.

Paketle ilgili meta veriler (örneğin, açıklama, bağımlılıklar,. nupkg boyutu vb.) ile ilgileniyorsanız, özelliğini kullanarak [Katalog yaprak belgesini](../../api/catalog-resource.md#catalog-leaf) getirebilirsiniz `@id` .

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

Bu belge, [paket meta verileri kaynağında](../../api/registration-base-url-resource.md)bulunan tüm meta verilere sahiptir ve daha fazla!

Bu adım, özel mantığınızı uyguladığınız yerdir. Bu kılavuzdaki diğer adımlar, Katalog yaprakları ile yaptığınız bağımsız şekilde oldukça benzer şekilde uygulanır.

### <a name="downloading-the-nupkg"></a>. Nupkg indiriliyor

Kataloğunda bulunan paketler için. nupkg 'yı indirmek istiyorsanız [paket içerik kaynağını](../../api/package-base-address-resource.md)kullanabilirsiniz. Ancak, katalogda bir paketin bulunduğu ve paket içerik kaynağında kullanılabildiği zaman arasında kısa bir gecikme olduğunu unutmayın. Bu nedenle, `404 Not Found` katalogda bulduğunuz bir paket için. nupkg 'yı indirmeye çalışırken karşılaşırsanız, daha sonra kısa bir süre sonra yeniden deneyin. Bu gecikmeyi düzeltmek, GitHub sorunu [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455)tarafından izlenir.

## <a name="move-the-cursor-forward"></a>İmleci öne taşı

Katalog öğelerini başarıyla işledikten sonra kaydedilecek yeni imleç değerini belirlemeniz gerekir. Bunu yapmak için, istediğiniz tüm Katalog öğelerinin en yüksek (en son kronolojik) `commitTimeStamp` sayısını bulun. Bu, yeni imlecinizin değeridir. Veritabanı, dosya sistemi veya blob depolama gibi bir kalıcı depoya kaydedin. Daha fazla katalog öğesi almak istediğinizde, bu kalıcı mağazadan imlecinizin değerini başlatarak [ilk adımdan](#initialize-a-cursor) başlamanız yeterlidir.

Uygulamanız bir özel durum veya hatalar oluşturursa, imleci öne taşımayın. İmleci ileriye doğru taşımak, imlecinizin öncesinde katalog öğelerini işlemek için hiçbir değişiklik yapmanıza gerek kalmaz.

Bazı nedenlerle, Katalog yaprakları sırasında bir hata varsa imlecinizi geri doğru bir şekilde hareket ettirmeniz ve kodunuzun eski katalog öğelerini yeniden işlemesini sağlayabilirsiniz.

## <a name="c-sample-code"></a>C# örnek kodu

Katalog, HTTP üzerinden kullanılabilen bir JSON belgeleri kümesi olduğundan, HTTP istemcisi ve JSON seri hale getiricisi olan herhangi bir programlama dili kullanılarak ile etkileşim kurabilirsiniz.

C# örnekleri [NuGet/Samples deposunda](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample)mevcuttur.

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog SDK 'Sı

Kataloğu kullanmanın en kolay yolu `NuGet.Protocol.Catalog` , aşağıdaki NuGet paketi kaynak URL 'si kullanılarak Azure Artifacts sağlanan yayın öncesi .net Catalog SDK paketini kullanmaktır: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .

Bu paketi, `netstandard1.3` veya daha büyük (.NET Framework 4,6 gibi) uyumlu bir projeye yükleyebilirsiniz.

Bu paketi kullanan bir örnek, [NuGet. Protocol. Catalog. Sample projesinde](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)GitHub 'da bulunabilir.

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

Daha ayrıntılı olarak katalogla etkileşimi gösteren daha az bağımlılıklara sahip bir örnek için bkz. [Catalogreadersample örnek projesi](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/CatalogReaderExample). Proje, `netcoreapp2.0` [NuGet. Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (hizmet dizinini çözümlemek için) ve [ 9.0.1 üzerindeNewtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON serisini kaldırma için) öğesine bağımlıdır.

Kodun ana mantığı [program. cs dosyasında](https://github.com/NuGet/Samples/blob/main/CatalogReaderExample/CatalogReaderExample/Program.cs)görünür.

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
