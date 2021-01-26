---
title: NuGet 1,4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,4 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777144"
---
# <a name="nuget-14-release-notes"></a>NuGet 1,4 sürüm notları

[NuGet 1,3 sürüm notları](../release-notes/nuget-1.3.md)  |  [NuGet 1,5 sürüm notları](../release-notes/nuget-1.5.md)

NuGet 1,4, 17 Haziran 2011 tarihinde yayınlanmıştır.

## <a name="features"></a>Özellikler

### <a name="update-package-improvements"></a>Update-Package iyileştirmeler
NuGet 1,4, bir çözümde birden çok proje üzerinde paketlerin aynı sürümde tutulmasını kolaylaştıran Update-Package komutuna yönelik birçok geliştirme sunar. Örneğin, bir paketi en son sürüme yükseltirken, bu paketin yüklü olduğu tüm projelerin aynı Verision güncelleştirilmesini istemeniz çok yaygındır.

`Update-Package`Komut şu anda şunları kolaylaştırır:

#### <a name="update-all-packages-in-a-single-project"></a>Tek bir projedeki tüm paketleri Güncelleştir

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a>Tüm projelerdeki bir paketi güncelleştirme

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a>Tüm projelerdeki tüm paketleri Güncelleştir

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a>Tüm paketlerde "güvenli" bir güncelleştirme gerçekleştir
`-Safe`Bayrak, yükseltmeleri yalnızca aynı ana ve alt sürüm bileşeni olan sürümlerle kısıtlar. Örneğin, bir paketin 1.0.0 sürümü yüklüyse ve 1.0.1, 1.0.2 ve 1,1 sürümleri akışta varsa, `-Safe` bayrak paketi 1.0.2 olarak güncelleştirir. Bayrak olmadan yükseltme, `-Safe` paketi en son 1,1 sürümüne yükseltir.

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a>Çözüm düzeyinde paketleri yönetme
NuGet 1,4 ' den önce, iletişim kutusunu kullanarak bir paketin birden fazla projeye yüklenmesi çok daha fazla. Her proje için iletişim kutusunun bir kez başlatılmasını gerektirdi.

NuGet 1,4 aynı anda birden çok projedeki paketleri yükleme/kaldırma/güncelleştirme desteği ekler. Çözümü sağ tıklayıp **NuGet Paketlerini Yönet** menü seçeneğini belirleyerek başlatmanız yeterlidir.

