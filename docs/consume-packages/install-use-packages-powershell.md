---
title: Visual Studio 'da Konsolu kullanarak NuGet paketlerini yükleyip yönetme
description: Paketlerle birlikte çalışmak üzere Visual Studio 'da NuGet Paket Yöneticisi konsolunu kullanmaya yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428956"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Visual Studio 'da Paket Yöneticisi konsolu ile paket yükleyip yönetme (PowerShell)

NuGet Paket Yöneticisi konsolu NuGet paketlerini bulmak, yüklemek, kaldırmak ve güncelleştirmek için [NuGet PowerShell komutlarını](../reference/powershell-reference.md) kullanmanıza olanak sağlar. Konsolunu kullanmak, Paket Yöneticisi Kullanıcı arabiriminin bir işlemi gerçekleştirmek için bir yol sağlamayan durumlarda gereklidir. Konsolunda `nuget.exe` CLı komutlarını kullanmak için, bkz. [konsolundaki NuGet. exe CLI kullanma](#use-the-nugetexe-cli-in-the-console).

Konsol, Windows üzerinde Visual Studio 'da yerleşik olarak bulunur. Mac için Visual Studio veya Visual Studio Code dahil değildir.

## <a name="find-and-install-a-package"></a>Paket bulma ve yüklemeyi

Örneğin, bir paketi bulmak ve yüklemek üç kolay adımla yapılır:

1. Visual Studio 'da projeyi/çözümü açın ve **araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** komutunu kullanarak konsolunu açın.

1. Yüklemek istediğiniz paketi bulun. Bunu zaten biliyorsanız adım 3 ' e atlayın.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Install komutunu çalıştırın:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Konsolda bulunan tüm işlemler [NUGET CLI](../reference/nuget-exe-cli-reference.md)ile de yapılabilir. Ancak konsol komutları, Visual Studio bağlamı ve kaydedilen bir proje/çözüm içinde çalışır ve genellikle eşdeğer CLı komutlarından daha fazlasını yapar. Örneğin, konsolu aracılığıyla bir paket yüklemek, CLı komutu olmadığı halde projeye bir başvuru ekler. Bu nedenle, Visual Studio 'da çalışan geliştiriciler genellikle konsolu CLı için kullanmayı tercih eder.

> [!Tip]
> Birçok konsol işlemi, Visual Studio 'da bilinen bir yol adı ile bir çözüme açık olmasına bağlıdır. Kaydedilmemiş bir çözümünüz varsa veya çözüm yoksa, "çözüm açılmadı veya kaydedilmedi" hatasını görebilirsiniz. Lütfen açık ve kaydedilmiş bir çözümünüz olduğundan emin olun. " Bu, konsolunun çözüm klasörünü belirleyemediğini belirtir. Kaydedilmemiş bir çözümü kaydetme veya bir açık hesabınız yoksa bir çözüm oluşturup kaydetme, hatayı düzeltmeniz gerekir.

## <a name="opening-the-console-and-console-controls"></a>Konsol ve konsol denetimlerini açma

1. **Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** komutunu kullanarak Visual Studio 'da konsolunu açın. Konsol, istediğiniz şekilde düzenlenebileceği ve konumlandırılmış bir Visual Studio penceresidir (bkz. [Visual Studio 'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Varsayılan olarak, konsol komutları pencerenin üst kısmındaki denetimde ayarlandığı şekilde belirli bir paket kaynağına ve projeye karşı çalışır:

    ![Paket kaynağı ve proje için Paket Yöneticisi konsol denetimleri](media/PackageManagerConsoleControls1.png)

1. Farklı bir paket kaynağı ve/veya proje seçildiğinde, Bu varsayılanlar sonraki komutlara göre değişir. Varsayılanları değiştirmeden bu ayarları fazla devre dışı bırakmak için çoğu komut `-Source` ve `-ProjectName` seçeneklerini destekler.

1. Paket kaynaklarını yönetmek için dişli simgesini seçin. Bu, [Paket Yöneticisi Kullanıcı arabirimi](install-use-packages-visual-studio.md#package-sources) sayfasında açıklandığı şekilde, **> araçlar > NuGet Paket Yöneticisi > paket kaynakları** iletişim kutusunun bir kısayoludur. Ayrıca, proje seçicisinin sağında bulunan denetim konsolun içeriğini de temizler:

    ![Paket Yöneticisi konsol ayarları ve Temizleme denetimleri](media/PackageManagerConsoleControls2.png)

1. En sağdaki düğme uzun süre çalışan bir komutu keser. Örneğin `Get-Package -ListAvailable -PageSize 500` çalıştırmak, varsayılan kaynakta (örneğin, nuget.org) ilk 500 paketi listeler ve bu da çalışması birkaç dakika sürebilir.

    ![Paket Yöneticisi konsolu denetimi durdur](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Paket yükler

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

Konsola bir paket yüklemek, [bir paket yüklendiğinde ne olacağı](../concepts/package-installation-process.md)ile ilgili adımların aynısını aşağıdaki eklemelerle gerçekleştirir:

- Konsol, ilgili lisans koşullarını örtülü anlaşmayla penceresinde görüntüler. Koşulları kabul etmiyorsanız, paketi hemen kaldırmanız gerekir.
- Ayrıca, proje dosyasına pakete bir başvuru eklenir ve **Başvurular** düğümü altında **Çözüm Gezgini** görünür, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmeniz gerekir.

## <a name="uninstall-a-package"></a>Bir paketi kaldırma

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Bkz. [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Bir tanımlayıcı bulmanız gerekiyorsa varsayılan projede yüklü olan tüm paketleri görmek için [Get-Package](../reference/ps-reference/ps-ref-get-package.md) ' i kullanın.

Bir paketin kaldırılması aşağıdaki eylemleri gerçekleştirir:

- Projedeki paketin başvurularını kaldırır (ve hangi yönetim biçiminin kullanımda olduğunu). Başvurular artık **Çözüm Gezgini**görünmüyor. ( **Bin** klasöründen kaldırıldığını görmek için projeyi yeniden oluşturmanız gerekebilir.)
- Paket yüklendiğinde `app.config` veya `web.config` yapılan tüm değişiklikleri tersine çevirir.
- Kalan hiçbir paket bu bağımlılıkları kullanıyorsa, önceden yüklenmiş bağımlılıkları kaldırır.

## <a name="update-a-package"></a>Bir paketi güncelleştirme

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

Bkz. [Get-Package](../reference/ps-reference/ps-ref-get-package.md) ve [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Bir paket bulun

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

Bkz. [bul-Package](../reference/ps-reference/ps-ref-find-package.md). Visual Studio 2013 ve önceki sürümlerde, [Get-Package](../reference/ps-reference/ps-ref-get-package.md) kullanın.

## <a name="availability-of-the-console"></a>Konsolun kullanılabilirliği

Visual Studio 2017 ' den başlayarak, herhangi birini seçtiğinizde NuGet ve NuGet Paket Yöneticisi otomatik olarak yüklenir. NET ilgili iş yükleri; Visual Studio yükleyicisindeki **tek tek bileşenler > Code araçları > NuGet Paket Yöneticisi** seçeneğini tek tek denetleyerek de yükleyebilirsiniz.

Ayrıca, Visual Studio 2015 ve önceki sürümlerde NuGet Paket Yöneticisi eksik ise **araçlar > Uzantılar ve güncelleştirmeler...** ' ı Işaretleyin ve NuGet Paket Yöneticisi uzantısını arayın. Visual Studio 'da uzantılar yükleyicisini kullandıysanız, uzantıyı doğrudan [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)yükleyebilirsiniz.

Paket Yöneticisi konsolu Mac için Visual Studio şu anda kullanılamıyor. Ancak eşdeğer komutlar [NUGET CLI](../reference/nuget-exe-CLI-reference.md)aracılığıyla kullanılabilir. Mac için Visual Studio NuGet paketlerini yönetmek için bir kullanıcı arabirimine sahiptir. Bkz. [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough).

Paket Yöneticisi konsolu Visual Studio Code dahil değildir.

## <a name="extend-the-package-manager-console"></a>Paket Yöneticisi konsolunu genişletme

Bazı paketler konsol için yeni komutlar yükler. Örneğin, `MvcScaffolding` aşağıda gösterilen `Scaffold` gibi komutları oluşturur ve bu, ASP.NET MVC denetleyicileri ve görünümleri oluşturur:

![MvcScaffold yükleme ve kullanma](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>NuGet PowerShell profili ayarlama

PowerShell profili, PowerShell kullandığınızda yaygın olarak kullanılan komutların kullanılabilmesini sağlar. NuGet, genellikle aşağıdaki konumda bulunan NuGet 'e özgü bir profili destekler:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Profili bulmak için konsola `$profile` yazın:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Daha fazla ayrıntı için [Windows PowerShell profillerine](https://technet.microsoft.com/library/bb613488.aspx)bakın.

## <a name="use-the-nugetexe-cli-in-the-console"></a>Konsolda NuGet. exe CLı 'yı kullanma

[`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) 'Yı Paket Yöneticisi konsolunda kullanılabilir hale getirmek için, konsolundan [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) paketini yüklemek için:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
