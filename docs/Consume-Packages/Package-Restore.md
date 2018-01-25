---
title: "NuGet paket geri yüklemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Nasıl NuGet üzerinde bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükler açıklaması."
keywords: "NuGet paket geri yüklemesi, NuGet paket yükleme paketini, paketleri, bağımlılık sürümleri otomatik geri yükleme, devre dışı bırakma, geri yükleme, paket sürümlerinin sınırlama"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8af70cff522e1f6c285d17ad0bbc20d23a0734a4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="package-restore"></a><span data-ttu-id="a50d0-104">Paket geri yüklemesi</span><span class="sxs-lookup"><span data-stu-id="a50d0-104">Package Restore</span></span>

<span data-ttu-id="a50d0-105">Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paketi geri yüklemesi** proje oluşturulmadan önce tüm başvurulmuş paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="a50d0-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="a50d0-106">Yaygın olarak kullanılan bu özellik&mdash;Visual Studio, .NET Core 2.0 + ve xbuild Mono üzerinde kullanılabilir&mdash;kaynak denetiminde depolanması için bu paketleri gerek kalmadan tüm bağımlılıkları projede kullanılabilir olmasını sağlar (bkz: [ Paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) paket ikili dosyaları hariç tutulacak deponuza yapılandırma).</span><span class="sxs-lookup"><span data-stu-id="a50d0-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="a50d0-107">Herhangi bir zamanda paketleri de el ile geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50d0-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="a50d0-108">Yapı sunucuları paket geri yükleme hakkında daha fazla ayrıntı için bkz: [TFBuild ile paket geri yükleme](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="a50d0-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="a50d0-109">Paket geri yükleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="a50d0-109">Package restore overview</span></span>

<span data-ttu-id="a50d0-110">Paketleri geri ilk proje doğrudan bağımlılıklarını, tüm bağımlılık grafiğinin boyunca bu paketlerin bağımlılıkları yükleme gerektiğinde yükler.</span><span class="sxs-lookup"><span data-stu-id="a50d0-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="a50d0-111">Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="a50d0-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="a50d0-112">Paket önbellekte değilse, NuGet sonra paketi etkin kaynaklardan içinde listelenen indirmeyi deneme **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını**, kaynakları görünür sırada.</span><span class="sxs-lookup"><span data-stu-id="a50d0-112">If the package is not in the cache, NuGet then attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="a50d0-113">İndirilen paketler önbellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="a50d0-113">Downloaded packages are stored in the cache.</span></span>

> [!Note]
> <span data-ttu-id="a50d0-114">NuGet paketi tüm kaynakları iade kadar isteğe bağlı olarak hangi aynı anda yalnızca listedeki son kaynak için hata raporları bulmak için bir hata olduğunu göstermez.</span><span class="sxs-lookup"><span data-stu-id="a50d0-114">NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="a50d0-115">Hataları bu kaynakları için ayrı ayrı gösterilmeyen olsa bile tarafından uygulanır böyle bir hata Ayrıca paket herhangi diğer kaynakları ya da, mevcut değildi olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a50d0-115">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>

<span data-ttu-id="a50d0-116">Paket geri yüklemesi, aşağıdaki yollarla tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="a50d0-116">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="a50d0-117">**Paket Yöneticisi kullanıcı Arabirimi (Windows için Visual Studio)**: paketler geri yüklenir otomatik olarak bir şablondan bir proje oluşturma ve proje oluşturma (açıklanan seçeneği tabi [etkinleştirme ve paket devre dışı bırakmageriyükleme](#enabling-and-disabling-package-restore)).</span><span class="sxs-lookup"><span data-stu-id="a50d0-117">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="a50d0-118">NuGet içinde 4.0 +, geri yükleme de otomatik olarak .NET Core SDK tabanlı bir projeye yapılan bir değişiklik olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="a50d0-118">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="a50d0-119">El ile geri yüklemek için Çözüm Gezgini'ndeki çözüme sağ tıklayın ve seçin **NuGet paketleri geri**.</span><span class="sxs-lookup"><span data-stu-id="a50d0-119">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="a50d0-120">Bir veya daha fazla tek tek paket olması durumunda düzgün yüklenmemiş hala (yani Çözüm Gezgini bir hata simgesi gösterir), sonra kullanım etkilenen paketler kaldırıp için Paket Yöneticisi kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="a50d0-120">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="a50d0-121">Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="a50d0-121">See [Reinstalling and updating packages](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span></span>

    <span data-ttu-id="a50d0-122">"Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="a50d0-122">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="a50d0-123">**NuGet CLI**: kullanmak [nuget restore](../tools/cli-ref-restore.md) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)) veya bir [packages.config](../schema/packages-config.md)dosya.</span><span class="sxs-lookup"><span data-stu-id="a50d0-123">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)) or in a [packages.config](../schema/packages-config.md) file.</span></span> <span data-ttu-id="a50d0-124">Çözüm dosyası da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50d0-124">You can also specify a solution file.</span></span>

- <span data-ttu-id="a50d0-125">**DotNet CLI**: kullanmak [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore.md?tabs=netcore2x) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span><span class="sxs-lookup"><span data-stu-id="a50d0-125">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore.md?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span></span> <span data-ttu-id="a50d0-126">.NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak yapılır `dotnet build` ve `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="a50d0-126">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="a50d0-127">**MSBuild**: kullanmak [msbuild /t:restore](../schema/msbuild-targets.md#restore-target) , hangi geri yüklemeler paketler proje dosyasında listelenen paketler komutu (bkz [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span><span class="sxs-lookup"><span data-stu-id="a50d0-127">**MSBuild**: use the [msbuild /t:restore](../schema/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span></span> <span data-ttu-id="a50d0-128">Yalnızca Visual Studio 2017 ile birlikte NuGet 4.x+ ve MSBuild 15.1 + kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a50d0-128">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="a50d0-129">`nuget restore`ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a50d0-129">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="a50d0-130">**Visual Studio Team Services**: bir derleme tanımınız Team Services oluştururken dahil [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) veya [.NET Core geri](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) herhangi bir görev oluşturmadan önce tanımında görev.</span><span class="sxs-lookup"><span data-stu-id="a50d0-130">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="a50d0-131">Bu görev varsayılan derleme şablonları sayısı olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="a50d0-131">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="a50d0-132">**Team Foundation Server**: TFS 2013 ve üzeri sürümler otomatik olarak yükler paketler derleme sırasında koşuluyla yapı TFS 2013 veya üzeri Team şablonu kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="a50d0-132">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="a50d0-133">TFS önceki sürümü için yukarıdaki komut satırı geri yükleme seçeneklerinden birini çağırmak için bir derleme adımı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a50d0-133">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="a50d0-134">İsteğe bağlı olarak, TFS 2013 için derleme şablonu geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50d0-134">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="a50d0-135">Daha fazla bilgi için bkz: [paket geri yüklemesi izlenecek Team Foundation Build ile](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="a50d0-135">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="a50d0-136">Paket geri yüklemesi devre dışı bırakma ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a50d0-136">Enabling and disabling package restore</span></span>

<span data-ttu-id="a50d0-137">Paket geri yüklemesi aracılığıyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'da:</span><span class="sxs-lookup"><span data-stu-id="a50d0-137">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Paket geri yükleme davranışları NuGet Paket Yöneticisi seçeneklerle denetleme](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="a50d0-139">**Nuget'in eksik paketleri indirmesine izin ver**: değiştirerek denetimleri paket geri yükleme tüm forms `packageRestore/enabled` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="a50d0-139">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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
    >  <span data-ttu-id="a50d0-140">`packageRestore/enabled` Ayarını geçersiz kılındı genel olarak adlandırılan bir ortam değişkeni ayarlayarak **EnableNuGetPackageRestore** doğru veya yanlış Visual Studio başlatılıyor veya bir yapı başlatmadan önce bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="a50d0-140">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="a50d0-141">**Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: değiştirerek otomatik geri yükleme denetimleri `packageRestore/automatic` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="a50d0-141">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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

<span data-ttu-id="a50d0-142">Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölüm](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="a50d0-142">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="a50d0-143">Bazı durumlarda, bir geliştirici veya şirket etkinleştirmek veya bir bilgisayardaki tüm kullanıcılar için paket geri yüklemesi devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50d0-143">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="a50d0-144">Bu bulunan genel NuGet yapılandırma dosyasını yukarıdaki aynı ayarları ekleyerek yapılır `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="a50d0-144">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="a50d0-145">Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50d0-145">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="a50d0-146">Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="a50d0-146">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="a50d0-147">Geri yükleme ile kısıtlayan paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="a50d0-147">Constraining package versions with restore</span></span>

<span data-ttu-id="a50d0-148">Herhangi bir yöntemini paketleri geri yükleniyor, NuGet belirtilen kısıtlamalar yapılırken `packages.config` veya proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="a50d0-148">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="a50d0-149">`packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği.</span><span class="sxs-lookup"><span data-stu-id="a50d0-149">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="a50d0-150">Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="a50d0-150">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="a50d0-151">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a50d0-151">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="a50d0-152">PackageReference: doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="a50d0-152">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="a50d0-153">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a50d0-153">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="a50d0-154">Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a50d0-154">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a50d0-155">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a50d0-155">Troubleshooting</span></span>

<span data-ttu-id="a50d0-156">Bkz: [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a50d0-156">See [Troubleshooting package restore](Package-restore-troubleshooting.md).</span></span>