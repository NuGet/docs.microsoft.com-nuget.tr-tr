---
title: Visual Studio'da NuGet paketlerini yükleyin ve yönetin
description: NuGet paketleri ile çalışmak için Visual Studio'da NuGet Paket Yöneticisi UI'yi kullanma talimatları.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428697"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="f3846-103">NuGet Paket Yöneticisi'ni kullanarak Visual Studio'da paketleri yükleyin ve yönetin</span><span class="sxs-lookup"><span data-stu-id="f3846-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="f3846-104">Windows'daki Visual Studio'daki NuGet Paket Yöneticisi Kullanıcı UI, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncellemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f3846-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f3846-105">Mac için Visual Studio'daki deneyim için, [projenize bir NuGet paketi dahil etme](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)hakkında bakınız.</span><span class="sxs-lookup"><span data-stu-id="f3846-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="f3846-106">Paket Yöneticisi UI Visual Studio Code ile birlikte değildir.</span><span class="sxs-lookup"><span data-stu-id="f3846-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="f3846-107">Visual Studio 2015'te NuGet Paket Yöneticisi'ni kaçırıyorsanız, **Araçlar > Uzantıları ve Güncellemeler...'ı** kontrol edin ve *NuGet Paket Yöneticisi* uzantısını arayın.</span><span class="sxs-lookup"><span data-stu-id="f3846-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="f3846-108">Visual Studio'daki uzantıları yükleyicisi kullanamıyorsanız, uzantıyı [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)doğrudan 'den indirin.</span><span class="sxs-lookup"><span data-stu-id="f3846-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="f3846-109">Visual Studio 2017'den itibaren NuGet ve NuGet Paket Yöneticisi otomatik olarak herhangi bir . NET ile ilgili iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="f3846-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="f3846-110">Visual Studio yükleyicisinde **NuGet paket yöneticisi** seçeneği > Tek tek bileşenleri > Kod araçlarını seçerek tek tek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3846-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="f3846-111">Bir paket bulma ve yükleme</span><span class="sxs-lookup"><span data-stu-id="f3846-111">Find and install a package</span></span>

1. <span data-ttu-id="f3846-112">**Çözüm Gezgini'nde,** **Referanslar** veya proje için sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin...**</span><span class="sxs-lookup"><span data-stu-id="f3846-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet Paketleri menüsü seçeneğini yönetin](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="f3846-114">**Gözat** sekmesi paketleri şu anda seçili kaynaktan popülerlik olarak görüntüler [(paket kaynaklarına](#package-sources)bakın).</span><span class="sxs-lookup"><span data-stu-id="f3846-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="f3846-115">Sol üstteki arama kutusunu kullanarak belirli bir paketi arayın.</span><span class="sxs-lookup"><span data-stu-id="f3846-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="f3846-116">Bilgilerini görüntülemek için listeden bir paket seçin ve **Install** bu da sürüm seçimi açılır bırakma düğmesini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f3846-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet Paketleri İletişim Sekmesini Yönet](media/Search.png)

1. <span data-ttu-id="f3846-118">Açılan açılır dan istenilen sürümü seçin ve **Yükle'yi**seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="f3846-119">Visual Studio paketi ve bağımlılıklarını projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="f3846-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="f3846-120">Lisans koşullarını kabul etmeniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="f3846-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="f3846-121">Yükleme tamamlandığında, eklenen paketler **Yüklenen** sekmesinde görünür. Paketler, Çözüm Gezgini'nin **Başvuru düğümünde** de listelenir ve bu `using` da projede deyimlerle bunlara başvurabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="f3846-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Çözüm Gezgini'ndeki Referanslar](media/References.png)

> [!Tip]
> <span data-ttu-id="f3846-123">Aramada ön sürüm sürümlerini eklemek ve sürüm açılır sürümünde ön sürüm sürümlerini kullanılabilir hale getirmek **için, ön sürüm ekle** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f3846-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="f3846-124">NuGet,bir projenin paketleri kullanabileceği iki biçimi [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)vardır: ve .</span><span class="sxs-lookup"><span data-stu-id="f3846-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="f3846-125">[Varsayılan değer Visual Studio'nun seçenekler penceresinde ayarlanabilir.](Package-Restore.md#choose-default-package-management-format)</span><span class="sxs-lookup"><span data-stu-id="f3846-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="f3846-126">Paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="f3846-126">Uninstall a package</span></span>

