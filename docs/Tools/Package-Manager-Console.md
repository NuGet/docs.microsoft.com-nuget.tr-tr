---
title: "NuGet Paket Yöneticisi konsolu Kılavuzu | Microsoft Docs"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Paketlerle çalışmak için Visual Studio'da NuGet Paket Yöneticisi Konsolu kullanma için yönergeler."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet powershell, NuGet paketlerini yönetme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc11963a9b9bfe9aa456d8cd4c8397e1084f660b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="15fa5-104">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="15fa5-104">Package Manager Console</span></span>

<span data-ttu-id="15fa5-105">NuGet Paket Yöneticisi Konsolu Windows 2012 ve sonraki sürümleri Visual Studio içinde yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="15fa5-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="15fa5-106">(Bu Mac veya Visual Studio Code için Visual Studio ile dahil değildir.)</span><span class="sxs-lookup"><span data-stu-id="15fa5-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="15fa5-107">Konsol kullanmanıza olanak sağlayan [NuGet PowerShell komutlarını](../tools/powershell-reference.md) bulmak için yükleme, kaldırma ve NuGet paketlerini güncelleştirmeyi.</span><span class="sxs-lookup"><span data-stu-id="15fa5-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="15fa5-108">Konsolunu kullanarak, burada Paket Yöneticisi kullanıcı Arabirimi bir işlem gerçekleştirmek için bir yöntem sağlamaz durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="15fa5-109">Örneğin, bulma ve bir paket yükleme ile üç kolay adımı gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="15fa5-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="15fa5-110">Proje/çözüm Visual Studio'da açın ve konsol kullanarak açın **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.</span><span class="sxs-lookup"><span data-stu-id="15fa5-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="15fa5-111">Yüklemek istediğiniz paketi bulun.</span><span class="sxs-lookup"><span data-stu-id="15fa5-111">Find the package you want to install.</span></span> <span data-ttu-id="15fa5-112">Bu zaten biliyorsanız, 3. adıma atlayın.</span><span class="sxs-lookup"><span data-stu-id="15fa5-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="15fa5-113">Yükleme komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="15fa5-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="15fa5-114">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="15fa5-114">In this topic:</span></span>

