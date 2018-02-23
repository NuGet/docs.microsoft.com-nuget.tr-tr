---
title: "NuGet paket geri yüklemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Nasıl NuGet bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükleyen bir genel bakış."
keywords: "NuGet paket geri yüklemesi, NuGet paket yükleme paketini, paketleri, bağımlılık sürümleri otomatik geri yükleme, devre dışı bırakma, geri yükleme, paket sürümlerinin sınırlama"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1980e00f865344927d105513f62923d14971b17b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/20/2018
---
# <a name="package-restore"></a><span data-ttu-id="3bab6-104">Paket geri yüklemesi</span><span class="sxs-lookup"><span data-stu-id="3bab6-104">Package Restore</span></span>

<span data-ttu-id="3bab6-105">Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paketi geri yüklemesi** proje oluşturulmadan önce tüm başvurulmuş paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="3bab6-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="3bab6-106">Yaygın olarak kullanılan bu özellik&mdash;Visual Studio, .NET Core 2.0 + ve xbuild Mono üzerinde kullanılabilir&mdash;kaynak denetiminde depolanması için bu paketleri gerek kalmadan tüm bağımlılıkları projede kullanılabilir olmasını sağlar (bkz: [ Paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) paket ikili dosyaları hariç tutulacak deponuza yapılandırma).</span><span class="sxs-lookup"><span data-stu-id="3bab6-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="3bab6-107">Herhangi bir zamanda paketleri de el ile geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bab6-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="3bab6-108">Yapı sunucuları paket geri yükleme hakkında daha fazla ayrıntı için bkz: [TFBuild ile paket geri yükleme](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="3bab6-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="3bab6-109">Paket geri yükleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="3bab6-109">Package restore overview</span></span>

<span data-ttu-id="3bab6-110">Paketleri geri ilk proje doğrudan bağımlılıklarını, tüm bağımlılık grafiğinin boyunca bu paketlerin bağımlılıkları yükleme gerektiğinde yükler.</span><span class="sxs-lookup"><span data-stu-id="3bab6-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="3bab6-111">Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="3bab6-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="3bab6-112">Paketi önbellekte değil NuGet sonra indirin (ve önbelleğe) paket tüm etkin kaynaklardan çalışır (bkz [NuGet yapılandırma davranışı](Configuring-NuGet-Behavior.md)); kaynakları da görüntülenir **Araçlar > Seçenekler > NuGet paketi Yöneticisi > paket kaynaklarını** Visual Studio listesinde).</span><span class="sxs-lookup"><span data-stu-id="3bab6-112">If the package is not in the cache, NuGet then attempts to download (and cache) the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md)); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="3bab6-113">NuGet paket kaynaklarını sırasını isteklerini yanıtlamak için hangi kaynak olan gelen paket ilk kullanarak yok sayar.</span><span class="sxs-lookup"><span data-stu-id="3bab6-113">NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="3bab6-114">NuGet tüm kaynakları doğrulayana kadar bir paket geri yükleme hatası göstermez.</span><span class="sxs-lookup"><span data-stu-id="3bab6-114">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="3bab6-115">O anda NuGet yalnızca listedeki son kaynağı için hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="3bab6-115">At that time, NuGet reports the failure for only the last source in the list.</span></span> <span data-ttu-id="3bab6-116">Paket mevcut değildi hata gösterir *herhangi* diğer kaynaklardan rağmen hataları gösterilmiyor görüntülerin her birini ayrı ayrı kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="3bab6-116">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="3bab6-117">Paket geri yüklemesi, aşağıdaki yollarla tetiklenir:</span><span class="sxs-lookup"><span data-stu-id="3bab6-117">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="3bab6-118">**DotNet CLI**: kullanmak [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="3bab6-118">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="3bab6-119">.NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak yapılır `dotnet build` ve `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="3bab6-119">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="3bab6-120">**Paket Yöneticisi kullanıcı Arabirimi (Windows için Visual Studio)**: paketler geri yüklenir otomatik olarak bir şablondan bir proje oluşturma ve proje oluşturma (açıklanan seçeneği tabi [etkinleştirme ve paket devre dışı bırakmageriyükleme](#enabling-and-disabling-package-restore)).</span><span class="sxs-lookup"><span data-stu-id="3bab6-120">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="3bab6-121">NuGet içinde 4.0 +, geri yükleme de otomatik olarak .NET Core SDK tabanlı bir projeye yapılan bir değişiklik olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="3bab6-121">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="3bab6-122">El ile geri yüklemek için Çözüm Gezgini'ndeki çözüme sağ tıklayın ve seçin **NuGet paketleri geri**.</span><span class="sxs-lookup"><span data-stu-id="3bab6-122">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="3bab6-123">Bir veya daha fazla tek tek paket olması durumunda düzgün yüklenmemiş hala (yani Çözüm Gezgini bir hata simgesi gösterir), sonra kullanım etkilenen paketler kaldırıp için Paket Yöneticisi kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="3bab6-123">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="3bab6-124">Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="3bab6-124">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="3bab6-125">"Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="3bab6-125">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="3bab6-126">**NuGet CLI**: kullanmak [nuget restore](../tools/cli-ref-restore.md) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)) veya bir [packages.config](../reference/packages-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="3bab6-126">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)) or in a [packages.config](../reference/packages-config.md) file.</span></span> <span data-ttu-id="3bab6-127">Çözüm dosyası da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bab6-127">You can also specify a solution file.</span></span>

- <span data-ttu-id="3bab6-128">**MSBuild**: kullanmak [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) , hangi geri yüklemeler paketler proje dosyasında listelenen paketler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="3bab6-128">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="3bab6-129">Yalnızca Visual Studio 2017 ile birlikte NuGet 4.x+ ve MSBuild 15.1 + kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3bab6-129">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="3bab6-130">`nuget restore` ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3bab6-130">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="3bab6-131">**Visual Studio Team Services**: bir derleme tanımınız Team Services oluştururken dahil [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) veya [.NET Core geri](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) herhangi bir görev oluşturmadan önce tanımında görev.</span><span class="sxs-lookup"><span data-stu-id="3bab6-131">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="3bab6-132">Bu görev varsayılan derleme şablonları sayısı olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="3bab6-132">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="3bab6-133">**Team Foundation Server**: TFS 2013 ve üzeri sürümler otomatik olarak yükler paketler derleme sırasında koşuluyla yapı TFS 2013 veya üzeri Team şablonu kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3bab6-133">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="3bab6-134">TFS önceki sürümü için yukarıdaki komut satırı geri yükleme seçeneklerinden birini çağırmak için bir derleme adımı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3bab6-134">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="3bab6-135">İsteğe bağlı olarak, TFS 2013 için derleme şablonu geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bab6-135">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="3bab6-136">Daha fazla bilgi için bkz: [paket geri yüklemesi izlenecek Team Foundation Build ile](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="3bab6-136">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="3bab6-137">Paket geri yüklemesi devre dışı bırakma ve etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3bab6-137">Enabling and disabling package restore</span></span>

<span data-ttu-id="3bab6-138">Paket geri yüklemesi aracılığıyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'da:</span><span class="sxs-lookup"><span data-stu-id="3bab6-138">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Paket geri yükleme davranışları NuGet Paket Yöneticisi seçeneklerle denetleme](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="3bab6-140">**Nuget'in eksik paketleri indirmesine izin ver**: değiştirerek denetimleri paket geri yükleme tüm forms `packageRestore/enabled` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="3bab6-140">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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
    >  <span data-ttu-id="3bab6-141">`packageRestore/enabled` Ayarını geçersiz kılındı genel olarak adlandırılan bir ortam değişkeni ayarlayarak **EnableNuGetPackageRestore** doğru veya yanlış Visual Studio başlatılıyor veya bir yapı başlatmadan önce bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="3bab6-141">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="3bab6-142">**Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: değiştirerek otomatik geri yükleme denetimleri `packageRestore/automatic` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="3bab6-142">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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

<span data-ttu-id="3bab6-143">Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölüm](../reference/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="3bab6-143">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="3bab6-144">Bazı durumlarda, bir geliştirici veya şirket etkinleştirmek veya bir bilgisayardaki tüm kullanıcılar için paket geri yüklemesi devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bab6-144">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="3bab6-145">Bu bulunan genel NuGet yapılandırma dosyasını yukarıdaki aynı ayarları ekleyerek yapılır `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="3bab6-145">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="3bab6-146">Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bab6-146">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="3bab6-147">Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="3bab6-147">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="3bab6-148">Geri yükleme ile kısıtlayan paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="3bab6-148">Constraining package versions with restore</span></span>

<span data-ttu-id="3bab6-149">Herhangi bir yöntemini paketleri geri yükleniyor, NuGet belirtilen kısıtlamalar yapılırken `packages.config` veya proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="3bab6-149">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="3bab6-150">`packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği.</span><span class="sxs-lookup"><span data-stu-id="3bab6-150">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="3bab6-151">Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="3bab6-151">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="3bab6-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3bab6-152">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="3bab6-153">PackageReference: doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="3bab6-153">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="3bab6-154">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3bab6-154">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="3bab6-155">Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="3bab6-155">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3bab6-156">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3bab6-156">Troubleshooting</span></span>

<span data-ttu-id="3bab6-157">Bkz: [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3bab6-157">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>