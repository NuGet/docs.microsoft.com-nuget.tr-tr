---
title: NuGet istemci araçlarını yükleme
description: İstemci araçları, DotNet ve NuGet komut satırı arabirimleri (CLı) ve Visual Studio için Paket Yöneticisi yükleme kılavuzu.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 09c859c0ab6767ea80b6a64c194aa2623ee5c505
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610513"
---
# <a name="install-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paket yüklemek mi istiyorsunuz? Bkz. [NuGet paketlerini yüklemeye yönelik yollar](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

NuGet ile bir paket tüketicisi veya Oluşturucu olarak çalışmak için, komut satırı arabirimi (CLı) araçlarının yanı sıra Visual Studio 'da NuGet özelliklerini de kullanabilirsiniz. Bu makale, farklı araçların yeteneklerini, nasıl yükleneceğini ve karşılaştırılma [özelliklerinin kullanılabilirliğini](#feature-availability)kısaca özetler. Paketleri kullanmak üzere NuGet kullanmaya başlamak için bkz. [bir paket (DotNet CLI) yüklemek ve kullanmak](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) ve [bir paketi yüklemek ve kullanmak (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). NuGet paketleri oluşturmaya başlamak için bkz. [BIR ağ standart paketi (DotNet CLI) oluşturma ve yayımlama](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ve [bir ağ standart paketi oluşturma ve yayımlama (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Araç&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | İndirin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [DotNet. exe](#dotnetexe-cli) | .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefleyen her bir [SDK stili proje](resources/check-project-format.md) . .NET Core SDK eklenmiştir ve tüm platformlarda çekirdek NuGet özellikleri sağlar. (Visual Studio 2017 ' den itibaren, DotNet CLı, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir.)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [NuGet. exe](#nugetexe-cli) | .NET Framework kitaplıkları ve .NET Standard kitaplıklarını hedefleyen biri gibi [SDK olmayan](resources/check-project-format.md) herhangi bir proje için CLI aracı. Tüm NuGet yeteneklerini Windows üzerinde sağlar. Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar. | [NuGet. exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows 'da, Paket Yöneticisi Kullanıcı arabirimi ve Paket Yöneticisi konsolu aracılığıyla NuGet özellikleri sağlar; ile dahildir. NET ilgili iş yükleri. Mac 'te, Kullanıcı arabirimi aracılığıyla belirli özellikleri sağlar. Visual Studio Code, NuGet özellikleri uzantılar aracılığıyla sağlanır. | [Visual Studio](https://www.visualstudio.com/downloads/) |

[MSBUILD CLI](reference/msbuild-targets.md) , temel olarak yapı sunucularında yararlı olan paketleri geri yükleme ve oluşturma özelliği de sağlar. MSBuild, NuGet ile çalışmak için genel amaçlı bir araç değildir.

## <a name="cli-tools"></a>CLı araçları

İki NuGet CLı aracı `dotnet.exe` ve `nuget.exe`. Karşılaştırma için [özellik kullanılabilirliğine](#feature-availability) bakın.

* .NET Core veya .NET Standard hedeflemek için DotNet CLı kullanın. SDK [özniteliğini](/dotnet/core/tools/csproj#additions)kullanan SDK stili proje biçimi IÇIN `dotnet` CLI gereklidir.
* .NET Framework (yalnızca SDK olmayan proje) hedeflemek için `nuget.exe` CLı kullanın. Proje `packages.config` ' den PackageReference 'a geçirilirse DotNet CLı kullanın.

### <a name="dotnetexe-cli"></a>DotNet. exe CLı

.NET Core 2,0 CLı, `dotnet.exe`, tüm platformlarda (Windows, Mac ve Linux) çalışarak, paketleri yükleme, geri yükleme ve yayımlama gibi temel NuGet özellikleri sağlar. `dotnet`, Çoğu senaryoda yararlı olacak şekilde .NET Core proje dosyaları (`.csproj`gibi) ile doğrudan tümleştirme sağlar. `dotnet` Ayrıca her platform için doğrudan yerleşiktir ve mono yüklemenizi gerektirmez.

Yüklemesinden

- Geliştirici bilgisayarlarında [.NET Core SDK](https://aka.ms/dotnetcoregs)' yi yükler. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.
- Yapı sunucuları için [sürekli tümleştirmede .NET Core SDK ve araçları kullanma](/dotnet/core/tools/using-ci-with-cli)yönergelerini izleyin.

DotNet CLı ile temel komutları kullanmayı öğrenmek için bkz. [DotNet CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>NuGet. exe CLı

`nuget.exe` CLı, `nuget.exe`, tüm NuGet yeteneklerini sağlayan Windows için komut satırı yardımcı programıdır; Ayrıca, Mac OSX ve Linux 'ta, bazı sınırlamalara sahip [mono](https://www.mono-project.com/docs/getting-started/install/) kullanılarak da çalıştırılabilir.

`nuget.exe` CLı ile temel komutları kullanmayı öğrenmek için bkz. [NuGet. exe CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-nuget-cli.md).

Yüklemesinden

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Mevcut bir NuGet. exe ' yi en son sürüme güncelleştirmek için Windows üzerinde `nuget update -self` kullanın.

> [!Note]
> En son önerilen NuGet CLı `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`' de her zaman kullanılabilir. Önceki bir URL olan daha eski bir sürekli tümleştirme sistemiyle uyumluluk amaçları için `https://nuget.org/nuget.exe` Şu anda [kullanım dışı 2.8.6 CLI aracını](https://github.com/NuGet/NuGetGallery/issues/5381)sunmaktadır.

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet özellikleri Market uzantıları aracılığıyla kullanılabilir veya `dotnet.exe` veya `nuget.exe` CLı araçlarını kullanır.

- Mac için Visual Studio: belirli NuGet özellikleri doğrudan yerleşiktir. İzlenecek yol için [projenize bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough) bölümüne bakın. Diğer yetenekler için `dotnet.exe` veya `nuget.exe` CLı araçlarını kullanın.

- Windows üzerinde Visual Studio: **NuGet Paket Yöneticisi** , visual Studio 2012 ve üzeri sürümlerde bulunur. Visual Studio, çoğu NuGet işlemini çalıştırabileceğiniz [Paket Yöneticisi Kullanıcı arabirimi](consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolu](consume-packages/install-use-packages-powershell.md)sağlar.
  - Visual Studio 2017 ' den başlayarak, yükleyici, .NET kullanan herhangi bir iş yüküne sahip NuGet Paket Yöneticisi 'Ni içerir. Ayrı olarak yüklemek veya paket yöneticisinin yüklendiğini doğrulamak için, Visual Studio yükleyicisi 'ni çalıştırın ve **tek tek bileşenler altında, NuGet paket yöneticisi > kod araçları >** .
  - Paket Yöneticisi Kullanıcı arabirimi ve konsolu, Windows üzerinde Visual Studio 'ya özeldir. Mac için Visual Studio şu anda mevcut değildir.
  - IDE 'de NuGet özelliklerini desteklemek için bir CLı aracı gereklidir. `dotnet` CLı ya da `nuget.exe` CLı kullanabilirsiniz. `dotnet` CLı, .NET Core gibi bazı Visual Studio iş yükleri ile yüklenir. `nuget.exe` CLı, daha önce açıklandığı gibi ayrı olarak yüklenmelidir.
  - Paket Yöneticisi konsol komutları yalnızca Windows üzerinde Visual Studio 'da çalışır ve diğer PowerShell ortamları içinde çalışmaz.
  - Visual Studio 2010 ve önceki sürümlerde, "Visual Studio için NuGet Paket Yöneticisi" uzantısını yükler.
  - Visual Studio 2013 ve 2015 için NuGet uzantıları, [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)de indirilebilir.
  - Yaklaşan NuGet özelliklerini önizlemek istiyorsanız, Visual Studio 'nun kararlı sürümleriyle yan yana çalışan bir [Visual Studio önizlemesi](https://www.visualstudio.com/vs/preview/)yüklersiniz. Sorunları bildirmek veya önizlemelerde fikir paylaşmak için [NuGet GitHub deposunda](https://github.com/Nuget/Home/issues)bir sorun açın.

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Özellik | DotNet CLı | NuGet CLı (Windows) | NuGet CLı (mono) | Visual Studio (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Paketleri ara |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004; | &#10004;(1 | &#10004; | &#10004; | &#10004; |
| Güncelleştirme paketleri | &#10004; | &#10004; | | &#10004; | &#10004; |
| Paketleri geri yükle | &#10004; | &#10004; | &#10004;( | &#10004; | &#10004; |
| Paket akışlarını yönetme (kaynaklar) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Bir akıştaki paketleri yönetme | &#10004; | &#10004; | &#10004; | | |
| Akışlar için API anahtarlarını ayarlama | | &#10004; | &#10004; | | |
| Paket oluşturma (3) | &#10004; | &#10004; | &#10004;4 | &#10004; | |
| Paketleri yayımlama | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Paketleri Çoğalt |  | &#10004; | &#10004; | | |
| *Genel paket* ve önbellek klasörlerini yönetme | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmasını Yönet | | &#10004; | &#10004; | | |

(1) proje dosyalarını etkilemez; Bunun yerine `dotnet.exe` kullanın.

(2), çözüm (`.sln`) dosyalarıyla değil yalnızca `packages.config` dosyası ile kullanılabilir.

(3) CLı aracılığıyla yalnızca Visual Studio Kullanıcı arabirimi araçlarında temsil edilmeyen çeşitli gelişmiş paket özellikleri vardır.

(4) `.nuspec` dosyalarla birlikte çalışarak, proje dosyalarıyla birlikte değildir.

### <a name="related-topics"></a>İlgili konular

- [Visual Studio kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell kullanarak paket yükleyip yönetme](consume-packages/install-use-packages-powershell.md)
- [DotNet CLı kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-dotnet-cli.md)
- [NuGet. exe CLı kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-nuget-cli.md)
- [Paket Yöneticisi konsolu PowerShell Başvurusu](reference/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Paket yayımlama](nuget-org/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler, NuGet paketlerini görsel olarak keşfetmeye, oluşturmaya ve düzenlemeye yönelik açık kaynaklı, tek başına bir araç olan [NuGet paket Gezginini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)de keşfedebilir. Örneğin, paketi yeniden oluşturmadan bir paket yapısında deneysel değişiklikler yapmak çok faydalı olur.
