---
title: NuGet istemci araçlarını yükleme
description: İstemci araçlarını Yükleme Kılavuzu dotnet ve nuget komut satırı arabirimi (CLI) ve Visual Studio Paket Yöneticisi.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: a4a3f5509792e56c09d18b3da98588d17f4756ee
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841936"
---
# <a name="install-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paketi yüklemek mi istiyorsunuz? Bkz: [NuGet paketlerini yükleme yolları](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Bir paket kullanıcısı veya Oluşturucu, NuGet ile çalışmak için Visual Studio'da NuGet özelliklerin yanı sıra komut satırı arabirimi (CLI) araçlarını kullanabilirsiniz. Bu makalede farklı araçları özelliklerini kısaca özetler. bunları ve bunların karşılaştırmalı yükleme [Özellik kullanılabilirliği](#feature-availability). NuGet paketlerini kullanmak için kullanmaya başlamak için bkz: [yükleme ve kullanma (.NET CLI) bir paket](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) ve [yükleme ve kullanma (Visual Studio) bir paket](quickstart/install-and-use-a-package-in-visual-studio.md). NuGet paketleri oluşturmaya başlamak için bkz. [oluştur ve NET Standard paketi (dotnet CLI) yayımlama](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ve [oluştur ve NET Standard paketi (Visual Studio) yayımlama](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | İndirme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core ve .NET standart kitaplıkları ve tüm CLI aracı [SDK stilinde proje](resources/check-project-format.md) gibi .NET Framework hedefleyen bir. .NET Core SDK'sı ile dahil ve tüm platformlarda temel NuGet özellikleri sağlar. (Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlangıç iş yükleri ile ilişkili.)| [.NET core SDK'sı](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | CLI aracı ve .NET Framework kitaplıkları için [SDK stil projeyi](resources/check-project-format.md) .NET standart kitaplıkları hedefleyin. Windows üzerinde NuGet özelliklerin tümünü sağlar, Mono altında çalışırken çoğu özelliği Mac ve Linux'ta sağlar. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows üzerinde Paket Yöneticisi UI ve Paket Yöneticisi konsolu üzerinden NuGet özellikleri sağlar. bulunan. NET ilgili iş yükleri. Mac bilgisayarlarda, kullanıcı Arabirimi aracılığıyla belirli özellikleri sağlar. Visual Studio Code, uzantılar aracılığıyla NuGet özellikleri sağlanır. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) geri yükleme ve yapı sunucularında öncelikle faydalı olan paketler, oluşturma olanağı da sağlar. MSBuild, NuGet ile çalışmak için genel amaçlı bir aracı değil.

## <a name="cli-tools"></a>CLI araçları

