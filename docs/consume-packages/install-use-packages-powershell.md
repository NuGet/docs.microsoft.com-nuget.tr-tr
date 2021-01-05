---
title: Visual Studio 'da Konsolu kullanarak NuGet paketlerini yükleyip yönetme
description: Paketlerle birlikte çalışmak üzere Visual Studio 'da NuGet Paket Yöneticisi konsolunu kullanmaya yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699832"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="bce3b-103">Visual Studio 'da Paket Yöneticisi konsolu ile paket yükleyip yönetme (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="bce3b-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="bce3b-104">NuGet Paket Yöneticisi konsolu NuGet paketlerini bulmak, yüklemek, kaldırmak ve güncelleştirmek için [NuGet PowerShell komutlarını](../reference/powershell-reference.md) kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bce3b-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="bce3b-105">Konsolunu kullanmak, Paket Yöneticisi Kullanıcı arabiriminin bir işlemi gerçekleştirmek için bir yol sağlamayan durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="bce3b-106">`nuget.exe`Konsolunda CLI komutlarını kullanmak için, bkz. [nuget.exe CLI 'Yi konsolda kullanma](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="bce3b-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="bce3b-107">Konsol, Windows üzerinde Visual Studio 'da yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="bce3b-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="bce3b-108">Mac için Visual Studio veya Visual Studio Code dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="bce3b-109">Burada listelenen komutlar, Visual Studio 'da Paket Yöneticisi konsoluna özgüdür ve genel bir PowerShell ortamında kullanılabilir olan [paket yönetimi modülü komutlarından](/powershell/module/packagemanagement/) farklıdır.</span><span class="sxs-lookup"><span data-stu-id="bce3b-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="bce3b-110">Özellikle, her ortamın diğeri üzerinde kullanılamayan komutları vardır ve aynı ada sahip komutlar, belirli bağımsız değişkenlerinde de farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="bce3b-111">Visual Studio 'da Paket Yönetimi konsolunu kullanırken, bu konu başlığı altında belgelenen komutlar ve bağımsız değişkenler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="bce3b-112">Paket bulma ve yüklemeyi</span><span class="sxs-lookup"><span data-stu-id="bce3b-112">Find and install a package</span></span>

<span data-ttu-id="bce3b-113">Örneğin, bir paketi bulmak ve yüklemek üç kolay adımla yapılır:</span><span class="sxs-lookup"><span data-stu-id="bce3b-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="bce3b-114">Visual Studio 'da projeyi/çözümü açın ve **araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** komutunu kullanarak konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="bce3b-115">Yüklemek istediğiniz paketi bulun.</span><span class="sxs-lookup"><span data-stu-id="bce3b-115">Find the package you want to install.</span></span> <span data-ttu-id="bce3b-116">Bunu zaten biliyorsanız adım 3 ' e atlayın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="bce3b-117">Yükleme komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bce3b-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="bce3b-118">Konsolda bulunan tüm işlemler [NUGET CLI](../reference/nuget-exe-cli-reference.md)ile de yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="bce3b-119">Ancak konsol komutları, Visual Studio bağlamı ve kaydedilen bir proje/çözüm içinde çalışır ve genellikle eşdeğer CLı komutlarından daha fazlasını yapar.</span><span class="sxs-lookup"><span data-stu-id="bce3b-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="bce3b-120">Örneğin, konsolu aracılığıyla bir paket yüklemek, CLı komutu olmadığı halde projeye bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="bce3b-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="bce3b-121">Bu nedenle, Visual Studio 'da çalışan geliştiriciler genellikle konsolu CLı için kullanmayı tercih eder.</span><span class="sxs-lookup"><span data-stu-id="bce3b-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="bce3b-122">Birçok konsol işlemi, Visual Studio 'da bilinen bir yol adı ile bir çözüme açık olmasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bce3b-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="bce3b-123">Kaydedilmemiş bir çözümünüz varsa veya çözüm yoksa, "çözüm açılmadı veya kaydedilmedi" hatasını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce3b-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="bce3b-124">Lütfen açık ve kaydedilmiş bir çözümünüz olduğundan emin olun. "</span><span class="sxs-lookup"><span data-stu-id="bce3b-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="bce3b-125">Bu, konsolunun çözüm klasörünü belirleyemediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="bce3b-126">Kaydedilmemiş bir çözümü kaydetme veya bir açık hesabınız yoksa bir çözüm oluşturup kaydetme, hatayı düzeltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="bce3b-127">Konsol ve konsol denetimlerini açma</span><span class="sxs-lookup"><span data-stu-id="bce3b-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="bce3b-128">**Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** komutunu kullanarak Visual Studio 'da konsolunu açın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="bce3b-129">Konsol, istediğiniz şekilde düzenlenebileceği ve konumlandırılmış bir Visual Studio penceresidir (bkz. [Visual Studio 'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="bce3b-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="bce3b-130">Varsayılan olarak, konsol komutları pencerenin üst kısmındaki denetimde ayarlandığı şekilde belirli bir paket kaynağına ve projeye karşı çalışır:</span><span class="sxs-lookup"><span data-stu-id="bce3b-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket kaynağı ve proje için Paket Yöneticisi konsol denetimleri](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="bce3b-132">Farklı bir paket kaynağı ve/veya proje seçildiğinde, Bu varsayılanlar sonraki komutlara göre değişir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="bce3b-133">Varsayılanları değiştirmeden bu ayarları fazla bir şekilde değiştirmek için, çoğu komut destek `-Source` ve `-ProjectName` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="bce3b-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="bce3b-134">Paket kaynaklarını yönetmek için dişli simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bce3b-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="bce3b-135">Bu, [Paket Yöneticisi Kullanıcı arabirimi](install-use-packages-visual-studio.md#package-sources) sayfasında açıklandığı şekilde, **> Araçlar > NuGet Paket Yöneticisi > paket kaynakları** iletişim kutusunun bir kısayoludur.</span><span class="sxs-lookup"><span data-stu-id="bce3b-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="bce3b-136">Ayrıca, proje seçicisinin sağında bulunan denetim konsolun içeriğini de temizler:</span><span class="sxs-lookup"><span data-stu-id="bce3b-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paket Yöneticisi konsol ayarları ve Temizleme denetimleri](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="bce3b-138">En sağdaki düğme uzun süre çalışan bir komutu keser.</span><span class="sxs-lookup"><span data-stu-id="bce3b-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="bce3b-139">Örneğin, `Get-Package -ListAvailable -PageSize 500` çalıştırmak birkaç dakika sürebilen varsayılan kaynakta (örneğin, NuGet.org) ilk 500 paketi listeler.</span><span class="sxs-lookup"><span data-stu-id="bce3b-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket Yöneticisi konsolu denetimi durdur](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="bce3b-141">Paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="bce3b-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="bce3b-142">Bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="bce3b-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="bce3b-143">Konsola bir paket yüklemek, [bir paket yüklendiğinde ne olacağı](../concepts/package-installation-process.md)ile ilgili adımların aynısını aşağıdaki eklemelerle gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="bce3b-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="bce3b-144">Konsol, ilgili lisans koşullarını örtülü anlaşmayla penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bce3b-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="bce3b-145">Koşulları kabul etmiyorsanız, paketi hemen kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="bce3b-146">Ayrıca, proje dosyasına pakete bir başvuru eklenir ve **Başvurular** düğümü altında **Çözüm Gezgini** görünür, proje dosyasındaki değişiklikleri doğrudan görmek için projeyi kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="bce3b-147">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="bce3b-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="bce3b-148">Bkz. [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="bce3b-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="bce3b-149">Bir tanımlayıcı bulmanız gerekiyorsa varsayılan projede yüklü olan tüm paketleri görmek için [Get-Package](../reference/ps-reference/ps-ref-get-package.md) ' i kullanın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="bce3b-150">Bir paketin kaldırılması aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="bce3b-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="bce3b-151">Projedeki paketin başvurularını kaldırır (ve hangi yönetim biçiminin kullanımda olduğunu).</span><span class="sxs-lookup"><span data-stu-id="bce3b-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="bce3b-152">Başvurular artık **Çözüm Gezgini** görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="bce3b-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="bce3b-153">( **Bin** klasöründen kaldırıldığını görmek için projeyi yeniden oluşturmanız gerekebilir.)</span><span class="sxs-lookup"><span data-stu-id="bce3b-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="bce3b-154">Paket yüklendiğinde veya ' de yapılan tüm değişiklikleri tersine çevirir `app.config` `web.config` .</span><span class="sxs-lookup"><span data-stu-id="bce3b-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="bce3b-155">Kalan hiçbir paket bu bağımlılıkları kullanıyorsa, önceden yüklenmiş bağımlılıkları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bce3b-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="bce3b-156">Bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bce3b-156">Update a package</span></span>

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

<span data-ttu-id="bce3b-157">Bkz. [Get-Package](../reference/ps-reference/ps-ref-get-package.md) ve [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="bce3b-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="bce3b-158">Paketi bulma</span><span class="sxs-lookup"><span data-stu-id="bce3b-158">Find a package</span></span>

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

<span data-ttu-id="bce3b-159">Bkz. [bul-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="bce3b-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="bce3b-160">Visual Studio 2013 ve önceki sürümlerde, [Get-Package](../reference/ps-reference/ps-ref-get-package.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="bce3b-161">Konsolun kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="bce3b-161">Availability of the console</span></span>

<span data-ttu-id="bce3b-162">Visual Studio 2017 ' den başlayarak, herhangi birini seçtiğinizde NuGet ve NuGet Paket Yöneticisi otomatik olarak yüklenir. NET ilgili iş yükleri; Visual Studio yükleyicisindeki **tek tek bileşenler > Code araçları > NuGet Paket Yöneticisi** seçeneğini tek tek denetleyerek de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bce3b-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="bce3b-163">Ayrıca, Visual Studio 2015 ve önceki sürümlerde NuGet Paket Yöneticisi eksik ise **araçlar > Uzantılar ve güncelleştirmeler...** ' ı Işaretleyin ve NuGet Paket Yöneticisi uzantısını arayın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="bce3b-164">Visual Studio 'da uzantılar yükleyicisini kullandıysanız, doğrudan uzantıyı konumundan indirebilirsiniz [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .</span><span class="sxs-lookup"><span data-stu-id="bce3b-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="bce3b-165">Paket Yöneticisi konsolu Mac için Visual Studio şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="bce3b-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="bce3b-166">Ancak eşdeğer komutlar [NUGET CLI](../reference/nuget-exe-CLI-reference.md)aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="bce3b-167">Mac için Visual Studio NuGet paketlerini yönetmek için bir kullanıcı arabirimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="bce3b-168">Bkz. [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="bce3b-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="bce3b-169">Paket Yöneticisi konsolu Visual Studio Code dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="bce3b-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="bce3b-170">Paket Yöneticisi konsolunu genişletme</span><span class="sxs-lookup"><span data-stu-id="bce3b-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="bce3b-171">Bazı paketler konsol için yeni komutlar yükler.</span><span class="sxs-lookup"><span data-stu-id="bce3b-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="bce3b-172">Örneğin, `MvcScaffolding` `Scaffold` aşağıda gösterildiği gibi, ASP.NET MVC denetleyicileri ve görünümleri üreten komutlar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="bce3b-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![MvcScaffold yükleme ve kullanma](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="bce3b-174">NuGet PowerShell profili ayarlama</span><span class="sxs-lookup"><span data-stu-id="bce3b-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="bce3b-175">PowerShell profili, PowerShell kullandığınızda yaygın olarak kullanılan komutların kullanılabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bce3b-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="bce3b-176">NuGet, genellikle aşağıdaki konumda bulunan NuGet 'e özgü bir profili destekler:</span><span class="sxs-lookup"><span data-stu-id="bce3b-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="bce3b-177">Profili bulmak için konsola şunu yazın `$profile` :</span><span class="sxs-lookup"><span data-stu-id="bce3b-177">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="bce3b-178">Daha fazla ayrıntı için [Windows PowerShell profillerine](/previous-versions//bb613488(v=vs.85))bakın.</span><span class="sxs-lookup"><span data-stu-id="bce3b-178">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="bce3b-179">Konsolda nuget.exe CLı 'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="bce3b-179">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="bce3b-180">[ `nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) 'Yı Paket Yöneticisi konsolunda kullanılabilir hale getirmek Için, konsolundan [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) paketini yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="bce3b-180">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
