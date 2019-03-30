---
title: NuGet Paket Yöneticisi kullanıcı Arabirimi başvurusu
description: NuGet paketleri ile çalışmak için Visual Studio'da NuGet Paket Yöneticisi UI kullanarak yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 422faf99e58e058d86db774a8f3c1c576b3dc393
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637629"
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="45b28-103">NuGet Paket Yöneticisi UI</span><span class="sxs-lookup"><span data-stu-id="45b28-103">NuGet Package Manager UI</span></span>

<span data-ttu-id="45b28-104">Windows üzerinde Visual Studio'da NuGet Paket Yöneticisi UI kolayca yükleme, kaldırma ve projelerde ve çözümlerde NuGet paketlerini güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="45b28-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="45b28-105">Mac için Visual Studio deneyim için bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="45b28-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="45b28-106">Paket Yöneticisi UI, Visual Studio Code ile dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="45b28-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="45b28-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="45b28-107">In this topic:</span></span>

- [<span data-ttu-id="45b28-108">Bulma ve bir paket (Gözat sekmesi) yükleme</span><span class="sxs-lookup"><span data-stu-id="45b28-108">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="45b28-109">Bir paket (yüklü sekmesi) kaldırma</span><span class="sxs-lookup"><span data-stu-id="45b28-109">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="45b28-110">[Bir paket (yüklü ve güncelleştirmeleri sekmeleri) güncelleştirme](#updating-a-package) (içerir ["Örtük olarak bir SDK'sı tarafından başvurulan" veya "AutoReferenced" iletisi](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="45b28-110">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="45b28-111">[Çözüm için paketleri yönetme](#managing-packages-for-the-solution) (aynı anda birden fazla projeyle çalışma).</span><span class="sxs-lookup"><span data-stu-id="45b28-111">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="45b28-112">Paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="45b28-112">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="45b28-113">Paket Yöneticisi seçeneklerini denetleme</span><span class="sxs-lookup"><span data-stu-id="45b28-113">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="45b28-114">Visual Studio 2015'te NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  araması *NuGet Paket Yöneticisi* uzantısı.</span><span class="sxs-lookup"><span data-stu-id="45b28-114">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="45b28-115">Visual Studio Uzantıları yükleyici yapamıyorsanız doğrudan uzantısını [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="45b28-115">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="45b28-116">Visual Studio 2017'de NuGet ve NuGet Paket Yöneticisi otomatik olarak ile yüklenir. NET ilgili iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="45b28-116">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="45b28-117">Tek tek seçerek yüklemek **tek tek bileşenler > kod Araçlar > NuGet Paket Yöneticisi** Visual Studio 2017 yükleyicisindeki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="45b28-117">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="45b28-118">Bulma ve bir paket yükleme</span><span class="sxs-lookup"><span data-stu-id="45b28-118">Finding and installing a package</span></span>

1. <span data-ttu-id="45b28-119">İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya bir proje ve select **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="45b28-119">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Menü seçeneği NuGet paketlerini Yönet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="45b28-121">**Gözat** sekmesi seçili kaynaktan popülerliği tarafından paketleri görüntüler (bkz [paket kaynakları](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="45b28-121">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="45b28-122">Sol üst arama kutusunu kullanarak belirli bir paket için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="45b28-122">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="45b28-123">Ayrıca sağlar, bilgilerini görüntülemek için listeden bir paket seçin **yükleme** sürüm seçimi açılan listesi ile birlikte düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-123">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet paketleri iletişim Gözat sekmesini yönetme](media/Search.png)

1. <span data-ttu-id="45b28-125">Açılan listeden istediğiniz sürümü seçin ve seçin **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="45b28-125">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="45b28-126">Visual Studio projesine paketi ve bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="45b28-126">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="45b28-127">Lisans koşullarını kabul etmeniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="45b28-127">You may be asked to accept license terms.</span></span> <span data-ttu-id="45b28-128">Yükleme tamamlandığında, eklenen paketler görünür **yüklü** sekmesi. Paketler ayrıca listelenir **başvuruları** kendisine ile projedeki başvurabilirsiniz olduğunu gösteren Çözüm Gezgini düğümünün `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="45b28-128">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Çözüm Gezgini'nde başvuruların](media/References.png)

> [!Tip]
> <span data-ttu-id="45b28-130">Yayın öncesi sürümler Aramaya eklenecek ve yayın öncesi sürümler açılan sürüm kullanılabilir hale getirmek için seçin **ön sürümü dahil et** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="45b28-130">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="45b28-131">Bir paket kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="45b28-131">Uninstalling a package</span></span>

1. <span data-ttu-id="45b28-132">İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="45b28-132">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="45b28-133">Seçin **yüklü** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-133">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="45b28-134">(Gerekirse listeyi filtrelemek için arama kullanarak) kaldırmak için paketini seçin ve Seç **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="45b28-134">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Bir paket kaldırılıyor](media/UninstallPackage.png)

1. <span data-ttu-id="45b28-136">Unutmayın **INCLUDE yayın öncesi** ve **paket kaynağı** denetimleri, paketleri kaldırılırken etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="45b28-136">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="45b28-137">Bir paketi güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="45b28-137">Updating a package</span></span>

1. <span data-ttu-id="45b28-138">İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** . (Web sitesi projelerinde sağ **Bin** klasör.)</span><span class="sxs-lookup"><span data-stu-id="45b28-138">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="45b28-139">Seçin **güncelleştirmeleri** seçili paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="45b28-139">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="45b28-140">Seçin **ön sürümü dahil et** yayın öncesi paketleri güncelleştirme listeye dahil edilecek.</span><span class="sxs-lookup"><span data-stu-id="45b28-140">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="45b28-141">Güncelleştirme, sağdaki açılır listeden istediğiniz sürümü seçin ve seçin için paketi seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="45b28-141">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Bir paketi güncelleştiriliyor](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="45b28-143">Bazı paketler için **güncelleştirme** düğmesi devre dışıdır ve bunu "örtük olarak bir SDK'sı tarafından başvuruda bulunulan" bildiren bir ileti görüntülenir (veya "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="45b28-143">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="45b28-144">Bu ileti, paket büyük bir çerçeve veya SDK'sı parçasıdır ve bağımsız olarak güncelleştirilmemelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="45b28-144">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="45b28-145">(Bu paketleri dahili olarak ile işaretlenen `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK'sının bir parçasıdır ve Paket sürümü uygulama tarafından kullanılan çalışma zamanı framework sürümü ile aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="45b28-145">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="45b28-146">Şunları yapmanız [.NET Core yüklemenizi güncelleştirin](https://aka.ms/dotnet-download) ASP.NET Core ve .NET Core çalışma zamanı yeni sürümlerini almak için.</span><span class="sxs-lookup"><span data-stu-id="45b28-146">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="45b28-147">[.NET Core meta paketler ve sürüm oluşturma hakkında daha fazla ayrıntı için bu belgeye bakın](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="45b28-147">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="45b28-148">Bu, aşağıdaki yaygın olarak kullanılan paketler için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="45b28-148">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="45b28-149">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="45b28-149">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="45b28-150">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="45b28-150">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="45b28-151">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="45b28-151">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="45b28-152">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="45b28-152">NETStandard.Library</span></span>

    ![Örnek paket başvuruları veya AutoReferenced dolaylı olarak işaretlendi](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="45b28-154">Birden çok paket en yeni sürümlerine güncelleştirmek için bunları seçin ve liste içinde seçin **güncelleştirme** düğmesi listesinin üstünde.</span><span class="sxs-lookup"><span data-stu-id="45b28-154">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="45b28-155">Tek bir paketten de güncelleştirebilirsiniz **yüklü** sekmesi. Bu durumda, bir sürüm Seçici Paket ayrıntılarını içerir (konusu **INCLUDE yayın öncesi** seçeneği) ve bir **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-155">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="45b28-156">Çözüm için paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="45b28-156">Managing packages for the solution</span></span>

<span data-ttu-id="45b28-157">Bir çözüm için paketleri yönetme, aynı anda birden çok projeleriyle çalışmak için kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="45b28-157">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="45b28-158">Seçin **Araçlar > NuGet Paket Yöneticisi > çözüm için NuGet paketlerini Yönet...**  menü komutunu veya çözüme sağ tıklayıp seçin **NuGet paketlerini Yönet...** :</span><span class="sxs-lookup"><span data-stu-id="45b28-158">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Çözüm için NuGet paketlerini Yönet](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="45b28-160">Çözüm için paketler yönetirken işlemleri tarafından etkilenen projeleri seçin kullanıcı Arabirimi sağlar:</span><span class="sxs-lookup"><span data-stu-id="45b28-160">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Çözüm için paketler yönetirken proje Seçici](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="45b28-162">Sekme birleştirin</span><span class="sxs-lookup"><span data-stu-id="45b28-162">Consolidate tab</span></span>

<span data-ttu-id="45b28-163">Geliştiriciler genellikle aynı çözüm içindeki farklı projelerde aynı NuGet paketi farklı sürümlerini kullanmak için hatalı bir uygulama düşünün.</span><span class="sxs-lookup"><span data-stu-id="45b28-163">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="45b28-164">Bir çözüm için paketler yönetmek seçtiğinizde, Paket Yöneticisi kullanıcı Arabirimi sağlayan bir **Birleştir** üzerinde kolayca farklı sürüm numaralarını paketlerle çözüm içindeki farklı projelerde tarafından kullanıldığı sekmesinde görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45b28-164">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Paket Yöneticisi UI birleştirme sekmesi](media/ConsolidateTab.png)

<span data-ttu-id="45b28-166">EntityFramework 6.1.0 ConsoleApp1 kullanıyor ancak bu örnekte, EntityFramework 6.2.0, ClassLibrary1 proje kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="45b28-166">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="45b28-167">Paket sürümleri birleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="45b28-167">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="45b28-168">Proje listesinde güncelleştirmek için projeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="45b28-168">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="45b28-169">Bu projeleri içinde kullanılacak sürümünü seçin **sürüm** EntityFramework 6.2.0 gibi bir denetim.</span><span class="sxs-lookup"><span data-stu-id="45b28-169">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="45b28-170">Seçin **yükleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-170">Select the **Install** button.</span></span>

<span data-ttu-id="45b28-171">Paket Yöneticisi, seçilen tüm projeler, sonra paket artık görünür içine seçili Paket sürümü yükler. **Birleştir** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-171">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="45b28-172">Paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="45b28-172">Package sources</span></span>

<span data-ttu-id="45b28-173">Visual Studio paketleri alacağı kaynağını değiştirmek için bir kaynak Seçici'yi seçin:</span><span class="sxs-lookup"><span data-stu-id="45b28-173">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Paket kaynağı seçicide Paket Yöneticisi UI](media/PackageSourceDropDown.png)

<span data-ttu-id="45b28-175">Paket kaynaklarını yönetmek için:</span><span class="sxs-lookup"><span data-stu-id="45b28-175">To manage package sources:</span></span>

1. <span data-ttu-id="45b28-176">Seçin **ayarları** Paket Yöneticisi UI simgesine aşağıda özetlenen veya kullanın **Araçlar > Seçenekler** komut ve kaydırma **NuGet Paket Yöneticisi**:</span><span class="sxs-lookup"><span data-stu-id="45b28-176">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Paket Yöneticisi UI ayarlar simgesi](media/PackageSourceSettings.png)

1. <span data-ttu-id="45b28-178">Seçin **paket kaynaklarını** düğüm:</span><span class="sxs-lookup"><span data-stu-id="45b28-178">Select the **Package Sources** node:</span></span>

    ![Paket kaynağı seçenekleri](media/options.png)

1. <span data-ttu-id="45b28-180">Bir kaynak eklemek için seçin **+**, adı düzenleyin, URL veya yol girin **kaynak** denetlemek ve seçin **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="45b28-180">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="45b28-181">Kaynak Seçici açılan görünür.</span><span class="sxs-lookup"><span data-stu-id="45b28-181">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="45b28-182">Paket kaynağı değiştirmek için seçin, içinde düzenlemeler **adı** ve **kaynak** kutuları ve select **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="45b28-182">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="45b28-183">Paket kaynağı devre dışı bırakmak için listesinde adının sol tarafındaki kutuya temizleyin.</span><span class="sxs-lookup"><span data-stu-id="45b28-183">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="45b28-184">Paket kaynağı kaldırmak için onu seçin ve ardından **X** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="45b28-184">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="45b28-185">Kullanarak yukarı ve aşağı ok düğmelerini paket kaynaklarını öncelik sırasını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="45b28-185">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="45b28-186">Visual Studio isteklerine yanıt vermek için hangi kaynak gelen paketin ilk kullanarak paket kaynaklarını sırasını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="45b28-186">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="45b28-187">Daha fazla bilgi için [paket geri yükleme](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="45b28-187">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="45b28-188">Paket kaynağı sildikten sonra görünürse, bir bilgisayar düzeyinde veya kullanıcı düzeyi listelenebilir `NuGet.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="45b28-188">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="45b28-189">Bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md) bu dosyaları konumu için ardından dosyaları el ile düzenleme ya da kullanarak kaynak kaldırın [nuget komutu kaynakları](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="45b28-189">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="45b28-190">Paket Yöneticisi seçeneklerini denetleme</span><span class="sxs-lookup"><span data-stu-id="45b28-190">Package manager Options control</span></span>

<span data-ttu-id="45b28-191">Bir paket seçildiğinde, küçük bir paket Yöneticisi UI görüntüler Genişletilebilir **seçenekleri** altına (her ikisi de daraltılmış ve genişletilmiş burada gösterilmiştir) sürüm seçici denetimi.</span><span class="sxs-lookup"><span data-stu-id="45b28-191">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="45b28-192">Bazı proje için türleri, yalnızca unutmayın **Show Önizleme penceresini** seçeneği sağlanır.</span><span class="sxs-lookup"><span data-stu-id="45b28-192">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Paket Yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

<span data-ttu-id="45b28-194">Aşağıdaki bölümlerde, bu seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="45b28-194">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="45b28-195">Önizleme penceresini göster</span><span class="sxs-lookup"><span data-stu-id="45b28-195">Show preview window</span></span>

<span data-ttu-id="45b28-196">Paketi yüklenmeden önce kalıcı bir pencere seçildiğinde, seçilen Paket bağımlılıklarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="45b28-196">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Örnek Önizleme iletişim kutusu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="45b28-198">Yükleme ve güncelleştirme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="45b28-198">Install and Update Options</span></span>

<span data-ttu-id="45b28-199">(Kullanılamaz tüm proje türleri için.)</span><span class="sxs-lookup"><span data-stu-id="45b28-199">(Not available for all project types.)</span></span>

<span data-ttu-id="45b28-200">**Bağımlılık davranışı** NuGet bağımlı paketler yüklemek için hangi sürümlerinin nasıl karar yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="45b28-200">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="45b28-201">*Bağımlılıkları yoksay* herhangi bir bağımlılığın, genellikle yüklenen paket keser yükleme atlar.</span><span class="sxs-lookup"><span data-stu-id="45b28-201">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="45b28-202">*En düşük* [Varsayılan] birincil Seçilen paketin gereksinimlerini karşılayan en az sürüm numarasına sahip bağımlılık yükler.</span><span class="sxs-lookup"><span data-stu-id="45b28-202">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="45b28-203">*En yüksek düzeltme eki* aynı birincil ve ikincil sürüm numaralarını, ancak yüksek düzeltme numarası ile yeni sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="45b28-203">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="45b28-204">Sürüm 1.2.2 belirtilirse Örneğin, ardından 1.2 ile başlayan en yüksek sürümü yüklenir</span><span class="sxs-lookup"><span data-stu-id="45b28-204">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="45b28-205">*En yüksek ikincil* aynı büyük sürüm numarasına ancak en yüksek ikincil numara ve düzeltme numarası ile yeni sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="45b28-205">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="45b28-206">Sürüm 1.2.2 belirtilirse, 1 ile başlayan en yüksek sürümü yüklenir</span><span class="sxs-lookup"><span data-stu-id="45b28-206">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="45b28-207">*En yüksek* paket yüksek kullanılabilir sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="45b28-207">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="45b28-208">**Dosya çakışması eylem** NuGet proje veya yerel makinedeki mevcut paketleri nasıl işleyeceğini belirtir:</span><span class="sxs-lookup"><span data-stu-id="45b28-208">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="45b28-209">*Komut İstemi* tutmak veya var olan paketleri üzerine istemek için NuGet bildirir.</span><span class="sxs-lookup"><span data-stu-id="45b28-209">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="45b28-210">*Tümünü Yoksay* mevcut paketleri üzerine atlamak için NuGet bildirir.</span><span class="sxs-lookup"><span data-stu-id="45b28-210">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="45b28-211">*Tüm üzerine* mevcut paketleri üzerine yazmak için NuGet bildirir.</span><span class="sxs-lookup"><span data-stu-id="45b28-211">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="45b28-212">Kaldırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="45b28-212">Uninstall Options</span></span>

<span data-ttu-id="45b28-213">(Kullanılamaz tüm proje türleri için.)</span><span class="sxs-lookup"><span data-stu-id="45b28-213">(Not available for all project types.)</span></span>

<span data-ttu-id="45b28-214">**Bağımlılıkları kaldırın**: Seçili olduğunda, bunlar başka bir projede başvurulmuş değil, tüm bağımlı paketler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="45b28-214">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="45b28-215">**Zorla kaldırın olsa bile bağımlılıklar üzerinde**: Seçili olduğunda, bir paket kaldırır bile projede başvuruluyor.</span><span class="sxs-lookup"><span data-stu-id="45b28-215">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="45b28-216">Bu genellikle birlikte kullanılır **bağımlılıkları kaldırın** bir paket ve her şeyi kaldırmak için bağımlılıklar yüklü.</span><span class="sxs-lookup"><span data-stu-id="45b28-216">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="45b28-217">Bu seçenek kullanılarak ancak projedeki bozuk başvurularda açabilir.</span><span class="sxs-lookup"><span data-stu-id="45b28-217">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="45b28-218">Böyle durumlarda, gerekebilir [diğer paketleri yeniden](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="45b28-218">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