- [<span data-ttu-id="15fa5-115">Konsolunu açma</span><span class="sxs-lookup"><span data-stu-id="15fa5-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="15fa5-116">Bir paketi yükleniyor</span><span class="sxs-lookup"><span data-stu-id="15fa5-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="15fa5-117">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="15fa5-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="15fa5-118">Bir paket bulma</span><span class="sxs-lookup"><span data-stu-id="15fa5-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="15fa5-119">Paket güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="15fa5-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="15fa5-120">Konsolunun kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="15fa5-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="15fa5-121">Paket Yöneticisi konsolu genişletme</span><span class="sxs-lookup"><span data-stu-id="15fa5-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="15fa5-122">Bir NuGet PowerShell profili ayarlama</span><span class="sxs-lookup"><span data-stu-id="15fa5-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="15fa5-123">Konsolunda kullanılabilir tüm işlemleri ile de yapılabilir [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="15fa5-124">Ancak, Konsolu komutları Visual Studio ve kaydedilmiş bir proje/çözüm bağlamında çalışır ve genellikle kendi eşdeğer CLI komutları birden fazla gerçekleştirmek.</span><span class="sxs-lookup"><span data-stu-id="15fa5-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="15fa5-125">Örneğin, konsolu üzerinden bir paket yükleme CLI komut'in almadığı projesine bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="15fa5-126">Bu nedenle, CLI konsola kullanarak Visual Studio'da genellikle çalışan geliştiricilere tercih eder.</span><span class="sxs-lookup"><span data-stu-id="15fa5-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="15fa5-127">Visual Studio'da bilinen yol adı ile açılmış bir çözüme sahip birçok konsol işlemlerini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="15fa5-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="15fa5-128">Kaydedilmemiş bir çözüm ya da çözüm varsa, hatayı görmek, "Çözüm açılmadı veya kaydedilmedi.</span><span class="sxs-lookup"><span data-stu-id="15fa5-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="15fa5-129">Lütfen açık ve kaydedilmiş bir çözümünüz olduğundan emin olun."</span><span class="sxs-lookup"><span data-stu-id="15fa5-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="15fa5-130">Bu konsol Çözüm klasörü belirlenemiyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="15fa5-131">Kaydedilmemiş çözümünü kaydetme veya oluşturma ve bir çözüm, yoksa, kaydetme açın, hata düzeltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="15fa5-132">Konsol denetimleri ve konsolunu açma</span><span class="sxs-lookup"><span data-stu-id="15fa5-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="15fa5-133">Visual Studio kullanarak Konsolu **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** komutu.</span><span class="sxs-lookup"><span data-stu-id="15fa5-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="15fa5-134">Konsol düzenlenmiş ve ancak istediğiniz konumlandırılmış bir Visual Studio penceredir (bkz [Visual Studio'da pencere düzenlerini özelleştirme](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="15fa5-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="15fa5-135">Varsayılan olarak, Konsolu komutları, pencerenin üstündeki denetim kümesinde olarak belirli bir paket kaynağı ve proje karşı çalışır:</span><span class="sxs-lookup"><span data-stu-id="15fa5-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket kaynağı ve proje için Paket Yöneticisi konsolu denetimleri](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="15fa5-137">Farklı bir paket kaynağı ve/veya proje seçme sonraki komutları için bu varsayılan ayarları değiştirir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="15fa5-138">Overrride için varsayılanları değiştirmeden bu ayarları çoğu komut desteği `-Source` ve `-ProjectName` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="15fa5-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="15fa5-139">Paket kaynaklarını yönetmek için dişli simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="15fa5-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="15fa5-140">Bu kısayoludur **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını** açıklandığı gibi iletişim kutusu [Paket Yöneticisi kullanıcı Arabirimi](Package-Manager-UI.md#package-sources) sayfası.</span><span class="sxs-lookup"><span data-stu-id="15fa5-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="15fa5-141">Ayrıca, proje Seçici sağındaki denetim konsolun içeriği temizler:</span><span class="sxs-lookup"><span data-stu-id="15fa5-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Paket Yöneticisi konsolu ayarları ve denetimleri Temizle](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="15fa5-143">Sağdaki düğme uzun süre çalışan komutunu keser.</span><span class="sxs-lookup"><span data-stu-id="15fa5-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="15fa5-144">Örneğin, çalışan `Get-Package -ListAvailable -PageSize 500` çalıştırmak için birkaç dakika sürebilir (örneğin, nuget.org), varsayılan kaynak üst 500 paketlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket Yöneticisi konsolu durdurma denetimi](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="15fa5-146">Bir paketi yükleniyor</span><span class="sxs-lookup"><span data-stu-id="15fa5-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="15fa5-147">Bkz: [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="15fa5-148">Bir paketi yüklerken aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="15fa5-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="15fa5-149">Geçerli lisans şartları zımni Sözleşmesi ile Konsol penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="15fa5-150">Koşulları kabul etmiyorsanız, paketi hemen kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="15fa5-151">Her başvuru biçimi kullanımda içinde projesine bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="15fa5-152">Başvuruları daha sonra Çözüm Gezgini ve geçerli başvuru biçim dosyası görünür.</span><span class="sxs-lookup"><span data-stu-id="15fa5-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="15fa5-153">Ancak, doğrudan proje dosyasındaki değişiklikleri görmek için projeyi kaydedin gerek PackageReference ile unutmayın.</span><span class="sxs-lookup"><span data-stu-id="15fa5-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="15fa5-154">Paketi önbelleğe alır:</span><span class="sxs-lookup"><span data-stu-id="15fa5-154">Caches the package:</span></span>
    - <span data-ttu-id="15fa5-155">PackageReference: Paket konumundaki önbelleğe alınmış `%USERPROFILE%\.nuget\packages` ve kilidi dosya yani `project.assets.json` güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="15fa5-156">`packages.config`: oluşturur bir `packages` klasör paketi dosyalarını içindeki bir alt klasör içine çözüm kök ve kopyalar.</span><span class="sxs-lookup"><span data-stu-id="15fa5-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="15fa5-157">`package.config` Dosya güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="15fa5-158">Güncelleştirmeleri `app.config` ve/veya `web.config` paketi kullanıyorsa [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="15fa5-159">Henüz yoksa projedeki tüm bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="15fa5-160">Bu paket işleminde, açıklandığı gibi güncelleştirme sürümleri [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="15fa5-161">Paketin Benioku dosyası varsa, bir Visual Studio penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15fa5-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="15fa5-162">Paketleri yükleme birincil yararlarından biri `Install-Package` konsolunda komuttur Paket Yöneticisi kullanıcı Arabirimi kullandığınız sanki projesine bir başvuru ekleyen.</span><span class="sxs-lookup"><span data-stu-id="15fa5-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="15fa5-163">Buna karşılık, `nuget install` CLI komutu yalnızca paketi indirir ve otomatik olarak bir başvuru eklemez.</span><span class="sxs-lookup"><span data-stu-id="15fa5-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="15fa5-164">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="15fa5-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="15fa5-165">Bkz: [kaldırma paket](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="15fa5-166">Kullanım [Get-Package](../tools/ps-ref-get-package.md) tanımlayıcı bulmanız gerekiyorsa varsayılan projede yüklü tüm paketler görmek için.</span><span class="sxs-lookup"><span data-stu-id="15fa5-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="15fa5-167">Bir paketi aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="15fa5-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="15fa5-168">Proje (ve her başvuru biçimi kullanımda) paket başvuruları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="15fa5-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="15fa5-169">Başvurular, Çözüm Gezgini'nde artık görünür.</span><span class="sxs-lookup"><span data-stu-id="15fa5-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="15fa5-170">(Kaldırılmasını görmek için projeyi yeniden oluşturmanız gerekebilir **Bin** klasörü.)</span><span class="sxs-lookup"><span data-stu-id="15fa5-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="15fa5-171">Yapılan değişiklikleri geri alır `app.config` veya `web.config` paketin ne zaman yüklendi.</span><span class="sxs-lookup"><span data-stu-id="15fa5-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="15fa5-172">Bu bağımlılıklar hiçbir kalan paketleri kullanıyorsanız, önceden yüklenmiş kaldırır bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="15fa5-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="15fa5-173">Gibi `Install-Package`, `Uninstall-Package` komutu aksine projedeki başvuruları yönetme avantajına sahiptir `nuget uninstall` CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="15fa5-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="15fa5-174">Paket güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="15fa5-174">Updating a package</span></span>

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

<span data-ttu-id="15fa5-175">Bkz: [Get-Package](../tools/ps-ref-get-package.md) ve [güncelleştirme paketi](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="15fa5-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="15fa5-176">Bir paket bulma</span><span class="sxs-lookup"><span data-stu-id="15fa5-176">Finding a package</span></span>

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

<span data-ttu-id="15fa5-177">Bkz: [Bul paket](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="15fa5-178">Visual Studio 2013 ve önceki sürümlerinde kullanmak [Get-Package](../tools/ps-ref-get-package.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="15fa5-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="15fa5-179">Konsolunun kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="15fa5-179">Availability of the console</span></span>

<span data-ttu-id="15fa5-180">Visual Studio 2017 içinde NuGet ve NuGet Paket Yöneticisi herhangi seçtiğinizde otomatik olarak yüklenir. NET ilgili iş yükleri; Ayrıca ayrı ayrı kontrol ederek yükleyebilirsiniz **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi** Visual Studio 2017 yükleyici seçeneği.</span><span class="sxs-lookup"><span data-stu-id="15fa5-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="15fa5-181">Ayrıca, Visual Studio 2015 ve daha önce NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  NuGet Paket Yöneticisi uzantısı arayın.</span><span class="sxs-lookup"><span data-stu-id="15fa5-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="15fa5-182">Visual Studio Uzantıları yükleyici yapamıyorsanız doğrudan uzantısı indirebilirsiniz [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="15fa5-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="15fa5-183">Paket Yöneticisi konsolu, Visual Studio for Mac ile şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="15fa5-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="15fa5-184">Eşdeğer komutları ancak aracılığıyla kullanılabilir [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="15fa5-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="15fa5-185">Mac için Visual Studio, NuGet paketlerini yönetmek için bir kullanıcı Arabirimi yok.</span><span class="sxs-lookup"><span data-stu-id="15fa5-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="15fa5-186">Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="15fa5-186">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="15fa5-187">Paket Yöneticisi konsolu ile Visual Studio Code dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="15fa5-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="15fa5-188">Paket Yöneticisi konsolu genişletme</span><span class="sxs-lookup"><span data-stu-id="15fa5-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="15fa5-189">Bazı paketler yeni komutları Konsolu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="15fa5-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="15fa5-190">Örneğin, `MvcScaffolding` gibi komutları oluşturur `Scaffold` aşağıda gösterilen, oluşturur ASP.NET MVC denetleyicileri ve görünümler:</span><span class="sxs-lookup"><span data-stu-id="15fa5-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Yükleme ve MvcScaffold kullanma](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="15fa5-192">Bir NuGet PowerShell profili ayarlama</span><span class="sxs-lookup"><span data-stu-id="15fa5-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="15fa5-193">Bir PowerShell profili, PowerShell kullandığınız her yerde sık kullanılan komutlar kullanılabilir kılmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="15fa5-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="15fa5-194">NuGet genellikle aşağıdaki konumda bulunan NuGet özgü bir profili destekler:</span><span class="sxs-lookup"><span data-stu-id="15fa5-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="15fa5-195">Profil bulmak için şunu yazın `$profile` konsolunda:</span><span class="sxs-lookup"><span data-stu-id="15fa5-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="15fa5-196">Daha fazla ayrıntı için başvurmak [Windows PowerShell profilleri](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="15fa5-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
