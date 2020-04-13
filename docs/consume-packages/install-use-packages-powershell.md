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
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="d383c-103">Visual Studio'daki Paket Yöneticisi Konsolu (PowerShell) ile paketleri yükleyin ve yönetin</span><span class="sxs-lookup"><span data-stu-id="d383c-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="d383c-104">NuGet Package Manager Console, NuGet paketlerini bulmak, yüklemek, kaldırmak ve güncellemek için [NuGet PowerShell komutlarını](../reference/powershell-reference.md) kullanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d383c-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="d383c-105">Paket Yöneticisi UI'nin bir işlemi gerçekleştirmek için bir yol sağlamadığı durumlarda konsolu kullanmak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d383c-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="d383c-106">Konsolda `nuget.exe` CLI komutlarını kullanmak için [konsoldaki nuget.exe CLI'yi kullanma'ya](#use-the-nugetexe-cli-in-the-console)bakın.</span><span class="sxs-lookup"><span data-stu-id="d383c-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="d383c-107">Konsol, Windows'ta Visual Studio'da yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="d383c-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="d383c-108">Mac veya Visual Studio Code için Visual Studio ile birlikte değildir.</span><span class="sxs-lookup"><span data-stu-id="d383c-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="d383c-109">Bir paket bulma ve yükleme</span><span class="sxs-lookup"><span data-stu-id="d383c-109">Find and install a package</span></span>

<span data-ttu-id="d383c-110">Örneğin, bir paketi bulma ve yükleme üç kolay adımla yapılır:</span><span class="sxs-lookup"><span data-stu-id="d383c-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="d383c-111">Visual Studio'da projeyi/çözümü açın ve **NuGet Paket Yöneticisi > Paket Yöneticisi Konsol** komutu > Araçları kullanarak konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="d383c-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="d383c-112">Yüklemek istediğiniz paketi bulun.</span><span class="sxs-lookup"><span data-stu-id="d383c-112">Find the package you want to install.</span></span> <span data-ttu-id="d383c-113">Bunu zaten biliyorsanız, adım 3'e atlayın.</span><span class="sxs-lookup"><span data-stu-id="d383c-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="d383c-114">Yükleme komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d383c-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="d383c-115">Konsolda bulunan tüm işlemler [NuGet CLI](../reference/nuget-exe-cli-reference.md)ile de yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d383c-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="d383c-116">Ancak konsol komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle eşdeğer CLI komutlarından daha fazlasını gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d383c-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="d383c-117">Örneğin, konsol üzerinden bir paket yüklemek projeye bir başvuru eklerken, CLI komutu göndermez.</span><span class="sxs-lookup"><span data-stu-id="d383c-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="d383c-118">Bu nedenle Visual Studio'da çalışan geliştiriciler genellikle konsolu CLI'ye tercih ediyor.</span><span class="sxs-lookup"><span data-stu-id="d383c-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="d383c-119">Birçok konsol işlemi, Visual Studio'da bilinen bir yol adı ile açılan bir çözüme bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d383c-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="d383c-120">Kaydedilmemiş bir çözümünüz varsa veya çözüm yoksa, "Çözüm açılmaz veya kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="d383c-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="d383c-121">Lütfen açık ve kaydedilmiş bir çözüme sahip olduğundan emin olun."</span><span class="sxs-lookup"><span data-stu-id="d383c-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="d383c-122">Bu, konsolun çözüm klasörünü belirleyemeyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d383c-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="d383c-123">Kaydedilmemiş bir çözümü kaydetmek veya açık bir çözümünüz yoksa çözüm oluşturmak ve kaydetmek hatayı düzeltmelidir.</span><span class="sxs-lookup"><span data-stu-id="d383c-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="d383c-124">Konsol ve konsol denetimlerini açma</span><span class="sxs-lookup"><span data-stu-id="d383c-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="d383c-125">**NuGet Paket Yöneticisi > Paket Yöneticisi Konsol komutu > Araçları** kullanarak Visual Studio'da konsolu açın.</span><span class="sxs-lookup"><span data-stu-id="d383c-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="d383c-126">Konsol, istediğiniz gibi düzenlenebilecek ve konumlandırılabilen bir Visual Studio penceresidir [(Bkz. Visual Studio'da pencere düzenlerini özelleştir).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="d383c-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="d383c-127">Varsayılan olarak, konsol komutları pencerenin üst kısmındaki denetimde ayarlanan belirli bir paket kaynağına ve projeye karşı çalışır:</span><span class="sxs-lookup"><span data-stu-id="d383c-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket kaynağı ve proje için Paket Yöneticisi Konsol denetimleri](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="d383c-129">Farklı bir paket kaynağı ve/veya proje seçmek sonraki komutlar için bu varsayılanları değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d383c-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="d383c-130">Varsayılanları değiştirmeden bu ayarları aşırıya kakıştın, çoğu komut desteği `-Source` ve `-ProjectName` seçeneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="d383c-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="d383c-131">Paket kaynaklarını yönetmek için vites simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d383c-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="d383c-132">Bu, [Paket Yöneticisi UI](install-use-packages-visual-studio.md#package-sources) sayfasında açıklandığı gibi Paket Kaynakları > Paket Kaynakları iletişim kutusunu > Araçlar > **Seçenekleri'ne** bir kısayoldur.</span><span class="sxs-lookup"><span data-stu-id="d383c-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="d383c-133">Ayrıca, proje seçicinin sağındaki denetim konsolun içeriğini temizler:</span><span class="sxs-lookup"><span data-stu-id="d383c-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paket Yöneticisi Konsol ayarları ve net denetimler](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="d383c-135">En sağda olan düğme, uzun süren bir komutu keser.</span><span class="sxs-lookup"><span data-stu-id="d383c-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="d383c-136">Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` varsayılan kaynak (nuget.org gibi) üzerinde çalıştırmak için birkaç dakika sürebilir en üst 500 paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="d383c-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket Yöneticisi Konsol durdurma kontrolü](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="d383c-138">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="d383c-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="d383c-139">Bkz. [Yükle-Paket](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="d383c-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="d383c-140">Konsola bir paket yüklemek, aşağıdaki eklemelerle [birlikte, bir paket yüklendiğinde ne olduğu](../concepts/package-installation-process.md)konusunda açıklandığı gibi aynı adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="d383c-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="d383c-141">Konsol, penceresinde geçerli lisans koşullarını zımni anlaşma yla görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d383c-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="d383c-142">Şartları kabul etmiyorsanız, paketi derhal kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d383c-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="d383c-143">Ayrıca projeye bir başvuru proje dosyasına eklenir ve **Başvurudüğümün** altında **Çözüm Gezgini'nde** görünür, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d383c-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="d383c-144">Paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="d383c-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="d383c-145">Bkz. [Kaldır-Paket.](../reference/ps-reference/ps-ref-uninstall-package.md)</span><span class="sxs-lookup"><span data-stu-id="d383c-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="d383c-146">Bir tanımlayıcı bulmanız gerekiyorsa, varsayılan projede şu anda yüklü olan tüm paketleri görmek için [Get-Package'ı](../reference/ps-reference/ps-ref-get-package.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d383c-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="d383c-147">Paketi kaldırma aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="d383c-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="d383c-148">Pakete yapılan başvuruları projeden kaldırır (ve hangi yönetim biçimi kullanılıyorsa kullanılır).</span><span class="sxs-lookup"><span data-stu-id="d383c-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="d383c-149">Başvurular artık **Çözüm Gezgini'nde**görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="d383c-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="d383c-150">(Bin klasöründen kaldırıldığını görmek için **Bin** projeyi yeniden oluşturmanız gerekebilir.)</span><span class="sxs-lookup"><span data-stu-id="d383c-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="d383c-151">Paket yüklendiğinde `app.config` veya `web.config` yüklendiğinde yapılan değişiklikleri tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="d383c-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="d383c-152">Kalan paketler bu bağımlılıkları kullanmıyorsa, daha önce yüklenmiş bağımlılıkları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d383c-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="d383c-153">Paketi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d383c-153">Update a package</span></span>

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

<span data-ttu-id="d383c-154">[Bkz. Paket Al](../reference/ps-reference/ps-ref-get-package.md) ve [Güncelle-Paket](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="d383c-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="d383c-155">Bir paket bulun</span><span class="sxs-lookup"><span data-stu-id="d383c-155">Find a package</span></span>

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

<span data-ttu-id="d383c-156">Bkz. [Bul Paketi](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="d383c-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="d383c-157">Visual Studio 2013 ve önceki yıllarda [Get-Package'ı](../reference/ps-reference/ps-ref-get-package.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d383c-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="d383c-158">Konsolun kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="d383c-158">Availability of the console</span></span>

<span data-ttu-id="d383c-159">Visual Studio 2017'den itibaren, NuGet ve NuGet Paket Yöneticisi herhangi bir seçeneğini seçtiğinizde otomatik olarak yüklenir. NET ile ilgili iş yükleri; Ayrıca Visual Studio yükleyicisi > **NuGet paket yöneticisi** seçeneği > Bireysel bileşenleri > Kod araçları kontrol ederek tek tek yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d383c-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="d383c-160">Ayrıca, Visual Studio 2015 ve daha önce NuGet Paket Yöneticisi'ni kaçırıyorsanız, **Araçlar > Uzantıları ve Güncellemelerini** kontrol edin... ve NuGet Paket Yöneticisi uzantısını arayın.</span><span class="sxs-lookup"><span data-stu-id="d383c-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="d383c-161">Visual Studio'daki uzantıları yükleyicisi kullanamıyorsanız, uzantıyı doğrudan [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)'den indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d383c-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="d383c-162">Package Manager Console şu anda Mac için Visual Studio ile mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="d383c-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="d383c-163">Eşdeğer komutlar, ancak, [NuGet CLI](../reference/nuget-exe-CLI-reference.md)üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d383c-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="d383c-164">Mac için Visual Studio NuGet paketleri yönetmek için bir uI var.</span><span class="sxs-lookup"><span data-stu-id="d383c-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="d383c-165">Bkz. [Projenize Bir NuGet paketi dahil etmek.](/visualstudio/mac/nuget-walkthrough)</span><span class="sxs-lookup"><span data-stu-id="d383c-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="d383c-166">Paket Yöneticisi Konsolu Visual Studio Code ile birlikte değildir.</span><span class="sxs-lookup"><span data-stu-id="d383c-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="d383c-167">Paket Yöneticisi Konsolu'nu genişletin</span><span class="sxs-lookup"><span data-stu-id="d383c-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="d383c-168">Bazı paketler konsol için yeni komutlar yükler.</span><span class="sxs-lookup"><span data-stu-id="d383c-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="d383c-169">Örneğin, `MvcScaffolding` aşağıda gösterildiği gibi `Scaffold` komutlar oluşturur ve bu komutlar mvc denetleyicileri ve görünümleri ASP.NET oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d383c-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![MvcScaffold'un kurulumu ve kullanımı](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="d383c-171">NuGet PowerShell profili ayarlama</span><span class="sxs-lookup"><span data-stu-id="d383c-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="d383c-172">PowerShell profili, PowerShell'i kullandığınız her yerde yaygın olarak kullanılan komutları kullanıma sunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d383c-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="d383c-173">NuGet, genellikle aşağıdaki konumda bulunan NuGet'e özgü bir profili destekler:</span><span class="sxs-lookup"><span data-stu-id="d383c-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="d383c-174">Profili bulmak için `$profile` konsola yazın:</span><span class="sxs-lookup"><span data-stu-id="d383c-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="d383c-175">Daha fazla bilgi için [Windows PowerShell Profilleri'ne](https://technet.microsoft.com/library/bb613488.aspx)bakın.</span><span class="sxs-lookup"><span data-stu-id="d383c-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="d383c-176">Konsolda nuget.exe CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="d383c-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="d383c-177">[ `nuget.exe` CLI'yi](../reference/nuget-exe-cli-reference.md) Paket Yöneticisi Konsolunda kullanılabilir hale getirmek [için, NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) paketini konsoldan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="d383c-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
