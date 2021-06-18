---
title: Visual Studio'de NuGet Paketi Geri Yükleme sorunlarını giderme
description: Uygulama içinde sık karşılaşılan NuGet geri yükleme Visual Studio ve bu hataların nasıl giderilir?
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323628"
---
# <a name="troubleshooting-package-restore-errors"></a>Paket geri yükleme hatalarını giderme

Bu makale, paketleri geri yükleme sırasında karşılaşılan yaygın hatalara ve bunları çözme adımlarına odaklanır. 

Paket Geri Yükleme, tüm paket bağımlılıklarını proje dosyanıza (*.csproj*) veya dosya dosyanıza paket başvuruları ile eşleşen doğru *packages.config* çalışır. (Visual Studio, başvurular Bağımlılıklar **\ NuGet** Çözüm Gezgini Veya Başvurular düğümü **altında** görünür.) Paketleri geri yüklemek için gerekli adımları takip etmek için bkz. [Paketleri geri yükleme.](../consume-packages/package-restore.md#restore-packages) Paket, proje dosyanıza (*.csproj*) veya *packages.config* dosyanıza başvurursa (Paket Geri Yükleme sonrasında istediğiniz durumla eşleşmez) paket geri yükleme yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.

Buradaki yönergeler sizin için uygunsa, senaryoyu daha dikkatli inceleyene kadar [gitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin. "Bu sayfa yararlı mı?" denetimi bu sayfada görünebilir çünkü daha fazla bilgi için size ulaşabilme olanağını bize vermez.

## <a name="quick-solution-for-visual-studio-users"></a>Kullanıcılar için hızlı Visual Studio çözümü

Visual Studio kullanıyorsanız, önce paket geri yüklemesini aşağıdaki gibi etkinleştirin. Aksi takdirde, aşağıdaki bölümlere devam edin.

1. Araçlar ve **NuGet > Ayarlar Paket Yöneticisi > Paket Yöneticisi komutunu** seçin.
1. Paket Geri Yükleme altında her **iki seçeneği de ayarlayın.**
1. **Tamam**’ı seçin.
1. Projenizi yeniden derleme.

![Araç/Seçenekler'de NuGet paketi geri yüklemesini etkinleştirme](../consume-packages/media/restore-01-autorestoreoptions.png)

Bu ayarlar dosyanız içinde de `NuGet.Config` değiştirilebilir; onay [](#consent) bölümüne bakın. Projeniz MSBuild ile tümleşik paket geri yüklemesini kullanan eski bir proje ise, otomatik paket geri [yüklemeye](package-restore.md#migrate-to-automatic-package-restore-visual-studio) geçirmeniz gerekir.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvurur

Tam hata iletisi:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Bu hata, bir veya daha fazla NuGet paketine başvuru içeren bir proje derlemeye çalışırken oluşur, ancak bu paketler şu anda bilgisayarda veya projede yüklü değildir.

- [PackageReference](package-references-in-project-files.md) yönetim biçimini kullanırken, bu hata bir packages.config PackageReference geçişini kaldırma işlemi [](/nuget/resources/nuget-faq#working-with-packages) olabilir ve proje dosyasından el ile kaldırılması gerekir.
- bu [packages.config](../reference/packages-config.md)kullanırken hata, paketin çözüm kökünde `packages` klasöre yüklenmemiş olduğu anlamına gelir.

Bu durum genellikle projenin kaynak kodunu kaynak denetiminden veya başka bir indirmeden edinilen durumlarda oluşur. Paketler genellikle kaynak denetiminden veya indirmelerden atlanır çünkü bunlar nuget.org gibi paket akışlarından geri yüklenebilir (bkz. [Paketler ve kaynak denetimi).](Packages-and-Source-Control.md) Bunları dahil etmek aksi takdirde depoyu şişirir veya gereksiz yere büyük .zip oluşturabilir.

Proje dosyanız paket konumlarını mutlak yollar içeriyorsa ve projeyi taşısanız da bu hatayla karşınıza olabilir.

Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:

- Proje dosyasını taşıdıysanız, paket başvurularını güncelleştirmek için dosyayı doğrudan düzenleyin.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ( otomatik[geri yükleme](package-restore.md#restore-packages-automatically-using-visual-studio) veya el ile geri [yükleme](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Geri yükleme başarılı olduktan sonra paketin *global-packages klasöründe mevcut olması* gerekir. PackageReference kullanan projeler için, geri yükleme işlemi dosyayı yeniden oluşturmalı; kullanan projeler `obj/project.assets.json` için paket projenin klasöründe `packages.config` `packages` görünmektedir. Projenin şimdi başarıyla derlemesi gerekir. Yoksa, [sizi takip etmek için GitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Varlıklar project.assets.jsdosya bulunamadı

Tam hata iletisi:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Dosya, gerekli tüm paketlerin bilgisayarda yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimini kullanırken projenin bağımlılık `project.assets.json` grafiğini sürdürür. Bu dosya paket geri yüklemesi aracılığıyla dinamik olarak oluşturulduğundan, genellikle kaynak denetimine eklenmez. Sonuç olarak, paketleri otomatik olarak geri yüklemez gibi bir araçla proje `msbuild` oluşturulurken bu hata oluşur.

Bu durumda, ardından `msbuild -t:restore` çalıştırın veya `msbuild` kullanın `dotnet build` (paketleri otomatik olarak geri yüklenir). Önceki bölümde paket geri yükleme yöntemlerden herhangi birini de [kullanabilirsiniz.](#missing)

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Bir veya daha fazla NuGet paketi geri yüklendi ancak onay verilmedi

Tam hata iletisi:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Bu hata, NuGet yapılandırmanız içinde paket geri yüklemenin devre dışı bırakılmıştır.

Daha önce kullanıcılar için hızlı çözüm altında açıklandığı Visual Studio [sayfasındaki ilgili ayarları Visual Studio değiştirebilirsiniz.](#quick-solution-for-visual-studio-users)

Ayrıca bu ayarları doğrudan ilgili dosyada `nuget.config` (genellikle Windows ve `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde) düzenleyebilirsiniz. altındaki ve `enabled` anahtarlarının `automatic` True olarak ayarlanmış olduğundan `packageRestore` emin olun:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Ayarları doğrudan içinde düzenlersiniz, seçenekler iletişim Visual Studio geçerli değerlerin görünür olması için `packageRestore` ayarları yeniden `nuget.config` başlatın.

## <a name="other-potential-conditions"></a>Diğer olası koşullar

- Eksik dosyalardan dolayı derleme hatalarına ve bunları indirmek için NuGet geri yüklemesini kullanmayı söyleyen bir iletiyle karşılaşabilirsiniz. Ancak, bir geri yükleme çalıştırarak "Tüm paketler zaten yüklenmiştir ve geri yüklenecek bir şey yoktur." Bu durumda, klasörü `packages` (kullanırken) veya dosyayı `packages.config` `obj/project.assets.json` (PackageReference kullanırken) silin ve geri yüklemeyi yeniden çalıştırın. Hata devam ederse, genel paketleri ve önbellek klasörlerini yönetme konusunda açıklandığı gibi genel paketleri ve önbellek klasörlerini temizlemek için veya komut `nuget locals all -clear` `dotnet nuget locals all --clear` satırı [kullanın.](managing-the-global-packages-and-cache-folders.md) 

- Kaynak denetiminden bir proje elde edilirken proje klasörleriniz salt okunur olarak ayarlanmış olabilir. Klasör izinlerini değiştirerek paketleri geri yüklemeyi yeniden deneyin.

- NuGet'in eski bir sürümünü kullanıyor olabilirsiniz. Önerilen [nuget.org/downloads](https://www.nuget.org/downloads) sürümler için güncelleştirmeleri kontrol edin. 2015 Visual Studio için 3.6.0 önerilir.

Başka sorunlarla karşılaşırsanız, [daha fazla ayrıntı alamamız için GitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin.
