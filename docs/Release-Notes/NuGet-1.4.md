---
title: "NuGet 1.4 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.4 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 1.4 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bc0800361551b996d958e03b9cfa3d745b78e43d
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 sürüm notları

[NuGet 1.3 Sürüm Notları](../release-notes/nuget-1.3.md) | [NuGet 1.5 sürüm notları](../release-notes/nuget-1.5.md)

NuGet 1.4 17 Haziran 2011'de serbest bırakıldı.

## <a name="features"></a>Özellikler

### <a name="update-package-improvements"></a>Güncelleştirme paketi geliştirmeleri
NuGet 1.4 çok sayıda daha kolay bir çözümde birden çok proje arasında aynı sürümünde paketleri tutmak güncelleştirme paketi komut geliştirmeleri tanıtır. Örneğin, bir paketin en son sürümüne yükseltirken, tüm projeleri aynı verision güncelleştirilmesi yüklü, paketin istiyor için çok yaygındır.

`Update-Package` Komutu şimdi kolaylaştırır için:

#### <a name="update-all-packages-in-a-single-project"></a>Güncelleştirme tek projesindeki tüm paketleri

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Tüm projelerde paketi güncelleştir

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Güncelleştirme tüm projelerdeki tüm paketleri

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Tüm paketleri "safe" bir güncelleştirme gerçekleştirmek
`-Safe` Bayrağı yükseltmeleri aynı birincil ve ikincil sürüm bileşeni ile yalnızca sürümleri için kısıtlar. Örneğin bir paketin 1.0.0 sürümü yüklüyse ve akışta 1.0.1, 1.0.2 ve 1.1 sürümleri kullanılabilir `-Safe` bayrağı Paketi 1.0.2 sürümüne güncelleştirir. Olmadan yükseltme `-Safe` bayrağı en son sürüm 1.1 paket yükseltmeniz.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Çözüm düzeyinde paketlerini yönetme
NuGet 1.4 önce bir paket birden çok projeye yükleme iletişim kutusunu kullanarak sıkıcı. Bu, her proje için bir kez iletişim başlatma gerekli.

NuGet 1.4, aynı anda birden çok proje yükleme/kaldırma/güncelleştirme paketleri için destek ekler. Yalnızca başlatma çözüme sağ tıklatarak ve seçerek **NuGet paketlerini Yönet** menü seçeneği.

