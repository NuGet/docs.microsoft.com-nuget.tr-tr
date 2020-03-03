---
title: Package. config biçiminden PackageReference biçimlerine geçiriliyor
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen bir projenin Package. config yönetim biçiminden PackageReference 'a nasıl geçirileceğiyle ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231283"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages. config biçiminden PackageReference 'a geçiş

Visual Studio 2017 sürüm 15,7 ve üzeri, bir projenin [Packages. config](../reference/packages-config.md) yönetim biçiminden [packagereference](../consume-packages/Package-References-in-Project-Files.md) biçimine geçirilmesini destekler.

## <a name="benefits-of-using-packagereference"></a>PackageReference kullanmanın avantajları

* **Tüm proje bağımlılıklarını tek bir yerde yönetin**: proje başvuruları ve derleme başvuruları gibi, NuGet paket başvuruları (`PackageReference` düğümü kullanılarak), ayrı bir Package. config dosyası kullanmak yerine doğrudan proje dosyaları içinde yönetilir.
* **En üst düzey bağımlılıkların dağınık görünümü**: Packages. config aksine, packagereference yalnızca projeye doğrudan yüklediğiniz NuGet paketlerini listeler. Sonuç olarak, NuGet Paket Yöneticisi Kullanıcı arabirimi ve proje dosyası alt düzey bağımlılıklarla birlikte dağınık değildir.
* **Performans iyileştirmeleri**: packagereference kullanılırken, paketler *genel paketler* klasöründe tutulur ( [genel paketler ve önbellek klasörlerini,](../consume-packages/managing-the-global-packages-and-cache-folders.md) çözüm içindeki bir `packages` klasörü yerine yönetme bölümünde açıklandığı gibi). Sonuç olarak, PackageReference daha hızlı çalışır ve daha az disk alanı tüketir.
* **Bağımlılıklar ve içerik akışı üzerinde ince denetim**: MSBuild 'in var olan özelliklerini kullanarak [bir NuGet paketine koşullu başvuru](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve hedef çerçeve, yapılandırma, platform veya diğer özetler için paket başvuruları seçme olanağı sağlar.
* **Packagereference etkin geliştirme aşamasındadır**: [GitHub 'da packagereference sorunları](https://aka.ms/nuget-pr-improvements)bölümüne bakın. Packages. config artık etkin geliştirme aşamasındadır.

### <a name="limitations"></a>Sınırlamalar

* NuGet PackageReference, Visual Studio 2015 ve önceki sürümlerde kullanılamaz. Geçirilen projeler yalnızca Visual Studio 2017 ve üzeri sürümlerde açılabilir.
* Geçiş Şu anda ve ASP.NET projeleri C++ için kullanılabilir değil.
* Bazı paketler, PackageReference ile tamamen uyumlu olmayabilir. Daha fazla bilgi için bkz. [paket uyumluluk sorunları](#package-compatibility-issues).

Ayrıca, Packagereferinin Packages. config ile karşılaştırıldığında nasıl çalıştığı hakkında bazı farklılıklar vardır. Örneğin, [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) , packagereference tarafından bastırlanmaz ancak [kayan sürümler](../consume-packages/package-references-in-project-files.md#floating-versions)için destek ekler.

### <a name="known-issues"></a>Bilinen Sorunlar

1. `Migrate packages.config to PackageReference...` seçeneği sağ tıklama bağlam menüsünde kullanılamaz 

#### <a name="issue"></a>Sorun 
 
Bir proje ilk açıldığında NuGet bir NuGet işlemi gerçekleştirilene kadar başlatılmamış olabilir. Bu, geçiş seçeneğinin `packages.config` veya `References`sağ tıklama kısayol menüsünde gösterilmamasını sağlar. 

#### <a name="workaround"></a>Geçici çözüm 

Aşağıdaki NuGet eylemlerinden birini gerçekleştirin: 
* Paket Yöneticisi Kullanıcı arabirimini açın-`References` ' a sağ tıklayıp `Manage NuGet Packages...` ' ı seçin. 
* Paket Yöneticisi konsolunu açın-`Tools > NuGet Package Manager`' den `Package Manager Console` ' ı seçin. 
* NuGet geri yükleme Çalıştır-Çözüm Gezgini çözüm düğümüne sağ tıklayın ve `Restore NuGet Packages` ' ı seçin. 
* Ayrıca NuGet geri yüklemeyi tetikleyen projeyi oluştur 

Şimdi geçiş seçeneğini görebilmeniz gerekir. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmediğini unutmayın. 

## <a name="migration-steps"></a>Geçiş adımları

> [!Note]
> Geçiş başlamadan önce, Visual Studio, gerekirse [Packages. config 'e geri dönüp](#how-to-roll-back-to-packagesconfig) projenin bir yedeğini oluşturur.

1. `packages.config`kullanarak proje içeren bir çözüm açın.

1. **Çözüm Gezgini**, **başvurular** düğümüne veya `packages.config` dosyasına sağ tıklayın ve **Packages. config 'i packagereference öğesine geçir**' i seçin.

1. Migrator, projenin NuGet paketi başvurularını analiz eder ve bunları **en üst düzey bağımlılıklara** (doğrudan yüklediğiniz NuGet paketleri) ve **geçişli bağımlılıklara** (en üst düzey paketlere bağımlılıklar olarak yüklenen paketler) göre kategorilere ayırarak çalışır.

   > [!Note]
   > PackageReference geçişli paket geri yüklemeyi destekler ve bağımlılıkları dinamik olarak çözer, yani geçişli bağımlılıkların açıkça yüklenmesi gerekir.

1. Seçim Paket için **en üst düzey** seçeneğini belirleyerek geçişli bağımlılık olarak sınıflandırılan bir NuGet paketini en üst düzey bağımlılık olarak kabul edebilirsiniz. Bu seçenek, geçişli olarak (`build`, `buildCrossTargeting`, `contentFiles`veya `analyzers` klasörlerinde) ve bir geliştirme bağımlılığı (`developmentDependency = "true"`) olarak işaretlenen varlıkları içeren paketler için otomatik olarak ayarlanır.

1. Tüm [paket uyumluluk sorunlarını](#package-compatibility-issues)gözden geçirin.

1. Geçişe başlamak için **Tamam ' ı** seçin.

1. Geçişin sonunda, Visual Studio yedeklemenin yolunu, yüklü paketlerin listesini (üst düzey bağımlılıklar), geçişli bağımlılıklar olarak başvurulan paketlerin listesini ve başlangıcında tanımlanan uyumluluk sorunlarının bir listesini sağlar. geçiş. Rapor, yedekleme klasörüne kaydedilir.

1. Çözümün derlemediğini ve çalıştığını doğrulayın. Sorunlarla karşılaşırsanız, [GitHub 'da bir sorun](https://github.com/NuGet/Home/issues/)yapın.

## <a name="how-to-roll-back-to-packagesconfig"></a>Packages. config 'e geri dönme

1. Geçirilen projeyi kapatın.

1. Proje dosyasını ve `packages.config` yedeklemeden (genellikle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) proje klasörüne kopyalayın. Proje kök dizininde varsa obj klasörünü silin.

1. Projeyi açın.

1. **Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** menü komutunu kullanarak paket Yöneticisi konsolunu açın.

1. Konsolunda aşağıdaki komutu çalıştırın:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Geçişten sonra paket oluşturma

Geçiş işlemi tamamlandıktan sonra, [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) NuGet paketine bir başvuru eklemenizi ve ardından paketi oluşturmak için [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) ' i kullanmanızı öneririz. Bazı senaryolarda `msbuild -t:pack`yerine `dotnet.exe pack` kullanabilseniz de önerilmez.

## <a name="package-compatibility-issues"></a>Paket uyumluluk sorunları

Packages. config dosyasında desteklenen bazı yönler, PackageReference içinde desteklenmez. Migrator bu sorunları analiz eder ve algılar. Aşağıdaki sorunlardan birine veya daha fazlasına sahip herhangi bir paket, geçişten sonra beklendiği gibi davranmayabilir.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"Install. ps1" betikleri geçişten sonra paket yüklendiğinde yok sayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile, install. ps1 ve Uninstall. ps1 PowerShell betikleri, bir paket yüklenirken veya kaldırılırken yürütülmez. |
| **Olası etki** | Hedef projede bazı davranışları yapılandırmak için bu betiklerin bağımlı olduğu paketler beklendiği gibi çalışmayabilir. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>geçişten sonra paket yüklendiğinde "içerik" varlıkları kullanılamaz

| | |
| --- | --- |
| **Açıklama** | Bir paketin `content` klasöründeki varlıklar, PackageReference ile desteklenmez ve yok sayılır. PackageReference, daha iyi geçişli desteğe ve paylaşılan içeriğe sahip `contentFiles` için destek ekler.  |
| **Olası etki** | `content` varlıklar projeye kopyalanmaz ve bu varlıkların varlığına bağlı olarak proje kodu yeniden düzenleme gerektirir.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Yükseltmeden sonra paket yüklendiğinde XDT dönüştürmeleri uygulanmaz

| | |
| --- | --- |
| **Açıklama** | XDT dönüştürmeleri, PackageReference ile desteklenmez ve bir paket yüklenirken veya kaldırılırken `.xdt` dosyalar yok sayılır.   |
| **Olası etki** | XDT dönüştürmeleri, en yaygın olarak, `web.config.install.xdt` ve `web.config.uninstall.xdt`hiçbir proje XML dosyasına uygulanmaz; bu, paket yüklenirken veya kaldırıldığında projenin` web.config` dosyasının güncelleştirilmediği anlamına gelir. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paket yüklendiğinde LIB kökündeki derlemeler yok sayılır

| | |
| --- | --- |
| **Açıklama** | PackageReference ile, hedef çerçeveye özgü alt klasör olmadan `lib` klasörünün kökünde bulunan derlemeler yok sayılır. NuGet, projenin hedef çerçevesine karşılık gelen hedef çerçeve bilinen adı (tfd) ile eşleşen bir alt klasör arar ve eşleşen derlemeleri projeye kurar. |
| **Olası etki** | Projenin hedef çerçevesine karşılık gelen hedef çerçeve adı (tfd) ile eşleşen bir alt klasörü olan paketler, geçiş sırasında geçişten veya yüklemeden sonra beklendiği gibi davranmayabilir |

## <a name="found-an-issue-report-it"></a>Bir sorun bulundu mı? Rapor It!

Geçiş deneyimiyle ilgili bir sorunla karşılaşırsanız lütfen [NuGet GitHub deposunda bir sorun](https://github.com/NuGet/Home/issues/)bildirin.
