---
title: NuGet 1.4 sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.4 için sürüm notları.
keywords: Özellikler, dcr bilinen sorunlar, NuGet 1.4 sürüm notları, hata düzeltmeleri eklendi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="8301b-104">NuGet 1.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="8301b-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="8301b-105">[NuGet 1.3 Sürüm Notları](../release-notes/nuget-1.3.md) | [NuGet 1.5 sürüm notları](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="8301b-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="8301b-106">NuGet 1.4 17 Haziran 2011'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8301b-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="8301b-107">Özellikler</span><span class="sxs-lookup"><span data-stu-id="8301b-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="8301b-108">Güncelleştirme paketi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-108">Update-Package improvements</span></span>
<span data-ttu-id="8301b-109">NuGet 1.4 çok sayıda daha kolay bir çözümde birden çok proje arasında aynı sürümünde paketleri tutmak güncelleştirme paketi komut geliştirmeleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="8301b-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="8301b-110">Örneğin, bir paketin en son sürümüne yükseltirken, tüm projeleri aynı verision güncelleştirilmesi yüklü, paketin istiyor için çok yaygındır.</span><span class="sxs-lookup"><span data-stu-id="8301b-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="8301b-111">`Update-Package` Komutu şimdi kolaylaştırır için:</span><span class="sxs-lookup"><span data-stu-id="8301b-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="8301b-112">Güncelleştirme tek projesindeki tüm paketleri</span><span class="sxs-lookup"><span data-stu-id="8301b-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="8301b-113">Tüm projelerde paketi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8301b-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="8301b-114">Güncelleştirme tüm projelerdeki tüm paketleri</span><span class="sxs-lookup"><span data-stu-id="8301b-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="8301b-115">Tüm paketleri "safe" bir güncelleştirme gerçekleştirmek</span><span class="sxs-lookup"><span data-stu-id="8301b-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="8301b-116">`-Safe` Bayrağı yükseltmeleri aynı birincil ve ikincil sürüm bileşeni ile yalnızca sürümleri için kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="8301b-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="8301b-117">Örneğin bir paketin 1.0.0 sürümü yüklüyse ve akışta 1.0.1, 1.0.2 ve 1.1 sürümleri kullanılabilir `-Safe` bayrağı Paketi 1.0.2 sürümüne güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8301b-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="8301b-118">Olmadan yükseltme `-Safe` bayrağı en son sürüm 1.1 paket yükseltmeniz.</span><span class="sxs-lookup"><span data-stu-id="8301b-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="8301b-119">Çözüm düzeyinde paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="8301b-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="8301b-120">NuGet 1.4 önce bir paket birden çok projeye yükleme iletişim kutusunu kullanarak sıkıcı.</span><span class="sxs-lookup"><span data-stu-id="8301b-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="8301b-121">Bu, her proje için bir kez iletişim başlatma gerekli.</span><span class="sxs-lookup"><span data-stu-id="8301b-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="8301b-122">NuGet 1.4, aynı anda birden çok proje yükleme/kaldırma/güncelleştirme paketleri için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="8301b-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="8301b-123">Yalnızca başlatma çözüme sağ tıklatarak ve seçerek **NuGet paketlerini Yönet** menü seçeneği.</span><span class="sxs-lookup"><span data-stu-id="8301b-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Çözüm düzeyi NuGet paketlerini Yönet iletişim kutusu](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="8301b-125">Çözüm adı iletişim başlık çubuğunda görüntülenir dikkat edin, bir proje adı değil.</span><span class="sxs-lookup"><span data-stu-id="8301b-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="8301b-126">Paket işlemleri şimdi listesiyle işlemi uygulanması gereken projelerinin listesini onay kutularını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8301b-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet paketleri proje seçimi yönetme](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="8301b-128">Daha fazla ayrıntı için üzerinde konusuna [çözüm paketlerini yönetme](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="8301b-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="8301b-129">İzin için sürümler sınırlama yükseltir</span><span class="sxs-lookup"><span data-stu-id="8301b-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="8301b-130">Varsayılan olarak çalışırken, `Update-Package` bir paket (veya iletişim kutusu kullanılarak paketi güncellemeden) komutunu akıştaki en son sürümüne güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8301b-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="8301b-131">Tüm paketler güncelleştirmek için yeni destek ile bir pakete belirli sürüm aralığı kilitlemek istediğiniz durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="8301b-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="8301b-132">Örneğin, uygulamanızın yalnızca sürüm 2.\* bir paketin, ancak değil 3.0 ve üstü ile çalışıp çalışmayacağını önceden bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="8301b-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="8301b-133">Yanlışlıkla Paketi 3'e güncelleştirme önlemek için NuGet 1.4 aralığını paketler için elle düzenleyerek yükseltilebilir sürümleri için destek ekler `packages.config` kullanarak yeni dosya `allowedVersions` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8301b-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="8301b-134">Örneğin, aşağıdaki örnekte kilitlemek gösterilmektedir `SomePackage` paket sürüm 2.0-3.0 (özel) aralık.</span><span class="sxs-lookup"><span data-stu-id="8301b-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="8301b-135">`allowedVersions` Öznitelik değerlerini kullanarak kabul [sürüm aralığı biçimi](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="8301b-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="8301b-136">1.4 içinde belirli sürüm aralığı için bir paket kilitleme el ile düzenleyebilirsiniz olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8301b-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="8301b-137">Bu aralık aracılığıyla yerleştirmek için destek eklemeyi planlıyoruz NuGet 1.5 `Install-Package` komutu.</span><span class="sxs-lookup"><span data-stu-id="8301b-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="8301b-138">Paket Görselleştirici</span><span class="sxs-lookup"><span data-stu-id="8301b-138">Package Visualizer</span></span>
<span data-ttu-id="8301b-139">Aracılığıyla başlatılan yeni paket Görselleştirici **Araçları** -> **kitaplık Paket Yöneticisi** -> **paket Görselleştirici** menü seçeneği olanak sağlar kolayca tüm projeleri ve Paket bağımlılıklarını bir çözüm içinde görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="8301b-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="8301b-140">_**Önemli Not:** bu özellik DGML destek Visual Studio'da yararlanır. Görselleştirme oluşturuluyor yalnızca bu kadar Visual Studio Ultimate'ta desteklenir. DGML diyagramını görüntülemek, yalnızca Visual Studio Premium veya yüksek desteklenmez._</span><span class="sxs-lookup"><span data-stu-id="8301b-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Paket Görselleştirici](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="8301b-142">NuGet iletişim için otomatik güncelleştirme denetimi</span><span class="sxs-lookup"><span data-stu-id="8301b-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="8301b-143">NuGet'ın bazı sürümleri aracılığıyla ifade yeni özellikleri tanıtır `.nuspec` NuGet iletişim eski sürümleri tarafından anlaşılmayan dosya.</span><span class="sxs-lookup"><span data-stu-id="8301b-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="8301b-144">Bir örnektir için NuGet 1.4 içindeki giriş [framework derlemeleri belirtme](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="8301b-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="8301b-145">Bu nedenle, en son özelliklere yararlanarak paketlerini kullanmadan emin olmak için NuGet'ın en son sürümünü kullanmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8301b-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="8301b-146">Güncelleştirmeler için NuGet daha görünür hale getirmek için NuGet iletişim daha yeni bir sürümü kullanılabilir olduğunda vurgulamak için mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="8301b-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="8301b-147">_**Not**: denetimi yalnızca varsa yapılan **çevrimiçi** sekmesinde geçerli oturumdaki seçildi._</span><span class="sxs-lookup"><span data-stu-id="8301b-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![NuGet paketlerini iletişim yeni sürümü kullanılabilir ile yönetme](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="8301b-149">Güncelleştirmeleri otomatik olarak denetlenmesi kapatmak için NuGet Ayarları iletişim kutusuna gidin ve onay kutusunu temizleyin **güncelleştirmeleri otomatik olarak denetle**.</span><span class="sxs-lookup"><span data-stu-id="8301b-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet ayarları](./media/nuget-settings.png)

<span data-ttu-id="8301b-151">Bu özellik NuGet 1.3 içinde gerçekte eklendi ancak doğal olarak, NuGet 1.4 gibi 1.3 için bir güncelleştirme kadar görünür olmaz, kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="8301b-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="8301b-152">Paket Yöneticisi iletişim geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="8301b-153">**Menü adları geliştirilmiş**: Menü Seçenekleri iletişim kutusunu başlatmak için daha anlaşılır olması için yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="8301b-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="8301b-154">Menü seçeneği sunulmuştur **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="8301b-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="8301b-155">**Ayrıntılar bölmesinde, en son güncelleştirme tarihi gösterilir**: NuGet iletişim Ayrıntılar bölmesinde bir paket için en son güncelleştirme tarihi görüntüler zaman **çevrimiçi** veya **güncelleştirmeleri** sekmesi seçilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8301b-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="8301b-156">**Görüntülenen etiketler listesi**: Nuget iletişim etiketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8301b-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="8301b-157">PowerShell geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-157">Powershell Improvements</span></span>
* <span data-ttu-id="8301b-158">**PowerShell komut dosyalarını imzalı**: NuGet daha kısıtlayıcı ortamlarda kullanım etkinleştirme imzalı Powershell komut dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="8301b-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="8301b-159">**Destek isteyen**: Paket Yöneticisi konsolu artık destekliyor aracılığıyla isteyen `$host.ui.Prompt` ve `$host.ui.PromptForChoice` komutları.</span><span class="sxs-lookup"><span data-stu-id="8301b-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="8301b-160">**Paket kaynağı adları**: bir paket kaynağının adı sağladığını desteklenir kullanarak bir paket kaynak belirtirken `-Source` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="8301b-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="8301b-161">nuget.exe komut satırı geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="8301b-162">**NuGet özel komutları**: nuget.exe MEF kullanarak özel komutları genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="8301b-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="8301b-163">**Daha basit simge paketleri oluşturmak için iş akışı**: `-Symbols` bayrağı yalnızca kaynak ekleyerek simgeleri paket oluşturma normal kurala dayalı klasör yapısı uygulanabilir ve `.pdb` klasördeki dosyalar.</span><span class="sxs-lookup"><span data-stu-id="8301b-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="8301b-164">**Birden çok kaynakları belirtme**: `NuGet install` komutu destekler noktalı ayırıcı olarak veya belirterek kullanarak birden çok kaynakları belirtme `-Source` birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="8301b-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="8301b-165">**Proxy kimlik doğrulama desteği**: NuGet 1.4 NuGet kimlik doğrulaması gerektiren bir proxy kullanırken kullanıcı kimlik bilgileri için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="8301b-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="8301b-166">**nuget.exe sonu değişiklik güncelleştirme**: `-Self` bayrağı olan şimdi kendisini güncelleştirmek nuget.exe için gerekli.</span><span class="sxs-lookup"><span data-stu-id="8301b-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="8301b-167">`nuget.exe Update` Şimdi bir yolunda alır `packages.config` dosya ve güncelleştirme paketleri dener.</span><span class="sxs-lookup"><span data-stu-id="8301b-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="8301b-168">İçinde değil, bu güncelleştirme sınırlı olduğunu unutmayın: ** güncelleştirme eklemek için içerik proje dosyasında kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8301b-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="8301b-169">** Paketin içinde Powershell betikleri çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="8301b-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="8301b-170">Nuget.exe kullanarak paketleri gönderilmesi için NuGet sunucu desteği</span><span class="sxs-lookup"><span data-stu-id="8301b-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="8301b-171">NuGet barındırmak için basit bir yol içeren bir [basit bir web tabanlı NuGet deposu](../hosting-packages/nuget-server.md) aracılığıyla `NuGet.Server` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="8301b-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="8301b-172">NuGet 1.4 ile basit sunucunun itme ve nuget.exe kullanarak paketleri silme destekler.</span><span class="sxs-lookup"><span data-stu-id="8301b-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="8301b-173">En son sürümünü `NuGet.Server` yeni ekler `appSetting`, adlandırılmış `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="8301b-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="8301b-174">Anahtar atlanmış ya da boş bırakılırsa, paketleri akışa Ftp'den devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="8301b-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="8301b-175">Apikey ile yapılan bir değere (İdeal olarak güçlü bir parola) ayarlamak nuget.exe kullanarak koymadan paketleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8301b-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="8301b-176">Windows Phone araçları Mango Edition için destek</span><span class="sxs-lookup"><span data-stu-id="8301b-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="8301b-177">NuGet Mango için Windows Phone Araçları Sürüm Adayı sürümünde artık desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="8301b-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="8301b-178">Şu anda, Windows Phone araçları şekilde NuGet Windows Phone için araçları yüklemek Visual Studio uzantısı Yöneticisi için destek yok, indirin ve VSIX elle çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8301b-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="8301b-179">Windows Phone araçları NuGet kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8301b-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="8301b-180">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-180">Bug Fixes</span></span>
<span data-ttu-id="8301b-181">NuGet 1.4 iş öğeleri sabit 88 toplam vardı.</span><span class="sxs-lookup"><span data-stu-id="8301b-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="8301b-182">Bu 71 hata olarak işaretlendi.</span><span class="sxs-lookup"><span data-stu-id="8301b-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="8301b-183">Tam bir listesi için iş öğeleri NuGet 1.4 içinde lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="8301b-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="8301b-184">Eşitlenmeyeceği hata düzeltmeleri:</span><span class="sxs-lookup"><span data-stu-id="8301b-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="8301b-185">[Sorunu 603](http://nuget.codeplex.com/workitem/603): Paket bağımlılıklarını farklı depoları arasında çözümler doğru belirli paket kaynak belirtirken.</span><span class="sxs-lookup"><span data-stu-id="8301b-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="8301b-186">[Sorunu 1036](http://nuget.codeplex.com/workitem/1036): ekleme `NuGet Pack SomeProject.csproj` olay derleme artık sonrası için sonsuz bir döngüye neden olur.</span><span class="sxs-lookup"><span data-stu-id="8301b-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="8301b-187">[Sorunu 961](http://nuget.codeplex.com/workitem/961): `-Source` bayrağı göreli yollar destekler.</span><span class="sxs-lookup"><span data-stu-id="8301b-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="8301b-188">NuGet 1.4 Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="8301b-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="8301b-189">Kısa süre içinde sürümünden NuGet 1.4 sonra birkaç düzeltmek önemli sorunları bulduk.</span><span class="sxs-lookup"><span data-stu-id="8301b-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="8301b-190">Belirli bir sürüm 1.4 bu güncelleştirmeye 1.4.20615.9020 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="8301b-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="8301b-191">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8301b-191">Bug Fixes</span></span>
* <span data-ttu-id="8301b-192">[Sorunu 1220](http://nuget.codeplex.com/workitem/1220): değil güncelleştirme paketi yürütmek `install.ps1` / `uninstall.ps1` birden fazla proje olduğunda tüm projelerdeki</span><span class="sxs-lookup"><span data-stu-id="8301b-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="8301b-193">[Sorun 1156](http://nuget.codeplex.com/workitem/1156): Paket Yöneticisi konsol takılmış W2K3/XP'de (Powershell 2 yüklü olmadığında)</span><span class="sxs-lookup"><span data-stu-id="8301b-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
