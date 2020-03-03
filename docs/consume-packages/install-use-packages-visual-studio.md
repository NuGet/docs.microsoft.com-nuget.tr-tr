---
title: Visual Studio 'da NuGet paketlerini yükleyip yönetme
description: NuGet paketleri ile çalışma için Visual Studio 'da NuGet Paket Yöneticisi Kullanıcı arabirimini kullanmaya yönelik yönergeler.
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
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231013"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="dc4ae-103">NuGet Paket Yöneticisi 'Ni kullanarak Visual Studio 'da paket yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="dc4ae-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="dc4ae-104">Windows üzerinde Visual Studio 'daki NuGet Paket Yöneticisi Kullanıcı arabirimi, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncelleştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="dc4ae-105">Mac için Visual Studio deneyim için, bkz. [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="dc4ae-106">Paket Yöneticisi Kullanıcı arabirimi Visual Studio Code dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="dc4ae-107">Visual Studio 2015 ' de NuGet Paket Yöneticisi eksik ise **araçlar > Uzantılar ve güncelleştirmeler...** ' ı Işaretleyin ve *NuGet Paket Yöneticisi* uzantısını arayın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="dc4ae-108">Visual Studio 'da uzantılar yükleyicisini kullandıysanız, uzantıyı doğrudan [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)' den indirin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="dc4ae-109">Visual Studio 2017 ' den başlayarak NuGet ve NuGet Paket Yöneticisi ile birlikte otomatik olarak yüklenir. NET ilgili iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="dc4ae-110">Visual Studio yükleyicisindeki **tek tek bileşenler > kod araçları > NuGet Paket Yöneticisi** seçeneğini seçerek tek tek yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="dc4ae-111">Paket bulma ve yüklemeyi</span><span class="sxs-lookup"><span data-stu-id="dc4ae-111">Find and install a package</span></span>

