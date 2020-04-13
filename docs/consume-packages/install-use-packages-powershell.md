---
title: Visual Studio'daki konsolu kullanarak NuGet paketlerini yükleyin ve yönetin
description: Paketlerle çalışmak için Visual Studio'da NuGet Paket Yöneticisi Konsolu'nu kullanma talimatları.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428956"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Visual Studio'daki Paket Yöneticisi Konsolu (PowerShell) ile paketleri yükleyin ve yönetin

NuGet Package Manager Console, NuGet paketlerini bulmak, yüklemek, kaldırmak ve güncellemek için [NuGet PowerShell komutlarını](../reference/powershell-reference.md) kullanmanıza olanak tanır. Paket Yöneticisi UI'nin bir işlemi gerçekleştirmek için bir yol sağlamadığı durumlarda konsolu kullanmak gereklidir. Konsolda `nuget.exe` CLI komutlarını kullanmak için [konsoldaki nuget.exe CLI'yi kullanma'ya](#use-the-nugetexe-cli-in-the-console)bakın.

Konsol, Windows'ta Visual Studio'da yerleşiktir. Mac veya Visual Studio Code için Visual Studio ile birlikte değildir.

## <a name="find-and-install-a-package"></a>Bir paket bulma ve yükleme

Örneğin, bir paketi bulma ve yükleme üç kolay adımla yapılır:

1. Visual Studio'da projeyi/çözümü açın ve **NuGet Paket Yöneticisi > Paket Yöneticisi Konsol** komutu > Araçları kullanarak konsolu açın.

1. Yüklemek istediğiniz paketi bulun. Bunu zaten biliyorsanız, adım 3'e atlayın.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Yükleme komutunu çalıştırın:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Konsolda bulunan tüm işlemler [NuGet CLI](../reference/nuget-exe-cli-reference.md)ile de yapılabilir. Ancak konsol komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle eşdeğer CLI komutlarından daha fazlasını gerçekleştirir. Örneğin, konsol üzerinden bir paket yüklemek projeye bir başvuru eklerken, CLI komutu göndermez. Bu nedenle Visual Studio'da çalışan geliştiriciler genellikle konsolu CLI'ye tercih ediyor.

> [!Tip]
> Birçok konsol işlemi, Visual Studio'da bilinen bir yol adı ile açılan bir çözüme bağlıdır. Kaydedilmemiş bir çözümünüz varsa veya çözüm yoksa, "Çözüm açılmaz veya kaydedilmez. Lütfen açık ve kaydedilmiş bir çözüme sahip olduğundan emin olun." Bu, konsolun çözüm klasörünü belirleyemeyeceğini gösterir. Kaydedilmemiş bir çözümü kaydetmek veya açık bir çözümünüz yoksa çözüm oluşturmak ve kaydetmek hatayı düzeltmelidir.

## <a name="opening-the-console-and-console-controls"></a>Konsol ve konsol denetimlerini açma

1. **NuGet Paket Yöneticisi > Paket Yöneticisi Konsol komutu > Araçları** kullanarak Visual Studio'da konsolu açın. Konsol, istediğiniz gibi düzenlenebilecek ve konumlandırılabilen bir Visual Studio penceresidir [(Bkz. Visual Studio'da pencere düzenlerini özelleştir).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)

1. Varsayılan olarak, konsol komutları pencerenin üst kısmındaki denetimde ayarlanan belirli bir paket kaynağına ve projeye karşı çalışır:

    ![Paket kaynağı ve proje için Paket Yöneticisi Konsol denetimleri](media/PackageManagerConsoleControls1.png)

1. Farklı bir paket kaynağı ve/veya proje seçmek sonraki komutlar için bu varsayılanları değiştirir. Varsayılanları değiştirmeden bu ayarları aşırıya kakıştın, çoğu komut desteği `-Source` ve `-ProjectName` seçeneği kullanır.

