---
title: packages.config ' den PackageReference biçimlerine geçme
description: Bir projenin packages.config yönetim biçiminden NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen PackageReference 'a nasıl geçirileceğiyle ilgili ayrıntılar
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8161f4a39d4adfdb9efb25bcb840b20b85a58e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774777"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>packages.config ' den PackageReference 'a geçir

Visual Studio 2017 sürüm 15,7 ve üzeri, bir projenin [packages.config](../reference/packages-config.md) Management biçiminden [packagereference](../consume-packages/Package-References-in-Project-Files.md) biçimine geçirilmesini destekler.

## <a name="benefits-of-using-packagereference"></a>PackageReference kullanmanın avantajları

* **Tüm proje bağımlılıklarını tek bir yerde yönetin**: projede proje başvuruları ve derleme başvuruları gibi, NuGet paket başvuruları (düğümü kullanılarak), `PackageReference` ayrı bir packages.config dosyası kullanmak yerine doğrudan proje dosyaları içinde yönetilir.
* **Üst düzey bağımlılıkların dağınık görünümü**: packages.config aksine, packagereference yalnızca doğrudan projeye yüklediğiniz NuGet paketlerini listeler. Sonuç olarak, NuGet Paket Yöneticisi Kullanıcı arabirimi ve proje dosyası alt düzey bağımlılıklarla birlikte dağınık değildir.
* **Performans iyileştirmeleri**: packagereference kullanılırken, paketler *genel paketler* klasöründe tutulur (çözüm içindeki bir klasör yerine [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md) bölümünde açıklandığı gibi) `packages` . Sonuç olarak, PackageReference daha hızlı çalışır ve daha az disk alanı tüketir.
* **Bağımlılıklar ve içerik akışı üzerinde ince denetim**: MSBuild 'in var olan özelliklerini kullanarak [bir NuGet paketine koşullu başvuru](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve hedef çerçeve, yapılandırma, platform veya diğer özetler için paket başvuruları seçme olanağı sağlar.
* **Packagereference etkin geliştirme aşamasındadır**: [GitHub 'da packagereference sorunları](https://aka.ms/nuget-pr-improvements)bölümüne bakın. packages.config artık etkin geliştirme aşamasındadır.

### <a name="limitations"></a>Sınırlamalar

* NuGet PackageReference, Visual Studio 2015 ve önceki sürümlerde kullanılamaz. Geçirilen projeler yalnızca Visual Studio 2017 ve üzeri sürümlerde açılabilir.
* Geçiş Şu anda C++ ve ASP.NET projeleri için kullanılabilir değil.
* Bazı paketler, PackageReference ile tamamen uyumlu olmayabilir. Daha fazla bilgi için bkz. [paket uyumluluk sorunları](#package-compatibility-issues).

Ayrıca, Packagereferilakinin packages.config kıyasla bazı farklılıklar vardır. Örneğin, [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) , packagereference tarafından bastırlanmaz ancak [kayan sürümler](../consume-packages/package-references-in-project-files.md#floating-versions)için destek ekler.

### <a name="known-issues"></a>Bilinen Sorunlar

1. `Migrate packages.config to PackageReference...`Seçenek, sağ tıklama bağlam menüsünde kullanılamaz 

#### <a name="issue"></a>Sorun 
 
Bir proje ilk açıldığında NuGet bir NuGet işlemi gerçekleştirilene kadar başlatılmamış olabilir. Bu, veya üzerindeki sağ tıklama bağlam menüsünde geçiş seçeneğinin gösterilmamasını sağlar `packages.config` `References` . 

#### <a name="workaround"></a>Geçici çözüm 

Aşağıdaki NuGet eylemlerinden birini gerçekleştirin: 
* Paket Yöneticisi Kullanıcı arabirimini açın-sağ tıklayıp `References` seçin `Manage NuGet Packages...` 
* Paket Yöneticisi konsolunu açın-Kimden `Tools > NuGet Package Manager` ' i seçin `Package Manager Console` 
* NuGet geri yükleme Çalıştır-Çözüm Gezgini çözüm düğümüne sağ tıklayın ve şu seçeneği belirleyin `Restore NuGet Packages` 
* Ayrıca NuGet geri yüklemeyi tetikleyen projeyi oluştur 

Şimdi geçiş seçeneğini görebilmeniz gerekir. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmediğini unutmayın. 

## <a name="migration-steps"></a>Geçiş adımları

> [!Note]
> Geçiş başlamadan önce, Visual Studio, gerekirse [packages.configgeri ](#how-to-roll-back-to-packagesconfig) almanıza olanak tanımak için projenin bir yedeğini oluşturur.

1. Kullanarak proje içeren bir çözüm açın `packages.config` .

1. **Çözüm Gezgini**, **Başvurular** düğümüne veya dosyaya sağ tıklayın `packages.config` ve packages.config, **packagereference...**' a geçir ' i seçin.

1. Migrator, projenin NuGet paketi başvurularını analiz eder ve bunları **en üst düzey bağımlılıklara** (doğrudan yüklediğiniz NuGet paketleri) ve **geçişli bağımlılıklara** (en üst düzey paketlere bağımlılıklar olarak yüklenen paketler) göre kategorilere ayırarak çalışır.

   > [!Note]
   > PackageReference geçişli paket geri yüklemeyi destekler ve bağımlılıkları dinamik olarak çözer, yani geçişli bağımlılıkların açıkça yüklenmesi gerekir.

1. Seçim Paket için **en üst düzey** seçeneğini belirleyerek geçişli bağımlılık olarak sınıflandırılan bir NuGet paketini en üst düzey bağımlılık olarak kabul edebilirsiniz. Bu seçenek, geçişli olarak ( `build` ,, `buildCrossTargeting` `contentFiles` veya `analyzers` klasörlerinde) ve bir geliştirme bağımlılığı () olarak işaretlenmeyen varlıkları içeren paketler için otomatik olarak ayarlanır `developmentDependency = "true"` .

1. Tüm [paket uyumluluk sorunlarını](#package-compatibility-issues)gözden geçirin.

1. Geçişe başlamak için **Tamam ' ı** seçin.

1. Geçişin sonunda, Visual Studio yedeklemenin yolunu, yüklü paketlerin listesini (üst düzey bağımlılıklar), geçişli bağımlılıklar olarak başvurulan paketlerin listesini ve geçiş başlangıcında tanımlanan uyumluluk sorunlarının bir listesini sağlar. Rapor, yedekleme klasörüne kaydedilir.

1. Çözümün derlemediğini ve çalıştığını doğrulayın. Sorunlarla karşılaşırsanız, [GitHub 'da bir sorun](https://github.com/NuGet/Home/issues/)yapın.

## <a name="how-to-roll-back-to-packagesconfig"></a>packages.config geri alma

1. Geçirilen projeyi kapatın.

1. Proje dosyasını ve `packages.config` yedekten (genellikle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\` ) proje klasörüne kopyalayın. Proje kök dizininde varsa obj klasörünü silin.

1. Projeyi açın.

1. **Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** menü komutunu kullanarak paket Yöneticisi konsolunu açın.

1. Konsolunda aşağıdaki komutu çalıştırın:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Geçişten sonra paket oluşturma

Geçiş işlemi tamamlandıktan sonra, [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) NuGet paketine bir başvuru eklemenizi ve ardından paketi oluşturmak için [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) ' i kullanmanızı öneririz. Yerine kullanabileceğiniz bazı senaryolarda `dotnet.exe pack` `msbuild -t:pack` , bu önerilmez.

## <a name="package-compatibility-issues"></a>Paket uyumluluk sorunları

packages.config desteklenen bazı yönleri PackageReference içinde desteklenmez. Migrator bu sorunları analiz eder ve algılar. Aşağıdaki sorunlardan birine veya daha fazlasına sahip herhangi bir paket, geçişten sonra beklendiği gibi davranmayabilir.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install.ps1" betikleri, paket geçişten sonra yüklendiğinde yok sayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile, bir paket yüklenirken veya kaldırılırken install.ps1 ve uninstall.ps1 PowerShell betikleri yürütülmez. |
| **Olası etki** | Hedef projede bazı davranışları yapılandırmak için bu betiklerin bağımlı olduğu paketler beklendiği gibi çalışmayabilir. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>geçişten sonra paket yüklendiğinde "içerik" varlıkları kullanılamaz

| | |
| --- | --- |
| **Açıklama** | Bir paket `content` klasöründeki varlıklar, PackageReference ile desteklenmez ve yok sayılır. PackageReference `contentFiles` , daha iyi geçişli desteğe ve paylaşılan içeriğe sahip olmak için için destek ekler.  |
| **Olası etki** | İçindeki varlıklar `content` projeye kopyalanmaz ve bu varlıkların varlığına bağlı olarak proje kodu yeniden düzenleme gerektirir.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Yükseltmeden sonra paket yüklendiğinde XDT dönüştürmeleri uygulanmaz

| | |
| --- | --- |
| **Açıklama** | XDT dönüştürmeleri, PackageReference ile desteklenmez ve `.xdt` bir paket yüklenirken veya kaldırılırken dosyalar yok sayılır.   |
| **Olası etki** | XDT dönüştürmeleri, en yaygın olarak ve olan herhangi bir proje XML dosyasına uygulanmaz `web.config.install.xdt` ; `web.config.uninstall.xdt` Bu, ` web.config` paket yüklenirken veya kaldırıldığında projenin dosyasının güncelleştirilmediği anlamına gelir. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paket yüklendiğinde LIB kökündeki derlemeler yok sayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile, `lib` hedef çerçeveye özgü alt klasör olmadan klasörün kökünde bulunan derlemeler yok sayılır. NuGet, projenin hedef çerçevesine karşılık gelen hedef çerçeve bilinen adı (tfd) ile eşleşen bir alt klasör arar ve eşleşen derlemeleri projeye kurar. |
| **Olası etki** | Projenin hedef çerçevesine karşılık gelen hedef çerçeve adı (tfd) ile eşleşen bir alt klasörü olan paketler, geçiş sırasında geçişten veya yüklemeden sonra beklendiği gibi davranmayabilir |

## <a name="found-an-issue-report-it"></a>Bir sorun bulundu mı? Rapor It!

Geçiş deneyimiyle ilgili bir sorunla karşılaşırsanız lütfen [NuGet GitHub deposunda bir sorun](https://github.com/NuGet/Home/issues/)bildirin.
