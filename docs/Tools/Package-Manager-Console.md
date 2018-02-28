---
title: "NuGet Paket Yöneticisi konsolu Kılavuzu | Microsoft Docs"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.nuget.packagemanager.console
description: "Paketlerle çalışmak için Visual Studio'da NuGet Paket Yöneticisi Konsolu kullanma için yönergeler."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet powershell, NuGet paketlerini yönetme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 60c7edd0497e162cc511424e9acfbbfd6f53fd46
ms.sourcegitcommit: a40a6ce6897b2d9411397b2e29b1be234eb6e50c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/27/2018
---
# <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

NuGet Paket Yöneticisi Konsolu Windows 2012 ve sonraki sürümleri Visual Studio içinde yerleşik olarak bulunur. (Bu Mac veya Visual Studio Code için Visual Studio ile dahil değildir.)

Konsol kullanmanıza olanak sağlayan [NuGet PowerShell komutlarını](../tools/powershell-reference.md) bulmak için yükleme, kaldırma ve NuGet paketlerini güncelleştirmeyi. Konsolunu kullanarak, burada Paket Yöneticisi kullanıcı Arabirimi bir işlem gerçekleştirmek için bir yöntem sağlamaz durumlarda gereklidir. Kullanılacak `nuget.exe` Konsolu komutları görmek [konsolunda nuget.exe CLI kullanarak](#using-the-nugetexe-cli-in-the-console).

Örneğin, bulma ve bir paket yükleme ile üç kolay adımı gerçekleştirilir:

1. Proje/çözüm Visual Studio'da açın ve konsol kullanarak açın **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.

1. Yüklemek istediğiniz paketi bulun. Bu zaten biliyorsanız, 3. adıma atlayın.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Yükleme komutu çalıştırın:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Konsolunda kullanılabilir tüm işlemleri ile de yapılabilir [NuGet CLI](../tools/nuget-exe-cli-reference.md). Ancak, Konsolu komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle kendi eşdeğer CLI komutları birden fazla gerçekleştirmek. Örneğin, konsolu üzerinden bir paket yükleme CLI komut'in almadığı projesine bir başvuru ekler. Bu nedenle, CLI konsola kullanarak Visual Studio'da genellikle çalışan geliştiricilere tercih eder.

> [!Tip]
> Visual Studio'da bilinen yol adı ile açılmış bir çözüme sahip birçok konsol işlemlerini bağlıdır. Kaydedilmemiş bir çözüm ya da çözüm varsa, hatayı görmek, "Çözüm açılmadı veya kaydedilmedi. Lütfen açık ve kaydedilmiş bir çözümünüz olduğundan emin olun." Bu konsol Çözüm klasörü belirlenemiyor gösterir. Kaydedilmemiş çözümünü kaydetme veya oluşturma ve bir çözüm, yoksa, kaydetme açın, hata düzeltmeniz gerekir.

## <a name="opening-the-console-and-console-controls"></a>Konsol denetimleri ve konsolunu açma

1. Visual Studio kullanarak Konsolu **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu. Konsol düzenlenmiş ve ancak istediğiniz konumlandırılmış bir Visual Studio penceredir (bkz [Visual Studio'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Varsayılan olarak, Konsolu komutları, pencerenin üstündeki denetim kümesinde olarak belirli bir paket kaynağı ve proje karşı çalışır:

    ![Paket kaynağı ve proje için Paket Yöneticisi konsolu denetimleri](media/PackageManagerConsoleControls1.png)

1. Farklı bir paket kaynağı ve/veya proje seçme sonraki komutları için bu varsayılan ayarları değiştirir. Overrride için varsayılanları değiştirmeden bu ayarları çoğu komut desteği `-Source` ve `-ProjectName` seçenekleri.

1. Paket kaynaklarını yönetmek için dişli simgesini seçin. Bu kısayoludur **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını** açıklandığı gibi iletişim kutusu [Paket Yöneticisi kullanıcı Arabirimi](package-manager-ui.md#package-sources) sayfası. Ayrıca, proje Seçici sağındaki denetim konsolun içeriği temizler:

    ![Paket Yöneticisi konsolu ayarları ve denetimleri Temizle](media/PackageManagerConsoleControls2.png)

1. Sağdaki düğme uzun süre çalışan komutunu keser. Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` çalıştırmak için birkaç dakika sürebilir (örneğin, nuget.org), varsayılan kaynak üst 500 paketlerini listeler.

    ![Paket Yöneticisi konsolu durdurma denetimi](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Bir paketi yükleniyor

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Bkz: [Install-Package](../tools/ps-ref-install-package.md).

Bir paketi yüklerken aşağıdaki eylemleri gerçekleştirir:

- Geçerli lisans şartları zımni Sözleşmesi ile Konsol penceresinde görüntüler. Koşulları kabul etmiyorsanız, paketi hemen kaldırmanız gerekir.
- Her başvuru biçimi kullanımda içinde projesine bir başvuru ekler. Başvuruları daha sonra Çözüm Gezgini ve geçerli başvuru biçim dosyası görünür. Ancak, doğrudan proje dosyasındaki değişiklikleri görmek için projeyi kaydedin gerek PackageReference ile unutmayın.
- Paketi önbelleğe alır:
  - PackageReference: Paket konumundaki önbelleğe alınmış `%USERPROFILE%\.nuget\packages` ve kilidi dosya yani `project.assets.json` güncelleştirilir.
  - `packages.config`: oluşturur bir `packages` klasör paketi dosyalarını içindeki bir alt klasör içine çözüm kök ve kopyalar. `package.config` Dosya güncelleştirilir.
- Güncelleştirmeleri `app.config` ve/veya `web.config` paketi kullanıyorsa [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md).
- Henüz yoksa projedeki tüm bağımlılıkları yükler. Bu paket işleminde, açıklandığı gibi güncelleştirme sürümleri [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).
- Paketin Benioku dosyası varsa, bir Visual Studio penceresinde görüntüler.

> [!Tip]
> Paketleri yükleme birincil yararlarından biri `Install-Package` konsolunda komuttur Paket Yöneticisi kullanıcı Arabirimi kullandığınız sanki projesine bir başvuru ekleyen. Buna karşılık, `nuget install` CLI komutu yalnızca paketi indirir ve otomatik olarak bir başvuru eklemez.

## <a name="uninstalling-a-package"></a>Bir paketi kaldırma

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Bkz: [kaldırma paket](../tools/ps-ref-uninstall-package.md). Kullanım [Get-Package](../tools/ps-ref-get-package.md) tanımlayıcı bulmanız gerekiyorsa varsayılan projede yüklü tüm paketler görmek için.

Bir paketi aşağıdaki eylemleri gerçekleştirir:

- Proje (ve her başvuru biçimi kullanımda) paket başvuruları kaldırır. Başvurular, Çözüm Gezgini'nde artık görünür. (Kaldırılmasını görmek için projeyi yeniden oluşturmanız gerekebilir **Bin** klasörü.)
- Yapılan değişiklikleri geri alır `app.config` veya `web.config` paketin ne zaman yüklendi.
- Bu bağımlılıklar hiçbir kalan paketleri kullanıyorsanız, önceden yüklenmiş kaldırır bağımlılıkları.

> [!Tip]
> Gibi `Install-Package`, `Uninstall-Package` komutu aksine projedeki başvuruları yönetme avantajına sahiptir `nuget uninstall` CLI komutu.

## <a name="updating-a-package"></a>Paket güncelleştirme

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

## <a name="finding-a-package"></a>Bir paket bulma

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

Bkz: [Bul paket](../tools/ps-ref-find-package.md). Visual Studio 2013 ve önceki sürümlerinde kullanmak [Get-Package](../tools/ps-ref-get-package.md) yerine.

## <a name="availability-of-the-console"></a>Konsolunun kullanılabilirliğini

Visual Studio 2017 içinde NuGet ve NuGet Paket Yöneticisi herhangi seçtiğinizde otomatik olarak yüklenir. NET ilgili iş yükleri; Ayrıca ayrı ayrı kontrol ederek yükleyebilirsiniz **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi** Visual Studio 2017 yükleyici seçeneği.

Ayrıca, Visual Studio 2015 ve daha önce NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  NuGet Paket Yöneticisi uzantısı arayın. Visual Studio Uzantıları yükleyici yapamıyorsanız doğrudan uzantısı indirebilirsiniz [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Paket Yöneticisi konsolu, Visual Studio for Mac ile şu anda kullanılabilir değil. Eşdeğer komutları ancak aracılığıyla kullanılabilir [NuGet CLI](nuget-exe-CLI-reference.md). Mac için Visual Studio, NuGet paketlerini yönetmek için bir kullanıcı Arabirimi yok. Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).

Paket Yöneticisi konsolu ile Visual Studio Code dahil değildir.

## <a name="extending-the-package-manager-console"></a>Paket Yöneticisi konsolu genişletme

Bazı paketler yeni komutları Konsolu yükleyin. Örneğin, `MvcScaffolding` gibi komutları oluşturur `Scaffold` aşağıda gösterilen, oluşturur ASP.NET MVC denetleyicileri ve görünümler:

![Yükleme ve MvcScaffold kullanma](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Bir NuGet PowerShell profili ayarlama

Bir PowerShell profili, PowerShell kullandığınız her yerde sık kullanılan komutlar kullanılabilir kılmanızı sağlar. NuGet genellikle aşağıdaki konumda bulunan NuGet özgü bir profili destekler:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Profil bulmak için şunu yazın `$profile` konsolunda:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Daha fazla ayrıntı için başvurmak [Windows PowerShell profilleri](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Konsolunda CLI nuget.exe kullanma

Yapmak için [ `nuget.exe` CLI](nuget-exe-cli-reference.md) Paket Yöneticisi konsolunda kullanılabilir yükleme [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) konsolundan paketi:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
