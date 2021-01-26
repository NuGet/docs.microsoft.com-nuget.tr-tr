---
title: NuGet istemci araçlarını yükleme
description: İstemci araçları, DotNet ve NuGet komut satırı arabirimleri (CLı) ve Visual Studio için Paket Yöneticisi yükleme kılavuzu.
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775897"
---
# <a name="install-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paket yüklemek mi istiyorsunuz? Bkz. [NuGet paketlerini yüklemeye yönelik yollar](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

NuGet ile bir paket tüketicisi veya Oluşturucu olarak çalışmak için, komut satırı arabirimi (CLı) araçlarının yanı sıra Visual Studio 'da NuGet özelliklerini de kullanabilirsiniz. Bu makale, farklı araçların yeteneklerini, nasıl yükleneceğini ve karşılaştırılma [özelliklerinin kullanılabilirliğini](#feature-availability)kısaca özetler. Paketleri kullanmak üzere NuGet kullanmaya başlamak için bkz. [bir paket (DotNet CLI) yüklemek ve kullanmak](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) ve [bir paketi yüklemek ve kullanmak (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). NuGet paketleri oluşturmaya başlamak için bkz. [BIR ağ standart paketi (DotNet CLI) oluşturma ve yayımlama](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ve [bir ağ standart paketi oluşturma ve yayımlama (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | İndirme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefleyen her bir [SDK stili proje](resources/check-project-format.md) . .NET Core SDK eklenmiştir ve tüm platformlarda çekirdek NuGet özellikleri sağlar. (Visual Studio 2017 ' den itibaren, DotNet CLı, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir.)| [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | .NET Framework kitaplıkları ve .NET Standard kitaplıklarını hedefleyen biri gibi [SDK olmayan](resources/check-project-format.md) herhangi bir proje için CLI aracı. Tüm NuGet yeteneklerini Windows üzerinde sağlar. Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows 'da, **NuGet Paket Yöneticisi** Visual Studio 2012 ve üzeri sürümlerde bulunur. Visual Studio, çoğu NuGet işlemini çalıştırabileceğiniz [Paket Yöneticisi Kullanıcı arabirimi](consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolu](consume-packages/install-use-packages-powershell.md)sağlar. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Mac için Visual Studio](/visualstudio/mac/nuget-walkthrough) | Mac 'te, belirli NuGet özellikleri doğrudan yerleşik olarak bulunur. Paket Yöneticisi konsolu Şu anda kullanılamıyor. Diğer yetenekler için `dotnet.exe` veya `nuget.exe` CLI araçlarını kullanın.  | [Mac için Visual Studio](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | Windows, Mac veya Linux 'ta NuGet özellikleri Market uzantıları aracılığıyla kullanılabilir veya `dotnet.exe` ya da `nuget.exe` CLI araçlarını kullanır. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[MSBUILD CLI](reference/msbuild-targets.md) , temel olarak yapı sunucularında yararlı olan paketleri geri yükleme ve oluşturma özelliği de sağlar. MSBuild, NuGet ile çalışmak için genel amaçlı bir araç değildir.

Paket Yöneticisi konsol komutları yalnızca Windows üzerinde Visual Studio 'da çalışır ve diğer PowerShell ortamları içinde çalışmaz.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Visual Studio 2017 ve daha yeni bir sürüme yüklensin
Visual Studio 2017 ' den başlayarak, yükleyici, .NET kullanan herhangi bir iş yüküne sahip NuGet Paket Yöneticisi 'Ni içerir. Ayrı olarak yüklemek veya paket yöneticisinin yüklendiğini doğrulamak için, Visual Studio yükleyicisi 'ni çalıştırın ve **tek tek bileşenler altında, NuGet paket yöneticisi > kod araçları >**.

### <a name="install-on-visual-studio-2015-and-older"></a>Visual Studio 2015 ve üzeri sürümlerde yüklensin
Visual Studio 2013 ve 2015 için NuGet uzantıları, adresinden indirilebilir [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

Visual Studio 2010 ve önceki sürümlerde, "Visual Studio için NuGet Paket Yöneticisi" uzantısını yükler. Uzantıyı arama sonuçlarının ilk sayfasında göremiyorsanız, sıralama ölçütü açılır listesini "en fazla Indirilen" veya alfabetik bir sıralama olarak değiştirmeyi deneyin.

## <a name="cli-tools"></a>CLı araçları
`dotnet` `nuget.exe` IDE 'de NuGet özelliklerini desteklemek için CLI veya CLI kullanabilirsiniz. `dotnet`CLI, .NET Core gibi bazı Visual Studio iş yükleri ile yüklenir. `nuget.exe`CLI, daha önce açıklandığı gibi ayrı olarak yüklenmelidir.

İki NuGet CLı aracı `dotnet.exe` ve ' dir `nuget.exe` . Karşılaştırma için [özellik kullanılabilirliğine](#feature-availability) bakın.

* .NET Core veya .NET Standard hedeflemek için DotNet CLı kullanın. SDK `dotnet` [ÖZNITELIĞINI](/dotnet/core/tools/csproj#additions)kullanan SDK stili proje biçimi için CLI gereklidir.
* .NET Framework (yalnızca SDK olmayan proje) hedeflemek için `nuget.exe` CLI kullanın. Proje öğesinden `packages.config` PackageReference öğesine geçirilirse DotNet CLI kullanın.

### <a name="dotnetexe-cli"></a>dotnet.exe CLı

.NET Core 2,0 CLı, `dotnet.exe` tüm platformlarda (Windows, Mac ve Linux) çalışarak paketleri yükleme, geri yükleme ve yayımlama gibi temel NuGet özellikleri sağlar. `dotnet` Çoğu senaryoda yararlı olan .NET Core proje dosyaları (gibi) ile doğrudan tümleştirme sağlar `.csproj` . `dotnet` , her platform için doğrudan de oluşturulmuştur ve mono yüklemenizi gerektirmez.

Yükleme:

- Geliştirici bilgisayarlarında [.NET Core SDK](https://aka.ms/dotnetcoregs)' yi yükler. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.
- Yapı sunucuları için [sürekli tümleştirmede .NET Core SDK ve araçları kullanma](/dotnet/core/tools/using-ci-with-cli)yönergelerini izleyin.

DotNet CLı ile temel komutları kullanmayı öğrenmek için bkz. [DotNet CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe`CLI, `nuget.exe` Tüm NuGet yeteneklerini sağlayan Windows için komut satırı yardımcı programıdır; Ayrıca, bazı sınırlamalar ile [mono](https://www.mono-project.com/docs/getting-started/install/) kullanarak Mac OSX ve Linux 'ta de çalıştırılabilir.

CLI ile temel komutları kullanmayı öğrenmek için `nuget.exe` bkz. [nuget.exe CLI kullanarak paketleri yüklemek ve kullanmak](consume-packages/install-use-packages-nuget-cli.md).

Yükleme:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> `nuget update -self`Mevcut bir nuget.exe en son sürüme güncelleştirmek Için Windows üzerinde kullanın.

> [!Note]
> En son önerilen NuGet CLı, ' de her zaman kullanılabilir `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` . Önceki bir URL olan eski bir sürekli tümleştirme sistemiyle uyumluluk amaçları için `https://nuget.org/nuget.exe` Şu anda [kullanım DıŞı 2.8.6 CLI aracını](https://github.com/NuGet/NuGetGallery/issues/5381)sağlamaktadır.

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Öne çıkan özelliği | dotnet CLI | NuGet CLı (Windows) | NuGet CLı (mono) | Visual Studio (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Paketleri ara |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004; | &#10004; (1) | &#10004; | &#10004; | &#10004; |
| Güncelleştirme paketleri | &#10004; | &#10004; | | &#10004; | &#10004; |
| Paketleri geri yükleme | &#10004; | &#10004; | &#10004; (2) | &#10004; | &#10004; |
| Paket akışlarını yönetme (kaynaklar) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Bir akıştaki paketleri yönetme | &#10004; | &#10004; | &#10004; | | |
| Akışlar için API anahtarlarını ayarlama | | &#10004; | &#10004; | | |
| Paket oluşturma (3) | &#10004; | &#10004; | &#10004; (4) | &#10004; | |
| Paketleri yayımlama | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Paketleri Çoğalt |  | &#10004; | &#10004; | | |
| *Genel paket* ve önbellek klasörlerini yönetme | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmasını Yönet | | &#10004; | &#10004; | | |

(1) proje dosyalarını etkilemez; `dotnet.exe` bunun yerine kullanın.

(2) yalnızca dosya ile birlikte çalışarak `packages.config` Çözüm ( `.sln` ) dosyaları ile değil.

(3) CLı aracılığıyla yalnızca Visual Studio Kullanıcı arabirimi araçlarında temsil edilmeyen çeşitli gelişmiş paket özellikleri vardır.

(4) dosyalarla birlikte çalışarak, `.nuspec` proje dosyaları ile değil.

## <a name="upcoming-features"></a>Yaklaşan Özellikler
Yaklaşan NuGet özelliklerini önizlemek istiyorsanız, Visual Studio 'nun kararlı sürümleriyle yan yana çalışan bir [Visual Studio önizlemesi](https://www.visualstudio.com/vs/preview/)yüklersiniz. Sorunları bildirmek veya önizlemelerde fikir paylaşmak için [NuGet GitHub deposunda](https://github.com/Nuget/Home/issues)bir sorun açın.

### <a name="related-topics"></a>İlgili konular

- [Visual Studio kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell kullanarak paket yükleyip yönetme](consume-packages/install-use-packages-powershell.md)
- [DotNet CLı kullanarak paketleri yükleyip yönetme](consume-packages/install-use-packages-dotnet-cli.md)
- [nuget.exe CLı kullanarak paket yükleyip yönetme](consume-packages/install-use-packages-nuget-cli.md)
- [Paket Yöneticisi konsolu PowerShell Başvurusu](reference/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Paket yayımlama](nuget-org/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler, NuGet paketlerini görsel olarak keşfetmeye, oluşturmaya ve düzenlemeye yönelik açık kaynaklı, tek başına bir araç olan [NuGet paket Gezginini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)de keşfedebilir. Örneğin, paketi yeniden oluşturmadan bir paket yapısında deneysel değişiklikler yapmak çok faydalı olur.
