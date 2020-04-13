---
title: package.config'den PackageReference biçimlerine geçiş
description: NuGet 4.0+ ve VS2017 ve .NET Core 2.0 tarafından desteklenen packagereference yönetim formatından packagereference'a nasıl bir proje geçirilir hakkında ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428893"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>packages.config'den PackageReference'a geçirin

Visual Studio 2017 Sürüm 15.7 ve daha sonra [package.config](../reference/packages-config.md) yönetim formatından [PackageReference](../consume-packages/Package-References-in-Project-Files.md) biçimine bir proje nin geçişini destekler.

## <a name="benefits-of-using-packagereference"></a>PackageReference kullanmanın faydaları

* **Tüm proje bağımlılıklarını tek bir yerde yönetme**: Projeden proje başvurularına ve `PackageReference` montaj başvurularına kadar, NuGet paket başvuruları (düğüm kullanılarak) ayrı bir paket kullanmak yerine doğrudan proje dosyaları içinde yönetilir.
* **Üst düzey bağımlılıkların derli toplu görünümü**: packages.config'in aksine, PackageReference yalnızca projeye doğrudan yüklediğiniz NuGet paketlerini listeler. Sonuç olarak, NuGet Paket Yöneticisi UI ve proje dosyası alt düzey bağımlılıklarla dolu değildir.
* **Performans iyileştirmeleri**: PackageReference kullanırken, paketler *genel paketler* klasöründe tutulur (çözüm içinde bir `packages` klasör yerine genel paketleri ve [önbellek klasörlerini yönetmede](../consume-packages/managing-the-global-packages-and-cache-folders.md) açıklandığı gibi). Sonuç olarak, PackageReference daha hızlı gerçekleştirir ve daha az disk alanı tüketir.
* **Bağımlılıklar ve içerik akışı üzerinde ince kontrol**: MSBuild'in varolan özelliklerini [kullanmak, bir NuGet paketine koşullu olarak başvurmanızı](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve hedef çerçeve, yapılandırma, platform veya diğer pivotlar başına paket referanslarını seçmenize olanak tanır.
* **PackageReference aktif geliştirme aşamasındadır**: [Bkz. GitHub'daki PackageReference sorunları.](https://aka.ms/nuget-pr-improvements) packages.config artık aktif geliştirme aşamasında değildir.

### <a name="limitations"></a>Sınırlamalar

* NuGet PackageReference Visual Studio 2015 ve önceki gün için kullanılamaz. Taşınan projeler sadece Visual Studio 2017 ve sonrası yıllarda açılabilir.
* Geçiş şu anda C++ ve ASP.NET projeleri için kullanılamıyor.
* Bazı paketler PackageReference ile tam uyumlu olmayabilir. Daha fazla bilgi için [paket uyumluluğu sorunlarına](#package-compatibility-issues)bakın.

Buna ek olarak, packagereferences paketleri.config göre nasıl çalıştığını bazı farklılıklar vardır. Örneğin - [kısıtlayıcı yükseltme sürümleri](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) PackageReference tarafından supprted değil, [Kayan Sürümleri](../consume-packages/package-references-in-project-files.md#floating-versions)için destek ekleyin.

### <a name="known-issues"></a>Bilinen Sorunlar

1. Seçenek `Migrate packages.config to PackageReference...` sağ tıklama bağlam menüsünde kullanılamıyor 

#### <a name="issue"></a>Sorun 
 
Bir proje ilk açıldığında, NuGet işlemi gerçekleştirilene kadar önbaşlatma olmayabilir. Bu, geçiş seçeneğinin sağ tıklatma bağlam menüsünde `packages.config` `References`veya . 

#### <a name="workaround"></a>Geçici çözüm 

Aşağıdaki NuGet eylemlerinden herhangi birini gerçekleştirin: 
* Paket Yöneticisi UI'yi açın `References` - Sağ tıklayın ve seçin`Manage NuGet Packages...` 
* Paket Yöneticisi Konsolu'nu açın - From `Tools > NuGet Package Manager`, seçin`Package Manager Console` 
* NuGet geri yükleme çalıştırın - Çözüm Gezgini'ndeki çözüm düğümüne sağ tıklayın ve`Restore NuGet Packages` 
* NuGet geri yüklemesini de tetikleyen projeyi oluşturun 

Artık geçiş seçeneğini görebilmelisin. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmeyeceğini unutmayın. 

## <a name="migration-steps"></a>Geçiş adımları

> [!Note]
> Geçiş başlamadan önce Visual Studio, gerekirse [packages.config'e geri dönmenizi](#how-to-roll-back-to-packagesconfig) sağlamak için projenin bir yedeklemesini oluşturur.

1. Project'i kullanarak `packages.config`bir çözüm açın.

1. **Çözüm Gezgini'nde,** **Başvuru düğümüne** veya `packages.config` dosyaya sağ tıklayın ve **PackageReference'a geçir paketleri.config'i seçin...**.

1. Göçmen, projenin NuGet paket başvurularını analiz eder ve bunları **üst düzey bağımlılıklar** (doğrudan yüklediğiniz NuGet paketleri) ve **Geçişli bağımlılıklar** (üst düzey paketlerin bağımlılıkları olarak yüklenen paketler) olarak kategorilere ayırmaya çalışır.

   > [!Note]
   > PackageReference geçişli paket geri yüklemeyi destekler ve bağımlılıkları dinamik olarak çözer, yani geçişli bağımlılıkların açıkça yüklenmesi gerekmez.

1. (İsteğe bağlı) Paket için **Üst Düzey** seçeneğini seçerek, geçişli bağımlılık olarak sınıflandırılan bir NuGet paketini üst düzey bağımlılık olarak ele almayı seçebilirsiniz. Bu seçenek, geçişli olarak `build`akmayan varlıklar (, , , `buildCrossTargeting` `contentFiles`veya `analyzers` klasörlerde) ve geliştirme bağımlılığı olarak işaretlenmiş`developmentDependency = "true"`kıymetleri içeren paketler için otomatik olarak ayarlanır.

1. Paket [uyumluluğu sorunlarını gözden geçirin.](#package-compatibility-issues)

1. Geçişe başlamak için **Tamam'ı** seçin.

1. Geçişin sonunda Visual Studio yedeklemeye giden bir yol, yüklü paketlerin listesi (üst düzey bağımlılıklar), geçişli bağımlılıklar olarak başvurulan paketlerin listesi ve geçiş başlangıcında tanımlanan uyumluluk sorunlarının listesini içeren bir rapor sağlar. Rapor yedek klasöre kaydedilir.

1. Çözümün oluşturduğunu ve çalıştığını doğrulayın. Sorunlarla karşılaşırsanız, [GitHub'da bir sorun dosya.](https://github.com/NuGet/Home/issues/)

## <a name="how-to-roll-back-to-packagesconfig"></a>Nasıl packages.config geri rulo

1. Geçirilen projeyi kapatın.

1. Proje dosyasını `packages.config` ve yedeklemeden (genellikle) `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`proje klasörüne kopyalayın. Proje kök dizini içinde varsa obj klasörünü silin.

1. Projeyi açın.

1. Paket Yöneticisi Konsolu'nu **NuGet Paket Yöneticisi > Paket Yöneticisi konsolu** menü komutu > Araçları kullanarak Paket Yöneticisi Konsolu'nu açın.

1. Konsolda aşağıdaki komutu çalıştırın:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Geçişten sonra paket oluşturma

Geçiş tamamlandıktan sonra [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget paketine bir başvuru eklemenizi ve paketi oluşturmak için [msbuild -t:pack'i](../reference/msbuild-targets.md#pack-target) kullanmanızı öneririz. Bazı senaryolarda yerine kullanabilirsiniz `dotnet.exe pack` `msbuild -t:pack`rağmen, bu önerilmez.

## <a name="package-compatibility-issues"></a>Paket uyumluluğu sorunları

Packages.config'de desteklenen bazı yönler PackageReference'da desteklenmez. Göçmen bu tür sorunları analiz eder ve algılar. Aşağıdaki sorunlardan biri veya birkaçı olan herhangi bir paket, geçişten sonra beklendiği gibi şekilde şekilde şekilde olmayabilir.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install.ps1" komut dosyaları, geçişten sonra paket yüklendiğinde yoksayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile install.ps1 ve uninstall.ps1 PowerShell komut dosyaları bir paketi yüklerken veya yüklerken yürütülmez. |
| **Olası etki** | Hedef projedeki bazı davranışları yapılandırmak için bu komut dosyalarına bağlı paketler beklendiği gibi çalışmayabilir. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"içerik" varlıkları, geçişten sonra paket yüklendiğinde kullanılamaz

| | |
| --- | --- |
| **Açıklama** | Paketin `content` klasöründeki varlıklar PackageReference ile desteklenmez ve yoksayılır. PackageReference, daha `contentFiles` iyi geçişli destek ve paylaşılan içeriğe sahip olmak için destek ekler.  |
| **Olası etki** | Varlıklar `content` proje ye kopyalanmaz ve bu varlıkların varlığına bağlı olarak proje kodu yeniden düzenleme gerektirir.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Paket yükseltmeden sonra yüklendiğinde XDT dönüşümleri uygulanmaz

| | |
| --- | --- |
| **Açıklama** | XDT dönüşümleri PackageReference ile desteklenmez ve `.xdt` bir paketi yüklerken veya yüklerken dosyalar yoksayılır.   |
| **Olası etki** | XDT dönüşümleri, en sık karşılaşılan herhangi bir `web.config.install.xdt` proje `web.config.uninstall.xdt`XML dosyasına` web.config` uygulanmaz ve bu da paket yüklendiğinde veya kaldırıldığında projenin dosyasının güncelleştirilen olmadığı anlamına gelir. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paket yüklendiğinde lib kökündeki derlemeler yoksayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile, hedef çerçevesine `lib` özgü alt klasör olmadan klasörün kökünde bulunan derlemeler yoksayılır. NuGet, projenin hedef çerçevesine karşılık gelen hedef çerçeve lakabıyla (TFM) eşleşen bir alt klasör arar ve eşleşen derlemeleri projeye yükler. |
| **Olası etki** | Projenin hedef çerçevesine karşılık gelen hedef çerçeve lakabıyla (TFM) eşleşen bir alt klasörü olmayan paketler geçiş sırasında beklendiği gibi veya yüklemede başarısız olamaz |

## <a name="found-an-issue-report-it"></a>Bir sorun mu buldun? Rapor edin!

Geçiş deneyimiyle ilgili bir sorunla karşılaşırsanız, lütfen [NuGet GitHub deposunda bir sorun dosyalayın.](https://github.com/NuGet/Home/issues/)
