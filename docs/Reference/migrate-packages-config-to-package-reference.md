---
title: Package.config PackageReference biçimlerine geçirme | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Bir proje package.config yönetim biçiminden NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi PackageReference nasıl geçirileceği hakkında ayrıntılar
keywords: NuGet migrator geçirmek, paket başvuruları, dosyaları, PackageReference, packages.config proje VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="4038d-104">Packages.config PackageReference için geçirme</span><span class="sxs-lookup"><span data-stu-id="4038d-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="4038d-105">Visual Studio 2017 sürüm 15.7 Preview 3 ve sonraki destekler projeden geçirme [packages.config](./packages-config.md) yönetim biçimine [PackageReference](../consume-packages/Package-References-in-Project-Files.md) biçimi.</span><span class="sxs-lookup"><span data-stu-id="4038d-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="4038d-106">PackageReference kullanmanın yararları</span><span class="sxs-lookup"><span data-stu-id="4038d-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="4038d-107">**Tek bir yerde tüm proje bağımlılıklarını yönetme**: Proje için proje başvuruları ve derleme başvurularını yalnızca gibi NuGet paketi başvuruyor (kullanarak `PackageReference` düğüm) ayrı bir kullanmak yerine doğrudan proje dosyalarını içinde yönetilir Packages.config dosyası.</span><span class="sxs-lookup"><span data-stu-id="4038d-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="4038d-108">**Üst düzey bağımlılıkları KARMAŞASIZ görünümünü**: packages.config PackageReference projede doğrudan yüklü NuGet paketlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="4038d-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="4038d-109">Sonuç olarak, NuGet Paket Yöneticisi kullanıcı Arabirimi ve proje dosyası ile alt düzey bağımlılıkları kalabalık değil.</span><span class="sxs-lookup"><span data-stu-id="4038d-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="4038d-110">**Performans iyileştirmeleri**: PackageReference kullanırken, paket içinde korunur *paketleri genel* klasörü (açıklandığı gibi [genel paketleri ve önbellek klasörleri yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md) yerine, bir `packages` çözüm klasördeki.</span><span class="sxs-lookup"><span data-stu-id="4038d-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="4038d-111">Sonuç olarak, PackageReference daha hızlı gerçekleştirir ve daha az disk alanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="4038d-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="4038d-112">**İnce bağımlılıkları ve içerik akışı üzerinde denetim**: MSBuild varolan özelliklerini kullanarak olanak tanır [koşullu bir NuGet paketi başvuru](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) ve paket referanslarını başına hedef Framework'ü seçin yapılandırması Platform veya diğer özetlere.</span><span class="sxs-lookup"><span data-stu-id="4038d-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="4038d-113">**PackageReference etkin geliştirilmekte olan**: bkz [PackageReference sorunları Github'da](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="4038d-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="4038d-114">Packages.config artık etkin geliştirilme aşamasındadır.</span><span class="sxs-lookup"><span data-stu-id="4038d-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="4038d-115">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="4038d-115">Limitations</span></span>

* <span data-ttu-id="4038d-116">NuGet PackageReference, Visual Studio 2015'te kullanılabilir ve önceki değil.</span><span class="sxs-lookup"><span data-stu-id="4038d-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="4038d-117">Geçirilen projeleri yalnızca Visual Studio 2017 açılabilir.</span><span class="sxs-lookup"><span data-stu-id="4038d-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="4038d-118">Geçiş C++ ve ASP.NET projesi için şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="4038d-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="4038d-119">Bazı paketler PackageReference ile tamamen uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4038d-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="4038d-120">Daha fazla bilgi için bkz: [paketini uyumluluk sorunları](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="4038d-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="4038d-121">Geçiş adımları</span><span class="sxs-lookup"><span data-stu-id="4038d-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="4038d-122">Geçiş başlamadan önce Visual Studio olanak tanımak için bir yedek projenin oluşturur [packages.config dönmeyi](#how-to-roll-back-to-packagesconfig) gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="4038d-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="4038d-123">Project'i kullanarak içeren bir çözüm açmak `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4038d-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="4038d-124">İçinde **Çözüm Gezgini**, sağ tıklayın **başvuruları** düğümü veya `packages.config` dosya ve seçin **PackageReference için packages.config geçirmek...** .</span><span class="sxs-lookup"><span data-stu-id="4038d-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="4038d-125">Migrator projenin NuGet paket referanslarını analiz eder ve bunları kategorilere ayırma girişiminde **en üst düzey bağımlılıkları** (NuGet paketleri bu yüklediğiniz dizine) ve **geçişli bağımlılıkları**(en üst düzey paketler bağımlılık olarak yüklü olan paketleri).</span><span class="sxs-lookup"><span data-stu-id="4038d-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="4038d-126">PackageReference geçişli paket geri yüklemesi destekler ve geçişli bağımlılıkları açıkça yüklü olması değil anlamına bağımlılıkları dinamik olarak çözer.</span><span class="sxs-lookup"><span data-stu-id="4038d-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="4038d-127">(İsteğe bağlı) Seçerek en üst düzey bir bağımlılık olarak geçişli bağımlılık olarak sınıflandırılmış bir NuGet paketi işlemek seçebilirsiniz **en üst düzey** paketi için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4038d-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="4038d-128">Bu seçenek geçişli geçmez varlıklar içeren paketler için otomatik olarak ayarlanır (de `build`, `buildCrossTargeting`, `contentFiles`, veya `analyzers` klasörleri) ve geliştirme bağımlılık olarak işaretlenmiş olanlar (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="4038d-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="4038d-129">Gözden [paketini uyumluluk sorunları](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="4038d-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="4038d-130">Seçin **Tamam** geçişi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="4038d-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="4038d-131">Geçiş işleminin sonunda, Visual Studio bir yola sahip bir rapor yedekleme, (üst düzey bağımlılıkları) yüklü olan paketlerin listesini, geçişli bağımlılıklar olarak başvurulan paketlerin listesini ve uyumluluk sorunları başlangıcında tanımlanan listesini sağlar geçiş.</span><span class="sxs-lookup"><span data-stu-id="4038d-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="4038d-132">Rapor yedekleme klasörüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="4038d-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="4038d-133">Çözüm oluşturur ve çalıştırır doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4038d-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="4038d-134">Sorunlar karşılaşırsanız [bir sorun Github'da dosya](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="4038d-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="4038d-135">Packages.config için geri almak nasıl</span><span class="sxs-lookup"><span data-stu-id="4038d-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="4038d-136">Geçirilen projeyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="4038d-136">Close the migrated project.</span></span>

1. <span data-ttu-id="4038d-137">Proje dosyasını kopyalayın ve `packages.config` yedekten (genellikle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) proje klasörüne.</span><span class="sxs-lookup"><span data-stu-id="4038d-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="4038d-138">Projeyi açın.</span><span class="sxs-lookup"><span data-stu-id="4038d-138">Open the project.</span></span>

1. <span data-ttu-id="4038d-139">Paket Yöneticisi konsolunu kullanarak açmak **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="4038d-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="4038d-140">Konsolunda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4038d-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="4038d-141">Paket uyumluluk sorunları</span><span class="sxs-lookup"><span data-stu-id="4038d-141">Package compatibility issues</span></span>

<span data-ttu-id="4038d-142">Packages.config içinde desteklenen bazı yönleri PackageReference içinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4038d-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="4038d-143">Migrator analiz eder ve bu tür sorunları algılar.</span><span class="sxs-lookup"><span data-stu-id="4038d-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="4038d-144">Bir veya daha fazla aşağıdaki sorunlardan biri olan herhangi bir paket geçişten sonra beklendiği gibi çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4038d-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4038d-145">Geçişten sonra paketi yüklendiğinde "install.ps1" betikleri göz ardı edilir</span><span class="sxs-lookup"><span data-stu-id="4038d-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4038d-146">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="4038d-146">**Description**</span></span> | <span data-ttu-id="4038d-147">PackageReference ile install.ps1 ve uninstall.ps1 PowerShell komut dosyaları, yükleme veya bir paket kaldırma sırasında yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="4038d-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="4038d-148">**Olası etkisini**</span><span class="sxs-lookup"><span data-stu-id="4038d-148">**Potential impact**</span></span> | <span data-ttu-id="4038d-149">Hedef projesindeki bazı davranışı yapılandırmak için bu komut dosyalarını bağımlı paketler beklendiği gibi çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4038d-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4038d-150">Geçişten sonra paketi yüklendiğinde "içerik" varlıklar kullanılabilir değil</span><span class="sxs-lookup"><span data-stu-id="4038d-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4038d-151">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="4038d-151">**Description**</span></span> | <span data-ttu-id="4038d-152">Bir paketin varlıkları `content` klasörü ile PackageReference desteklenmez ve yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="4038d-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="4038d-153">PackageReference için destek ekler `contentFiles` daha iyi geçişli desteği ve paylaşılan içeriği sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="4038d-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="4038d-154">**Olası etkisini**</span><span class="sxs-lookup"><span data-stu-id="4038d-154">**Potential impact**</span></span> | <span data-ttu-id="4038d-155">Varlıkları `content` değil kopyalanır proje ve proje yeniden düzenleme bu varlıkları varlığına bağlıdır kodu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4038d-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="4038d-156">Yükseltmeden sonra paketi yüklendiğinde XDT dönüşümler uygulanmaz</span><span class="sxs-lookup"><span data-stu-id="4038d-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4038d-157">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="4038d-157">**Description**</span></span> | <span data-ttu-id="4038d-158">XDT dönüşümler ile PackageReference desteklenmiyor ve `.xdt` dosyaları yüklerken veya bir paket kaldırma yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="4038d-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="4038d-159">**Olası etkisini**</span><span class="sxs-lookup"><span data-stu-id="4038d-159">**Potential impact**</span></span> | <span data-ttu-id="4038d-160">XDT dönüşümler tüm proje XML dosyaları için en yaygın olarak uygulanmaz `web.config.install.xdt` ve `web.config.uninstall.xdt`, başka bir deyişle, projenin` web.config` dosya paket eklendiğinde veya kaldırıldığında güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="4038d-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="4038d-161">Geçişten sonra paketi yüklendiğinde lib kök derlemelerde göz ardı edilir</span><span class="sxs-lookup"><span data-stu-id="4038d-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4038d-162">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="4038d-162">**Description**</span></span> | <span data-ttu-id="4038d-163">PackageReference ile derlemeleri sunmak kökünde `lib` klasörü hedef framework belirli bir alt klasör olmadan yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="4038d-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="4038d-164">NuGet projenin hedef çerçevesi için karşılık gelen hedef framework bilinen ad (TFM) eşleşen bir alt klasöre arar ve eşleşen derlemeleri projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="4038d-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="4038d-165">**Olası etkisini**</span><span class="sxs-lookup"><span data-stu-id="4038d-165">**Potential impact**</span></span> | <span data-ttu-id="4038d-166">Projenin hedef çerçevesi için karşılık gelen hedef framework bilinen ad (TFM) eşleşen bir alt klasörünüz yoksa paketleri değil geçişten sonra beklendiği gibi davranır veya geçirme sırasında yükleme başarısız</span><span class="sxs-lookup"><span data-stu-id="4038d-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="4038d-167">Bir sorun bulundu?</span><span class="sxs-lookup"><span data-stu-id="4038d-167">Found an issue?</span></span> <span data-ttu-id="4038d-168">Bu rapor!</span><span class="sxs-lookup"><span data-stu-id="4038d-168">Report it!</span></span>

<span data-ttu-id="4038d-169">Geçiş deneyimi ile ilgili bir sorun alıyorsanız, lütfen [NuGet GitHub deposunu bir sorun dosya](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="4038d-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