1. Paket kaynaklarını yönetmek için vites simgesini seçin. Bu, [Paket Yöneticisi UI](install-use-packages-visual-studio.md#package-sources) sayfasında açıklandığı gibi Paket Kaynakları > Paket Kaynakları iletişim kutusunu > Araçlar > **Seçenekleri'ne** bir kısayoldur. Ayrıca, proje seçicinin sağındaki denetim konsolun içeriğini temizler:

    ![Paket Yöneticisi Konsol ayarları ve net denetimler](media/PackageManagerConsoleControls2.png)

1. En sağda olan düğme, uzun süren bir komutu keser. Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` varsayılan kaynak (nuget.org gibi) üzerinde çalıştırmak için birkaç dakika sürebilir en üst 500 paketleri listeler.

    ![Paket Yöneticisi Konsol durdurma kontrolü](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Paket yükleme

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Bkz. [Yükle-Paket](../reference/ps-reference/ps-ref-install-package.md).

Konsola bir paket yüklemek, aşağıdaki eklemelerle [birlikte, bir paket yüklendiğinde ne olduğu](../concepts/package-installation-process.md)konusunda açıklandığı gibi aynı adımları gerçekleştirir:

- Konsol, penceresinde geçerli lisans koşullarını zımni anlaşma yla görüntüler. Şartları kabul etmiyorsanız, paketi derhal kaldırmanız gerekir.
- Ayrıca projeye bir başvuru proje dosyasına eklenir ve **Başvurudüğümün** altında **Çözüm Gezgini'nde** görünür, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmeniz gerekir.

## <a name="uninstall-a-package"></a>Paketi kaldırma

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Bkz. [Kaldır-Paket.](../reference/ps-reference/ps-ref-uninstall-package.md) Bir tanımlayıcı bulmanız gerekiyorsa, varsayılan projede şu anda yüklü olan tüm paketleri görmek için [Get-Package'ı](../reference/ps-reference/ps-ref-get-package.md) kullanın.

Paketi kaldırma aşağıdaki eylemleri gerçekleştirir:

- Pakete yapılan başvuruları projeden kaldırır (ve hangi yönetim biçimi kullanılıyorsa kullanılır). Başvurular artık **Çözüm Gezgini'nde**görünmüyor. (Bin klasöründen kaldırıldığını görmek için **Bin** projeyi yeniden oluşturmanız gerekebilir.)
- Paket yüklendiğinde `app.config` veya `web.config` yüklendiğinde yapılan değişiklikleri tersine çevirir.
- Kalan paketler bu bağımlılıkları kullanmıyorsa, daha önce yüklenmiş bağımlılıkları kaldırır.

## <a name="update-a-package"></a>Paketi güncelleştir

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

[Bkz. Paket Al](../reference/ps-reference/ps-ref-get-package.md) ve [Güncelle-Paket](../reference/ps-reference/ps-ref-update-package.md)

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

Bkz. [Bul Paketi](../reference/ps-reference/ps-ref-find-package.md). Visual Studio 2013 ve önceki yıllarda [Get-Package'ı](../reference/ps-reference/ps-ref-get-package.md) kullanın.

## <a name="availability-of-the-console"></a>Konsolun kullanılabilirliği

Visual Studio 2017'den itibaren, NuGet ve NuGet Paket Yöneticisi herhangi bir seçeneğini seçtiğinizde otomatik olarak yüklenir. NET ile ilgili iş yükleri; Ayrıca Visual Studio yükleyicisi > **NuGet paket yöneticisi** seçeneği > Bireysel bileşenleri > Kod araçları kontrol ederek tek tek yükleyebilirsiniz.

Ayrıca, Visual Studio 2015 ve daha önce NuGet Paket Yöneticisi'ni kaçırıyorsanız, **Araçlar > Uzantıları ve Güncellemelerini** kontrol edin... ve NuGet Paket Yöneticisi uzantısını arayın. Visual Studio'daki uzantıları yükleyicisi kullanamıyorsanız, uzantıyı doğrudan [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)'den indirebilirsiniz.

Package Manager Console şu anda Mac için Visual Studio ile mevcut değildir. Eşdeğer komutlar, ancak, [NuGet CLI](../reference/nuget-exe-CLI-reference.md)üzerinden kullanılabilir. Mac için Visual Studio NuGet paketleri yönetmek için bir uI var. Bkz. [Projenize Bir NuGet paketi dahil etmek.](/visualstudio/mac/nuget-walkthrough)

Paket Yöneticisi Konsolu Visual Studio Code ile birlikte değildir.

## <a name="extend-the-package-manager-console"></a>Paket Yöneticisi Konsolu'nu genişletin

Bazı paketler konsol için yeni komutlar yükler. Örneğin, `MvcScaffolding` aşağıda gösterildiği gibi `Scaffold` komutlar oluşturur ve bu komutlar mvc denetleyicileri ve görünümleri ASP.NET oluşturur:

![MvcScaffold'un kurulumu ve kullanımı](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>NuGet PowerShell profili ayarlama

PowerShell profili, PowerShell'i kullandığınız her yerde yaygın olarak kullanılan komutları kullanıma sunabilirsiniz. NuGet, genellikle aşağıdaki konumda bulunan NuGet'e özgü bir profili destekler:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Profili bulmak için `$profile` konsola yazın:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Daha fazla bilgi için [Windows PowerShell Profilleri'ne](https://technet.microsoft.com/library/bb613488.aspx)bakın.

## <a name="use-the-nugetexe-cli-in-the-console"></a>Konsolda nuget.exe CLI kullanın

[ `nuget.exe` CLI'yi](../reference/nuget-exe-cli-reference.md) Paket Yöneticisi Konsolunda kullanılabilir hale getirmek [için, NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) paketini konsoldan yükleyin:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