İki NuGet CLI Araçları `dotnet.exe` ve `nuget.exe`. Bkz: [Özellik kullanılabilirliği](#feature-availability) bir karşılaştırma için.

* .NET Core veya .NET Standard hedeflemek için ' % s'dotnet CLI kullanın. Dotnet CLI kullanan SDK stilinde proje biçimi için gerekli olan [SDK özniteliği](/dotnet/core/tools/csproj#additions).
* (Yalnızca SDK stili Proje), .NET Framework kullanan hedef `nuget.exe CLI`. Proje geçiş yaptıysanız `packages.config` dotnet CLI PackageReference için kullanın.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe`, tüm platformlar (Windows, Mac ve Linux) çalışır ve paketleri yayımlama yükleme ve geri yükleme gibi temel NuGet özellikleri sağlar. `dotnet` .NET Core proje dosyaları ile doğrudan tümleştirme sağlar (gibi `.csproj`), çoğu senaryoda faydalı olduğu. `dotnet` Ayrıca doğrudan her platform için yerleşik olarak bulunur ve Mono yükleme gerektirmez.

Yükleme:

- Geliştirici bilgisayarlara yüklemek [.NET Core SDK'sı](https://aka.ms/dotnetcoregs). Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlayarak, iş yüklerini ilgili.
- Derleme sunucuları için yönergeleri izleyin [kullanarak .NET Core SDK'sını ve sürekli tümleştirme araçlarını](/dotnet/core/tools/using-ci-with-cli).

Temel komutlar dotnet CLI ile kullanmayı öğrenmek için bkz [yükleyin ve dotnet CLI kullanarak paketleri kullanma](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI `nuget.exe`, komut satırı yardımcı programıdır Windows için NuGet özelliklerin tümünü sağlar; Mac OSX ve Linux'ı kullanarak da çalıştırılabilir [Mono](http://www.mono-project.com/docs/getting-started/install/) bazı sınırlamalarla birlikte.

Temel komutlarıyla kullanırsınız öğrenmek için `nuget.exe` CLI bkz [yükleyin ve CLI nuget.exe kullanarak paketleri kullanma](consume-packages/install-use-packages-nuget-cli.md).

Yükleme:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Kullanım `nuget update -self` var olan bir nuget.exe en son sürüme güncelleştirmek için Windows üzerinde.

> [!Note]
> NuGet CLI bulunabilir, her zaman en son önerilen `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Eski sürekli tümleştirme sistemleri, önceki bir URL ile uyumluluk amacıyla `https://nuget.org/nuget.exe` şu anda sağlar [2.8.6 kullanım dışı CLI aracı](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio kodu: NuGet yetenekleri Market uzantıları kullanılabilir veya kullanın `dotnet.exe` veya `nuget.exe` CLI araçları.

- Mac için Visual Studio: belirli NuGet özellikleri doğrudan yerleşiktir. Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough) kılavuz. Diğer yeteneklerini kullanan `dotnet.exe` veya `nuget.exe` CLI araçları.

- Windows üzerinde Visual Studio: **NuGet Paket Yöneticisi** Visual Studio 2012 ile birlikte sunulan ve üzerinde desteklenir. Visual Studio sağlar [Paket Yöneticisi UI](tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](tools/package-manager-console.md), aracılığıyla NuGet işlemlerinin çoğu çalıştırabilirsiniz.
  - Visual Studio 2017'den itibaren NuGet Paket Yöneticisi .NET kullanan herhangi bir iş yüküyle yükleyici içerir. Ayrı olarak yüklemeniz veya Paket Yöneticisi'nin yüklü olduğunu doğrulamak için Visual Studio Yükleyicisi'ni çalıştırın ve altında seçeneği işaretleyin **tek tek bileşenler > kod Araçlar > NuGet Paket Yöneticisi**.
  - Paket Yöneticisi UI ve konsol Windows üzerinde Visual Studio için benzersizdir. Mac için Visual Studio şu anda kullanılabilir değil
  - CLI aracını IDE içinde NuGet özellikleri desteklemek için gereklidir. Kullanabilirsiniz `dotnet` CLI veya `nuget.exe` CLI. `dotnet` CLI, .NET Core gibi bazı Visual Studio iş yükleri ile yüklenir. `nuget.exe` CLI ayrı olarak daha önce anlatıldığı gibi yüklenmelidir.
  - Paket Yöneticisi Konsolu komutları yalnızca Visual Studio içinde Windows üzerinde çalışır ve diğer PowerShell ortamlar içinde çalışmaz.
  - Visual Studio 2010 ve önceki sürümlerinde, "NuGet Paket Yöneticisi için Visual Studio" uzantıyı yükleyin.
  - NuGet uzantıları Visual Studio 2013 ve 2015 de nden indirilebilir [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
  - Yaklaşan NuGet özelliklerin önizlemesini sağlamak isterseniz yükleme [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), yan yana kararlı Visual Studio sürümleriyle çalışır. Sorun bildirin veya Önizleme için fikir alışverişinde bulunmak için bir sorun açın [NuGet GitHub deposu](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Özellik | DotNet CLI | nuget CLI (Windows) | nuget CLI (tekli) | Visual Studio (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Paketleri Ara |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Güncelleştirme paketleri | &#10004; | &#10004; | | &#10004; | &#10004; |
| Paketleri geri yükle | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Paket akışları (kaynaklar) yönetme | | &#10004; | &#10004; | &#10004; | &#10004; |
| Bir akış paketleri yönetin | &#10004; | &#10004; | &#10004; | | |
| Akışları kümesi API anahtarları | | &#10004; | &#10004; | | |
| Packages(3) oluşturma | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Paketleri yayımlama | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Çoğaltma paketleri |  | &#10004; | &#10004; | | |
| Yönetme *paket genel* ve önbellek klasörleri | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmasını yönetme | | &#10004; | &#10004; | | |

(1) proje dosyalarını etkilemez. kullanma `dotnet.exe` yerine.

(2) yalnızca ile çalışır `packages.config` dosya ve çözümü ile değil (`.sln`) dosyaları.

(3) çeşitli Gelişmiş paket özelliklerini yalnızca, Visual Studio kullanıcı Arabirimi araçları temsil olmayan CLI aracılığıyla kullanıma sunuldu.

(4) çalışır `.nuspec` dosyaları ancak proje dosyaları ile değil.

### <a name="related-topics"></a>İlgili konular

- [Yükleme ve Visual Studio kullanarak paketleri yönetme](tools/package-manager-ui.md)
- [Yükleme ve Paket Yöneticisi konsolu kullanarak paketleri yönetme](tools/package-manager-console.md)
- [Yükleme ve dotnet CLI kullanarak paketleri yönetme](consume-packages/install-use-packages-dotnet-cli.md)
- [Yükleme ve CLI nuget.exe kullanarak paketleri yönetme](consume-packages/install-use-packages-nuget-cli.md)
- [Paket Yöneticisi konsolu PowerShell başvurusu](tools/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Paket yayımlama](nuget-org/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler de keşfedebilir [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), görsel olarak keşfedin, oluşturmak ve NuGet paketleri düzenlemek için açık kaynak, tek başına bir araç. Örneğin, Deneysel bir paket yapısı için paket derlenmeden değişiklik çok yararlı olduğu.
