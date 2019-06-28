---
title: Yükleme ve PowerShell kullanarak Visual Studio'da NuGet paketlerini Yönet
description: Paketlerle çalışmak için Visual Studio'da NuGet Paket Yöneticisi konsolu kullanarak yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426214"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a><span data-ttu-id="8429f-103">Yükleme ve Visual Studio'da PowerShell kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="8429f-103">Install and manage packages using PowerShell in Visual Studio</span></span>

<span data-ttu-id="8429f-104">NuGet Paket Yöneticisi konsolu kullanmanıza olanak tanıyan [NuGet PowerShell komutlarını](../tools/powershell-reference.md) bulmak için yükleme, kaldırma ve NuGet paketlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8429f-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="8429f-105">Konsolunu kullanarak, burada Paket Yöneticisi UI bir işlemi gerçekleştirmek için bir yol sağlamaz durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8429f-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="8429f-106">Kullanılacak `nuget.exe` konsolunda, CLI komutları görmek [konsolunda nuget.exe CLI kullanarak](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="8429f-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="8429f-107">Windows üzerinde Visual Studio konsol yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="8429f-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="8429f-108">Mac veya Visual Studio Code için Visual Studio ile dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="8429f-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="8429f-109">Bulma ve bir paket yükleme</span><span class="sxs-lookup"><span data-stu-id="8429f-109">Find and install a package</span></span>

<span data-ttu-id="8429f-110">Örneğin, bulma ve bir paket yükleme üç kolay adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="8429f-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="8429f-111">Proje/çözüm Visual Studio'da açın ve konsol kullanarak açın **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.</span><span class="sxs-lookup"><span data-stu-id="8429f-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="8429f-112">Yüklemek istediğiniz paketi bulmak.</span><span class="sxs-lookup"><span data-stu-id="8429f-112">Find the package you want to install.</span></span> <span data-ttu-id="8429f-113">Bunu zaten biliyorsanız, 3. adımına geçin.</span><span class="sxs-lookup"><span data-stu-id="8429f-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="8429f-114">İnstall komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8429f-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="8429f-115">Konsolunda kullanılabilir tüm işlemleri ile de yapılabilir [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8429f-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="8429f-116">Ancak, Konsolu komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle birden çok eşdeğer CLI komutları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8429f-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="8429f-117">Örneğin, bir paket Konsolu aracılığıyla yüklenmesi CLI komutunu desteklemez projeye bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="8429f-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="8429f-118">Bu nedenle, CLI konsola kullanarak Visual Studio'da genellikle çalışan geliştiriciler tercih eder.</span><span class="sxs-lookup"><span data-stu-id="8429f-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="8429f-119">Visual Studio'da bilinen yol adı ile açık bir çözüm açık olması birçok konsol işlemlerini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8429f-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="8429f-120">Kaydedilmemiş bir çözüm ya da çözüm varsa, bir hata görebilirsiniz, "Çözüm açık değil veya kaydedilmedi.</span><span class="sxs-lookup"><span data-stu-id="8429f-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="8429f-121">Lütfen bir açık ve kaydedilen çözümüne sahip olun."</span><span class="sxs-lookup"><span data-stu-id="8429f-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="8429f-122">Bu konsol Çözüm klasörü belirlenemiyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="8429f-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="8429f-123">Kaydedilmemiş bir çözüm kaydetme veya oluşturma ve bir çözümü, yoksa, kaydetme açın, hatayı düzeltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8429f-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="8429f-124">Konsol ve konsol denetimlerini açma</span><span class="sxs-lookup"><span data-stu-id="8429f-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="8429f-125">Visual Studio kullanarak Uçbirimi **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.</span><span class="sxs-lookup"><span data-stu-id="8429f-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="8429f-126">Düzenlenmiş ve istediğiniz gibi konumlandırılmış bir Visual Studio pencere konsoludur (bkz [Visual Studio'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="8429f-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="8429f-127">Konsolu komutları, varsayılan olarak, pencerenin üst kısmındaki denetim kümesindeki olarak belirli bir paket kaynağı ve proje karşı çalışır:</span><span class="sxs-lookup"><span data-stu-id="8429f-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket kaynağı ve proje için Paket Yöneticisi konsolu denetimleri](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="8429f-129">Farklı bir paket kaynağı ve/veya proje seçmek için sonraki komutlarda bu Varsayılanları değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8429f-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="8429f-130">Overrride için varsayılan değerleri değiştirmeden bu ayarlar, komutların çoğu destekler `-Source` ve `-ProjectName` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="8429f-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="8429f-131">Paket kaynaklarını yönetmek için dişli simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="8429f-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="8429f-132">Bu kısayol, **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını** üzerinde açıklandığı gibi iletişim kutusunu [Paket Yöneticisi UI](package-manager-ui.md#package-sources) sayfası.</span><span class="sxs-lookup"><span data-stu-id="8429f-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="8429f-133">Ayrıca, denetimin sağ tarafında proje Seçici için konsolun içeriği temizler:</span><span class="sxs-lookup"><span data-stu-id="8429f-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paket Yöneticisi konsolu ayarları ve denetimleri Temizle](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="8429f-135">Sağdaki düğme uzun süre çalışan komut kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="8429f-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="8429f-136">Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` çalıştırmak için birkaç dakika sürebilir varsayılan kaynak (nuget.org gibi), üst 500 paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="8429f-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket Yöneticisi konsolu durdurma denetimi](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="8429f-138">Bir paketi yükleniyor</span><span class="sxs-lookup"><span data-stu-id="8429f-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="8429f-139">Bkz: [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="8429f-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="8429f-140">Konsolunda bir paket yükleme aynı adımları gerçekleştirir üzerinde açıklandığı [paketi yüklendiğinde ne](../concepts/package-installation-process.md), aşağıdaki eklemelerle:</span><span class="sxs-lookup"><span data-stu-id="8429f-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="8429f-141">Konsol penceresi örtük anlaşma kapsamında olan geçerli lisans koşullarında görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8429f-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="8429f-142">Koşulları kabul etmiyorsanız, paket hemen kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8429f-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="8429f-143">Ayrıca, pakete bir başvuru proje dosyasına eklenir ve görünür **Çözüm Gezgini** altında **başvuruları** düğümü, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmek için ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="8429f-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="8429f-144">Bir paket kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="8429f-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="8429f-145">Bkz: [kaldırma-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="8429f-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="8429f-146">Kullanım [Get-Package](../tools/ps-ref-get-package.md) tanımlayıcı bulmanız gerekiyorsa varsayılan proje şu anda yüklü olan tüm paketleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="8429f-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="8429f-147">Bir paketi, aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="8429f-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="8429f-148">Paket başvuruları projeye (ve hangi yönetim biçimi kullanılır) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8429f-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="8429f-149">Başvuruları artık görünür **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="8429f-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="8429f-150">(Kaldırıldığında görmek için projeyi yeniden derlemek ihtiyacınız olabilecek **Bin** klasör.)</span><span class="sxs-lookup"><span data-stu-id="8429f-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="8429f-151">Yapılan tüm değişiklikler tersine `app.config` veya `web.config` paketin ne zaman yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8429f-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="8429f-152">Hiçbir kalan paketleri bu bağımlılıkların kullanırsanız bağımlılıkları önceden yüklenmiş kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8429f-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="8429f-153">Bir paketi güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="8429f-153">Updating a package</span></span>

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

<span data-ttu-id="8429f-154">Bkz: [Get-Package](../tools/ps-ref-get-package.md) ve [güncelleştirme paketi](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="8429f-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="8429f-155">Bir paketi bulma</span><span class="sxs-lookup"><span data-stu-id="8429f-155">Finding a package</span></span>

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

<span data-ttu-id="8429f-156">Bkz: [Bul-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="8429f-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="8429f-157">Visual Studio 2013 ve önceki sürümleri kullanın [Get-Package](../tools/ps-ref-get-package.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="8429f-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="8429f-158">Konsolunun kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="8429f-158">Availability of the console</span></span>

<span data-ttu-id="8429f-159">Tüm seçtiğinizde Visual Studio 2017'den itibaren NuGet ve NuGet Paket Yöneticisi otomatik olarak yüklenir. NET ilgili iş yükleri; Ayrıca ayrı ayrı kontrol ederek yükleyebilirsiniz **tek tek bileşenler > kod Araçlar > NuGet Paket Yöneticisi** seçeneği Visual Studio Yükleyicisi'nde.</span><span class="sxs-lookup"><span data-stu-id="8429f-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="8429f-160">Ayrıca, Visual Studio 2015'te ve daha önce NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  ve NuGet paket yöneticisini uzantısı arayın.</span><span class="sxs-lookup"><span data-stu-id="8429f-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="8429f-161">Visual Studio Uzantıları yükleyici yapamıyorsanız uzantısını doğrudan indirebileceğiniz [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="8429f-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="8429f-162">Paket Yöneticisi konsolu, Mac için Visual Studio ile şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="8429f-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="8429f-163">Ancak, eşdeğer komutları aracılığıyla [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8429f-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="8429f-164">Mac için Visual Studio, NuGet paketlerini yönetmek için bir kullanıcı Arabirimi yok.</span><span class="sxs-lookup"><span data-stu-id="8429f-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="8429f-165">Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8429f-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="8429f-166">Paket Yöneticisi konsolu, Visual Studio Code ile dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="8429f-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="8429f-167">Paket Yöneticisi konsolu genişletme</span><span class="sxs-lookup"><span data-stu-id="8429f-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="8429f-168">Bazı paketler yeni komutlar Konsolu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8429f-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="8429f-169">Örneğin, `MvcScaffolding` gibi komutlar oluşturur `Scaffold` aşağıda gösterilen, oluşturduğu ASP.NET MVC denetleyicileri ve görünümleri:</span><span class="sxs-lookup"><span data-stu-id="8429f-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Yükleme ve MvcScaffold kullanma](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="8429f-171">Bir NuGet PowerShell profili ayarlama</span><span class="sxs-lookup"><span data-stu-id="8429f-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="8429f-172">Bir PowerShell profili, PowerShell kullandığınız her yerde sık kullanılan komutları kullanılabilir kılmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8429f-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="8429f-173">NuGet, genellikle şu konumda bulunan bir NuGet özgü profili destekler:</span><span class="sxs-lookup"><span data-stu-id="8429f-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="8429f-174">Profil bulmak için yazın `$profile` konsolunda:</span><span class="sxs-lookup"><span data-stu-id="8429f-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="8429f-175">Daha fazla ayrıntı için başvurmak [Windows PowerShell profilleri](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="8429f-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="8429f-176">Konsolunda nuget.exe CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="8429f-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="8429f-177">Yapmak [ `nuget.exe` CLI](nuget-exe-cli-reference.md) Paket Yöneticisi konsolunda kullanılabilir yükleme [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) konsolundan paket:</span><span class="sxs-lookup"><span data-stu-id="8429f-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
