---
title: NuGet 1.4 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.4 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550637"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="41962-103">NuGet 1.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="41962-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="41962-104">[1.3 NuGet sürüm notları](../release-notes/nuget-1.3.md) | [1.5 NuGet sürüm notları](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="41962-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="41962-105">NuGet 1.4 17 Haziran 2011'de yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="41962-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="41962-106">Özellikler</span><span class="sxs-lookup"><span data-stu-id="41962-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="41962-107">Update-Package geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-107">Update-Package improvements</span></span>
<span data-ttu-id="41962-108">NuGet 1.4 birçok geliştirme paketlerini bir çözümde birden çok proje boyunca aynı sürümde tutmak kolaylaştırarak Update-Package komutuna tanıtır.</span><span class="sxs-lookup"><span data-stu-id="41962-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="41962-109">Örneğin, bir paketin en son sürüme yükselttiğinizde, tüm projeler için aynı verision güncelleştirilecek yüklü, paketin ile istediğiniz yaygın olarak.</span><span class="sxs-lookup"><span data-stu-id="41962-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="41962-110">`Update-Package` Komutu artık kolaylaştırır için:</span><span class="sxs-lookup"><span data-stu-id="41962-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="41962-111">Tek bir projede tüm paketleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="41962-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="41962-112">Bir paketteki tüm projeleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="41962-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="41962-113">Tüm projelerde tüm paketleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="41962-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="41962-114">Tüm paketleri "güvenli" güncelleştirme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="41962-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="41962-115">`-Safe` Bayrağı yükseltmeleri yalnızca sürümleri aynı ana ve alt sürüm bileşeni ile kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="41962-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="41962-116">Örneğin bir paket 1.0.0 sürümü yüklü ve 1.0.1, 1.0.2 ve 1.1 sürümleri akışında kullanılabilir `-Safe` bayrağı için 1.0.2 paketi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="41962-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="41962-117">Olmadan yükseltme `-Safe` bayrağı en son sürüm 1.1 paketi yükseltmeniz.</span><span class="sxs-lookup"><span data-stu-id="41962-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="41962-118">Paketleri çözüm düzeyinde yönetme</span><span class="sxs-lookup"><span data-stu-id="41962-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="41962-119">NuGet 1.4 önce hantal iletişim kutusunu kullanarak birden çok proje bir paketi yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="41962-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="41962-120">Her proje için bir kez iletişim kutusunu başlatarak gerekli.</span><span class="sxs-lookup"><span data-stu-id="41962-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="41962-121">NuGet 1.4, aynı anda birden çok proje yükleme/kaldırma/güncelleştirme paketleri için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="41962-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="41962-122">Yalnızca başlatma çözüme sağ tıklayarak ve seçerek **NuGet paketlerini Yönet** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="41962-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Çözüm düzeyi NuGet paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="41962-124">İletişim kutusunun başlık çubuğunda çözümün adına görüntülendiğini bildirimi, bir proje adı değil.</span><span class="sxs-lookup"><span data-stu-id="41962-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="41962-125">Paket işlemleri artık onay kutularını listesiyle işlemi uygulamalısınız projelerinin listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="41962-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet paketleri proje seçimi yönetme](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="41962-127">Daha fazla ayrıntı için üzerinde konusuna bakın. [çözüm için paketler yönetme](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="41962-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="41962-128">Sınırlamak için izin verilen sürümler yükseltme</span><span class="sxs-lookup"><span data-stu-id="41962-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="41962-129">Varsayılan olarak çalıştırırken `Update-Package` bir paket (veya iletişim kutusunu kullanarak paketi güncelleştiriliyor) komutunu akıştaki en son sürüme güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="41962-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="41962-130">Tüm paketleri güncelleştirmeye yönelik yeni destek sayesinde, belirli bir sürüm aralığı için bir paket kilitlemek istediğiniz durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="41962-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="41962-131">Örneğin, uygulamanızın yalnızca bir paketin, ancak değil 3.0 ve sonraki sürüm 2.\* ile çalışmasını önceden haberdar olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41962-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="41962-132">Yanlışlıkla Paketi 3'e güncelleştiriliyor önlemek için NuGet 1.4 aralığını paketleri elle düzenleyerek yükseltilebilir sürümleri için destek ekler `packages.config` kullanarak yeni dosya `allowedVersions` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="41962-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="41962-133">Örneğin, aşağıdaki örnekte nasıl kilitleneceği gösterilir `SomePackage` paket sürüm aralığı 2.0-3.0 (dışlamalı).</span><span class="sxs-lookup"><span data-stu-id="41962-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="41962-134">`allowedVersions` Öznitelik değerlerini kullanarak kabul [sürüm aralığı biçim](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="41962-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="41962-135">1.4 içinde belirli bir sürüm aralığı için bir paket kilitleme elle düzenlenerek olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="41962-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="41962-136">Bu aralık üzerinden yerleştirmek için destek eklemeyi planlıyoruz NuGet 1.5 `Install-Package` komutu.</span><span class="sxs-lookup"><span data-stu-id="41962-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="41962-137">Paket görselleştiricisi</span><span class="sxs-lookup"><span data-stu-id="41962-137">Package Visualizer</span></span>
<span data-ttu-id="41962-138">Aracılığıyla başlatılan yeni paket Görselleştirici **Araçları** -> **kitaplık Paket Yöneticisi** -> **paket Görselleştirici** menü seçeneğini olanak tanır kolayca tüm projeleri ve bir çözüm içindeki Paket bağımlılıklarını görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="41962-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="41962-139">_**Önemli Not:** bu özellik DGML destek Visual Studio'da yararlanır. Görselleştirmenin oluşturulması yalnızca bu kadar Visual Studio Ultimate içinde desteklenir. DGML diyagramını görüntüleme, yalnızca Visual Studio Premium veya yüksek desteklenir._</span><span class="sxs-lookup"><span data-stu-id="41962-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Paket görselleştiricisi](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="41962-141">NuGet iletişim kutusu için otomatik güncelleştirme denetimi</span><span class="sxs-lookup"><span data-stu-id="41962-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="41962-142">NuGet'ün bazı sürümleri ile ifade edilen yeni özellikleri tanıtan `.nuspec` NuGet iletişim daha eski sürümleri tarafından anlaşılmayan dosyası.</span><span class="sxs-lookup"><span data-stu-id="41962-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="41962-143">Bir örnektir giriş için NuGet 1.4 [framework derlemeleri belirtme](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="41962-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="41962-144">Bu nedenle, en yeni özelliklerinden yararlanarak paketleri kullanabilir emin olmak için en son sürümünü kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="41962-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="41962-145">Güncelleştirmeler için NuGet daha görünür yapmak için NuGet iletişim daha yeni bir sürümü kullanılabilir olduğunda vurgulamak için mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="41962-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="41962-146">_**Not**: onay ise yalnızca gerçekleştirilir **çevrimiçi** sekmesinde geçerli oturumda seçilmiştir._</span><span class="sxs-lookup"><span data-stu-id="41962-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![NuGet paketlerini iletişim yeni sürüm ile yönetme](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="41962-148">Güncelleştirmeleri otomatik olarak denetlenmesi kapatmak için NuGet Ayarları iletişim kutusuna gidin ve işaretini kaldırın **güncelleştirmeleri otomatik olarak denetle**.</span><span class="sxs-lookup"><span data-stu-id="41962-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet ayarları](./media/nuget-settings.png)

<span data-ttu-id="41962-150">Bu özellik, NuGet 1.3 aslında eklendi ancak Elbette, 1.3, 1.4 NuGet gibi bir güncelleştirme kadar görünür olmayacaktır, kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="41962-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="41962-151">Paket Yöneticisi iletişim kutusu iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="41962-152">**Menü adları geliştirilmiş**: Menü Seçenekleri iletişim kutusunu başlatmak için daha anlaşılır olması için yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="41962-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="41962-153">Menü seçeneği sunulmuştur **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="41962-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="41962-154">**Ayrıntılar bölmesinde, en son güncelleştirme tarihi gösterir**: NuGet iletişim Ayrıntılar bölmesinde bir paket için en son güncelleştirme tarihi görüntüler olduğunda **çevrimiçi** veya **güncelleştirmeleri** sekmesi seçili.</span><span class="sxs-lookup"><span data-stu-id="41962-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="41962-155">**Görüntülenen etiketler listesi**: Nuget iletişim kutusu, etiketler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="41962-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="41962-156">PowerShell iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-156">Powershell Improvements</span></span>
* <span data-ttu-id="41962-157">**PowerShell komut dosyalarını oturum açmış**: NuGet daha kısıtlayıcı ortamlarda kullanımını etkinleştirme imzalı Powershell betikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="41962-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="41962-158">**Destek isteyen**: Paket Yöneticisi konsolu destekler aracılığıyla isteyen `$host.ui.Prompt` ve `$host.ui.PromptForChoice` komutları.</span><span class="sxs-lookup"><span data-stu-id="41962-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="41962-159">**Paket kaynak adları**: bir paket kaynağının adını sağlama desteklenir kullanarak bir paket kaynak belirtirken `-Source` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="41962-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="41962-160">nuget.exe komut satırı geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="41962-161">**NuGet özel komutlar**: nuget.exe MEF kullanarak özel komutları genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="41962-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="41962-162">**Daha basit sembol paketleri oluşturmak için iş akışı**: `-Symbols` bayrağı yalnızca kaynak ekleyerek sembolleri paket oluşturma normal kuralına göre klasör yapısı uygulanabilir ve `.pdb` klasördeki dosyaları.</span><span class="sxs-lookup"><span data-stu-id="41962-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="41962-163">**Birden çok kaynaktan belirtme**: `NuGet install` komutu destekler belirterek veya sınırlayıcı olarak noktalı virgül kullanarak birden çok kaynaktan belirtme `-Source` birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="41962-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="41962-164">**Proxy kimlik doğrulaması desteği**: NuGet 1.4 NuGet kimlik doğrulaması gerektiren bir proxy kullanırken kullanıcı kimlik bilgileri istemi için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="41962-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="41962-165">**nuget.exe yeni değişiklik güncelleştirme**: `-Self` bayrağı, artık kendisini güncelleştirmek nuget.exe için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41962-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="41962-166">`nuget.exe Update` artık bir yol alır `packages.config` dosya ve güncelleştirme paketleri dener.</span><span class="sxs-lookup"><span data-stu-id="41962-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="41962-167">Gerçekleştirmez, bu güncelleştirme sınırlı olduğunu unutmayın: ** güncelleştirme, Ekle, içeriğini proje dosyasında kaldırın.</span><span class="sxs-lookup"><span data-stu-id="41962-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="41962-168">** Paket içindeki Powershell betiklerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41962-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="41962-169">Nuget.exe kullanarak paketleri gönderme için NuGet sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="41962-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="41962-170">NuGet içeren basit bir yol barındırmak için bir [basit bir web tabanlı NuGet depo](../hosting-packages/nuget-server.md) aracılığıyla `NuGet.Server` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="41962-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="41962-171">NuGet 1.4 ile dağıtmaya ve nuget.exe kullanarak paketleri silme basit sunucusu destekler.</span><span class="sxs-lookup"><span data-stu-id="41962-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="41962-172">En son sürümünü `NuGet.Server` yeni ekler `appSetting`, adlandırılmış `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="41962-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="41962-173">Anahtar atlanırsa veya boş bırakılması, akışa paketleri gönderme devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="41962-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="41962-174">ApiKey (İdeal olarak güçlü bir parola) bir değere ayarlama nuget.exe kullanarak koymadan paketleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="41962-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="41962-175">Windows Phone araçları Mango sürümü için destek</span><span class="sxs-lookup"><span data-stu-id="41962-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="41962-176">NuGet, Windows Phone araçları Mango için yayın adayı sürümünde artık desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="41962-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="41962-177">Şu anda Windows Phone araçları, bu nedenle Windows Phone araçları için NuGet yüklemek Visual Studio uzantısı Yöneticisi için destek yok, indirin ve VSIX elle çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="41962-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="41962-178">Windows Phone araçları için NuGet kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41962-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="41962-179">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-179">Bug Fixes</span></span>
<span data-ttu-id="41962-180">NuGet 1.4 88 toplam iş öğeleri sabit vardı.</span><span class="sxs-lookup"><span data-stu-id="41962-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="41962-181">Bu 71 hataları olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="41962-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="41962-182">Tam bir listesi için iş öğeleri NuGet 1.4 içinde lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="41962-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="41962-183">Önemli hata düzeltmeleri:</span><span class="sxs-lookup"><span data-stu-id="41962-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="41962-184">[Sorun 603](http://nuget.codeplex.com/workitem/603): farklı depoları Paket bağımlılıklarını çözümler doğru şekilde belirli bir paket kaynağını belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="41962-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="41962-185">[Sorun 1036](http://nuget.codeplex.com/workitem/1036): ekleme `NuGet Pack SomeProject.csproj` artık derleme sonrası olay için sonsuz bir döngüye neden olur.</span><span class="sxs-lookup"><span data-stu-id="41962-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="41962-186">[Sorun 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrağı göreli yolları destekler.</span><span class="sxs-lookup"><span data-stu-id="41962-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="41962-187">NuGet 1.4 Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="41962-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="41962-188">Kısa bir süre içinde sürümünden NuGet 1.4 sonra birkaç düzeltmek önemli sorunları bulduk.</span><span class="sxs-lookup"><span data-stu-id="41962-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="41962-189">Belirli sürüm 1.4 Bu güncelleştirmeyi 1.4.20615.9020 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="41962-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="41962-190">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="41962-190">Bug Fixes</span></span>
* <span data-ttu-id="41962-191">[Sorun 1220](http://nuget.codeplex.com/workitem/1220): Update-Package değil yürütme `install.ps1` / `uninstall.ps1` birden fazla proje olduğunda tüm projelerde</span><span class="sxs-lookup"><span data-stu-id="41962-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="41962-192">[Sorunu 1156](http://nuget.codeplex.com/workitem/1156): Paket Yöneticisi konsol takılı W2K3/XP'de (Powershell 2 yüklü olmadığında)</span><span class="sxs-lookup"><span data-stu-id="41962-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
