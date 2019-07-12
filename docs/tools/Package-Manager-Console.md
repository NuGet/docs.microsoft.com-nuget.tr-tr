---
title: Yükleme ve konsolu kullanarak Visual Studio'da NuGet paketlerini Yönet
description: Paketlerle çalışmak için Visual Studio'da NuGet Paket Yöneticisi konsolu kullanarak yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842589"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Yükleme ve paketleri (PowerShell) Visual Studio'da Paket Yöneticisi konsolu ile yönetme

NuGet Paket Yöneticisi konsolu kullanmanıza olanak tanıyan [NuGet PowerShell komutlarını](../tools/powershell-reference.md) bulmak için yükleme, kaldırma ve NuGet paketlerini güncelleştirin. Konsolunu kullanarak, burada Paket Yöneticisi UI bir işlemi gerçekleştirmek için bir yol sağlamaz durumlarda gereklidir. Kullanılacak `nuget.exe` konsolunda, CLI komutları görmek [konsolunda nuget.exe CLI kullanarak](#using-the-nugetexe-cli-in-the-console).

Windows üzerinde Visual Studio konsol yerleşiktir. Mac veya Visual Studio Code için Visual Studio ile dahil değildir.

## <a name="find-and-install-a-package"></a>Bulma ve bir paket yükleme

Örneğin, bulma ve bir paket yükleme üç kolay adımda gerçekleştirilir:

1. Proje/çözüm Visual Studio'da açın ve konsol kullanarak açın **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.

1. Yüklemek istediğiniz paketi bulmak. Bunu zaten biliyorsanız, 3. adımına geçin.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. İnstall komutu çalıştırın:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Konsolunda kullanılabilir tüm işlemleri ile de yapılabilir [NuGet CLI](../tools/nuget-exe-cli-reference.md). Ancak, Konsolu komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle birden çok eşdeğer CLI komutları gerçekleştirin. Örneğin, bir paket Konsolu aracılığıyla yüklenmesi CLI komutunu desteklemez projeye bir başvuru ekler. Bu nedenle, CLI konsola kullanarak Visual Studio'da genellikle çalışan geliştiriciler tercih eder.

> [!Tip]
> Visual Studio'da bilinen yol adı ile açık bir çözüm açık olması birçok konsol işlemlerini bağlıdır. Kaydedilmemiş bir çözüm ya da çözüm varsa, bir hata görebilirsiniz, "Çözüm açık değil veya kaydedilmedi. Lütfen bir açık ve kaydedilen çözümüne sahip olun." Bu konsol Çözüm klasörü belirlenemiyor gösterir. Kaydedilmemiş bir çözüm kaydetme veya oluşturma ve bir çözümü, yoksa, kaydetme açın, hatayı düzeltmeniz gerekir.

## <a name="opening-the-console-and-console-controls"></a>Konsol ve konsol denetimlerini açma

1. Visual Studio kullanarak Uçbirimi **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu. Düzenlenmiş ve istediğiniz gibi konumlandırılmış bir Visual Studio pencere konsoludur (bkz [Visual Studio'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Konsolu komutları, varsayılan olarak, pencerenin üst kısmındaki denetim kümesindeki olarak belirli bir paket kaynağı ve proje karşı çalışır:

    ![Paket kaynağı ve proje için Paket Yöneticisi konsolu denetimleri](media/PackageManagerConsoleControls1.png)

1. Farklı bir paket kaynağı ve/veya proje seçmek için sonraki komutlarda bu Varsayılanları değiştirir. Overrride için varsayılan değerleri değiştirmeden bu ayarlar, komutların çoğu destekler `-Source` ve `-ProjectName` seçenekleri.

1. Paket kaynaklarını yönetmek için dişli simgesini seçin. Bu kısayol, **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını** üzerinde açıklandığı gibi iletişim kutusunu [Paket Yöneticisi UI](package-manager-ui.md#package-sources) sayfası. Ayrıca, denetimin sağ tarafında proje Seçici için konsolun içeriği temizler:

    ![Paket Yöneticisi konsolu ayarları ve denetimleri Temizle](media/PackageManagerConsoleControls2.png)

1. Sağdaki düğme uzun süre çalışan komut kesintiye uğratır. Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` çalıştırmak için birkaç dakika sürebilir varsayılan kaynak (nuget.org gibi), üst 500 paketleri listeler.

    ![Paket Yöneticisi konsolu durdurma denetimi](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Bir paketi yükleniyor

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Bkz: [Install-Package](../tools/ps-ref-install-package.md).

Konsolunda bir paket yükleme aynı adımları gerçekleştirir üzerinde açıklandığı [paketi yüklendiğinde ne](../concepts/package-installation-process.md), aşağıdaki eklemelerle:

- Konsol penceresi örtük anlaşma kapsamında olan geçerli lisans koşullarında görüntüler. Koşulları kabul etmiyorsanız, paket hemen kaldırmanız gerekir.
- Ayrıca, pakete bir başvuru proje dosyasına eklenir ve görünür **Çözüm Gezgini** altında **başvuruları** düğümü, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmek için ihtiyacınız.

## <a name="uninstalling-a-package"></a>Bir paket kaldırılıyor

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Bkz: [kaldırma-Package](../tools/ps-ref-uninstall-package.md). Kullanım [Get-Package](../tools/ps-ref-get-package.md) tanımlayıcı bulmanız gerekiyorsa varsayılan proje şu anda yüklü olan tüm paketleri görmek için.

Bir paketi, aşağıdaki eylemleri gerçekleştirir:

- Paket başvuruları projeye (ve hangi yönetim biçimi kullanılır) kaldırır. Başvuruları artık görünür **Çözüm Gezgini**. (Kaldırıldığında görmek için projeyi yeniden derlemek ihtiyacınız olabilecek **Bin** klasör.)
- Yapılan tüm değişiklikler tersine `app.config` veya `web.config` paketin ne zaman yüklendi.
- Hiçbir kalan paketleri bu bağımlılıkların kullanırsanız bağımlılıkları önceden yüklenmiş kaldırır.

## <a name="updating-a-package"></a>Bir paketi güncelleştiriliyor

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Bkz: [Get-Package](../tools/ps-ref-get-package.md) ve [güncelleştirme paketi](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Bir paketi bulma

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Bkz: [Bul-Package](../tools/ps-ref-find-package.md). Visual Studio 2013 ve önceki sürümleri kullanın [Get-Package](../tools/ps-ref-get-package.md) yerine.

## <a name="availability-of-the-console"></a>Konsolunun kullanılabilirliğini

Tüm seçtiğinizde Visual Studio 2017'den itibaren NuGet ve NuGet Paket Yöneticisi otomatik olarak yüklenir. NET ilgili iş yükleri; Ayrıca ayrı ayrı kontrol ederek yükleyebilirsiniz **tek tek bileşenler > kod Araçlar > NuGet Paket Yöneticisi** seçeneği Visual Studio Yükleyicisi'nde.

Ayrıca, Visual Studio 2015'te ve daha önce NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  ve NuGet paket yöneticisini uzantısı arayın. Visual Studio Uzantıları yükleyici yapamıyorsanız uzantısını doğrudan indirebileceğiniz [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Paket Yöneticisi konsolu, Mac için Visual Studio ile şu anda kullanılabilir değil. Ancak, eşdeğer komutları aracılığıyla [NuGet CLI](nuget-exe-CLI-reference.md). Mac için Visual Studio, NuGet paketlerini yönetmek için bir kullanıcı Arabirimi yok. Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).

Paket Yöneticisi konsolu, Visual Studio Code ile dahil değildir.

## <a name="extending-the-package-manager-console"></a>Paket Yöneticisi konsolu genişletme

Bazı paketler yeni komutlar Konsolu yükleyin. Örneğin, `MvcScaffolding` gibi komutlar oluşturur `Scaffold` aşağıda gösterilen, oluşturduğu ASP.NET MVC denetleyicileri ve görünümleri:

![Yükleme ve MvcScaffold kullanma](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Bir NuGet PowerShell profili ayarlama

Bir PowerShell profili, PowerShell kullandığınız her yerde sık kullanılan komutları kullanılabilir kılmanızı sağlar. NuGet, genellikle şu konumda bulunan bir NuGet özgü profili destekler:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Profil bulmak için yazın `$profile` konsolunda:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Daha fazla ayrıntı için başvurmak [Windows PowerShell profilleri](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Konsolunda nuget.exe CLI kullanma

Yapmak [ `nuget.exe` CLI](nuget-exe-cli-reference.md) Paket Yöneticisi konsolunda kullanılabilir yükleme [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) konsolundan paket:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