1. <span data-ttu-id="dc4ae-112">**Çözüm Gezgini**, **başvuruya** veya bir projeye sağ tıklayın ve **NuGet Paketlerini Yönet..**. seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet Paketlerini Yönet menü seçeneği](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="dc4ae-114">**Gözden** geçirme sekmesi, paketleri şu anda seçili olan kaynaktan popülerlik olarak görüntüler (bkz. [paket kaynakları](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="dc4ae-115">Sol üstteki arama kutusunu kullanarak belirli bir paketi arayın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="dc4ae-116">Bilgileri göstermek için listeden bir paket seçin. Bu, Ayrıca, bir sürüm seçimi açılır ile birlikte de **Install** düğmesine de olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet Paketlerini Yönet Iletişim kutusu tarama sekmesi](media/Search.png)

1. <span data-ttu-id="dc4ae-118">Açılan listeden istediğiniz **sürümü seçin ve**ardından Kaldır ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="dc4ae-119">Visual Studio, paketi ve bağımlılıklarını projeye kurar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="dc4ae-120">Lisans koşullarını kabul etmeniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="dc4ae-121">Yükleme tamamlandığında, eklenen paketler **yüklü** sekmesinde görünür. paketler ayrıca, Çözüm Gezgini **Başvurular** düğümünde listelenir ve bu, bunlara `using` deyimleriyle projede başvurabileceğiniz anlamına gelen.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Çözüm Gezgini başvurular](media/References.png)

> [!Tip]
> <span data-ttu-id="dc4ae-123">Aramaya yayın öncesi sürümleri eklemek ve sürüm açılır penceresinde ön sürüm sürümlerini kullanabilmek için, **ön sürümü dahil et** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="dc4ae-124">NuGet, bir projenin paketleri kullanabileceği iki biçimi vardır: [`PackageReference`](package-references-in-project-files.md) ve [`packages.config`](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="dc4ae-125">[Varsayılan, Visual Studio 'nun seçenekler penceresinde ayarlanabilir](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="dc4ae-126">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="dc4ae-126">Uninstall a package</span></span>

1. <span data-ttu-id="dc4ae-127">**Çözüm Gezgini**, **başvuruya** veya istenen projeye sağ tıklayın ve **NuGet Paketlerini Yönet...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dc4ae-128">**Yüklü öğeler** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="dc4ae-129">Kaldırılacak paketi seçin (gerekirse listeyi filtrelemek için arama ' yı kullanarak) ve **Kaldır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Paket kaldırılıyor](media/UninstallPackage.png)

1. <span data-ttu-id="dc4ae-131">Paket kaldırılırken, **ön sürümü** ve **paket kaynak** denetimlerinin dahil edileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="dc4ae-132">Bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="dc4ae-132">Update a package</span></span>

1. <span data-ttu-id="dc4ae-133">**Çözüm Gezgini**, **başvuruya** veya istenen projeye sağ tıklayın ve **NuGet Paketlerini Yönet...** seçeneğini belirleyin. (Web sitesi projelerinde **bin** klasörüne sağ tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="dc4ae-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="dc4ae-134">Seçilen paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için **güncelleştirmeler** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="dc4ae-135">Güncelleştirme listesine yayın öncesi paketleri dahil etmek için **ön sürümü dahil et** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="dc4ae-136">Güncelleştirilecek paketi seçin, sağ taraftaki açılan listeden istediğiniz sürümü seçin ve **Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Paket güncelleştiriliyor](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="dc4ae-138">Bazı paketlerde **Güncelleştir** düğmesi devre dışıdır ve "bir SDK tarafından örtük olarak başvurulduğunu" (veya "Oto başvurulan") bildiren bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="dc4ae-139">Bu ileti, paketin daha büyük bir Framework veya SDK 'nın parçası olduğunu ve bağımsız olarak güncelleştirilmemiş olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="dc4ae-140">(Bu tür paketler dahili olarak `<IsImplicitlyDefined>True</IsImplicitlyDefined>`olarak işaretlenir.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK bir parçasıdır ve paket sürümü, uygulama tarafından kullanılan çalışma zamanı çerçevesinin sürümü ile aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="dc4ae-141">ASP.NET Core ve .NET Core çalışma zamanının yeni sürümlerini almak için [.NET Core yüklemenizi güncelleştirmeniz](https://aka.ms/dotnet-download) gerekir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="dc4ae-142">[.NET Core Metapackages ve sürüm oluşturma hakkında daha fazla bilgi için bu belgeye bakın](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="dc4ae-143">Bu, aşağıdaki yaygın olarak kullanılan paketler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="dc4ae-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="dc4ae-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="dc4ae-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="dc4ae-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="dc4ae-146">Microsoft. NETCore. app</span><span class="sxs-lookup"><span data-stu-id="dc4ae-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="dc4ae-147">NETStandard. Library</span><span class="sxs-lookup"><span data-stu-id="dc4ae-147">NETStandard.Library</span></span>

    ![Örtülü başvurular veya oto başvurulan olarak işaretlenen örnek paket](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="dc4ae-149">Birden çok paketi en yeni sürümlerine güncelleştirmek için listeden seçin ve listenin üzerindeki **Güncelleştir** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="dc4ae-150">Ayrıca, **yüklü** sekmesinden tek bir paketi de güncelleştirebilirsiniz. Bu durumda, paketin ayrıntıları bir sürüm seçici ( **ön sürümü dahil et** seçeneğine tabidir) ve bir **Güncelleştir** düğmesi içerir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="dc4ae-151">Çözüm için paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="dc4ae-151">Manage packages for the solution</span></span>

<span data-ttu-id="dc4ae-152">Bir çözüm için paketlerin yönetilmesi, birden çok projeyle aynı anda çalışması için uygun bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="dc4ae-153">**NuGet paket yöneticisi > araçlar > çözüm Için NuGet Paketlerini Yönet..** . menü komutunu seçin veya çözüme sağ tıklayıp **NuGet Paketlerini Yönet..**. öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Çözüm için NuGet Paketlerini Yönet](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="dc4ae-155">Çözüm için paketleri yönetirken, Kullanıcı arabirimi işlemlerden etkilenen projeleri seçmenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Çözüm için paketleri yönetirken proje Seçicisi](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="dc4ae-157">Birleştirme sekmesi</span><span class="sxs-lookup"><span data-stu-id="dc4ae-157">Consolidate tab</span></span>

<span data-ttu-id="dc4ae-158">Geliştiriciler tipik olarak aynı NuGet paketinin farklı sürümlerini aynı çözümde farklı projeler arasında kullanmak için kötü bir uygulama ele alalım.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="dc4ae-159">Bir çözüm için paketleri yönetmeyi seçtiğinizde, Paket Yöneticisi Kullanıcı arabirimi, farklı sürüm numaralarına sahip paketlerin çözümdeki farklı projeler tarafından kullanıldığı yerleri kolayca görebileceğiniz bir **birleştirme** sekmesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Paket Yöneticisi UI birleştirme sekmesi](media/ConsolidateTab.png)

<span data-ttu-id="dc4ae-161">Bu örnekte, ClassLibrary1 projesi EntityFramework 6.2.0 kullanıyor, ancak ConsoleApp1 EntityFramework 6.1.0 kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="dc4ae-162">Paket sürümlerini birleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="dc4ae-163">Proje listesinde güncelleştirilecek projeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="dc4ae-164">**Sürüm** denetimindeki tüm projelerde kullanılacak sürümü (EntityFramework 6.2.0 gibi) seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="dc4ae-165">**Install** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-165">Select the **Install** button.</span></span>

<span data-ttu-id="dc4ae-166">Paket Yöneticisi seçili paket sürümünü seçili tüm projelere yükleyerek, bu paket artık **birleştirme** sekmesinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="dc4ae-167">Paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="dc4ae-167">Package sources</span></span>

<span data-ttu-id="dc4ae-168">Visual Studio 'Nun paketleri alacağı kaynağı değiştirmek için kaynak seçiciden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Paket Yöneticisi Kullanıcı arabiriminde paket kaynak Seçicisi](media/PackageSourceDropDown.png)

<span data-ttu-id="dc4ae-170">Paket kaynaklarını yönetmek için:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-170">To manage package sources:</span></span>

1. <span data-ttu-id="dc4ae-171">Aşağıda belirtilen Paket Yöneticisi Kullanıcı arabirimindeki **Ayarlar** simgesini seçin veya **Araçlar > Seçenekler** komutunu kullanın ve **NuGet Paket Yöneticisi**' ne kaydırın:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Paket Yöneticisi Kullanıcı arabirimi ayarları simgesi](media/PackageSourceSettings.png)

1. <span data-ttu-id="dc4ae-173">**Paket kaynakları** düğümünü seçin:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-173">Select the **Package Sources** node:</span></span>

    ![Paket kaynakları seçenekleri](media/options.png)

1. <span data-ttu-id="dc4ae-175">Kaynak eklemek için **+** seçin, adı düzenleyin, **kaynak** denetimine URL veya yol girin ve **Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="dc4ae-176">Kaynak artık seçici açılan penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="dc4ae-177">Bir paket kaynağını değiştirmek için, seçin, **ad** ve **kaynak** kutularında düzenlemeler yapın ve **Güncelleştir**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="dc4ae-178">Bir paket kaynağını devre dışı bırakmak için listedeki adının solundaki kutuyu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="dc4ae-179">Bir paket kaynağını kaldırmak için, seçin ve sonra **X** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="dc4ae-180">Yukarı ve aşağı ok düğmelerinin kullanılması, paket kaynaklarının öncelik sırasını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="dc4ae-181">Visual Studio, isteklere yanıt vermek için ilk kaynak olan paketin kullanıldığı paket kaynaklarının sırasını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="dc4ae-182">Daha fazla bilgi için bkz. [paket geri yükleme](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="dc4ae-183">Bir paket kaynağı silindikten sonra yeniden görünürse, bilgisayar düzeyinde veya kullanıcı düzeyindeki `NuGet.Config` dosyalarında listelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="dc4ae-184">Bu dosyaların konumu için [ortak NuGet yapılandırmalarına](../consume-packages/configuring-nuget-behavior.md) bakın, ardından dosyaları el ile düzenleyerek veya [NuGet kaynakları komutunu](../reference/nuget-exe-CLI-reference.md)kullanarak kaynağı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="dc4ae-185">Paket Yöneticisi seçenekler denetimi</span><span class="sxs-lookup"><span data-stu-id="dc4ae-185">Package manager Options control</span></span>

<span data-ttu-id="dc4ae-186">Bir paket seçildiğinde, Paket Yöneticisi Kullanıcı arabirimi, sürüm seçicinin altında küçük, genişletilebilir bir **Seçenekler** denetimi görüntüler (burada hem daraltılmış hem de genişletilmiş olarak gösterilmiştir).</span><span class="sxs-lookup"><span data-stu-id="dc4ae-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="dc4ae-187">Bazı proje türleri için yalnızca **Önizleme penceresini göster** seçeneğinin sağlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Paket Yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

<span data-ttu-id="dc4ae-189">Aşağıdaki bölümlerde bu seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="dc4ae-190">Önizleme penceresini göster</span><span class="sxs-lookup"><span data-stu-id="dc4ae-190">Show preview window</span></span>

<span data-ttu-id="dc4ae-191">Seçildiğinde, bir kalıcı pencere, paket yüklenmeden önce seçilen bir paketin bağımlılıklarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Örnek önizleme Iletişim kutusu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="dc4ae-193">Yüklemeyi ve güncelleştirme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="dc4ae-193">Install and Update Options</span></span>

<span data-ttu-id="dc4ae-194">(Tüm proje türleri için kullanılamaz.)</span><span class="sxs-lookup"><span data-stu-id="dc4ae-194">(Not available for all project types.)</span></span>

<span data-ttu-id="dc4ae-195">**Bağımlılık davranışı** , NuGet 'in hangi bağımlı paket sürümlerinin yükleneceğini nasıl karar verdiği hakkında bir yapılandırma sağlar:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="dc4ae-196">*Bağımlılıkları yoksay* , genellikle yüklenen paketi kesen tüm bağımlılıkları yüklemeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="dc4ae-197">*En düşük* [varsayılan] bağımlılığı, seçilen birincil paketin gereksinimlerini karşılayan en az sürüm numarasıyla birlikte kurar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="dc4ae-198">*En yüksek düzeltme eki* , aynı büyük ve küçük sürüm numaralarına sahip sürümü, ancak en yüksek düzeltme eki numarasını yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="dc4ae-199">Örneğin, 1.2.2 sürümü belirtilmişse 1,2 ile başlayan en yüksek sürüm yüklenir</span><span class="sxs-lookup"><span data-stu-id="dc4ae-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="dc4ae-200">*En yüksek ikincil* sürüm, aynı ana sürüm numarası, ancak en yüksek küçük sayı ve düzeltme eki numarası ile birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="dc4ae-201">Sürüm 1.2.2 belirtilmişse, 1 ile başlayan en yüksek sürüm yüklenir</span><span class="sxs-lookup"><span data-stu-id="dc4ae-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="dc4ae-202">*En yüksek* paketin kullanılabilir en yüksek sürümünü yükleme.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="dc4ae-203">**Dosya çakışması eylemi** , NuGet 'in projede veya yerel makinede zaten var olan paketleri nasıl işleyeceğini belirtir:</span><span class="sxs-lookup"><span data-stu-id="dc4ae-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="dc4ae-204">*İstem* , NuGet 'e mevcut paketlerin tutulup tutulmayacağını veya üzerine yazılıp yazılmayacağını sorar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="dc4ae-205">*Tümünü Yoksay* , NuGet 'in varolan paketlerin üzerine yazılmasını atlayıp değiştirmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="dc4ae-206">*Tüm* mevcut paketlerin üzerine yazmak Için tüm NuGet 'e yazın.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="dc4ae-207">Kaldırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="dc4ae-207">Uninstall Options</span></span>

<span data-ttu-id="dc4ae-208">(Tüm proje türleri için kullanılamaz.)</span><span class="sxs-lookup"><span data-stu-id="dc4ae-208">(Not available for all project types.)</span></span>

<span data-ttu-id="dc4ae-209">**Bağımlılıkları kaldır**: seçildiğinde, tüm bağımlı paketleri projenin başka bir yerinde başvurulmuyorsa kaldırır.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="dc4ae-210">**Üzerinde bağımlılıklar olsa bile kaldırma Işlemini zorla**: seçildiğinde, hala projede başvuruluyorsa bile bir paketi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="dc4ae-211">Bu genellikle bir paketi kaldırmak için **bağımlılıkları kaldır** ile birlikte kullanılır ve bu, yüklü bağımlılıkları ve herhangi bir bağımlılığı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="dc4ae-212">Ancak bu seçeneğin kullanılması, projedeki bozuk başvurulara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="dc4ae-213">Bu gibi durumlarda, [diğer paketleri yeniden yüklemeniz](../consume-packages/reinstalling-and-updating-packages.md)gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dc4ae-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
