---
title: Package.config PackageReference biçimlerine geçirme | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Bir proje package.config yönetim biçiminden NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi PackageReference nasıl geçirileceği hakkında ayrıntılar
keywords: NuGet migrator geçirmek, paket başvuruları, dosyaları, PackageReference, packages.config proje VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Packages.config PackageReference için geçirme

Visual Studio 2017 sürüm 15.7 Preview 3 ve sonraki destekler projeden geçirme [packages.config](./packages-config.md) yönetim biçimine [PackageReference](../consume-packages/Package-References-in-Project-Files.md) biçimi.

## <a name="benefits-of-using-packagereference"></a>PackageReference kullanmanın yararları

* **Tek bir yerde tüm proje bağımlılıklarını yönetme**: Proje için proje başvuruları ve derleme başvurularını yalnızca gibi NuGet paketi başvuruyor (kullanarak `PackageReference` düğüm) ayrı bir kullanmak yerine doğrudan proje dosyalarını içinde yönetilir Packages.config dosyası.
* **Üst düzey bağımlılıkları KARMAŞASIZ görünümünü**: packages.config PackageReference projede doğrudan yüklü NuGet paketlerini listeler. Sonuç olarak, NuGet Paket Yöneticisi kullanıcı Arabirimi ve proje dosyası ile alt düzey bağımlılıkları kalabalık değil.
* **Performans iyileştirmeleri**: PackageReference kullanırken, paket içinde korunur *paketleri genel* klasörü (açıklandığı gibi [genel paketleri ve önbellek klasörleri yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md) yerine, bir `packages` çözüm klasördeki. Sonuç olarak, PackageReference daha hızlı gerçekleştirir ve daha az disk alanı kullanır.
* **İnce bağımlılıkları ve içerik akışı üzerinde denetim**: MSBuild varolan özelliklerini kullanarak olanak tanır [koşullu bir NuGet paketi başvuru](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve paket referanslarını başına hedef Framework'ü seçin yapılandırması Platform veya diğer özetlere.
* **PackageReference etkin geliştirilmekte olan**: bkz [PackageReference sorunları Github'da](https://aka.ms/nuget-pr-improvements). Packages.config artık etkin geliştirilme aşamasındadır.

### <a name="limitations"></a>Sınırlamalar

* NuGet PackageReference, Visual Studio 2015'te kullanılabilir ve önceki değil. Geçirilen projeleri yalnızca Visual Studio 2017 açılabilir.
* Geçiş C++ ve ASP.NET projesi için şu anda kullanılabilir değil.
* Bazı paketler PackageReference ile tamamen uyumlu olmayabilir. Daha fazla bilgi için bkz: [paketini uyumluluk sorunları](#package-compatibility-issues).

## <a name="migration-steps"></a>Geçiş adımları

> [!Note]
> Geçiş başlamadan önce Visual Studio olanak tanımak için bir yedek projenin oluşturur [packages.config dönmeyi](#how-to-roll-back-to-packagesconfig) gerekiyorsa.

1. Project'i kullanarak içeren bir çözüm açmak `packages.config`.

1. İçinde **Çözüm Gezgini**, sağ tıklayın **başvuruları** düğümü veya `packages.config` dosya ve seçin **PackageReference için packages.config geçirmek...** .

1. Migrator projenin NuGet paket referanslarını analiz eder ve bunları kategorilere ayırma girişiminde **en üst düzey bağımlılıkları** (NuGet paketleri bu yüklediğiniz dizine) ve **geçişli bağımlılıkları**(en üst düzey paketler bağımlılık olarak yüklü olan paketleri).

   > [!Note]
   > PackageReference geçişli paket geri yüklemesi destekler ve geçişli bağımlılıkları açıkça yüklü olması değil anlamına bağımlılıkları dinamik olarak çözer.

1. (İsteğe bağlı) Seçerek en üst düzey bir bağımlılık olarak geçişli bağımlılık olarak sınıflandırılmış bir NuGet paketi işlemek seçebilirsiniz **en üst düzey** paketi için seçeneği. Bu seçenek geçişli geçmez varlıklar içeren paketler için otomatik olarak ayarlanır (de `build`, `buildCrossTargeting`, `contentFiles`, veya `analyzers` klasörleri) ve geliştirme bağımlılık olarak işaretlenmiş olanlar (`developmentDependency = "true"`).

1. Gözden [paketini uyumluluk sorunları](#package-compatibility-issues).

1. Seçin **Tamam** geçişi başlatmak için.

1. Geçiş işleminin sonunda, Visual Studio bir yola sahip bir rapor yedekleme, (üst düzey bağımlılıkları) yüklü olan paketlerin listesini, geçişli bağımlılıklar olarak başvurulan paketlerin listesini ve uyumluluk sorunları başlangıcında tanımlanan listesini sağlar geçiş. Rapor yedekleme klasörüne kaydedilir.

1. Çözüm oluşturur ve çalıştırır doğrulayın. Sorunlar karşılaşırsanız [bir sorun Github'da dosya](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Packages.config için geri almak nasıl

1. Geçirilen projeyi kapatın.

1. Proje dosyasını kopyalayın ve `packages.config` yedekten (genellikle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) proje klasörüne.

1. Projeyi açın.

1. Paket Yöneticisi konsolunu kullanarak açmak **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.

1. Konsolunda aşağıdaki komutu çalıştırın:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Paket uyumluluk sorunları

Packages.config içinde desteklenen bazı yönleri PackageReference içinde desteklenmez. Migrator analiz eder ve bu tür sorunları algılar. Bir veya daha fazla aşağıdaki sorunlardan biri olan herhangi bir paket geçişten sonra beklendiği gibi çalışmayabilir.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paketi yüklendiğinde "install.ps1" betikleri göz ardı edilir

| | |
| --- | --- |
| **Açıklama** | PackageReference ile install.ps1 ve uninstall.ps1 PowerShell komut dosyaları, yükleme veya bir paket kaldırma sırasında yürütülmez. |
| **Olası etkisini** | Hedef projesindeki bazı davranışı yapılandırmak için bu komut dosyalarını bağımlı paketler beklendiği gibi çalışmayabilir. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paketi yüklendiğinde "içerik" varlıklar kullanılabilir değil

| | |
| --- | --- |
| **Açıklama** | Bir paketin varlıkları `content` klasörü ile PackageReference desteklenmez ve yok sayılır. PackageReference için destek ekler `contentFiles` daha iyi geçişli desteği ve paylaşılan içeriği sağlamak için.  |
| **Olası etkisini** | Varlıkları `content` değil kopyalanır proje ve proje yeniden düzenleme bu varlıkları varlığına bağlıdır kodu gerektirir.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Yükseltmeden sonra paketi yüklendiğinde XDT dönüşümler uygulanmaz

| | |
| --- | --- |
| **Açıklama** | XDT dönüşümler ile PackageReference desteklenmiyor ve `.xdt` dosyaları yüklerken veya bir paket kaldırma yoksayılır.   |
| **Olası etkisini** | XDT dönüşümler tüm proje XML dosyaları için en yaygın olarak uygulanmaz `web.config.install.xdt` ve `web.config.uninstall.xdt`, başka bir deyişle, projenin` web.config` dosya paket eklendiğinde veya kaldırıldığında güncelleştirilmez. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Geçişten sonra paketi yüklendiğinde lib kök derlemelerde göz ardı edilir

| | |
| --- | --- |
| **Açıklama** | PackageReference ile derlemeleri sunmak kökünde `lib` klasörü hedef framework belirli bir alt klasör olmadan yok sayılır. NuGet projenin hedef çerçevesi için karşılık gelen hedef framework bilinen ad (TFM) eşleşen bir alt klasöre arar ve eşleşen derlemeleri projeye yükler. |
| **Olası etkisini** | Projenin hedef çerçevesi için karşılık gelen hedef framework bilinen ad (TFM) eşleşen bir alt klasörünüz yoksa paketleri değil geçişten sonra beklendiği gibi davranır veya geçirme sırasında yükleme başarısız |

## <a name="found-an-issue-report-it"></a>Bir sorun bulundu? Bu rapor!

Geçiş deneyimi ile ilgili bir sorun alıyorsanız, lütfen [NuGet GitHub deposunu bir sorun dosya](https://github.com/NuGet/Home/issues/).
