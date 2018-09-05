---
title: NuGet 1.4 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.4 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550637"
---
# <a name="nuget-14-release-notes"></a>NuGet 1.4 sürüm notları

[1.3 NuGet sürüm notları](../release-notes/nuget-1.3.md) | [1.5 NuGet sürüm notları](../release-notes/nuget-1.5.md)

NuGet 1.4 17 Haziran 2011'de yayınlanmıştır.

## <a name="features"></a>Özellikler

### <a name="update-package-improvements"></a>Update-Package geliştirmeleri
NuGet 1.4 birçok geliştirme paketlerini bir çözümde birden çok proje boyunca aynı sürümde tutmak kolaylaştırarak Update-Package komutuna tanıtır. Örneğin, bir paketin en son sürüme yükselttiğinizde, tüm projeler için aynı verision güncelleştirilecek yüklü, paketin ile istediğiniz yaygın olarak.

`Update-Package` Komutu artık kolaylaştırır için:

#### <a name="update-all-packages-in-a-single-project"></a>Tek bir projede tüm paketleri güncelleştir

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Bir paketteki tüm projeleri güncelleştir

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Tüm projelerde tüm paketleri güncelleştir

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Tüm paketleri "güvenli" güncelleştirme gerçekleştirme
`-Safe` Bayrağı yükseltmeleri yalnızca sürümleri aynı ana ve alt sürüm bileşeni ile kısıtlar. Örneğin bir paket 1.0.0 sürümü yüklü ve 1.0.1, 1.0.2 ve 1.1 sürümleri akışında kullanılabilir `-Safe` bayrağı için 1.0.2 paketi güncelleştirir. Olmadan yükseltme `-Safe` bayrağı en son sürüm 1.1 paketi yükseltmeniz.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Paketleri çözüm düzeyinde yönetme
NuGet 1.4 önce hantal iletişim kutusunu kullanarak birden çok proje bir paketi yükleniyor. Her proje için bir kez iletişim kutusunu başlatarak gerekli.

NuGet 1.4, aynı anda birden çok proje yükleme/kaldırma/güncelleştirme paketleri için destek ekler. Yalnızca başlatma çözüme sağ tıklayarak ve seçerek **NuGet paketlerini Yönet** menü seçeneği.

