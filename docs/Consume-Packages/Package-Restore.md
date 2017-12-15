---
title: "NuGet paket geri yüklemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Nasıl NuGet üzerinde bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükler açıklaması."
keywords: "NuGet paket geri yüklemesi, NuGet paket yükleme paketini, paketleri, bağımlılık sürümleri otomatik geri yükleme, devre dışı bırakma, geri yükleme, paket sürümlerinin sınırlama"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="85528-104">Paket geri yüklemesi</span><span class="sxs-lookup"><span data-stu-id="85528-104">Package Restore</span></span>

<span data-ttu-id="85528-105">Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paketi geri yüklemesi** proje oluşturulmadan önce tüm başvurulmuş paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="85528-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="85528-106">Yaygın olarak kullanılan bu özellik tüm bağımlılıkları kaynak denetiminde depolanması için bu paketleri gerek kalmadan bir projede kullanılabilir olmasını sağlar (bkz [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) deponuz dışlamak için yapılandırma Paket ikili dosyaları).</span><span class="sxs-lookup"><span data-stu-id="85528-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="85528-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="85528-107">In this topic:</span></span>
- [<span data-ttu-id="85528-108">Hızlı Kılavuz paket geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="85528-109">Paket geri yükleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="85528-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="85528-110">Paket geri yüklemesi devre dışı bırakma ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="85528-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="85528-111">Geri yükleme ile kısıtlayan paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="85528-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="85528-112">[Komut satırı geri yükleme](#command-line-restore), NuGet'in tüm sürümleri için</span><span class="sxs-lookup"><span data-stu-id="85528-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="85528-113">[Visual Studio'da otomatik geri yükleme](#automatic-restore-in-visual-studio), NuGet 2.7 için ve daha sonra.</span><span class="sxs-lookup"><span data-stu-id="85528-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="85528-114">[Visual Studio geri yükleme MSBuild tümleşik](#msbuild-integrated-restore), NuGet 2.6 ve önceki sürümler için.</span><span class="sxs-lookup"><span data-stu-id="85528-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="85528-115">Team Foundation Build ile paket geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="85528-116">Geri yükleme davranışını sürümü tarafından; değişir NuGet sürümünüzü denetlemek için çalıştırmanız yeterlidir `nuget.exe` komut satırı ve çıktısının ilk satırı bakın.</span><span class="sxs-lookup"><span data-stu-id="85528-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="85528-117">Yapı sunucuları paket geri yükleme hakkında daha fazla ayrıntı için bkz: [TFBuild ile paket geri yükleme](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="85528-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="85528-118">Paket için yapılandırılan projeleri de xbuild Mono üzerinde çalışmak geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="85528-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="85528-119">Hızlı Kılavuz paket geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="85528-120">"Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="85528-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="85528-121">Paket geri yükleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="85528-121">Package restore overview</span></span>

<span data-ttu-id="85528-122">İlk olarak, paket referanslarını proje türü ve NuGet sürümü bağlı olarak aşağıdaki paket Yönetimi biçimlerden birinde saklanır.</span><span class="sxs-lookup"><span data-stu-id="85528-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="85528-123">(NuGet 4 ve MSBuild 15.1 ile Visual Studio 2017 yüklendiğini unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="85528-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="85528-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="85528-124">Method</span></span> | <span data-ttu-id="85528-125">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="85528-125">NuGet Version</span></span> | <span data-ttu-id="85528-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="85528-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="85528-127">2.x +</span><span class="sxs-lookup"><span data-stu-id="85528-127">2.x+</span></span> | <span data-ttu-id="85528-128">Derin tamamını bağımlılıkları listeler.</span><span class="sxs-lookup"><span data-stu-id="85528-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="85528-129">Eklenen paketler `packages.config` da proje dosyasına eklenmelidir ve hedefleri ve özellik de eklenmelidir proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="85528-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="85528-130">Bu, tüm sürümleri NuGet, ancak için diğer seçenekleri ile karşılaştırıldığında daha yavaş performans taban çizgisi yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="85528-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="85528-131">(Bkz [packages.config şema](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="85528-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="85528-132">3.x +</span><span class="sxs-lookup"><span data-stu-id="85528-132">3.x+</span></span> | <span data-ttu-id="85528-133">Yalnızca UWP projeleri ile varsayılan olarak kullanılır, ancak projeleri, gelen dönüştürülebilir `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="85528-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="85528-134">`project.json`yalnızca üst düzey bağımlılıkları listeler.</span><span class="sxs-lookup"><span data-stu-id="85528-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="85528-135">Başvurular, hedefleri ve özellik eklenir dinamik olarak proje derleme sırasında karşılaştırıldığında daha iyi performans elde edilen `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="85528-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="85528-136">(Bkz [project.json şema](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="85528-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="85528-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="85528-137">PackageReference</span></span> | <span data-ttu-id="85528-138">4.x +</span><span class="sxs-lookup"><span data-stu-id="85528-138">4.x+</span></span> | <span data-ttu-id="85528-139">Proje dosyasında doğrudan bağımlılıkları listeler `<PackageReference>` düğümü, alongside `<Reference>` ve `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="85528-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="85528-140">Benzer şekilde çalışır `project.json`; bkz [paketini proje dosyalarını başvurularında](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="85528-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="85528-141">İkinci olarak, çeşitli yollarla başvuru listesinde kullanarak geri yüklemeyi başlat:</span><span class="sxs-lookup"><span data-stu-id="85528-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="85528-142">Komut satırından veya [Paket Yöneticisi Konsolu](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="85528-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="85528-143">Komut</span><span class="sxs-lookup"><span data-stu-id="85528-143">Command</span></span> | <span data-ttu-id="85528-144">İlgili senaryolar</span><span class="sxs-lookup"><span data-stu-id="85528-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="85528-145">NuGet ve tüm başvuru türleri tüm sürümleri.</span><span class="sxs-lookup"><span data-stu-id="85528-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="85528-146">Bkz: [komut satırı geri yükleme](#command-line-restore) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="85528-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="85528-147">Aynı `nuget restore` .NET Core projeleri için.</span><span class="sxs-lookup"><span data-stu-id="85528-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="85528-148">Bkz: [dotnet geri yükleme](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="85528-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="85528-149">Nuget 4.x+ ve MSBuild 15.1 + ile [paketini proje dosyalarını başvurularında](../Consume-Packages/Package-References-in-Project-Files.md) yalnızca.</span><span class="sxs-lookup"><span data-stu-id="85528-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="85528-150">`nuget restore`ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="85528-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="85528-151">Bkz: [NuGet paketi ve geri yükleme olarak MSBuild hedefleri-geri yükleme hedefi](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="85528-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="85528-152">Visual Studio kendisini paketleri farklı zamanlarda da yükler:</span><span class="sxs-lookup"><span data-stu-id="85528-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="85528-153">Tür</span><span class="sxs-lookup"><span data-stu-id="85528-153">Type</span></span> | <span data-ttu-id="85528-154">Geri yükleme durumda</span><span class="sxs-lookup"><span data-stu-id="85528-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="85528-155">Şablon geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-155">Template restore</span></span> | <span data-ttu-id="85528-156">Yeni bir proje oluşturma sırasında bazı şablonlar dış paketlere bağımlı.</span><span class="sxs-lookup"><span data-stu-id="85528-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="85528-157">Geri yükleme derleme</span><span class="sxs-lookup"><span data-stu-id="85528-157">Build restore</span></span> | <span data-ttu-id="85528-158">Bir yapı ilk adım olarak.</span><span class="sxs-lookup"><span data-stu-id="85528-158">As the first step of a build.</span></span> |
| <span data-ttu-id="85528-159">Çözüm geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-159">Solution restore</span></span> | <span data-ttu-id="85528-160">Kullanıcı ne zaman bir çözüm sağ tıklatır ve seçer **NuGet paketleri geri**.</span><span class="sxs-lookup"><span data-stu-id="85528-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="85528-161">Proje değişiminde geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-161">Restore on project change</span></span> | <span data-ttu-id="85528-162">*(NuGet yalnızca 4.x)*  Zaman bir .NET Core SDK tabanlı proje kullanılır, ne zaman dahil olmak üzere proje durum değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="85528-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="85528-163">Paket geri yüklemesi devre dışı bırakma ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="85528-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="85528-164">Paket geri yüklemesi aracılığıyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'da:</span><span class="sxs-lookup"><span data-stu-id="85528-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Paket geri yükleme davranışları NuGet Paket Yöneticisi seçeneklerle denetleme](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="85528-166">**Nuget'in eksik paketleri indirmesine izin ver**: değiştirerek denetimleri paket geri yükleme tüm forms `packageRestore/enabled` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="85528-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="85528-167">`packageRestore/enabled` Ayarını geçersiz kılındı genel olarak adlandırılan bir ortam değişkeni ayarlayarak **EnableNuGetPackageRestore** doğru veya yanlış Visual Studio başlatılıyor veya bir yapı başlatmadan önce bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="85528-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="85528-168">**Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: Otomatik geri yükleme NuGet 2.7 için ve daha sonra değiştirerek denetimleri `packageRestore/automatic` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="85528-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="85528-169">Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölüm](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="85528-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="85528-170">Bazı durumlarda, bir geliştirici veya şirket, etkinleştirmek veya paket geri yüklemesi bir makinedeki tüm kullanıcılar için varsayılan olarak devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85528-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="85528-171">Bu bulunan genel NuGet yapılandırma dosyasını yukarıdaki aynı ayarları ekleyerek yapılabilir `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="85528-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="85528-172">Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85528-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="85528-173">Bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="85528-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="85528-174">Geri yükleme ile kısıtlayan paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="85528-174">Constraining package versions with restore</span></span>

<span data-ttu-id="85528-175">NuGet paketleri herhangi bir yöntemini yüklediğinde belirtilen kısıtlamalar dokunmaz `packages.config`, `project.json`, ya da proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="85528-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="85528-176">`packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği.</span><span class="sxs-lookup"><span data-stu-id="85528-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="85528-177">Bkz: [yeniden yüklemeyi ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="85528-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="85528-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="85528-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="85528-179">`project.json`: Doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="85528-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="85528-180">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="85528-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="85528-181">Proje dosyalarını başvurularında paketini: doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="85528-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="85528-182">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="85528-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="85528-183">Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="85528-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="85528-184">Komut satırı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-184">Command-line restore</span></span>

<span data-ttu-id="85528-185">NuGet 2.7 için ve üstü, kullanım [geri](../tools/cli-ref-restore.md) bir çözümde tüm paketler geri yüklemek için komut (bunu kullanıp kullanmadığını `packages.config`, `project.json`, veya paket proje dosyalarını başvurularında).</span><span class="sxs-lookup"><span data-stu-id="85528-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="85528-186">Belirtilen proje klasörü gibi `c:\proj\app`, her aşağıda ortak Çeşitlemeler paketler geri:</span><span class="sxs-lookup"><span data-stu-id="85528-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="85528-187">NuGet 4.0 + ve MSBuild 15.1 + için de kullanabilirsiniz `MSBuild /t:restore` açıklandığı gibi [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="85528-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="85528-188">Visual Studio'da derleme zamanı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="85528-189">Visual Studio eksik paketleri bir yapı başındaki varsayılan olarak otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="85528-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="85528-190">Bu davranış temizleyerek değiştirilebilir **Araçlar > Seçenekler > NuGet Paket Yöneticisi > Genel > Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**.</span><span class="sxs-lookup"><span data-stu-id="85528-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="85528-191">Etkinleştirildiğinde, otomatik geri yükleme gibi çalışır:</span><span class="sxs-lookup"><span data-stu-id="85528-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="85528-192">Visual Studio derleme işlemi başladığında, NuGet paketlerini geri yüklemek için bildirir.</span><span class="sxs-lookup"><span data-stu-id="85528-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="85528-193">NuGet özyinelemeli olarak arar tüm `packages.config` çözüm dosyaları arar `project.json`, veya proje dosyasında bakar.</span><span class="sxs-lookup"><span data-stu-id="85528-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="85528-194">Çözümde zaten varsa, her paketleri denetimleri başvuru dosyaları, NuGet listelenen için ( `packages` klasörünü `project.lock.json`, veya `project.assets.json` proje kullanmanıza bağlı olarak `packages.config`, `project.json`, veya paket başvuruları Proje dosyaları).</span><span class="sxs-lookup"><span data-stu-id="85528-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="85528-195">Paket bulunamadı NuGet paketi, ilk önbellekten çalışır (bkz [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="85528-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="85528-196">Paket önbellekte değilse, NuGet paketi etkin kaynaklardan içinde listelenen indirmeyi dener **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını**, sırayla kaynakları görünür.</span><span class="sxs-lookup"><span data-stu-id="85528-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="85528-197">Bu durumda, NuGet paketi tüm kaynakları iade kadar isteğe bağlı olarak hangi aynı anda yalnızca listedeki son kaynak için hata raporları bulmak için bir hata olduğunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="85528-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="85528-198">Hataları bu kaynakları için ayrı ayrı gösterilmeyen olsa bile tarafından uygulanır böyle bir hata Ayrıca paket herhangi diğer kaynakları ya da, mevcut değildi olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="85528-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="85528-199">Yükleme başarılı olursa, NuGet paketini önbelleğe alır ve çözüme yükler (ya da içine yeniden `packages` klasörünü `project.lock.json`, veya `project.assets.json`); Aksi takdirde NuGet başarısız olur ve derleme başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="85528-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="85528-200">Bu işlem sırasında paket geri yüklemesi iptal etme seçeneği ile ilerleme iletişim kutusu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="85528-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="85528-201">Team Foundation derlemesi ile paket geri yükleme</span><span class="sxs-lookup"><span data-stu-id="85528-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="85528-202">Paket geri yüklemesi, Team Foundation Server (TFS) ve Visual Studio Team Services (yanı sıra gibi burada incelenmemiştir diğer yapı sistemleri) ile derleme sunucularda projeleri oluştururken, yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85528-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="85528-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="85528-203">Visual Studio Team Services</span></span>

<span data-ttu-id="85528-204">Yalnızca bir derleme tanımınız Team Services oluştururken, önce herhangi bir derleme görev tanımında NuGet paketleri geri görev içerir.</span><span class="sxs-lookup"><span data-stu-id="85528-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="85528-205">Bu görev varsayılan derleme şablonları sayısı olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="85528-205">This task is included by default in a number of build templates.</span></span>

![Visual Studio Team hizmeti yapı tanımında NuGet paket geri yükleme görevi](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="85528-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="85528-207">Team Foundation Server</span></span>

<span data-ttu-id="85528-208">Yapı Team Foundation Server 2013 veya üzeri Team şablonu kullanmakta olduğunuz koşuluyla TFS 2013 ve üzeri, paketleri otomatik olarak varsayılan derleme sırasında geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="85528-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="85528-209">Derleme şablonları (örn. TFS önceki sürümlerinden geçirilen bir proje) önceki bir sürümünü kullanıyorsanız, aynı zamanda geçirmek gerekir olanlar TFS 2013 için şablonlar oluşturma.</span><span class="sxs-lookup"><span data-stu-id="85528-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="85528-210">Bu temelde derleme şablonları özel bölümlerini yeniden uygun şablonu, kaynak denetimi için (TFVC'yi veya Git) kullanarak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="85528-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="85528-211">TFS önceki sürümü için çağrılacak bir derleme adımı yalnızca içerebilir [komut satırı geri yükleme](#command-line-restore) daha önce açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="85528-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="85528-212">Daha sonra daha fazla ayrıntı görmek için [gözden geçirme, paket geri yükleme ile Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="85528-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
