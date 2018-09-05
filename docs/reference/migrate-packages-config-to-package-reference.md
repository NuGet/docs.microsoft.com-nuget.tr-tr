---
title: PackageReference biçimlerine Package.config geçiş
description: Bir proje olarak NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen PackageReference package.config yönetim biçiminden geçirilecek hakkında ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 05a82e48c7083a19c50a05fa1df74ebfff8030d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546692"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages.config'i Packagereference'a geçirme

Visual Studio 2017 sürüm 15.7 ve üzeri destekler bir projeden geçirme [packages.config](./packages-config.md) yönetim biçimi [PackageReference](../consume-packages/Package-References-in-Project-Files.md) biçimi.

## <a name="benefits-of-using-packagereference"></a>PackageReference kullanmanın avantajları

* **Tüm proje bağımlılıkları tek bir yerden yönetmek**: projeden projeye başvurular ve derleme başvurularını hemen gibi NuGet paket başvuruları (kullanarak `PackageReference` düğümü) ayrı bir kullanmak yerine doğrudan proje dosyaları içinde yönetilir Packages.config dosyası.
* **Üst düzey bağımlılıkları sade görünümünü**: packages.config PackageReference doğrudan yüklediğiniz projedeki NuGet paketlerini listeler. Sonuç olarak, NuGet Paket Yöneticisi UI ve proje dosyası ile alt düzey bağımlılıkları dağınıktır değildir.
* **Performans iyileştirmeleri**: PackageReference kullanırken, paketleri içinde korunur *genel paketleri* klasörü (üzerinde açıklandığı [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md) yerine bir `packages` çözüm içinde klasör. Sonuç olarak, PackageReference daha hızlı gerçekleştirir ve daha az disk alanı kullanır.
* **İnce bağımlılıkları ve içerik akışı üzerinde denetim**: mevcut MSBuild özelliklerini kullanmaya izin verir [koşullu olarak NuGet paketine başvuru](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve paket başvuruları hedef çerçeve başına yapılandırması Platform veya diğer özetler.
* **PackageReference olan etkin geliştirilme**: bkz [PackageReference sorunları Github'da](https://aka.ms/nuget-pr-improvements). Packages.config artık etkin geliştirilme aşamasındadır.

### <a name="limitations"></a>Sınırlamalar

* NuGet Packagereference'a önceki ve Visual Studio 2015'te kullanılabilir değil. Geçirilen projeleri yalnızca Visual Studio 2017'de açılabilir.
* Geçiş, C++ ve ASP.NET projeleri için şu anda kullanılabilir değil.
* Bazı paketler PackageReference ile tam olarak uyumlu olmayabilir. Daha fazla bilgi için [paketini uyumluluk sorunlarını](#package-compatibility-issues).

### <a name="known-issues"></a>Bilinen Sorunlar

1. `Migrate packages.config to PackageReference...` Sağ bağlam menüsü seçeneği kullanılamaz 

#### <a name="issue"></a>Sorun 
 
Bir projeyi ilk defa açıldığında, NuGet işlemi gerçekleştirilene kadar NuGet başlatılmamış. Bu geçiş seçeneği sağ bağlam menüsü üzerinde görünmesini değil neden `packages.config` veya `References`. 

#### <a name="workaround"></a>Geçici Çözüm 

Aşağıdaki NuGet eylemlerden birini gerçekleştirin: 
* Paket Yöneticisi UI - açık sağ `References` seçin `Manage NuGet Packages...` 
* Paket Yöneticisi konsolu - açık `Tools > NuGet Package Manager`seçin `Package Manager Console` 
* Çalışma NuGet geri yükleme - Çözüm Gezgini'nde çözüm düğümüne sağ tıklayın ve seçin `Restore NuGet Packages` 
* Ayrıca NuGet geri yükleme tetikler projeyi derleyin 

Artık geçiş seçeneği görmeye olmalıdır. Bu seçenek desteklenmez ve ASP.NET ve C++ proje türleri için gösterilmez unutmayın. 

## <a name="migration-steps"></a>Geçiş adımları

> [!Note]
> Geçiş başlamadan önce Visual Studio olanak tanımak için bir yedekleme projenin oluşturur [packages.config dönmeyi](#how-to-roll-back-to-packagesconfig) gerekirse.

1. Project kullanarak içeren bir çözüm açın `packages.config`.

1. İçinde **Çözüm Gezgini**, sağ **başvuruları** düğümü veya `packages.config` seçin ve dosya **Packages.config'i Packagereference'a geçirme...** .

1. Migrator projenin NuGet paket başvuruları analiz eder ve bunları kategorilere dener **en üst düzey bağımlılıkları** (doğrudan yüklü NuGet paketlerini) ve **geçişli bağımlılıkları** (üst düzey paket bağımlılıkları olarak yüklenen paketler).

   > [!Note]
   > PackageReference, geçişli paket geri yükleme destekler ve bağımlılıkları geçişli bağımlılıkları açıkça yüklenmemesi, yani dinamik olarak çözer.

1. (İsteğe bağlı) Geçişli bağımlılık olarak en üst düzey bir bağımlılık olarak sınıflandırılan seçerek bir NuGet paketi değerlendirilecek seçebilirsiniz **en üst düzey** paketi için seçeneği. Bu seçenek, geçişli geçmez varlıkları içeren paketleri için otomatik olarak ayarlanır (penceresindekilerle `build`, `buildCrossTargeting`, `contentFiles`, veya `analyzers` klasörleri) ve bu bir geliştirme bağımlılığı işaretlendi (`developmentDependency = "true"`).

1. Gözden [paketini uyumluluk sorunlarını](#package-compatibility-issues).

1. Seçin **Tamam** geçişi başlatmak için.

1. Yedekleme, yüklü paketleri (üst düzey bağımlılıkları) listesinde, geçişli bağımlılıkları olarak başvurulan paketlerin bir listesi ve başında tanımlanan uyumluluk sorunların bir listesini geçiş sonunda, Visual Studio bir yola sahip bir rapor sağlar geçiş. Rapor yedekleme klasörüne kaydedilir.

1. Çözüm derlenir ve çalışır olduğunu doğrulayın. Sorunlar karşılaşırsanız [Github'da sorun kaydedebilir](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Nasıl packages.config için geri alma

1. Geçirilen proje kapatın.

1. Proje dosyasını kopyalayın ve `packages.config` yedekten (genellikle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) proje klasörüne. Proje kök dizininde varsa obj klasörü silin.

1. Projeyi açın.

1. Paket Yöneticisi Konsolu'nu kullanarak açmak **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.

1. Konsolunda aşağıdaki komutu çalıştırın:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Paket uyumluluk sorunları

Packagereference v Packages.config dosyasının içinde desteklenen bazı yönleri desteklenmez. Migrator analiz eder ve bu tür sorunları algılar. Bir veya daha fazla aşağıdaki sorunlardan biri olan herhangi bir paket, geçişten sonra beklendiği gibi çalışmayabilir.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paketi yüklendiğinde "install.ps1" komut dosyaları göz ardı edilir

| | |
| --- | --- |
| **Açıklama** | PackageReference ile yüklemeden veya kaldırmadan bir paket install.ps1 ve uninstall.ps1 PowerShell betikleri yürütülmez. |
| **Olası etki** | Hedef projesinde bazı davranışını yapılandırmak için bu betikleri bağımlı paketler beklendiği gibi çalışmayabilir. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paketi yüklendiğinde "içerik" varlıkları kullanılabilir değil

| | |
| --- | --- |
| **Açıklama** | Bir paketin varlıkları `content` klasörü ile PackageReference desteklenmez ve yok sayılır. PackageReference için destek ekler `contentFiles` daha iyi geçişli desteği ve paylaşılan içeriği.  |
| **Olası etki** | Varlıkları `content` kopyalanmaz proje ve proje bu varlıkları varlığını temel bağlı olan kod yeniden düzenlemeyi gerektirir.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Yükseltmeden sonra paketi yüklendiğinde XDT dönüşüm uygulanmaz

| | |
| --- | --- |
| **Açıklama** | XDT dönüşümler ile PackageReference desteklenmez ve `.xdt` dosyalar yok sayılır yüklerken veya bir paket kaldırılıyor.   |
| **Olası etki** | XDT dönüşümler hiçbir proje XML dosyaları çoğunlukla uygulanmaz `web.config.install.xdt` ve `web.config.uninstall.xdt`, projenin anlamına gelir` web.config` dosya paketi eklendiğinde veya kaldırıldığında güncelleştirilmez. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>LIB kök derlemeleri, geçişten sonra paketi yüklendiğinde göz ardı edilir

| | |
| --- | --- |
| **Açıklama** | PackageReference ile derlemeleri sunmak kökünde `lib` klasörü hedef framework belirli bir alt klasör olmadan yok sayılır. NuGet, projenin hedef çerçevesi için karşılık gelen hedef çerçeve adı (TFM) eşleşen bir alt klasöre arar ve eşleşen derlemeleri projeye yükler. |
| **Olası etki** | Projenin hedef çerçevesi için karşılık gelen hedef çerçeve adı (TFM) eşleşen bir alt klasörü olmayan paketleri değil geçişten sonra beklendiği gibi davranmaya veya geçirme sırasında yükleme başarısız |

## <a name="found-an-issue-report-it"></a>Bir sorun buldunuz? Rapor!

Geçiş deneyimi ile ilgili bir sorun yaşarsanız lütfen [sorun NuGet GitHub deposuna kaydedebilir](https://github.com/NuGet/Home/issues/).
