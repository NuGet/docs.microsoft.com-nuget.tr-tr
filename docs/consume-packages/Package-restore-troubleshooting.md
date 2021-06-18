---
title: Visual Studio'de NuGet Paketi Geri Yükleme sorunlarını giderme
description: Uygulama içinde sık karşılaşılan NuGet geri yükleme Visual Studio ve bu hataların nasıl giderilir?
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323628"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="acdd5-103">Paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="acdd5-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="acdd5-104">Bu makale, paketleri geri yükleme sırasında karşılaşılan yaygın hatalara ve bunları çözme adımlarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="acdd5-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="acdd5-105">Paket Geri Yükleme, tüm paket bağımlılıklarını proje dosyanıza (*.csproj*) veya dosya dosyanıza paket başvuruları ile eşleşen doğru *packages.config* çalışır.</span><span class="sxs-lookup"><span data-stu-id="acdd5-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="acdd5-106">(Visual Studio, başvurular Bağımlılıklar **\ NuGet** Çözüm Gezgini Veya Başvurular düğümü **altında** görünür.) Paketleri geri yüklemek için gerekli adımları takip etmek için bkz. [Paketleri geri yükleme.](../consume-packages/package-restore.md#restore-packages)</span><span class="sxs-lookup"><span data-stu-id="acdd5-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="acdd5-107">Paket, proje dosyanıza (*.csproj*) veya *packages.config* dosyanıza başvurursa (Paket Geri Yükleme sonrasında istediğiniz durumla eşleşmez) paket geri yükleme yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="acdd5-108">Buradaki yönergeler sizin için uygunsa, senaryoyu daha dikkatli inceleyene kadar [gitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="acdd5-109">"Bu sayfa yararlı mı?"</span><span class="sxs-lookup"><span data-stu-id="acdd5-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="acdd5-110">denetimi bu sayfada görünebilir çünkü daha fazla bilgi için size ulaşabilme olanağını bize vermez.</span><span class="sxs-lookup"><span data-stu-id="acdd5-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="acdd5-111">Kullanıcılar için hızlı Visual Studio çözümü</span><span class="sxs-lookup"><span data-stu-id="acdd5-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="acdd5-112">Visual Studio kullanıyorsanız, önce paket geri yüklemesini aşağıdaki gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="acdd5-113">Aksi takdirde, aşağıdaki bölümlere devam edin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="acdd5-114">Araçlar ve **NuGet > Ayarlar Paket Yöneticisi > Paket Yöneticisi komutunu** seçin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="acdd5-115">Paket Geri Yükleme altında her **iki seçeneği de ayarlayın.**</span><span class="sxs-lookup"><span data-stu-id="acdd5-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="acdd5-116">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-116">Select **OK**.</span></span>
1. <span data-ttu-id="acdd5-117">Projenizi yeniden derleme.</span><span class="sxs-lookup"><span data-stu-id="acdd5-117">Build your project again.</span></span>

![Araç/Seçenekler'de NuGet paketi geri yüklemesini etkinleştirme](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="acdd5-119">Bu ayarlar dosyanız içinde de `NuGet.Config` değiştirilebilir; onay [](#consent) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="acdd5-119">These settings can also be changed in your `NuGet.Config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="acdd5-120">Projeniz MSBuild ile tümleşik paket geri yüklemesini kullanan eski bir proje ise, otomatik paket geri [yüklemeye](package-restore.md#migrate-to-automatic-package-restore-visual-studio) geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="acdd5-121">Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvurur</span><span class="sxs-lookup"><span data-stu-id="acdd5-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="acdd5-122">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="acdd5-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="acdd5-123">Bu hata, bir veya daha fazla NuGet paketine başvuru içeren bir proje derlemeye çalışırken oluşur, ancak bu paketler şu anda bilgisayarda veya projede yüklü değildir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="acdd5-124">[PackageReference](package-references-in-project-files.md) yönetim biçimini kullanırken, bu hata bir packages.config PackageReference geçişini kaldırma işlemi [](/nuget/resources/nuget-faq#working-with-packages) olabilir ve proje dosyasından el ile kaldırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](/nuget/resources/nuget-faq#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="acdd5-125">bu [packages.config](../reference/packages-config.md)kullanırken hata, paketin çözüm kökünde `packages` klasöre yüklenmemiş olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="acdd5-126">Bu durum genellikle projenin kaynak kodunu kaynak denetiminden veya başka bir indirmeden edinilen durumlarda oluşur.</span><span class="sxs-lookup"><span data-stu-id="acdd5-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="acdd5-127">Paketler genellikle kaynak denetiminden veya indirmelerden atlanır çünkü bunlar nuget.org gibi paket akışlarından geri yüklenebilir (bkz. [Paketler ve kaynak denetimi).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="acdd5-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="acdd5-128">Bunları dahil etmek aksi takdirde depoyu şişirir veya gereksiz yere büyük .zip oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="acdd5-129">Proje dosyanız paket konumlarını mutlak yollar içeriyorsa ve projeyi taşısanız da bu hatayla karşınıza olabilir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="acdd5-130">Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="acdd5-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="acdd5-131">Proje dosyasını taşıdıysanız, paket başvurularını güncelleştirmek için dosyayı doğrudan düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="acdd5-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ( otomatik[geri yükleme](package-restore.md#restore-packages-automatically-using-visual-studio) veya el ile geri [yükleme](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="acdd5-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="acdd5-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="acdd5-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="acdd5-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="acdd5-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="acdd5-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="acdd5-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="acdd5-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="acdd5-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="acdd5-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="acdd5-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="acdd5-138">Geri yükleme başarılı olduktan sonra paketin *global-packages klasöründe mevcut olması* gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="acdd5-139">PackageReference kullanan projeler için, geri yükleme işlemi dosyayı yeniden oluşturmalı; kullanan projeler `obj/project.assets.json` için paket projenin klasöründe `packages.config` `packages` görünmektedir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="acdd5-140">Projenin şimdi başarıyla derlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-140">The project should now build successfully.</span></span> <span data-ttu-id="acdd5-141">Yoksa, [sizi takip etmek için GitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="acdd5-142">Varlıklar project.assets.jsdosya bulunamadı</span><span class="sxs-lookup"><span data-stu-id="acdd5-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="acdd5-143">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="acdd5-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="acdd5-144">Dosya, gerekli tüm paketlerin bilgisayarda yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimini kullanırken projenin bağımlılık `project.assets.json` grafiğini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="acdd5-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="acdd5-145">Bu dosya paket geri yüklemesi aracılığıyla dinamik olarak oluşturulduğundan, genellikle kaynak denetimine eklenmez.</span><span class="sxs-lookup"><span data-stu-id="acdd5-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="acdd5-146">Sonuç olarak, paketleri otomatik olarak geri yüklemez gibi bir araçla proje `msbuild` oluşturulurken bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="acdd5-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="acdd5-147">Bu durumda, ardından `msbuild -t:restore` çalıştırın veya `msbuild` kullanın `dotnet build` (paketleri otomatik olarak geri yüklenir).</span><span class="sxs-lookup"><span data-stu-id="acdd5-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="acdd5-148">Önceki bölümde paket geri yükleme yöntemlerden herhangi birini de [kullanabilirsiniz.](#missing)</span><span class="sxs-lookup"><span data-stu-id="acdd5-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="acdd5-149">Bir veya daha fazla NuGet paketi geri yüklendi ancak onay verilmedi</span><span class="sxs-lookup"><span data-stu-id="acdd5-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="acdd5-150">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="acdd5-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="acdd5-151">Bu hata, NuGet yapılandırmanız içinde paket geri yüklemenin devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="acdd5-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="acdd5-152">Daha önce kullanıcılar için hızlı çözüm altında açıklandığı Visual Studio [sayfasındaki ilgili ayarları Visual Studio değiştirebilirsiniz.](#quick-solution-for-visual-studio-users)</span><span class="sxs-lookup"><span data-stu-id="acdd5-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="acdd5-153">Ayrıca bu ayarları doğrudan ilgili dosyada `nuget.config` (genellikle Windows ve `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde) düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acdd5-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="acdd5-154">altındaki ve `enabled` anahtarlarının `automatic` True olarak ayarlanmış olduğundan `packageRestore` emin olun:</span><span class="sxs-lookup"><span data-stu-id="acdd5-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="acdd5-155">Ayarları doğrudan içinde düzenlersiniz, seçenekler iletişim Visual Studio geçerli değerlerin görünür olması için `packageRestore` ayarları yeniden `nuget.config` başlatın.</span><span class="sxs-lookup"><span data-stu-id="acdd5-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="acdd5-156">Diğer olası koşullar</span><span class="sxs-lookup"><span data-stu-id="acdd5-156">Other potential conditions</span></span>

- <span data-ttu-id="acdd5-157">Eksik dosyalardan dolayı derleme hatalarına ve bunları indirmek için NuGet geri yüklemesini kullanmayı söyleyen bir iletiyle karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acdd5-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="acdd5-158">Ancak, bir geri yükleme çalıştırarak "Tüm paketler zaten yüklenmiştir ve geri yüklenecek bir şey yoktur."</span><span class="sxs-lookup"><span data-stu-id="acdd5-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="acdd5-159">Bu durumda, klasörü `packages` (kullanırken) veya dosyayı `packages.config` `obj/project.assets.json` (PackageReference kullanırken) silin ve geri yüklemeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="acdd5-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="acdd5-160">Hata devam ederse, genel paketleri ve önbellek klasörlerini yönetme konusunda açıklandığı gibi genel paketleri ve önbellek klasörlerini temizlemek için veya komut `nuget locals all -clear` `dotnet nuget locals all --clear` satırı [kullanın.](managing-the-global-packages-and-cache-folders.md) </span><span class="sxs-lookup"><span data-stu-id="acdd5-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="acdd5-161">Kaynak denetiminden bir proje elde edilirken proje klasörleriniz salt okunur olarak ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="acdd5-162">Klasör izinlerini değiştirerek paketleri geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="acdd5-163">NuGet'in eski bir sürümünü kullanıyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acdd5-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="acdd5-164">Önerilen [nuget.org/downloads](https://www.nuget.org/downloads) sürümler için güncelleştirmeleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="acdd5-165">2015 Visual Studio için 3.6.0 önerilir.</span><span class="sxs-lookup"><span data-stu-id="acdd5-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="acdd5-166">Başka sorunlarla karşılaşırsanız, [daha fazla ayrıntı alamamız için GitHub'da](https://github.com/NuGet/docs.microsoft.com-nuget/issues) bir sorun kaydedin.</span><span class="sxs-lookup"><span data-stu-id="acdd5-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
