---
title: NuGet 1,4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,4 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5f1d3ed6a1b20fb07437f1718faafaac0a193773
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488705"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="be84f-103">NuGet 1,4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="be84f-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="be84f-104">[NuGet 1,3 sürüm notları](../release-notes/nuget-1.3.md) | [NuGet 1,5 sürüm notları](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="be84f-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="be84f-105">NuGet 1,4, 17 Haziran 2011 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="be84f-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="be84f-106">Özellikler</span><span class="sxs-lookup"><span data-stu-id="be84f-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="be84f-107">Güncelleştirme-paket iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-107">Update-Package improvements</span></span>
<span data-ttu-id="be84f-108">NuGet 1,4, bir çözümdeki birden çok projedeki paketleri aynı sürümde tutmayı kolaylaştıran Update-Package komutuna yönelik birçok geliştirme sunar.</span><span class="sxs-lookup"><span data-stu-id="be84f-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="be84f-109">Örneğin, bir paketi en son sürüme yükseltirken, bu paketin yüklü olduğu tüm projelerin aynı Verision güncelleştirilmesini istemeniz çok yaygındır.</span><span class="sxs-lookup"><span data-stu-id="be84f-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="be84f-110">`Update-Package` Komut şu anda şunları kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="be84f-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="be84f-111">Tek bir projedeki tüm paketleri Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="be84f-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="be84f-112">Tüm projelerdeki bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="be84f-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="be84f-113">Tüm projelerdeki tüm paketleri Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="be84f-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="be84f-114">Tüm paketlerde "güvenli" bir güncelleştirme gerçekleştir</span><span class="sxs-lookup"><span data-stu-id="be84f-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="be84f-115">Bayrak `-Safe` , yükseltmeleri yalnızca aynı ana ve alt sürüm bileşeni olan sürümlerle kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="be84f-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="be84f-116">Örneğin, bir paketin 1.0.0 sürümü yüklüyse ve 1.0.1, 1.0.2 ve 1,1 sürümleri akışta varsa, `-Safe` bayrak paketi 1.0.2 olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="be84f-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="be84f-117">`-Safe` Bayrak olmadan yükseltme, paketi en son 1,1 sürümüne yükseltir.</span><span class="sxs-lookup"><span data-stu-id="be84f-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="be84f-118">Çözüm düzeyinde paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="be84f-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="be84f-119">NuGet 1,4 ' den önce, iletişim kutusunu kullanarak bir paketin birden fazla projeye yüklenmesi çok daha fazla.</span><span class="sxs-lookup"><span data-stu-id="be84f-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="be84f-120">Her proje için iletişim kutusunun bir kez başlatılmasını gerektirdi.</span><span class="sxs-lookup"><span data-stu-id="be84f-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="be84f-121">NuGet 1,4 aynı anda birden çok projedeki paketleri yükleme/kaldırma/güncelleştirme desteği ekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="be84f-122">Çözümü sağ tıklayıp **NuGet Paketlerini Yönet** menü seçeneğini belirleyerek başlatmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="be84f-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Çözüm düzeyi NuGet Paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="be84f-124">İletişim kutusunun başlık çubuğunda, bir projenin adı değil, çözümün adının görüntülendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="be84f-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="be84f-125">Paket işlemleri artık işlemin uygulanması gereken projelerin listesine sahip onay kutularının bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="be84f-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet paketleri proje seçimini Yönet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="be84f-127">Daha fazla ayrıntı için, [çözüm Için paketleri yönetme](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="be84f-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="be84f-128">Yükseltmeleri Izin verilen sürümlere kısıtlama</span><span class="sxs-lookup"><span data-stu-id="be84f-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="be84f-129">Varsayılan olarak, bir pakette `Update-Package` komutu çalıştırırken (veya iletişim kutusunu kullanarak paketi güncelleştirirken), akıştaki en son sürüme güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="be84f-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="be84f-130">Tüm paketlerin güncelleştirilmesiyle ilgili yeni destek sayesinde, bir paketi belirli bir sürüm aralığına kilitlemek istediğiniz durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="be84f-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="be84f-131">Örneğin, uygulamanızın yalnızca bir paketin 2. \* sürümüyle çalışabileceklerini, ancak 3,0 ve üzeri olduğunu bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be84f-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="be84f-132">Paketin yanlışlıkla 3 ' e güncelleştirilmesini engellemek için, NuGet 1,4, paketlerin yükseltilecekse, yeni `packages.config` `allowedVersions` özniteliğini kullanarak dosyayı düzenleyerek sürümüne yükseltebilen sürüm aralığını kısıtlayan destek ekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="be84f-133">Örneğin, aşağıdaki örnek 2,0-3,0 (özel) sürüm `SomePackage` aralığını paketin nasıl kilitleneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="be84f-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="be84f-134">Öznitelik, [Sürüm aralığı biçimini](../concepts/package-versioning.md#version-ranges-and-wildcards)kullanarak değerleri kabul eder. `allowedVersions`</span><span class="sxs-lookup"><span data-stu-id="be84f-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="be84f-135">1,4 ' de, bir paketin belirli bir sürüm aralığına kilitlenmesini el ile düzenlenmiş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="be84f-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="be84f-136">NuGet 1,5 ' de, `Install-Package` bu aralığı komut aracılığıyla yerleştirmeye yönelik destek eklemeyi planlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="be84f-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="be84f-137">Paket görselleştiricisi</span><span class="sxs-lookup"><span data-stu-id="be84f-137">Package Visualizer</span></span>
<span data-ttu-id="be84f-138">**Araçlar** -> **kitaplığı Paket Yöneticisi** -> **paket görselleştiricisi** menü seçeneği aracılığıyla başlatılan yeni paket görselleştiricisi, tüm projeleri ve bunların paket bağımlılıklarını kolayca görselleştirmenizi sağlar. çözümden.</span><span class="sxs-lookup"><span data-stu-id="be84f-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="be84f-139">_**Önemli bir dikkat:** Bu özellik, Visual Studio 'daki DGML desteğinden yararlanır. Görselleştirmenin oluşturulması yalnızca Visual Studio Ultimate desteklenir. DGML diyagramını görüntülemek yalnızca Visual Studio Premium veya üzeri sürümlerde desteklenir._</span><span class="sxs-lookup"><span data-stu-id="be84f-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Paket görselleştiricisi](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="be84f-141">NuGet Iletişim kutusu için otomatik güncelleştirme denetimi</span><span class="sxs-lookup"><span data-stu-id="be84f-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="be84f-142">NuGet 'in bazı sürümleri, `.nuspec` NuGet iletişim kutusunun eski sürümleri tarafından anlaşılmayan dosya aracılığıyla ifade edilen yeni özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="be84f-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="be84f-143">Örnek olarak, [çerçeve derlemelerini belirtmek](../release-notes/nuget-1.2.md#framework-assembly-refs)için NuGet 1,4 ' de giriş bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="be84f-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="be84f-144">Bu nedenle, en son özelliklerden yararlanarak paketleri kullanabilmeniz için NuGet 'in en son sürümünü kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="be84f-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="be84f-145">NuGet güncelleştirmelerini daha görünür hale getirmek için NuGet iletişim kutusu, daha yeni bir sürüm kullanılabilir olduğunda vurgulanacak mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="be84f-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="be84f-146">_**Note**: Denetim yalnızca, geçerli oturumda **çevrimiçi** sekme seçiliyse yapılır._</span><span class="sxs-lookup"><span data-stu-id="be84f-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![NuGet Paketlerini Yönet iletişim kutusunu yeni sürümü kullanılabilir](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="be84f-148">Güncelleştirmelerin otomatik denetimini devre dışı bırakmak için NuGet ayarları iletişim kutusuna gidin ve **güncelleştirmeleri otomatik olarak denetle onay**kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="be84f-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet ayarları](./media/nuget-settings.png)

<span data-ttu-id="be84f-150">Bu özellik aslında NuGet 1,3 ' ye eklenmiştir, ancak, NuGet 1,4 gibi 1,3 ' ye bir güncelleştirme yapıldığından, bu özellik görünür olmaz.</span><span class="sxs-lookup"><span data-stu-id="be84f-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="be84f-151">Paket Yöneticisi Iletişim geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="be84f-152">**Gelişmiş menü adları**: İletişim kutusunu başlatmak için menü seçenekleri açıklık için yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="be84f-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="be84f-153">Menü seçeneği artık **NuGet paketlerini yönetir**.</span><span class="sxs-lookup"><span data-stu-id="be84f-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="be84f-154">**Ayrıntılar bölmesi en son güncelleştirme tarihini gösterir**: NuGet iletişim kutusu, **çevrimiçi** veya **güncelleştirmeler** sekmesi seçildiğinde bir paketin Ayrıntılar bölmesindeki en son güncelleştirme tarihini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="be84f-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="be84f-155">**Gösterilecek etiketlerin listesi**: NuGet iletişim kutusu etiketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="be84f-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="be84f-156">PowerShell geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-156">Powershell Improvements</span></span>
* <span data-ttu-id="be84f-157">**Imzalı PowerShell betikleri**: NuGet, daha kısıtlayıcı ortamlarda kullanımı etkinleştiren imzalı PowerShell betikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="be84f-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="be84f-158">**Destek sorma**: Paket Yöneticisi konsolu artık `$host.ui.Prompt` ve `$host.ui.PromptForChoice` komutları aracılığıyla sorma desteği desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="be84f-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="be84f-159">**Paket kaynağı adları**: Bir paket kaynağının adı, `-Source` bayrağını kullanarak bir paket kaynağı belirtirken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="be84f-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="be84f-160">NuGet. exe komut satırı geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="be84f-161">**NuGet özel komutları**: NuGet. exe, MEF kullanılarak özel komutlar aracılığıyla Genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="be84f-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="be84f-162">**Sembol paketleri oluşturmak için iş akışını daha basit**hale getirir: Bayrak `-Symbols` , yalnızca klasör içindeki kaynak ve `.pdb` dosyalar dahil olmak üzere bir semboller paketi oluşturan normal bir kural tabanlı klasör yapısına uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="be84f-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="be84f-163">**Birden çok kaynak belirtme**: Komutu ayırıcı olarak noktalı virgül kullanarak veya birden çok kez belirterek `-Source` birden çok kaynağı belirtmeyi destekler. `NuGet install`</span><span class="sxs-lookup"><span data-stu-id="be84f-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="be84f-164">**Proxy kimlik doğrulaması desteği**: NuGet 1,4, kimlik doğrulaması gerektiren bir proxy 'nin arkasında NuGet kullanılırken Kullanıcı kimlik bilgileri istemek için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="be84f-165">**NuGet. exe güncelleştirme bölünmesi değişikliği**: Artık `-Self` bayrak, NuGet. exe ' nin kendisini güncelleştirmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="be84f-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="be84f-166">`nuget.exe Update`Şimdi `packages.config` dosyanın bir yolunu alır ve paketleri güncelleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="be84f-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="be84f-167">Bu güncelleştirmenin sınırlı olduğunu unutmayın: \* \* proje dosyasındaki içeriği Güncelleştir, Ekle, kaldır.</span><span class="sxs-lookup"><span data-stu-id="be84f-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="be84f-168">\* \* Paket içinde PowerShell betikleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="be84f-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="be84f-169">NuGet. exe kullanarak paketleri göndermek için NuGet sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="be84f-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="be84f-170">NuGet, `NuGet.Server` NuGet paketi aracılığıyla [basit bir Web tabanlı NuGet deposunu](../hosting-packages/nuget-server.md) barındırmak için basit bir yol içerir.</span><span class="sxs-lookup"><span data-stu-id="be84f-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="be84f-171">NuGet 1,4 ile, hafif sunucu NuGet. exe kullanarak paketleri göndermeyi ve silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="be84f-172">En son sürümü `NuGet.Server` , adlı `apiKey`yeni `appSetting`bir ekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="be84f-173">Anahtar atlanmışsa veya boş bırakılırsa, paketleri akışa göndermek devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="be84f-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="be84f-174">ApiKey değerini bir değer olarak ayarlama (ideal bir parola), NuGet. exe kullanarak paketlerin ititmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="be84f-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="be84f-175">Windows Phone araçları Mango sürümü desteği</span><span class="sxs-lookup"><span data-stu-id="be84f-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="be84f-176">NuGet, şimdi Mango için Windows Phone araçları sürüm adayı sürümünde desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="be84f-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="be84f-177">Şu anda Windows Phone araçları Visual Studio Uzantı Yöneticisi için desteğe sahip olmadığından, Windows Phone araçları için NuGet 'i yüklemeniz, VSıX 'i el ile indirip çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="be84f-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="be84f-178">NuGet Windows Phone araçları 'nı kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="be84f-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="be84f-179">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-179">Bug Fixes</span></span>
<span data-ttu-id="be84f-180">NuGet 1,4, Toplam 88 iş öğesine sahipti.</span><span class="sxs-lookup"><span data-stu-id="be84f-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="be84f-181">71 tanesi hata olarak işaretlendi.</span><span class="sxs-lookup"><span data-stu-id="be84f-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="be84f-182">NuGet 1,4 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="be84f-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="be84f-183">Hata düzeltmeleri dikkat edilecek değer:</span><span class="sxs-lookup"><span data-stu-id="be84f-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="be84f-184">[Sorun 603](http://nuget.codeplex.com/workitem/603): Farklı depolardaki paket bağımlılıkları, belirli bir paket kaynağı belirtirken doğru şekilde çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="be84f-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="be84f-185">[Sorun 1036](http://nuget.codeplex.com/workitem/1036): Derleme `NuGet Pack SomeProject.csproj` sonrası olayına ekleme sonsuz bir döngüye neden oluyor.</span><span class="sxs-lookup"><span data-stu-id="be84f-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="be84f-186">[Sorun 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrak göreli yolları destekler.</span><span class="sxs-lookup"><span data-stu-id="be84f-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="be84f-187">NuGet 1,4 Güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="be84f-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="be84f-188">NuGet 1,4 yayımlandıktan kısa bir süre sonra, düzeltilmesi gereken birkaç sorunu bulduk.</span><span class="sxs-lookup"><span data-stu-id="be84f-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="be84f-189">Bu güncelleştirmenin 1,4 sürümüne özgü sürüm numarası 1.4.20615.9020 ' dir.</span><span class="sxs-lookup"><span data-stu-id="be84f-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="be84f-190">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="be84f-190">Bug Fixes</span></span>
* <span data-ttu-id="be84f-191">[Sorun 1220](http://nuget.codeplex.com/workitem/1220): Birden fazla proje olduğunda, `install.ps1` güncelleştirme paketi tüm projelerde yürütülmez / `uninstall.ps1`</span><span class="sxs-lookup"><span data-stu-id="be84f-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="be84f-192">[Sorun 1156](http://nuget.codeplex.com/workitem/1156): Paket Yöneticisi W2K3/XP 'de takıldı (PowerShell 2 yüklü olmadığında)</span><span class="sxs-lookup"><span data-stu-id="be84f-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
