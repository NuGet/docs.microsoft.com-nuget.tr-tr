---
title: Visual Studio 'da NuGet paketini geri yükleme sorunlarını giderme
description: Visual Studio 'da ortak NuGet geri yükleme hatalarının açıklaması ve bunların nasıl giderileceği.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860619"
---
# <a name="troubleshooting-package-restore-errors"></a>Paket geri yükleme hatalarını giderme

Bu makale, paketleri geri yüklerken yaygın hatalara ve bunları çözmeye yönelik adımlara odaklanmaktadır. 

Paket geri yükleme, tüm paket bağımlılıklarını proje dosyanızdaki ( *. csproj*) veya *Packages. config* dosyanızdaki paket başvurularıyla eşleşen doğru duruma yüklemeye çalışır. (Visual Studio 'da, başvurular **Bağımlılıklar \ NuGet** veya **başvurular** düğümü altında Çözüm Gezgini görüntülenir.) Paketleri geri yüklemek için gerekli adımları izlemek için bkz. [paketleri geri yükleme](../consume-packages/package-restore.md#restore-packages). Paket proje dosyanıza ( *. csproj*) veya *paketleriniz. config* dosyanız yanlışsa (paket geri yüklemesinin ardından istenen durumla eşleşmez), paket kullanmak yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir Yükleyebilmek.

Buradaki yönergeler sizin için çalışmadıysanız, senaryonuzu daha dikkatli bir şekilde incelemenize olanak sağlamak için [lütfen GitHub 'da bir sorun bildirin](https://github.com/NuGet/docs.microsoft.com-nuget/issues) . "Bu sayfa yardımcı oldu mu?" kullanmayın. daha fazla bilgi için sizinle iletişim kurma olanağı vermediğinden bu sayfada görünebilen denetim.

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio kullanıcıları için hızlı çözüm

Visual Studio kullanıyorsanız, önce paket geri yüklemeyi aşağıdaki gibi etkinleştirin. Aksi takdirde, izleyen bölümlerle devam edin.

1. **NuGet paket yöneticisi > Paket Yöneticisi ayarları menü komutunu > araçlar** ' ı seçin.
1. **Paket geri yükleme**altındaki her iki seçeneği de ayarlayın.
1. **Tamam**’ı seçin.
1. Projenizi yeniden derleyin.

![Araç/seçeneklerde NuGet paketini geri yüklemeyi etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

Bu ayarlar, `NuGet.config` dosyanızda de değiştirilebilir; [onay](#consent) bölümüne bakın. Projeniz MSBuild ile tümleşik paket geri yüklemeyi kullanan eski bir projem ise, otomatik paket geri yüklemeye [geçiş](package-restore.md#migrate-to-automatic-package-restore-visual-studio) yapmanız gerekebilir.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Bu proje, bu bilgisayarda eksik olan NuGet paketlerini referans yapıyor

Tamamlanan hata iletisi:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Bu hata, bir veya daha fazla NuGet paketine başvuru içeren bir proje oluşturmaya çalıştığınızda, ancak bu paketlerin bilgisayarda veya projede yüklü olmadığı durumlarda oluşur.

- [Packagereference](package-references-in-project-files.md) yönetim biçimi kullanılırken, hata, paketin genel [paketleri ve önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi *genel paketler* klasöründe yüklü olmadığı anlamına gelir.
- [Packages. config dosyası](../reference/packages-config.md)kullanılırken, hata paketin çözüm kökündeki `packages` klasöre yüklenmediği anlamına gelir.

Bu durum genellikle projenin kaynak kodunu kaynak denetiminden veya başka bir indirmenin edindiğinizde oluşur. Paketler, nuget.org gibi paket akışından geri yüklenebildiğinden genellikle kaynak denetiminden veya indirmelerden çıkarılır (bkz. [paketler ve kaynak denetimi](Packages-and-Source-Control.md)). Bunlar dahil olmak üzere depoyu veya gereksiz büyük. zip dosyaları oluşturur.

Ayrıca, proje dosyanız paket konumlarına mutlak yollar içeriyorsa ve projeyi taşıdığınız takdirde hata ortaya çıkabilir.

Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:

- Proje dosyasını taşıdıysanız, paket başvurularını güncelleştirmek için dosyayı doğrudan düzenleyin.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([otomatik geri yükleme](package-restore.md#restore-packages-automatically-using-visual-studio) veya [el ile geri yükleme](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Başarılı bir geri yüklemeden sonra, paketin *genel paketler* klasöründe mevcut olması gerekir. Packagereference kullanan projeler için, bir geri yükleme `obj/project.assets.json` dosyayı yeniden oluşturmanız gerekir; kullanan `packages.config`projeler için, paketin projenin `packages` klasöründe görünmesi gerekir. Projenin şimdi başarıyla oluşturulması gerekir. Aksi takdirde, [GitHub 'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) vererek sizinle ilgili bir sorun ile ilerleyebiliriz.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Proje. varlıklar. JSON varlık dosyası bulunamadı

Tamamlanan hata iletisi:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Dosya, gerekli tüm paketlerin bilgisayarda yüklü olduğundan emin olmak için kullanılan packagereference yönetim biçimini kullanırken bir projenin bağımlılık grafiğini tutar. Bu dosya paket geri yüklemesi aracılığıyla dinamik olarak oluşturulduğundan, genellikle kaynak denetimine eklenmez. Sonuç olarak, paketleri otomatik olarak geri yükleme gibi bir araçla `msbuild` bir proje derlerken bu hata oluşur.

Bu durumda, tarafından `msbuild -t:restore` `msbuild`izlenen ' i çalıştırın veya kullanın `dotnet build` (paketleri otomatik olarak geri yükler). [Önceki bölümde](#missing)bulunan paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz.

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmedi

Tamamlanan hata iletisi:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Bu hata, NuGet yapılandırmanızda paket geri yükleme 'nin devre dışı bırakıldığını gösterir.

Visual Studio 'da, Visual [Studio kullanıcıları Için hızlı çözüm](#quick-solution-for-visual-studio-users)altında açıklandığı gibi, geçerli ayarları değiştirebilirsiniz.

Ayrıca, bu ayarları doğrudan ilgili `nuget.config` dosyada (genellikle `%AppData%\NuGet\NuGet.Config` Windows ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux 'ta) düzenleyebilirsiniz. `enabled` Ve`automatic` anahtarlarının doğru`packageRestore` ayarlandığından emin olun:

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
> `packageRestore` Ayarları doğrudan ' de `nuget.config`düzenlerseniz, Seçenekler iletişim kutusunun geçerli değerleri gösterdiği şekilde Visual Studio 'yu yeniden başlatın.

## <a name="other-potential-conditions"></a>Diğer olası koşullar

- Eksik dosyalar nedeniyle derleme hatalarıyla karşılaşabilirsiniz ve bunları indirmek için NuGet geri yüklemeyi kullanmayı söyleyen bir ileti görürsünüz. Bununla birlikte, bir geri yükleme çalıştırmak "tüm paketler zaten yüklü ve geri yüklenecek bir şey yok" olabilir. Bu durumda, `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosyasını silin (packagereference kullanırken) ve geri yükle ' yi yeniden çalıştırın. Hata devam ederse, genel paketleri ve `nuget locals all -clear` [önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi `dotnet locals all --clear` *genel paketleri* ve önbellek klasörlerini temizlemek için komut satırını kullanın.

- Kaynak denetiminden bir proje edinirken, proje klasörleriniz salt okunurdur olarak ayarlanabilir. Klasör izinlerini değiştirin ve paketleri yeniden geri yüklemeyi deneyin.

- NuGet 'in eski bir sürümünü kullanıyor olabilirsiniz. Önerilen en son sürümler için [NuGet.org/downloads](https://www.nuget.org/downloads) denetleyin. Visual Studio 2015 için 3.6.0 önerilir.

Başka sorunlarla karşılaşırsanız, daha fazla ayrıntı almak için [GitHub 'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) yapın.
