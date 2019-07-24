---
title: NuGet istemci araçlarını yükleme
description: İstemci araçları, DotNet ve NuGet komut satırı arabirimleri (CLı) ve Visual Studio için Paket Yöneticisi yükleme kılavuzu.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: d7aa2e4bdb78dcc6747d9775cbdf0d6c41855b96
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419805"
---
# <a name="install-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paket yüklemek mi istiyorsunuz? Bkz. [NuGet paketlerini yüklemeye yönelik yollar](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

NuGet ile bir paket tüketicisi veya Oluşturucu olarak çalışmak için, komut satırı arabirimi (CLı) araçlarının yanı sıra Visual Studio 'da NuGet özelliklerini de kullanabilirsiniz. Bu makale, farklı araçların yeteneklerini, nasıl yükleneceğini ve karşılaştırılma [özelliklerinin kullanılabilirliğini](#feature-availability)kısaca özetler. Paketleri kullanmak üzere NuGet kullanmaya başlamak için bkz. [bir paket (DotNet CLI) yüklemek ve kullanmak](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) ve [bir paketi yüklemek ve kullanmak (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). NuGet paketleri oluşturmaya başlamak için bkz. [BIR ağ standart paketi (DotNet CLI) oluşturma ve yayımlama](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ve [bir ağ standart paketi oluşturma ve yayımlama (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | İndirme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefleyen her bir [SDK stili proje](resources/check-project-format.md) . .NET Core SDK eklenmiştir ve tüm platformlarda çekirdek NuGet özellikleri sağlar. (Visual Studio 2017 ' den itibaren, DotNet CLı, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir.)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | .NET Framework kitaplıkları ve .NET Standard kitaplıklarını hedefleyen biri gibi [SDK olmayan](resources/check-project-format.md) herhangi bir proje için CLI aracı. Tüm NuGet yeteneklerini Windows üzerinde sağlar. Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows 'da, Paket Yöneticisi Kullanıcı arabirimi ve Paket Yöneticisi konsolu aracılığıyla NuGet özellikleri sağlar; ile dahildir. NET ilgili iş yükleri. Mac 'te, Kullanıcı arabirimi aracılığıyla belirli özellikleri sağlar. Visual Studio Code, NuGet özellikleri uzantılar aracılığıyla sağlanır. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBUILD CLI](reference/msbuild-targets.md) , temel olarak yapı sunucularında yararlı olan paketleri geri yükleme ve oluşturma özelliği de sağlar. MSBuild, NuGet ile çalışmak için genel amaçlı bir araç değildir.

## <a name="cli-tools"></a>CLı araçları

İki NuGet CLI aracı ve ' `dotnet.exe` `nuget.exe`dir. Karşılaştırma için [özellik kullanılabilirliğine](#feature-availability) bakın.