![Çözüm düzeyi NuGet paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

İletişim kutusunun başlık çubuğunda çözümün adına görüntülendiğini bildirimi, bir proje adı değil.
Paket işlemleri artık onay kutularını listesiyle işlemi uygulamalısınız projelerinin listesini sağlar.

![NuGet paketleri proje seçimi yönetme](./media/manage-nuget-packages-project-selection.png)

Daha fazla ayrıntı için üzerinde konusuna bakın. [çözüm için paketler yönetme](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Sınırlamak için izin verilen sürümler yükseltme
Varsayılan olarak çalıştırırken `Update-Package` bir paket (veya iletişim kutusunu kullanarak paketi güncelleştiriliyor) komutunu akıştaki en son sürüme güncelleştirilir. Tüm paketleri güncelleştirmeye yönelik yeni destek sayesinde, belirli bir sürüm aralığı için bir paket kilitlemek istediğiniz durumlar olabilir. Örneğin, uygulamanızın yalnızca bir paketin, ancak değil 3.0 ve sonraki sürüm 2.* ile çalışmasını önceden haberdar olabilirsiniz. Yanlışlıkla Paketi 3'e güncelleştiriliyor önlemek için NuGet 1.4 aralığını paketleri elle düzenleyerek yükseltilebilir sürümleri için destek ekler `packages.config` kullanarak yeni dosya `allowedVersions` özniteliği.

Örneğin, aşağıdaki örnekte nasıl kilitleneceği gösterilir `SomePackage` paket sürüm aralığı 2.0-3.0 (dışlamalı).
`allowedVersions` Öznitelik değerlerini kullanarak kabul [sürüm aralığı biçim](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

1.4 içinde belirli bir sürüm aralığı için bir paket kilitleme elle düzenlenerek olması gerektiğini unutmayın. Bu aralık üzerinden yerleştirmek için destek eklemeyi planlıyoruz NuGet 1.5 `Install-Package` komutu.

### <a name="package-visualizer"></a>Paket görselleştiricisi
Aracılığıyla başlatılan yeni paket Görselleştirici **Araçları** -> **kitaplık Paket Yöneticisi** -> **paket Görselleştirici** menü seçeneğini olanak tanır kolayca tüm projeleri ve bir çözüm içindeki Paket bağımlılıklarını görselleştirin.

_**Önemli Not:** bu özellik DGML destek Visual Studio'da yararlanır. Görselleştirmenin oluşturulması yalnızca bu kadar Visual Studio Ultimate içinde desteklenir. DGML diyagramını görüntüleme, yalnızca Visual Studio Premium veya yüksek desteklenir._

![Paket görselleştiricisi](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>NuGet iletişim kutusu için otomatik güncelleştirme denetimi
NuGet'ün bazı sürümleri ile ifade edilen yeni özellikleri tanıtan `.nuspec` NuGet iletişim daha eski sürümleri tarafından anlaşılmayan dosyası.
Bir örnektir giriş için NuGet 1.4 [framework derlemeleri belirtme](../release-notes/nuget-1.2.md#framework-assembly-refs).
Bu nedenle, en yeni özelliklerinden yararlanarak paketleri kullanabilir emin olmak için en son sürümünü kullanmak önemlidir.
Güncelleştirmeler için NuGet daha görünür yapmak için NuGet iletişim daha yeni bir sürümü kullanılabilir olduğunda vurgulamak için mantığı içerir.

_**Not**: onay ise yalnızca gerçekleştirilir **çevrimiçi** sekmesinde geçerli oturumda seçilmiştir._

![NuGet paketlerini iletişim yeni sürüm ile yönetme](./media/manage-nuget-packages-update-notification.png)

Güncelleştirmeleri otomatik olarak denetlenmesi kapatmak için NuGet Ayarları iletişim kutusuna gidin ve işaretini kaldırın **güncelleştirmeleri otomatik olarak denetle**.

![NuGet ayarları](./media/nuget-settings.png)

Bu özellik, NuGet 1.3 aslında eklendi ancak Elbette, 1.3, 1.4 NuGet gibi bir güncelleştirme kadar görünür olmayacaktır, kullanıma sunuldu.

### <a name="package-manager-dialog-improvements"></a>Paket Yöneticisi iletişim kutusu iyileştirmeleri
* **Menü adları geliştirilmiş**: Menü Seçenekleri iletişim kutusunu başlatmak için daha anlaşılır olması için yeniden adlandırıldı. Menü seçeneği sunulmuştur **NuGet paketlerini Yönet**.
* **Ayrıntılar bölmesinde, en son güncelleştirme tarihi gösterir**: NuGet iletişim Ayrıntılar bölmesinde bir paket için en son güncelleştirme tarihi görüntüler olduğunda **çevrimiçi** veya **güncelleştirmeleri** sekmesi seçili.
* **Görüntülenen etiketler listesi**: Nuget iletişim kutusu, etiketler görüntüler.

### <a name="powershell-improvements"></a>PowerShell iyileştirmeleri
* **PowerShell komut dosyalarını oturum açmış**: NuGet daha kısıtlayıcı ortamlarda kullanımını etkinleştirme imzalı Powershell betikleri içerir.
* **Destek isteyen**: Paket Yöneticisi konsolu destekler aracılığıyla isteyen `$host.ui.Prompt` ve `$host.ui.PromptForChoice` komutları.
* **Paket kaynak adları**: bir paket kaynağının adını sağlama desteklenir kullanarak bir paket kaynak belirtirken `-Source` bayrağı.

### <a name="nugetexe-command-line-improvements"></a>nuget.exe komut satırı geliştirmeleri
* **NuGet özel komutlar**: nuget.exe MEF kullanarak özel komutları genişletilebilir.
* **Daha basit sembol paketleri oluşturmak için iş akışı**: `-Symbols` bayrağı yalnızca kaynak ekleyerek sembolleri paket oluşturma normal kuralına göre klasör yapısı uygulanabilir ve `.pdb` klasördeki dosyaları.
* **Birden çok kaynaktan belirtme**: `NuGet install` komutu destekler belirterek veya sınırlayıcı olarak noktalı virgül kullanarak birden çok kaynaktan belirtme `-Source` birden çok kez.
* **Proxy kimlik doğrulaması desteği**: NuGet 1.4 NuGet kimlik doğrulaması gerektiren bir proxy kullanırken kullanıcı kimlik bilgileri istemi için destek ekler.
* **nuget.exe yeni değişiklik güncelleştirme**: `-Self` bayrağı, artık kendisini güncelleştirmek nuget.exe için gereklidir. `nuget.exe Update` artık bir yol alır `packages.config` dosya ve güncelleştirme paketleri dener. Gerçekleştirmez, bu güncelleştirme sınırlı olduğunu unutmayın: ** güncelleştirme, Ekle, içeriğini proje dosyasında kaldırın.
** Paket içindeki Powershell betiklerini çalıştırın.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Nuget.exe kullanarak paketleri gönderme için NuGet sunucu desteği
NuGet içeren basit bir yol barındırmak için bir [basit bir web tabanlı NuGet depo](../hosting-packages/nuget-server.md) aracılığıyla `NuGet.Server` NuGet paketi. NuGet 1.4 ile dağıtmaya ve nuget.exe kullanarak paketleri silme basit sunucusu destekler.
En son sürümünü `NuGet.Server` yeni ekler `appSetting`, adlandırılmış `apiKey`. Anahtar atlanırsa veya boş bırakılması, akışa paketleri gönderme devre dışı bırakıldı. ApiKey (İdeal olarak güçlü bir parola) bir değere ayarlama nuget.exe kullanarak koymadan paketleri sağlar.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Windows Phone araçları Mango sürümü için destek
NuGet, Windows Phone araçları Mango için yayın adayı sürümünde artık desteklenmektedir.
Şu anda Windows Phone araçları, bu nedenle Windows Phone araçları için NuGet yüklemek Visual Studio uzantısı Yöneticisi için destek yok, indirin ve VSIX elle çalıştırmanız gerekebilir.

Windows Phone araçları için NuGet kaldırmak için aşağıdaki komutu çalıştırın.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.4 88 toplam iş öğeleri sabit vardı. Bu 71 hataları olarak işaretlenmiş.

Tam bir listesi için iş öğeleri NuGet 1.4 içinde lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Önemli hata düzeltmeleri:

* [Sorun 603](http://nuget.codeplex.com/workitem/603): farklı depoları Paket bağımlılıklarını çözümler doğru şekilde belirli bir paket kaynağını belirtmek için.
* [Sorun 1036](http://nuget.codeplex.com/workitem/1036): ekleme `NuGet Pack SomeProject.csproj` artık derleme sonrası olay için sonsuz bir döngüye neden olur.
* [Sorun 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrağı göreli yolları destekler.

## <a name="nuget-14-update"></a>NuGet 1.4 Güncelleştirme
Kısa bir süre içinde sürümünden NuGet 1.4 sonra birkaç düzeltmek önemli sorunları bulduk.
Belirli sürüm 1.4 Bu güncelleştirmeyi 1.4.20615.9020 sayısıdır.

### <a name="bug-fixes"></a>Hata Düzeltmeleri
* [Sorun 1220](http://nuget.codeplex.com/workitem/1220): Update-Package değil yürütme `install.ps1` / `uninstall.ps1` birden fazla proje olduğunda tüm projelerde
* [Sorunu 1156](http://nuget.codeplex.com/workitem/1156): Paket Yöneticisi konsol takılı W2K3/XP'de (Powershell 2 yüklü olmadığında)