![Çözüm düzeyi NuGet Paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

İletişim kutusunun başlık çubuğunda, bir projenin adı değil, çözümün adının görüntülendiğini unutmayın.
Paket işlemleri artık işlemin uygulanması gereken projelerin listesine sahip onay kutularının bir listesini sağlar.

![NuGet paketleri proje seçimini Yönet](./media/manage-nuget-packages-project-selection.png)

Daha fazla ayrıntı için, [çözüm Için paketleri yönetme](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)konusuna bakın.

### <a name="constraining-upgrades-to-allowed-versions"></a>Yükseltmeleri Izin verilen sürümlere kısıtlama
Varsayılan olarak, `Update-Package` bir pakette komutu çalıştırırken (veya iletişim kutusunu kullanarak paketi güncelleştirirken), akıştaki en son sürüme güncelleştirilir. Tüm paketlerin güncelleştirilmesiyle ilgili yeni destek sayesinde, bir paketi belirli bir sürüm aralığına kilitlemek istediğiniz durumlar olabilir. Örneğin, uygulamanızın yalnızca bir paketin 2. * sürümüyle çalışabileceklerini, ancak 3,0 ve üzeri olduğunu bilirsiniz. Paketin yanlışlıkla 3 ' e güncelleştirilmesini engellemek için, NuGet 1,4, paketlerin yükseltilecekse, `packages.config` Yeni özniteliğini kullanarak dosyayı düzenleyerek sürümüne yükseltebilen sürüm aralığını kısıtlayan destek ekler `allowedVersions` .

Örneğin, aşağıdaki örnek `SomePackage` 2,0-3,0 (özel) sürüm aralığını paketin nasıl kilitleneceği gösterilmektedir.
`allowedVersions`Öznitelik, [Sürüm aralığı biçimini](../concepts/package-versioning.md#version-ranges)kullanarak değerleri kabul eder.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1,4 ' de, bir paketin belirli bir sürüm aralığına kilitlenmesini el ile düzenlenmiş olması gerektiğini unutmayın. NuGet 1,5 ' de, bu aralığı komut aracılığıyla yerleştirmeye yönelik destek eklemeyi planlıyoruz `Install-Package` .

### <a name="package-visualizer"></a>Paket görselleştiricisi
**Araçlar**  ->  **kitaplığı Paket Yöneticisi**  ->  **paket görselleştiricisi** menü seçeneği aracılığıyla başlatılan yeni paket görselleştiricisi, bir çözüm içindeki tüm projeleri ve bunların paket bağımlılıklarını kolayca görselleştirmenizi sağlar.

_**Önemli bir dikkat:** Bu özellik, Visual Studio 'daki DGML desteğinden yararlanır. Görselleştirmenin oluşturulması yalnızca Visual Studio Ultimate desteklenir. DGML diyagramını görüntülemek yalnızca Visual Studio Premium veya üzeri sürümlerde desteklenir._

![Paket görselleştiricisi](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet Iletişim kutusu için otomatik güncelleştirme denetimi
NuGet 'in bazı sürümleri, `.nuspec` NuGet iletişim kutusunun eski sürümleri tarafından anlaşılmayan dosya aracılığıyla ifade edilen yeni özellikler sunar.
Örnek olarak, [çerçeve derlemelerini belirtmek](../release-notes/nuget-1.2.md#framework-assembly-refs)için NuGet 1,4 ' de giriş bir örnektir.
Bu nedenle, en son özelliklerden yararlanarak paketleri kullanabilmeniz için NuGet 'in en son sürümünü kullanmak önemlidir.
NuGet güncelleştirmelerini daha görünür hale getirmek için NuGet iletişim kutusu, daha yeni bir sürüm kullanılabilir olduğunda vurgulanacak mantığı içerir.

_**Note**: denetim, yalnızca **çevrimiçi** sekme geçerli oturumda seçildiyse yapılır._

![NuGet Paketlerini Yönet iletişim kutusunu yeni sürümü kullanılabilir](./media/manage-nuget-packages-update-notification.png)

Güncelleştirmelerin otomatik denetimini devre dışı bırakmak için NuGet ayarları iletişim kutusuna gidin ve **güncelleştirmeleri otomatik olarak denetle onay** kutusunun işaretini kaldırın.

![NuGet ayarları](./media/nuget-settings.png)

Bu özellik aslında NuGet 1,3 ' ye eklenmiştir, ancak, NuGet 1,4 gibi 1,3 ' ye bir güncelleştirme yapıldığından, bu özellik görünür olmaz.

### <a name="package-manager-dialog-improvements"></a>Paket Yöneticisi Iletişim geliştirmeleri
* **Gelişmiş menü adları**: iletişim kutusunu başlatmak için menü seçenekleri açıklık için yeniden adlandırıldı. Menü seçeneği artık **NuGet paketlerini yönetir**.
* **Ayrıntılar bölmesi en son güncelleştirme tarihini gösterir**: NuGet iletişim kutusu, **çevrimiçi** veya **güncelleştirmeler** sekmesi seçildiğinde bir paketin Ayrıntılar bölmesindeki en son güncelleştirme tarihini görüntüler.
* **Görüntülenen etiketlerin listesi**: NuGet iletişim kutusu etiketleri görüntüler.

### <a name="powershell-improvements"></a>PowerShell geliştirmeleri
* **Imzalı PowerShell betikleri**: NuGet, daha kısıtlayıcı ortamlarda kullanımı etkinleştiren imzalı PowerShell betikleri içerir.
* **Destek sorma**: Paket Yöneticisi konsolu artık ve komutları aracılığıyla sorma desteği `$host.ui.Prompt` desteklemektedir `$host.ui.PromptForChoice` .
* **Paket kaynak adları**: bayrağı kullanılarak bir paket kaynağı belirtildiğinde bir paket kaynağının adı sağlama desteklenir `-Source` .

### <a name="nugetexe-command-line-improvements"></a>nuget.exe komut satırı iyileştirmeleri
* **NuGet özel komutları**: nuget.exe MEF kullanılarak özel komutlar aracılığıyla Genişletilebilir.
* **Sembol paketleri oluşturmak Için daha basit iş akışı**: `-Symbols` bayrak, yalnızca klasör içindeki kaynak ve dosyalar dahil olmak üzere bir semboller paketi oluşturan normal bir kural tabanlı klasör yapısına uygulanabilir `.pdb` .
* **Birden çok kaynak belirtme**: `NuGet install` komut, noktalı virgül veya `-Source` birden çok kez belirterek birden çok kaynak belirtmeyi destekler.
* **Proxy kimlik doğrulaması desteği**: NuGet 1,4, kimlik doğrulaması gerektiren bir proxy 'Nin arkasında NuGet kullanılırken Kullanıcı kimlik bilgileri istemek için destek ekler.
* **nuget.exe güncelleştirme son değişikliği**: `-Self` nuget.exe kendisini güncelleştirmek için artık bayrak gereklidir. `nuget.exe Update` Şimdi dosyanın bir yolunu alır `packages.config` ve paketleri güncelleştirmeye çalışır. Bu güncelleştirmenin sınırlı olduğunu unutmayın: * * proje dosyasındaki içeriği Güncelleştir, Ekle, kaldır.
* * Paket içinde PowerShell betikleri çalıştırın.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>nuget.exe kullanarak paket göndermek için NuGet sunucu desteği
NuGet, NuGet paketi aracılığıyla [basit bir Web tabanlı NuGet deposunu](../hosting-packages/nuget-server.md) barındırmak için basit bir yol içerir `NuGet.Server` . NuGet 1,4 ile, hafif sunucu nuget.exe kullanarak paketleri göndermeyi ve silmeyi destekler.
En son sürümü `NuGet.Server` , adlı yeni bir ekler `appSetting` `apiKey` . Anahtar atlanmışsa veya boş bırakılırsa, paketleri akışa göndermek devre dışı bırakılır. ApiKey değerini bir değer olarak ayarlama (ideal bir parola), nuget.exe kullanarak paketlerin ititmesine olanak sağlar.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone araçları Mango sürümü desteği
NuGet, şimdi Mango için Windows Phone araçları sürüm adayı sürümünde desteklenmektedir.
Şu anda Windows Phone araçları Visual Studio Uzantı Yöneticisi için desteğe sahip olmadığından, Windows Phone araçları için NuGet 'i yüklemeniz, VSıX 'i el ile indirip çalıştırmanız gerekebilir.

NuGet Windows Phone araçları 'nı kaldırmak için aşağıdaki komutu çalıştırın.

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1,4, Toplam 88 iş öğesine sahipti. 71 tanesi hata olarak işaretlendi.

NuGet 1,4 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.

## <a name="bug-fixes-worth-noting"></a>Hata düzeltmeleri dikkat edilecek değer:

* [Sorun 603](http://nuget.codeplex.com/workitem/603): belirli bir paket kaynağını belirtirken farklı depolardaki paket bağımlılıkları doğru şekilde çözümleniyor.
* [Sorun 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` Derleme sonrası olaya ekleme artık sonsuz bir döngüye neden oluyor.
* [Sorun 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrak göreli yolları destekler.

## <a name="nuget-14-update"></a>NuGet 1,4 Güncelleştirmesi
NuGet 1,4 yayımlandıktan kısa bir süre sonra, düzeltilmesi gereken birkaç sorunu bulduk.
Bu güncelleştirmenin 1,4 sürümüne özgü sürüm numarası 1.4.20615.9020 ' dir.

### <a name="bug-fixes"></a>Hata Düzeltmeleri
* [Sorun 1220](http://nuget.codeplex.com/workitem/1220): birden `install.ps1` / `uninstall.ps1` fazla proje olduğunda Update-Package tüm projelerde yürütülmüyor
* [Sorun 1156](http://nuget.codeplex.com/workitem/1156): paket YÖNETICISI konsol w2k3/XP 'de takıldı (PowerShell 2 yüklü olmadığında)