![Çözüm düzeyi NuGet paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

Çözüm adı iletişim başlık çubuğunda görüntülenir dikkat edin, bir proje adı değil.
Paket işlemleri şimdi listesiyle işlemi uygulanması gereken projelerinin listesini onay kutularını sağlar.

![NuGet paketleri proje seçimi yönetme](./media/manage-nuget-packages-project-selection.png)

Daha fazla ayrıntı için üzerinde konusuna [çözüm paketlerini yönetme](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>İzin için sürümler sınırlama yükseltir
Varsayılan olarak çalışırken, `Update-Package` bir paket (veya iletişim kutusu kullanılarak paketi güncellemeden) komutunu akıştaki en son sürümüne güncelleştirilir. Tüm paketler güncelleştirmek için yeni destek ile bir pakete belirli sürüm aralığı kilitlemek istediğiniz durumlar olabilir. Örneğin, uygulamanızın yalnızca sürüm 2.* bir paketin, ancak değil 3.0 ve üstü ile çalışıp çalışmayacağını önceden bilmeniz. Yanlışlıkla Paketi 3'e güncelleştirme önlemek için NuGet 1.4 aralığını paketler için elle düzenleyerek yükseltilebilir sürümleri için destek ekler `packages.config` kullanarak yeni dosya `allowedVersions` özniteliği.

Örneğin, aşağıdaki örnekte kilitlemek gösterilmektedir `SomePackage` paket sürüm 2.0-3.0 (özel) aralık.
`allowedVersions` Öznitelik değerlerini kullanarak kabul [sürüm aralığı biçimi](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1.4 içinde belirli sürüm aralığı için bir paket kilitleme el ile düzenleyebilirsiniz olması gerektiğini unutmayın. Bu aralık aracılığıyla yerleştirmek için destek eklemeyi planlıyoruz NuGet 1.5 `Install-Package` komutu.

### <a name="package-visualizer"></a>Paket Görselleştirici
Aracılığıyla başlatılan yeni paket Görselleştirici **Araçları** -> **kitaplık Paket Yöneticisi** -> **paket Görselleştirici** menü seçeneği olanak sağlar kolayca tüm projeleri ve Paket bağımlılıklarını bir çözüm içinde görselleştirin.

_**Önemli Not:** bu özellik DGML destek Visual Studio'da yararlanır. Görselleştirme oluşturuluyor yalnızca bu kadar Visual Studio Ultimate'ta desteklenir. DGML diyagramını görüntülemek, yalnızca Visual Studio Premium veya yüksek desteklenmez._

![Paket Görselleştirici](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet iletişim için otomatik güncelleştirme denetimi
NuGet'ın bazı sürümleri aracılığıyla ifade yeni özellikleri tanıtır `.nuspec` NuGet iletişim eski sürümleri tarafından anlaşılmayan dosya.
Bir örnektir için NuGet 1.4 içindeki giriş [framework derlemeleri belirtme](../release-notes/nuget-1.2.md#framework-assembly-refs).
Bu nedenle, en son özelliklere yararlanarak paketlerini kullanmadan emin olmak için NuGet'ın en son sürümünü kullanmak önemlidir.
Güncelleştirmeler için NuGet daha görünür hale getirmek için NuGet iletişim daha yeni bir sürümü kullanılabilir olduğunda vurgulamak için mantığını içerir.

_**Not**: denetimi yalnızca varsa yapılan **çevrimiçi** sekmesinde geçerli oturumdaki seçildi._

![NuGet paketlerini iletişim yeni sürümü kullanılabilir ile yönetme](./media/manage-nuget-packages-update-notification.png)

Güncelleştirmeleri otomatik olarak denetlenmesi kapatmak için NuGet Ayarları iletişim kutusuna gidin ve onay kutusunu temizleyin **güncelleştirmeleri otomatik olarak denetle**.

![NuGet ayarları](./media/nuget-settings.png)

Bu özellik NuGet 1.3 içinde gerçekte eklendi ancak doğal olarak, NuGet 1.4 gibi 1.3 için bir güncelleştirme kadar görünür olmaz, kullanıma sunuldu.

### <a name="package-manager-dialog-improvements"></a>Paket Yöneticisi iletişim geliştirmeleri
* **Menü adları geliştirilmiş**: Menü Seçenekleri iletişim kutusunu başlatmak için daha anlaşılır olması için yeniden adlandırıldı. Menü seçeneği sunulmuştur **NuGet paketlerini Yönet**.
* **Ayrıntılar bölmesinde, en son güncelleştirme tarihi gösterilir**: NuGet iletişim Ayrıntılar bölmesinde bir paket için en son güncelleştirme tarihi görüntüler zaman **çevrimiçi** veya **güncelleştirmeleri** sekmesi seçilmiştir.
* **Görüntülenen etiketler listesi**: Nuget iletişim etiketleri görüntüler.

### <a name="powershell-improvements"></a>PowerShell geliştirmeleri
* **PowerShell komut dosyalarını imzalı**: NuGet daha kısıtlayıcı ortamlarda kullanım etkinleştirme imzalı Powershell komut dosyalarını içerir.
* **Destek isteyen**: Paket Yöneticisi konsolu artık destekliyor aracılığıyla isteyen `$host.ui.Prompt` ve `$host.ui.PromptForChoice` komutları.
* **Paket kaynağı adları**: bir paket kaynağının adı sağladığını desteklenir kullanarak bir paket kaynak belirtirken `-Source` bayrağı.

### <a name="nugetexe-command-line-improvements"></a>nuget.exe komut satırı geliştirmeleri
* **NuGet özel komutları**: nuget.exe MEF kullanarak özel komutları genişletilebilir.
* **Daha basit simge paketleri oluşturmak için iş akışı**: `-Symbols` bayrağı yalnızca kaynak ekleyerek simgeleri paket oluşturma normal kurala dayalı klasör yapısı uygulanabilir ve `.pdb` klasördeki dosyalar.
* **Birden çok kaynakları belirtme**: `NuGet install` komutu destekler noktalı ayırıcı olarak veya belirterek kullanarak birden çok kaynakları belirtme `-Source` birden çok kez.
* **Proxy kimlik doğrulama desteği**: NuGet 1.4 NuGet kimlik doğrulaması gerektiren bir proxy kullanırken kullanıcı kimlik bilgileri için destek ekler.
* **nuget.exe sonu değişiklik güncelleştirme**: `-Self` bayrağı olan şimdi kendisini güncelleştirmek nuget.exe için gerekli. `nuget.exe Update` Şimdi bir yolunda alır `packages.config` dosya ve güncelleştirme paketleri dener. İçinde değil, bu güncelleştirme sınırlı olduğunu unutmayın: ** güncelleştirme eklemek için içerik proje dosyasında kaldırın.
** Paketin içinde Powershell betikleri çalıştırmak.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe kullanarak paketleri gönderilmesi için NuGet sunucu desteği
NuGet barındırmak için basit bir yol içeren bir [basit bir web tabanlı NuGet deposu](../hosting-packages/nuget-server.md) aracılığıyla `NuGet.Server` NuGet paketi. NuGet 1.4 ile basit sunucunun itme ve nuget.exe kullanarak paketleri silme destekler.
En son sürümünü `NuGet.Server` yeni ekler `appSetting`, adlandırılmış `apiKey`. Anahtar atlanmış ya da boş bırakılırsa, paketleri akışa Ftp'den devre dışı bırakılır. Apikey ile yapılan bir değere (İdeal olarak güçlü bir parola) ayarlamak nuget.exe kullanarak koymadan paketleri sağlar.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone araçları Mango Edition için destek
NuGet Mango için Windows Phone Araçları Sürüm Adayı sürümünde artık desteklenmektedir.
Şu anda, Windows Phone araçları şekilde NuGet Windows Phone için araçları yüklemek Visual Studio uzantısı Yöneticisi için destek yok, indirin ve VSIX elle çalıştırmanız gerekebilir.

Windows Phone araçları NuGet kaldırmak için aşağıdaki komutu çalıştırın.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.4 iş öğeleri sabit 88 toplam vardı. Bu 71 hata olarak işaretlendi.

Tam bir listesi için iş öğeleri NuGet 1.4 içinde lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Eşitlenmeyeceği hata düzeltmeleri:

* [Sorunu 603](http://nuget.codeplex.com/workitem/603): Paket bağımlılıklarını farklı depoları arasında çözümler doğru belirli paket kaynak belirtirken.
* [Sorunu 1036](http://nuget.codeplex.com/workitem/1036): ekleme `NuGet Pack SomeProject.csproj` olay derleme artık sonrası için sonsuz bir döngüye neden olur.
* [Sorunu 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrağı göreli yollar destekler.

## <a name="nuget-14-update"></a>NuGet 1.4 Güncelleştirme
Kısa süre içinde sürümünden NuGet 1.4 sonra birkaç düzeltmek önemli sorunları bulduk.
Belirli bir sürüm 1.4 bu güncelleştirmeye 1.4.20615.9020 sayısıdır.

### <a name="bug-fixes"></a>Hata Düzeltmeleri
* [Sorunu 1220](http://nuget.codeplex.com/workitem/1220): değil güncelleştirme paketi yürütmek `install.ps1` / `uninstall.ps1` birden fazla proje olduğunda tüm projelerdeki
* [Sorun 1156](http://nuget.codeplex.com/workitem/1156): Paket Yöneticisi konsol takılmış W2K3/XP'de (Powershell 2 yüklü olmadığında)
