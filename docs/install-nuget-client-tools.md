---
title: "NuGet istemci Araçları'nı yükleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "İstemci Araçları'nı yükleme konusunda yönergeler dotnet ve nuget komut satırı arabirimi (CLI) ve Visual Studio için Paket Yöneticisi."
keywords: "DotNet.exe CLI, nuget.exe CLI, NuGet istemcisi araçları, NuGet Paket Yöneticisi, NuGet Paket Yöneticisi konsolu, NuGet Visual Studio, NuGet beta kanal"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec8de83c9e05981016215e487888ab68a616d977
ms.sourcegitcommit: dbcb872ec10430e1d761f34b851650e31c87a96d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/03/2018
---
# <a name="installing-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paketi yüklemek istiyorsunuz? Bkz: [NuGet paketlerini yüklemek için yol](consume-packages/ways-to-install-a-package.md).**

Bir paket tüketici ya da Oluşturucu, olarak NuGet ile çalışmak için kullanabileceğiniz [platformlar arası komut satırı arabirimi (CLI) araçları](#cli-tools) yanı [Visual Studio'da NuGet özellikleri](#visual-studio). Bu makalede bulunan farklı araçlar özelliklerini kısaca özetler bunları ve bunların karşılaştırmalı nasıl yükleneceği [Özellik kullanılabilirliği](#feature-availability).

| Aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | İndirme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core SDK'sı ile dahil ve tüm platformlarda core NuGet özellikleri sağlar. | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Windows ve çoğu özellikleri altında çalışan tüm NuGet özellikleri sağlayan [Mono](http://www.mono-project.com/docs/getting-started/install/) Mac ve Linux üzerinde. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | NuGet Paket Yöneticisi kullanıcı Arabirimi ve Paket Yöneticisi konsolu üzerinden özellikleri sağlar. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) da geri yükleme ve yapı sunucularda öncelikle faydalı olduğu paketlerini oluşturma olanağı sağlar. MSBuild, aksi takdirde NuGet ile çalışmak için genel amaçlı bir aracı değildir.

## <a name="cli-tools"></a>CLI araçlarını

İki NuGet CLI Araçları `dotnet.exe` ve `nuget.exe`. Bkz: [Özellik kullanılabilirliği](#feature-availability) bir karşılaştırması.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI `dotnet.exe`, çalışan tüm platformlarda (Windows, Mac ve Linux) ve yükleme, geri yükleme ve paketleri yayımlama gibi temel NuGet özellikleri sağlar. 'dotnet'.NET Core proje dosyalarını doğrudan tümleştirme sağlar (gibi `.csproj`), çoğu senaryoda yararlı olduğu. `dotnet`Ayrıca her platform için doğrudan yerleşik olarak bulunur ve Mono yüklemenizi gerektirmez.

Yükleme:

- Geliştirici bilgisayarlara yüklemek [.NET Core SDK](https://aka.ms/dotnetcoregs).
- Yapı sunucuları için yönergeleri izleyin [kullanarak .NET Core SDK ve sürekli tümleştirme Araçları](/dotnet/core/tools/using-ci-with-cli).

Daha fazla bilgi için bkz: [.NET Core komut satırı arabirimi Araçları](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>nuget.exe CLI

NuGet CLI `nuget.exe`, komut satırı yardımcı programıdır Windows için tüm NuGet yetenekleri sağlayan; Mac OSX ve Linux Mono bazı kısıtlamalarla kullanarak da çalıştırılabilir. Farklı `dotnet`, `nuget.exe` CLI proje dosyalarını etkilemez.

Yükleme:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> Kullanım `nuget update -self` varolan nuget.exe en son sürüme güncelleştirmek için.

> [!Note]
> NuGet CLI adresinde her zaman en son önerilen `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Eski sürekli tümleştirme sistemleri, önceki bir URL ile uyumluluk amacıyla `https://nuget.org/nuget.exe` şu anda 2.8.6 sağlar CLI aracı. [Bu kullanım dışı](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet yetenekleri Market uzantıları kullanılabilir veya kullanmak `dotnet.exe` veya `nuget.exe` CLI araçlarını.
- Mac için Visual Studio: bazı NuGet özellikleri doğrudan yerleşiktir. Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough) kılavuz. Diğer özellikler için kullanmak `dotnet.exe` veya `nuget.exe` CLI araçlarını.

- Visual Studio Windows: **NuGet Paket Yöneticisi** Visual Studio 2012 ile birlikte sunulan ve üzerinde desteklenir. Paket Yöneticisi sağlar [Paket Yöneticisi kullanıcı Arabirimi](tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](tools/package-manager-console.md), aracılığıyla NuGet işlemlerinin çoğu çalıştırabilirsiniz.
  - Paket Yöneticisi kullanıcı Arabirimi ve Konsolu Windows Visual Studio benzersizdir. Bunlar şu anda Mac için Visual Studio üzerinde kullanılabilir değil.
  - Visual Studio otomatik olarak içermez `nuget.exe` CLI, daha önce açıklandığı gibi ayrı olarak yüklenmesi gerekir.
  - Paket Yöneticisi Konsolu komutları iş yalnızca Visual Studio'dan Windows ve diğer PowerShell ortamlar içinde değil.
  - Visual Studio 2017 yükleyici .NET kullanan herhangi bir iş yükü ile NuGet Paket Yöneticisi'ni içerir. Ayrı olarak yüklemeniz ya da Paket Yöneticisi'nin yüklü olduğunu doğrulamak için Visual Studio 2017 yükleyiciyi çalıştırın ve altında seçeneğini **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi**.
  - Ve önceki sürümleri, Visual Studio 2010 için "NuGet Paket Yöneticisi için Visual Studio" uzantısını yükleyin.
  - Visual Studio 2013 ve 2015 için NuGet uzantıları da adresinden yüklenebilir [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Yaklaşan NuGet özellikleri Önizleme istiyorsanız, yükleme [Visual Studio 2017 Önizleme](https://www.visualstudio.com/vs/preview/), Visual Studio, kararlı sürümleriyle-yana çalışır. Sorunları rapor veya önizlemeleri fikirleri paylaşmak için bir sorun açmak [NuGet GitHub deposunu](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Özellik | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Arama paketleri |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Güncelleştirme paketleri | &#10004; | &#10004; | | &#10004; | &#10004; |
| geri yükleme paketleri | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Paket akışları (kaynakları) yönetme | | &#10004; | &#10004; | &#10004; | &#10004; |
| Bir akış üzerinde paketlerini yönetme | &#10004;(1) | &#10004; | &#10004; | | |
| Akışları kümesi API tuşları | | &#10004; | &#10004; | | |
| Packages(4) oluşturma | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Paketleri yayımlama | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Çoğaltma paketleri |  | &#10004; | &#10004; | | |
| NuGet önbelleği yönetme | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmasını Yönet | | &#10004; | &#10004; | | |

(1) yalnızca nuget.org paketleri

(2) proje dosyalarını etkilemez; kullanmak `dotnet.exe` yerine.

(3) yalnızca ile çalışır `packages.config` dosya ve çözüm ile değil (`.sln`) dosyaları.

(4) bunlar Visual Studio kullanıcı Arabirimi Araçları'nda yalnızca temsil değil olarak çeşitli Gelişmiş paket özellikleri CLI aracılığıyla kullanılabilir.

(5) çalışır `.nuspec` dosyaları proje dosyalarını birlikte değil.

### <a name="related-topics"></a>İlgili konular

- [DotNet komutları](tools/dotnet-commands.md)
- [NuGet CLI başvurusu](tools/nuget-exe-cli-reference.md)
- [Paket Yöneticisi kullanıcı Arabirimi başvurusu](tools/package-manager-ui.md)
- [Paket Yöneticisi konsolu başvurusu](tools/package-manager-console.md)
- [Paket Yöneticisi konsolu PowerShell başvurusu](tools/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Bir paketi yayımlama](create-packages/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler de keşfedin [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), görsel olarak araştırmak, oluşturmak ve NuGet paketleri düzenlemek için açık kaynaklı, tek başına bir araç. Bu örneğin, paket derlenmeden paket yapısına Deneysel değişiklik yapmak için çok, yararlıdır.