1. <span data-ttu-id="f3846-127">**Çözüm Gezgini'nde,** **Referanslar'a** veya istenilen projeye sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin... seçeneğini belirleyin.**</span><span class="sxs-lookup"><span data-stu-id="f3846-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f3846-128">**Yüklü öğeler** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="f3846-129">Kaldırmak için paketi seçin (gerekirse listeye filtre lemek için aramayı kullanarak) ve **Kaldır'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Paketi kaldırma](media/UninstallPackage.png)

1. <span data-ttu-id="f3846-131">**Paketleri** yüklerken Ön Sürüm Ekle ve **Paket kaynak** denetimleri üzerinde hiçbir etkisi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f3846-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="f3846-132">Paketi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f3846-132">Update a package</span></span>

1. <span data-ttu-id="f3846-133">**Çözüm Gezgini'nde,** **Referanslar'a** veya istenilen projeye sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin... seçeneğini belirleyin.** (Web sitesi projelerinde, **Bin** klasörüne sağ tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="f3846-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="f3846-134">Seçili paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için **Güncelleştirmeler** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="f3846-135">Güncelleştirme listesine yayın öncesi paketleri eklemek için yayın öncesi paketleri **ekle'yi** seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="f3846-136">Güncellemek için paketi seçin, sağdaki açılır yerden istenen sürümü seçin ve **Güncelleştir'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Paketi güncelleştirme](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="f3846-138">Bazı paketler için **Güncelleştirme** düğmesi devre dışı bırakılır ve "Örtülü olarak bir SDK tarafından başvurulan" (veya "AutoReferenced") olduğunu belirten bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f3846-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="f3846-139">Bu ileti, paketin daha büyük bir çerçevenin veya SDK'nın bir parçası olduğunu ve bağımsız olarak güncelleştirilmemesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f3846-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="f3846-140">(Bu tür paketler dahili olarak `<IsImplicitlyDefined>True</IsImplicitlyDefined>`işaretlenir.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK'nın bir parçasıdır ve paket sürümü, uygulama tarafından kullanılan çalışma zamanı çerçevesinin sürümüyle aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="f3846-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="f3846-141">ASP.NET Core ve .NET Core çalışma zamanının yeni sürümlerini almak için [.NET Core yüklemenizi güncelleştirmeniz](https://aka.ms/dotnet-download) gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3846-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="f3846-142">[.NET Core metapackages ve sürüm hakkında daha fazla bilgi için bu belgeye bakın.](/dotnet/core/packages)</span><span class="sxs-lookup"><span data-stu-id="f3846-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="f3846-143">Bu, sık kullanılan aşağıdaki paketler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="f3846-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="f3846-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="f3846-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="f3846-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="f3846-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="f3846-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="f3846-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="f3846-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="f3846-147">NETStandard.Library</span></span>

    ![Dolaylı referanslar veya AutoReferenced olarak işaretlenmiş örnek paket](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="f3846-149">Birden çok paketi en yeni sürümlerinde güncelleştirmek için, bunları listede seçin ve listenin üstündeki **Güncelleştir** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="f3846-150">Yüklü sekmesinden tek bir paketi de **güncelleştirebilirsiniz.** Bu durumda, paketin ayrıntıları bir sürüm seçici **(Ön sürüm ekle** seçeneğine tabidir) ve Güncelleştirme düğmesini içerir. **Update**</span><span class="sxs-lookup"><span data-stu-id="f3846-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="f3846-151">Çözüm için paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f3846-151">Manage packages for the solution</span></span>

<span data-ttu-id="f3846-152">Bir çözüm için paketleri yönetmek, aynı anda birden fazla projeyle çalışmak için kullanışlı bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="f3846-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="f3846-153">**NuGet Paket Yöneticisi > Paketleri Çözüm için Yönet' > Araçlar'ı seçin...** menü komutu veya çözüme sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin...**</span><span class="sxs-lookup"><span data-stu-id="f3846-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Çözüm için NuGet paketlerini yönetin](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="f3846-155">Çözüm için paketleri yönetirken, UI operasyonlardan etkilenen projeleri seçmenize olanak tanır:</span><span class="sxs-lookup"><span data-stu-id="f3846-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Çözüm için paketleri yönetirken proje seçici](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="f3846-157">Sekmeyi birleştir</span><span class="sxs-lookup"><span data-stu-id="f3846-157">Consolidate tab</span></span>

<span data-ttu-id="f3846-158">Geliştiriciler genellikle aynı çözümde farklı projeler arasında aynı NuGet paketinin farklı sürümlerini kullanmanın kötü bir uygulama olduğunu düşünür.</span><span class="sxs-lookup"><span data-stu-id="f3846-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="f3846-159">Bir çözüm için paketleri yönetmeyi seçtiğinizde, Paket Yöneticisi Kullanıcı Arabirimi, farklı sürüm numaralarına sahip paketlerin çözümde farklı projeler tarafından nerede kullanıldığını kolayca görebileceğiniz bir **Birleştirme** sekmesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="f3846-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Paket Yöneticisi UI Birleştirme sekmesi](media/ConsolidateTab.png)

<span data-ttu-id="f3846-161">Bu örnekte, ClassLibrary1 projesi EntityFramework 6.2.0 kullanırken, ConsoleApp1 EntityFramework 6.1.0'ı kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f3846-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="f3846-162">Paket sürümlerini birleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="f3846-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="f3846-163">Proje listesinde güncelleştirilecek projeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="f3846-164">EntityFramework 6.2.0 gibi **Sürüm** denetimindeki tüm bu projelerde kullanılacak sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="f3846-165">**Yükle** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-165">Select the **Install** button.</span></span>

<span data-ttu-id="f3846-166">Paket Yöneticisi, seçili paket sürümünü seçili tüm projelere yükler ve ardından paket **Birleştirme** sekmesinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="f3846-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="f3846-167">Paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="f3846-167">Package sources</span></span>

<span data-ttu-id="f3846-168">Visual Studio'nun paketleri aldığı kaynağı değiştirmek için kaynak seçiciden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="f3846-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Paket yöneticisi UI'deki paket kaynak seçici](media/PackageSourceDropDown.png)

<span data-ttu-id="f3846-170">Paket kaynaklarını yönetmek için:</span><span class="sxs-lookup"><span data-stu-id="f3846-170">To manage package sources:</span></span>

1. <span data-ttu-id="f3846-171">Aşağıda özetlenen Paket Yöneticisi UI'deki **Ayarlar** simgesini seçin veya **Araçlar > Seçenekleri** komutunu kullanın ve **NuGet Paket Yöneticisi'ne**gidin:</span><span class="sxs-lookup"><span data-stu-id="f3846-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Paket yöneticisi UI ayarları simgesi](media/PackageSourceSettings.png)

1. <span data-ttu-id="f3846-173">Paket **Kaynakları** düğümünü seçin:</span><span class="sxs-lookup"><span data-stu-id="f3846-173">Select the **Package Sources** node:</span></span>

    ![Paket Kaynakları seçenekleri](media/options.png)

1. <span data-ttu-id="f3846-175">Kaynak eklemek için, **+** adı seçin, adı seçin, **Kaynak** denetimine URL'yi veya yolu girin ve **Güncelleştir'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="f3846-176">Kaynak şimdi seçici açılır açılır görünür.</span><span class="sxs-lookup"><span data-stu-id="f3846-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="f3846-177">Paket kaynağını değiştirmek için, onu seçin, **Ad** ve **Kaynak** kutularında değişiklikler yapın ve **Güncelleştir'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="f3846-178">Paket kaynağını devre dışı kalmak için listedeki adın solundaki kutuyu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="f3846-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="f3846-179">Bir paket kaynağını kaldırmak için, onu seçin ve ardından **X** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="f3846-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="f3846-180">Yukarı ve aşağı ok düğmelerini kullanmak paket kaynaklarının öncelik sırasını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="f3846-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="f3846-181">Visual Studio, isteklere yanıt vermek için ilk hangi kaynaktan gelen paketi kullanarak paket kaynaklarının sırasını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="f3846-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="f3846-182">Daha fazla bilgi için [Paket geri yükleme'ye](../consume-packages/package-restore.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="f3846-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="f3846-183">Bir paket kaynağı siledikten sonra yeniden görünürse, bilgisayar düzeyinde veya kullanıcı `NuGet.Config` düzeyindeki dosyalarda listelenebilir.</span><span class="sxs-lookup"><span data-stu-id="f3846-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="f3846-184">Bu dosyaların konumu için [Ortak NuGet yapılandırmalarına](../consume-packages/configuring-nuget-behavior.md) bakın, ardından dosyaları el ile düzenleyerek veya [nuget kaynakları komutunu](../reference/nuget-exe-CLI-reference.md)kullanarak kaynağı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f3846-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="f3846-185">Paket yöneticisi Seçenekleri kontrolü</span><span class="sxs-lookup"><span data-stu-id="f3846-185">Package manager Options control</span></span>

<span data-ttu-id="f3846-186">Bir paket seçildiğinde, Paket Yöneticisi UI sürüm seçicinin altında küçük, genişletilebilir **seçenekler** denetimini görüntüler (burada hem daraltılmış hem de genişletilmiş olarak gösterilir).</span><span class="sxs-lookup"><span data-stu-id="f3846-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="f3846-187">Bazı proje türleri için yalnızca **Önizleme penceresini göster** seçeneğinin sağlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f3846-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Paket yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

<span data-ttu-id="f3846-189">Aşağıdaki bölümlerde bu seçenekleri açıklayınız.</span><span class="sxs-lookup"><span data-stu-id="f3846-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="f3846-190">Önizleme penceresini göster</span><span class="sxs-lookup"><span data-stu-id="f3846-190">Show preview window</span></span>

<span data-ttu-id="f3846-191">Seçildiğinde, bir modal pencere, seçilen paketin paket yüklenmeden önceki bağımlılıklarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f3846-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Örnek Önizleme İletişim](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="f3846-193">Yükleme ve Güncelleştirme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f3846-193">Install and Update Options</span></span>

<span data-ttu-id="f3846-194">(Tüm proje türleri için kullanılamaz.)</span><span class="sxs-lookup"><span data-stu-id="f3846-194">(Not available for all project types.)</span></span>

<span data-ttu-id="f3846-195">**Bağımlılık davranışı,** NuGet'in bağımlı paketlerin hangi sürümlerini yükleyeceklerine nasıl karar vereceğine göre yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="f3846-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="f3846-196">*Bağımlılıkları yoksay,* genellikle yüklenen paketi bozan bağımlılıkları yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="f3846-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="f3846-197">*En Düşük* [Varsayılan] bağımlılığı, birincil seçilen paketin gereksinimlerini karşılayan en az sürüm numarasıyla yükler.</span><span class="sxs-lookup"><span data-stu-id="f3846-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="f3846-198">*En Yüksek Yama,* sürümü aynı büyük ve küçük sürüm numaralarına, ancak en yüksek yama numarasına sahip olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="f3846-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="f3846-199">Örneğin, sürüm 1.2.2 belirtilirse, 1.2 ile başlayan en yüksek sürüm yüklenir</span><span class="sxs-lookup"><span data-stu-id="f3846-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="f3846-200">*En Yüksek Minor* aynı ana sürüm numarasına, ancak en yüksek küçük sayı ve yama numarasına sahip sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="f3846-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="f3846-201">Sürüm 1.2.2 belirtilirse, 1 ile başlayan en yüksek sürüm yüklenir</span><span class="sxs-lookup"><span data-stu-id="f3846-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="f3846-202">*En yüksek* paket, paketin mevcut en yüksek sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="f3846-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="f3846-203">**Dosya çakışması eylemi,** NuGet'in projede veya yerel makinede zaten var olan paketleri nasıl işlemesi gerektiğini belirtir:</span><span class="sxs-lookup"><span data-stu-id="f3846-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="f3846-204">*İstem,* NuGet'e varolan paketleri tutup tutmamayı veya üzerine yazıp yazmamayı sormasını ister.</span><span class="sxs-lookup"><span data-stu-id="f3846-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="f3846-205">Tüm tüm yetkileri *yoksayın* NuGet varolan paketlerin üzerine yazmayı atlamak için.</span><span class="sxs-lookup"><span data-stu-id="f3846-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="f3846-206">*Tüm Bunların Üzerine Yazın* NuGet'in varolan paketlerin üzerine yazmasını emreder.</span><span class="sxs-lookup"><span data-stu-id="f3846-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="f3846-207">Seçenekleri Kaldır</span><span class="sxs-lookup"><span data-stu-id="f3846-207">Uninstall Options</span></span>

<span data-ttu-id="f3846-208">(Tüm proje türleri için kullanılamaz.)</span><span class="sxs-lookup"><span data-stu-id="f3846-208">(Not available for all project types.)</span></span>

<span data-ttu-id="f3846-209">**Bağımlılıkları kaldırın**: seçildiğinde, projenin başka bir yerinde başvurulmuyorsa bağımlı paketleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f3846-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="f3846-210">**Bağımlılıklar olsa bile kaldırmayı zorlayın:** seçildiğinde, projede hala başvurulmakta olsa bile paketi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f3846-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="f3846-211">Bu genellikle bir paketi kaldırmak için **kaldır bağımlılıkları** ve yüklü ne olursa olsun bağımlılıkları ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f3846-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="f3846-212">Ancak, bu seçeneğin kullanılması projede bozuk başvurulara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f3846-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="f3846-213">Bu gibi durumlarda, [bu diğer paketleri yeniden yüklemeniz](../consume-packages/reinstalling-and-updating-packages.md)gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f3846-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
