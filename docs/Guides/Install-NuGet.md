---
title: "NuGet istemci Araçları'nı yükleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "İstemci araçlarında, komut satırı arabirimi (CLI) ve Paket Yöneticisi Visual Studio için Yükleme Kılavuzu."
keywords: "nuget.exe CLI, NuGet istemcisi araçları, NuGet Paket Yöneticisi, NuGet Paket Yöneticisi konsolu, NuGet Visual Studio, NuGet beta kanal"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>NuGet istemci araçlarını yükleme

> [!Tip]
> **Bir paketi yüklemek istiyorsunuz? Bkz: [hızlı başlangıç - kullanım bir paketi](../Quickstart/Use-a-Package.md).**

Yapı, yayımlama ve NuGet paketleri kullanmasına yardımcı olmak için kullanılabilen iki birincil araçlar vardır:

1. [ **NuGet CLI** ](#nuget-cli) komut satırı yardımcı programıdır Windows için tüm NuGet yetenekleri sağlayan; Mac OSX ve Linux Mono kullanarak veya .NET Core CLI aracılığıyla da çalıştırılabilir (`dotnet`).
1. [ **Visual Studio'da NuGet Paket Yöneticisi** ](#nuget-package-manager-in-visual-studio) (yalnızca Windows) yönetme ve paketleri doğrudan Visual içinde belirli NuGet komutlarını üzerinden kullanabileceğiniz bir PowerShell konsolunda içeren bir GUI araçtır Studio. Paket Yöneticisi kullanıcı Arabirimi ve konsol Visual Studio ile (Windows) 2012 ve üzeri dahil ve önceki sürümleri için el ile yüklenebilir.

    Mac için Visual Studio ile doğrudan NuGet özellikleri yerleşiktir. Bkz: [dahil olmak üzere bir NuGet paketini projenize](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) kılavuz.

    Visual Studio Code günümüzde hiçbir yerleşik NuGet destek yok. NuGet CLI kullanın veya [dotnet CLI](../Tools/dotnet-Commands.md).

NuGet CLI ve Paket Yöneticisi aşağıdaki işlemleri destekler:

- Arama paketleri
- Paket yüklemek için
- Güncelleştirme paketleri
- Paketlerini kaldırma
- Geri yükleme paketleri (yalnızca Paket Yöneticisi'nde kullanıcı Arabirimi)
- NuGet kaynaklarını yönet

Aşağıdaki özellikleri yalnızca NuGet CLI içinde desteklenir:

- (Nuget.org veya özel akış) paketlerini yönetme
- Paketleri oluşturma 
- Paketleri yayımlama
- Nuget.Config yönetme
- NuGet önbelleği yönetme
- Bir paket çoğaltma

> [!Note]
> Başka bir iyi araçtır [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), görsel olarak araştırmak, oluşturmak ve NuGet paketleri düzenlemek için açık kaynaklı, tek başına bir araç. Örneğin, paket her zaman yeniden oluşturmak zorunda kalmadan bir paket yapısı Deneysel değişiklik yapmak için çok yararlı olur.
> Platformlar arası [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) .NET Core uygulamaları geliştirmek için kullanılan araç zinciri, silebilir, yerel öğeler, gönderme, paketi ve geri yükleme gibi birkaç NuGet komutlarını destekler. 

## <a name="nuget-cli"></a>NuGet CLI

NuGet komut satırı arabirimi NuGet olanaklarına erişim sağlar ve Windows, Mac OSX ve aşağıdaki bölümlerde açıklandığı gibi Linux üzerinde çalıştırılabilir.

### <a name="windows"></a>Windows

**Doğrudan indirme:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> NuGet ile 1.4 +, kullandığınız `nuget update -self` varolan nuget.exe en son sürüme güncelleştirmek için.

**Diğer yöntemleri:**

- **Chocolatey**: yükleme [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey paketini kullanarak [Chocolatey](http://chocolatey.org) istemci. 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: yükleme [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) Visual Studio'da Paket Yöneticisi Konsolu'ndan paket.

    > [!Note]
    > **NuGet 2.x kullanıcılar için**: NuGet 3.2 sürümünde sunulan değişiklikler nedeniyle [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) noktaları en son kararlı sürekli tümleştirme sistemleri olası önlemek için NuGet 2.x sürüm kesiliyor.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX ve Linux

Mac OSX ve Linux üzerinde NuGet CLI çalıştırmak için iki yol vardır:

- Yükleme [.NET Core SDK](https://www.microsoft.com/net/download/core), çekirdek NuGet özellikler içerir. Yüklemeleri de listelenir [github.com/dotnet/cli](https://github.com/dotnet/cli). Daha eksiksiz özelliklerine ihtiyacınız varsa, ardından aşağıdaki ikinci seçeneği kullanmak için kullanmak `nuget.exe` Mono ile.

- Yükleme [Mono](http://www.mono-project.com/docs/getting-started/install/) ve sonra da `nuget.exe` (sürüm 3.2 ve üstü) Windows'dan komut satırı yürütülebilir dosyası [nuget.org/downloads](https://nuget.org/downloads). NuGet üzerinde Mono aşağıdaki sınırlamalara tabi çalışıyor:

    - Komutları çalışmaya test edilmiştir:
        - Yapılandırma
        - Sil
        - Yardım
        - Yükleme
        - liste
        - Anında iletme
        - setApiKey
        - Kaynakları
        - belirtimi

    - Kısmen çalışan komutlar:
        - paketi: ile çalışır `.nuspec` dosyaları proje dosyalarını birlikte değil.
        - geri yükleme: ile çalışır `packages.config` ve `project.json` dosyaları bilgisayardı çözüm (`.sln`) dosyaları.

    - İşe yaramazsa komutlar:
        - Güncelleştirme

### <a name="related-topics"></a>İlgili konular

- [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)
- [Paket oluşturma](../create-packages/creating-a-package.md)
- [Bir paketi yayımlama](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Visual Studio'da NuGet Paket Yöneticisi

NuGet Paket Yöneticisi Visual Studio 2012 ve sonraki Windows her sürümü dahil edilir. Paket Yöneticisi kullanıcı Arabirimi içerir ([başvuru](../tools/package-manager-ui.md)) ve Paket Yöneticisi konsolu üzerinden erişebilirsiniz belirli paketlerle gelen araçlar ([başvuru](../tools/package-manager-console.md)).

Visual Studio 2017 yükleyici .NET kullanan herhangi bir iş yükü ile NuGet Paket Yöneticisi'ni içerir. Ayrı olarak yüklemeniz ya da Paket Yöneticisi'nin yüklü olduğunu doğrulamak için Visual Studio 2017 yükleyiciyi çalıştırın ve altında seçeneğini **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi**.

> [!Note]
> Konsol gerektirir [PowerShell 2.0](http://support.microsoft.com/kb/968929), zaten olacak Windows 7 veya üstü ve Windows Server 2008 R2 üzerinde yüklü ya da daha yüksek.
>
> Paket Yöneticisi konsolu komutlar, yalnızca Visual Studio içinde Windows üzerinde de çalışır. Mac ve Visual Studio Code için Visual Studio ile de dahil olmak üzere bu ortam dışında NuGet CLI kullanın.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Paket Yöneticisi'ni yükleme ve önceki sürümler için Visual Studio 2010

*Bu adımları zaten Paket Yöneticisi içeren Visual Studio 2012 için gerekli ve daha sonra değildir.*

1. Visual Studio 2010 ve daha önce'ı **Araçlar > uzantısı ve güncelleştirmeleri**.
1. Gidin **çevrimiçi**, NuGet Paket Yöneticisi için Visual Studio için"" araması yapın ve tıklayın **karşıdan**.
1. Yükleyici iletişim kutusunda tıklatın **yükleme**.
1. Yükleme tamamlandığında, Visual Studio'yu yeniden başlatın.

> [!Tip]
> Kullanılacak yapamıyorsanız **Uzantılar ve güncelleştirmeler** iletişim (örneğin, bir proxy tarafından kendi engellenen) Visual Studio, Visual Studio 2013 ve doğrudan 2015 için uzantıları yükleyebilirsiniz [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Paket Yöneticisi güncelleştiriliyor

Visual Studio 2015 güncelleştirme 2 ve daha sonra Paket Yöneticisi otomatik olarak en son kararlı sürümüne güncelleştirilir.

Seçin ve önceki sürümleri, Visual Studio 2015 güncelleştirme 1 için **Araçlar > Uzantılar ve güncelleştirmeler** komut ve tıklayın **güncelleştirmeleri** Paket Yöneticisi'nin yeni bir sürümü kullanılabilir olup olmadığını görmek için sekmesini.  

### <a name="nuget-previews"></a>NuGet önizlemeleri

Yaklaşan NuGet özellikleri Önizleme istiyorsanız, yükleme [Visual Studio 2017 Önizleme](https://www.visualstudio.com/vs/preview/), Visual Studio, kararlı sürümleriyle-yana çalışır.

Önceki NuGet Beta kanal Not (`https://dotnet.myget.org/F/nuget-beta/vsix/`) Visual Studio 2015 artık kullanılır.

NuGet herhangi bir sürümünden sorunları rapor veya fikirleri paylaşmak için bir sorun açmak için [NuGet GitHub deposunu](https://github.com/Nuget/Home).

### <a name="related-topics"></a>İlgili konular

- [Paket Yöneticisi kullanıcı Arabirimi başvurusu](../tools/package-manager-ui.md)
- [Paket Yöneticisi konsolu başvurusu](../tools/package-manager-console.md)
- [Paket Yöneticisi konsolu PowerShell başvurusu](../tools/powershell-reference.md)