* .NET Core veya .NET Standard hedeflemek için DotNet CLı kullanın. SDK [özniteliğini](/dotnet/core/tools/csproj#additions)kullanan SDK stili proje biçimi için CLIgereklidir.`dotnet`
* .NET Framework (yalnızca SDK olmayan proje) hedeflemek için `nuget.exe` CLI kullanın. Proje öğesinden `packages.config` packagereference öğesine geçirilirse DotNet CLI kullanın.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2,0 CLI `dotnet.exe`, tüm platformlarda (Windows, Mac ve Linux) çalışarak paketleri yükleme, geri yükleme ve yayımlama gibi temel NuGet özellikleri sağlar. `dotnet`Çoğu senaryoda yararlı olan .NET Core proje dosyaları (gibi `.csproj`) ile doğrudan tümleştirme sağlar. `dotnet`, her platform için doğrudan de oluşturulmuştur ve mono yüklemenizi gerektirmez.

Yüklemesinden

- Geliştirici bilgisayarlarında [.NET Core SDK](https://aka.ms/dotnetcoregs)' yi yükler. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.
- Yapı sunucuları için [sürekli tümleştirmede .NET Core SDK ve araçları kullanma](/dotnet/core/tools/using-ci-with-cli)yönergelerini izleyin.

DotNet CLı ile temel komutları kullanmayı öğrenmek için bkz. [DotNet CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe CLI

CLI, tüm NuGet yeteneklerini sağlayan Windows için komut satırı yardımcı programıdır; Ayrıca, bazı sınırlamalar ile [mono](http://www.mono-project.com/docs/getting-started/install/) kullanarak Mac OSX ve Linux 'ta de çalıştırılabilir. `nuget.exe` `nuget.exe`

`nuget.exe` CLI ile temel komutları kullanmayı öğrenmek için bkz. [NuGet. exe CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-nuget-cli.md).

Yüklemesinden

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Mevcut `nuget update -self` bir NuGet. exe ' yi en son sürüme güncelleştirmek için Windows 'ta kullanın.

> [!Note]
> En son önerilen NuGet CLı, ' de her `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`zaman kullanılabilir. Önceki bir URL `https://nuget.org/nuget.exe` olan eski bir sürekli tümleştirme sistemiyle uyumluluk amaçları için şu anda [kullanım dışı 2.8.6 CLI aracını](https://github.com/NuGet/NuGetGallery/issues/5381)sağlamaktadır.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet özellikleri Market uzantıları aracılığıyla kullanılabilir veya `dotnet.exe` ya `nuget.exe` da CLI araçlarını kullanır.

- Mac için Visual Studio: belirli NuGet özellikleri doğrudan yerleşiktir. İzlenecek yol için [projenize bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough) bölümüne bakın. Diğer yetenekler için `dotnet.exe` veya `nuget.exe` CLI araçlarını kullanın.

- Windows üzerinde Visual Studio: **NuGet Paket Yöneticisi** , Visual Studio 2012 ve üzeri sürümlerde bulunur. Visual Studio, çoğu NuGet işlemini çalıştırabileceğiniz [Paket Yöneticisi Kullanıcı arabirimi](consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolu](consume-packages/install-use-packages-powershell.md)sağlar.
  - Visual Studio 2017 ' den başlayarak, yükleyici, .NET kullanan herhangi bir iş yüküne sahip NuGet Paket Yöneticisi 'Ni içerir. Ayrı olarak yüklemek veya paket yöneticisinin yüklendiğini doğrulamak için, Visual Studio yükleyicisi 'ni çalıştırın ve **tek tek bileşenler altında, NuGet paket yöneticisi > kod araçları >** .
  - Paket Yöneticisi Kullanıcı arabirimi ve konsolu, Windows üzerinde Visual Studio 'ya özeldir. Mac için Visual Studio şu anda mevcut değildir.
  - IDE 'de NuGet özelliklerini desteklemek için bir CLı aracı gereklidir. `dotnet` CLI veya`nuget.exe` CLI kullanabilirsiniz. `dotnet` CLI, .NET Core gibi bazı Visual Studio iş yükleri ile yüklenir. CLI `nuget.exe` , daha önce açıklandığı gibi ayrı olarak yüklenmelidir.
  - Paket Yöneticisi konsol komutları yalnızca Windows üzerinde Visual Studio 'da çalışır ve diğer PowerShell ortamları içinde çalışmaz.
  - Visual Studio 2010 ve önceki sürümlerde, "Visual Studio için NuGet Paket Yöneticisi" uzantısını yükler.
  - Visual Studio 2013 ve 2015 için NuGet uzantıları, adresinden [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)de indirilebilir.
  - Yaklaşan NuGet özelliklerini önizlemek istiyorsanız, Visual Studio 'nun kararlı sürümleriyle yan yana çalışan [Visual studio 2017 Preview](https://www.visualstudio.com/vs/preview/)sürümünü yükleyebilirsiniz. Sorunları bildirmek veya önizlemelerde fikir paylaşmak için [NuGet GitHub deposunda](https://github.com/Nuget/Home/issues)bir sorun açın.

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Özellik | DotNet CLı | NuGet CLı (Windows) | NuGet CLı (mono) | Visual Studio (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Paketleri ara |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Güncelleştirme paketleri | &#10004; | &#10004; | | &#10004; | &#10004; |
| Paketleri geri yükle | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Paket akışlarını yönetme (kaynaklar) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Bir akıştaki paketleri yönetme | &#10004; | &#10004; | &#10004; | | |
| Akışlar için API anahtarlarını ayarlama | | &#10004; | &#10004; | | |
| Paket oluşturma (3) | &#10004; | &#10004; | &#10004;4 | &#10004; | |
| Paketleri yayımlama | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Paketleri Çoğalt |  | &#10004; | &#10004; | | |
| *Genel paket* ve önbellek klasörlerini yönetme | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmasını Yönet | | &#10004; | &#10004; | | |

(1) proje dosyalarını etkilemez; Bunun `dotnet.exe` yerine kullanın.

(2) yalnızca dosya ile `packages.config` birlikte çalışarak çözüm (`.sln`) dosyaları ile değil.

(3) CLı aracılığıyla yalnızca Visual Studio Kullanıcı arabirimi araçlarında temsil edilmeyen çeşitli gelişmiş paket özellikleri vardır.

(4) dosyalarla birlikte `.nuspec` çalışarak, proje dosyaları ile değil.

### <a name="related-topics"></a>İlgili konular

- [Visual Studio kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell kullanarak paket yükleyip yönetme](consume-packages/install-use-packages-powershell.md)
- [DotNet CLı kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-dotnet-cli.md)
- [NuGet. exe CLı kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-nuget-cli.md)
- [Paket Yöneticisi konsolu PowerShell Başvurusu](reference/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Paket yayımlama](nuget-org/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler, NuGet paketlerini görsel olarak keşfetmeye, oluşturmaya ve düzenlemeye yönelik açık kaynaklı, tek başına bir araç olan [NuGet paket Gezginini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)de keşfedebilir. Örneğin, paketi yeniden oluşturmadan bir paket yapısında deneysel değişiklikler yapmak çok faydalı olur.
