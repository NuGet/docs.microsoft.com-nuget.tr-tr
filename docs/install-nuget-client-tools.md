---
title: NuGet istemci araçlarını yükleme
description: İstemci araçları, dotnet ve nuget komut satırı arabirimleri (CLI) ve Visual Studio için Paket Yöneticisi yükleme kılavuzu.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 2769f0ef0373b26eedb4bac6242fee0e814310c5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428823"
---
# <a name="install-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> **Bir paket yüklemek mi arıyorsunuz? NuGet [paketlerini yüklemenin yollarını](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)görün.**

NuGet ile çalışmak için, bir paket tüketicisi veya oluşturucu olarak, Visual Studio'da komut satırı arabirimi (CLI) araçlarının yanı sıra NuGet özelliklerini de kullanabilirsiniz. Bu makalede, farklı araçların yetenekleri, bunların nasıl yüklenir ve karşılaştırmalı [özellik kullanılabilirliği](#feature-availability)kısaca özetlenir. Paketleri tüketmek için NuGet'i kullanmaya başlamak için bir [paketi yükle ve kullanma (dotnet CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) ve paketi [(Visual Studio) yükleyin ve kullanın.](quickstart/install-and-use-a-package-in-visual-studio.md) NuGet paketleri oluşturmaya başlamak için, [bir NET Standart paketi oluştur ve yayımla (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) ve net standart paketi [(Visual Studio) oluştur ve yayımla.](quickstart/create-and-publish-a-package-using-visual-studio.md)

| Aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Açıklama | Indir&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core ve .NET Standart kitaplıkları için cli aracı ve .NET Framework'u hedefleyen herhangi bir [SDK tarzı proje](resources/check-project-format.md) için. .NET Core SDK ile birlikte tüm platformlarda çekirdek NuGet özellikleri sağlar. (Visual Studio 2017'den itibaren dotnet CLI ,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.)| [.NET Çekirdek SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | .NET Framework kitaplıkları ve .NET Standart kitaplıklarını hedefleyen bir proje gibi [SDK tarzı olmayan](resources/check-project-format.md) projeler için CLI aracı. Windows'daki tüm NuGet özelliklerini sağlar, Mono altında çalışırken Mac ve Linux'ta en çok özellik sağlar. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows'da, **NuGet Package Manager** Visual Studio 2012 ve sonraki yerleriyle birlikte verilir. Visual Studio, çoğu NuGet operasyonunu çalıştırabileceğiniz [Paket Yöneticisi Kullanıcı UI](consume-packages/install-use-packages-visual-studio.md) ve Package Manager [Konsolu](consume-packages/install-use-packages-powershell.md)sağlar. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Mac için Visual Studio](/visualstudio/mac/nuget-walkthrough) | Mac'te, belirli NuGet özellikleri doğrudan yerleşiktir. Paket Yöneticisi Konsolu şu anda kullanılamıyor. Diğer özellikler için `dotnet.exe` cli `nuget.exe` araçlarını kullanın.  | [Mac için Visual Studio](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | Windows, Mac veya Linux'ta, NuGet yetenekleri pazar uzantıları aracılığıyla `dotnet.exe` `nuget.exe` kullanılabilir veya veya cli araçlarını kullanabilir. | [Visual Studio Code](https://code.visualstudio.com/Download/)|

[MSBuild CLI](reference/msbuild-targets.md) ayrıca, öncelikle yapı sunucularında kullanışlı olan paketleri geri yükleme ve oluşturma olanağı da sağlar. MSBuild, NuGet ile çalışmak için genel amaçlı bir araç değildir.

Package Manager Console komutları yalnızca Windows'daki Visual Studio'da çalışır ve diğer PowerShell ortamlarında çalışmaz.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Visual Studio 2017 ve daha yeni yükleyin
Visual Studio 2017'den itibaren yükleyici, .NET'i kullanan her türlü iş yüküne sahip NuGet Paket Yöneticisi'ni içerir. Ayrı olarak yüklemek veya Paket Yöneticisi'nin yüklü olduğunu doğrulamak için Visual Studio yükleyicisini çalıştırın ve **NuGet paket yöneticisi > Bireysel Bileşenler > Kodu araçları**altında seçeneği kontrol edin.

### <a name="install-on-visual-studio-2015-and-older"></a>Visual Studio 2015 ve daha büyük yükleme
Visual Studio 2013 ve 2015 için NuGet [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Uzantıları indirebilirsiniz .

Visual Studio 2010 ve daha önce için "Visual Studio için NuGet Paket Yöneticisi" uzantısını yükleyin. Unutmayın, uzantıyı arama sonuçlarının ilk sayfasında göremiyorsanız, "En Çok İndirilenler" veya alfabetik sıralamayla Sırala'yı değiştirmeyi deneyin.

## <a name="cli-tools"></a>CLI araçları
IDE'deki `dotnet` NuGet özelliklerini `nuget.exe` desteklemek için CLI veya CLI'yi kullanabilirsiniz. `dotnet` CLI, .NET Core gibi bazı Visual Studio iş yükleriyle yüklenir. `nuget.exe` CLI daha önce açıklandığı gibi ayrı olarak yüklenmelidir.

İki NuGet CLI `dotnet.exe` araçları `nuget.exe`ve . Karşılaştırma için [özellik kullanılabilirliğine](#feature-availability) bakın.

* .NET Core veya .NET Standard'ı hedeflemek için dotnet CLI'yi kullanın. `dotnet` CLI, [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanan SDK stili proje biçimi için gereklidir.
* .NET Framework'ü (yalnızca SDK tarzı olmayan `nuget.exe` proje) hedeflemek için CLI'yi kullanın. Proje PackageReference'a `packages.config` geçirilirse, dotnet CLI'yi kullanın.

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI, `dotnet.exe`tüm platformlarda (Windows, Mac ve Linux) çalışır ve paketleri yükleme, geri yükleme ve yayımlama gibi temel NuGet özellikleri sağlar. `dotnet`çoğu senaryoda yararlı olan .NET `.csproj`Core proje dosyalarıyla (örneğin) doğrudan tümleştirme sağlar. `dotnet`ayrıca doğrudan her platform için üretilmiştir ve Mono'ya yüklemenizi gerektirmez.

Yükleme:

- Geliştirici bilgisayarlarda [.NET Core SDK'yı](https://aka.ms/dotnetcoregs)yükleyin. Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.
- Yapı sunucuları için [,NET Core SDK'yı kullanma yönergelerini ve Sürekli Tümleştirme'deki araçları](/dotnet/core/tools/using-ci-with-cli)izleyin.

Nokta cli ile temel komutları nasıl kullanacağınızı öğrenmek için, [dotnet CLI'yi kullanarak paketleri yükle'ye](consume-packages/install-use-packages-dotnet-cli.md)bakın ve kullanın.

### <a name="nugetexe-cli"></a>nuget.exe CLI

`nuget.exe` CLI, `nuget.exe`Tüm NuGet yeteneklerini sağlayan Windows için komut satırı yardımcı programıdır; ayrıca Bazı sınırlamalar ile [Mono](https://www.mono-project.com/docs/getting-started/install/) kullanarak Mac OSX ve Linux çalıştırılabilir.

CLI ile temel komutları nasıl kullanacağınızı öğrenmek için [nuget.exe CLI'yi kullanarak paketleri yükle ve kullanma](consume-packages/install-use-packages-nuget-cli.md)'ya bakın. `nuget.exe`

Yükleme:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Varolan bir nuget.exe'yi en son sürüme güncellemek için Windows'da kullanın. `nuget update -self`

> [!Note]
> En son önerilen NuGet CLI `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`her zaman mevcuttur. Eski sürekli tümleştirme sistemleri, önceki bir `https://nuget.org/nuget.exe` URL ile uyumluluk amacıyla, şu anda [amortismana 2.8.6 CLI aracı](https://github.com/NuGet/NuGetGallery/issues/5381)sağlar.

## <a name="feature-availability"></a>Özellik kullanılabilirliği

| Özellik | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Görsel Stüdyo (Windows) | Mac için Visual Studio |
| --- | --- | --- | --- | --- | --- |
| Arama paketleri |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri yükleme/kaldırma | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Paketleri güncelleştirin | &#10004; | &#10004; | | &#10004; | &#10004; |
| Paketleri geri yükleme | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Paket akışlarını (kaynakları) yönetme | | &#10004; | &#10004; | &#10004; | &#10004; |
| Paketleri akışta yönetme | &#10004; | &#10004; | &#10004; | | |
| Özet akışları için API anahtarlarını ayarlama | | &#10004; | &#10004; | | |
| Paket oluşturma(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Paketleri yayımlama | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Paketleri çoğaltma |  | &#10004; | &#10004; | | |
| *Genel paket* ve önbellek klasörlerini yönetme | &#10004; | &#10004; | &#10004; | | |
| NuGet yapılandırmalarını yönetin | | &#10004; | &#10004; | | |

(1) Proje dosyalarını etkilemez; bunun `dotnet.exe` yerine kullanın.

(2) Çözüm `packages.config` (`.sln`) dosyaları ile değil, yalnızca dosya ile çalışır.

(3) Çeşitli gelişmiş paket özellikleri, Yalnızca Visual Studio UI araçlarında temsil edilmeyen CLI aracılığıyla kullanılabilir.

(4) Dosyalarla çalışır, ancak proje dosyalarıyla `.nuspec` çalışmaz.

## <a name="upcoming-features"></a>Gelecek Özellikler
Yaklaşan NuGet özelliklerini önizlemek istiyorsanız, Visual [Studio'nun](https://www.visualstudio.com/vs/preview/)kararlı sürümleriyle yan yana çalışan bir Visual Studio Preview yükleyin. Sorunları bildirmek veya önizlemeler için fikir paylaşmak için [NuGet GitHub deposunda](https://github.com/Nuget/Home/issues)bir sorun açın.

### <a name="related-topics"></a>İlgili konular

- [Visual Studio'u kullanarak paketleri yükleyin ve yönetin](consume-packages/install-use-packages-visual-studio.md)
- [PowerShell kullanarak paketleri yükleme ve yönetme](consume-packages/install-use-packages-powershell.md)
- [Dotnet CLI kullanarak paketleri yükleme ve yönetme](consume-packages/install-use-packages-dotnet-cli.md)
- [nuget.exe CLI kullanarak paketleri yükleyin ve yönetin](consume-packages/install-use-packages-nuget-cli.md)
- [Paket Yöneticisi Konsol PowerShell referans](reference/powershell-reference.md)
- [Paket oluşturma](create-packages/creating-a-package.md)
- [Paket Yayınlama](nuget-org/publish-a-package.md)

Windows üzerinde çalışan geliştiriciler, NuGet paketlerini görsel olarak keşfetmek, oluşturmak ve düzenlemek için açık kaynak kodlu, tek başına bir araç olan [NuGet Paket](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)Gezgini'ni de keşfedebilir. Örneğin, paketi yeniden oluşturmadan bir paket yapısında deneysel değişiklikler yapmak çok yararlıdır.
