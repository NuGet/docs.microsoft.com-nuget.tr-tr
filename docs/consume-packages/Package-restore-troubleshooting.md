---
title: Visual Studio'da Sorun Giderme NuGet Paketi Geri Yükleme
description: Visual Studio'da sık karşılaşılan NuGet geri yükleme hatalarının ve bunların nasıl sorun giderilenin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860619"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="a1f6f-103">Sorun giderme paketi geri yükleme hataları</span><span class="sxs-lookup"><span data-stu-id="a1f6f-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="a1f6f-104">Bu makalede, paketleri geri ve bunları gidermek için adımlar geri alırken yaygın hatalar üzerinde duruluyor.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="a1f6f-105">Paket Geri Yükleme, tüm paket bağımlılıklarını proje dosyanızdaki paket başvurularıyla *(.csproj)* veya *packages.config* dosyanızla eşleşen doğru duruma yüklemeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="a1f6f-106">(Visual Studio'da, başvurular **Bağımlılıklar \ NuGet** veya **Başvuru düğümü** altında Çözüm Gezgini'nde görünür.) Paketleri geri yüklemek için gerekli adımları izlemek için [paketleri geri yükle'ye](../consume-packages/package-restore.md#restore-packages)bakın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="a1f6f-107">Proje dosyanızdaki paket başvuruları (*.csproj*) veya *packages.config* dosyanız yanlışsa (Paket Geri Yükleme'den sonra istediğiniz durumla eşleşmiyorsa), Paket Geri Yükleme'yi kullanmak yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="a1f6f-108">Buradaki talimatlar sizin için işe yaramazsa, senaryonuzu daha dikkatli inceleyebilmemiz için [lütfen GitHub'da bir sorun dosyalayın.](https://github.com/NuGet/docs.microsoft.com-nuget/issues)</span><span class="sxs-lookup"><span data-stu-id="a1f6f-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="a1f6f-109">"Bu sayfa yararlı mı?"</span><span class="sxs-lookup"><span data-stu-id="a1f6f-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="a1f6f-110">daha fazla bilgi için sizinle iletişim kurma olanağı vermediği için bu sayfada görünebilecek denetimi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="a1f6f-111">Visual Studio kullanıcıları için hızlı çözüm</span><span class="sxs-lookup"><span data-stu-id="a1f6f-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="a1f6f-112">Visual Studio kullanıyorsanız, önce aşağıdaki gibi paket geri yüklemeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="a1f6f-113">Aksi takdirde izleyen bölümlere devam edin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="a1f6f-114">**NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu > Araçlar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="a1f6f-115">Paket Geri **Yükleme**altında her iki seçeneği de ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="a1f6f-116">**Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-116">Select **OK**.</span></span>
1. <span data-ttu-id="a1f6f-117">Projenizi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-117">Build your project again.</span></span>

![Araç/Seçenekler'de NuGet paketini geri yüklemeyi etkinleştirme](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="a1f6f-119">Bu ayarlar dosyanızda `NuGet.config` da değiştirilebilir; [onay](#consent) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="a1f6f-120">Projeniz MSBuild tümleşik paket geri yüklemesini kullanan eski bir projeyse, otomatik paket geri yüklemesine [geçiş](package-restore.md#migrate-to-automatic-package-restore-visual-studio) yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="a1f6f-121">Bu proje, bu bilgisayarda eksik olan NuGet paketine(ler) başvurur</span><span class="sxs-lookup"><span data-stu-id="a1f6f-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="a1f6f-122">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="a1f6f-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="a1f6f-123">Bu hata, bir veya daha fazla NuGet paketine başvuru içeren bir proje oluşturmaya çalıştığınızda oluşur, ancak bu paketler şu anda bilgisayara veya projeye yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="a1f6f-124">[PackageReference](package-references-in-project-files.md) yönetim biçimini kullanırken, hata paketin [genel paketleri ve önbellek klasörlerini yönetmede](managing-the-global-packages-and-cache-folders.md)açıklandığı gibi *genel paketler* klasörüne yüklenmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="a1f6f-125">[packages.config](../reference/packages-config.md)kullanırken, hata paketin çözüm kökündeki `packages` klasöre yüklü olmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="a1f6f-126">Bu durum genellikle, projenin kaynak kodunu kaynak denetiminden veya başka bir karşıdan yüklemeden aldığınızda oluşur.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="a1f6f-127">Paketler genellikle kaynak denetiminden veya karşıdan yüklemelerden atlanır, çünkü nuget.org gibi paket akışlarından geri yüklenebilirler (bkz. [Paketler ve kaynak denetimi).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="a1f6f-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="a1f6f-128">Bunları da dahil etmek aksi takdirde depo şişirme veya gereksiz yere büyük .zip dosyaları oluşturmak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="a1f6f-129">Proje dosyanız paket konumlarına mutlak yollar içeriyorsa ve projeyi taşırsanız hata da olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="a1f6f-130">Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a1f6f-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="a1f6f-131">Proje dosyasını taşıdıysanız, paket başvurularını güncelleştirmek için dosyayı doğrudan güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="a1f6f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([otomatik geri yükleme](package-restore.md#restore-packages-automatically-using-visual-studio) veya manuel geri [yükleme](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="a1f6f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="a1f6f-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="a1f6f-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="a1f6f-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="a1f6f-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="a1f6f-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="a1f6f-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="a1f6f-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="a1f6f-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="a1f6f-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="a1f6f-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="a1f6f-138">Başarılı bir geri yüklemeden sonra, paket *genel paketler* klasöründe bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="a1f6f-139">PackageReference kullanan projeler için, geri `obj/project.assets.json` yükleme dosyayı yeniden oluşturmalı; kullanan `packages.config`projeler için, paket projenin `packages` klasöründe görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="a1f6f-140">Proje artık başarıyla inşa edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-140">The project should now build successfully.</span></span> <span data-ttu-id="a1f6f-141">Değilse, sizi takip edebilmemiz için [GitHub'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) dosyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="a1f6f-142">Varlıklar dosya project.assets.json bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a1f6f-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="a1f6f-143">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="a1f6f-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="a1f6f-144">Dosya, `project.assets.json` gerekli tüm paketlerin bilgisayara yüklendiğinden emin olmak için kullanılan PackageReference yönetim biçimini kullanırken projenin bağımlılık grafiğini tutar.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="a1f6f-145">Bu dosya paket geri yüklemesi yoluyla dinamik olarak oluşturulduğundan, genellikle kaynak denetimine eklenmez.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="a1f6f-146">Sonuç olarak, bu hata, paketleri otomatik olarak geri `msbuild` yüklemeyen bir araçla bir proje inşa ederken oluşur.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="a1f6f-147">Bu durumda, `msbuild -t:restore` ardından `msbuild`çalıştırın `dotnet build` , veya kullanın (paketleri otomatik olarak geri yükleyin).</span><span class="sxs-lookup"><span data-stu-id="a1f6f-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="a1f6f-148">Ayrıca [önceki bölümde](#missing)paket geri yükleme yöntemlerinden herhangi birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="a1f6f-149">Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekir, ancak onay verilmediği için bu durum olamaz</span><span class="sxs-lookup"><span data-stu-id="a1f6f-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="a1f6f-150">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="a1f6f-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="a1f6f-151">Bu hata, Paket geri yüklemenin NuGet yapılandırmanızda devre dışı bırakıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="a1f6f-152">Visual Studio [kullanıcıları için Hızlı çözüm](#quick-solution-for-visual-studio-users)altında daha önce açıklandığı gibi Visual Studio'daki geçerli ayarları değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="a1f6f-153">Bu ayarları doğrudan ilgili `nuget.config` dosyada (genellikle `%AppData%\NuGet\NuGet.Config` Windows ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta) da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="a1f6f-154">Altındaki `enabled` `packageRestore` tuşların `automatic` True olarak ayarlandıklarına emin olun:</span><span class="sxs-lookup"><span data-stu-id="a1f6f-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="a1f6f-155">`packageRestore` Ayarları doğrudan olarak `nuget.config`ayarlarsanız, seçenekler iletişim kutusu geçerli değerleri göstersin diye Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="a1f6f-156">Diğer potansiyel koşullar</span><span class="sxs-lookup"><span data-stu-id="a1f6f-156">Other potential conditions</span></span>

- <span data-ttu-id="a1f6f-157">Eksik dosyalar nedeniyle yapı hatalarıyla karşılaşabilirsiniz ve bunları indirmek için NuGet geri yüklemesini kullanacağınızı söyleyen bir ileti ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="a1f6f-158">Ancak, geri yükleme çalıştıran "Tüm paketler zaten yüklü ve geri yüklenmesi için hiçbir şey yok" diyebilir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="a1f6f-159">Bu durumda, klasörü `packages` (kullanırken) `packages.config` `obj/project.assets.json` veya dosyayı (PackageReference kullanırken) silin ve yeniden geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="a1f6f-160">Hata hala devam ederse, `nuget locals all -clear` `dotnet locals all --clear` genel paketleri ve [önbellek klasörlerini yönetmede](managing-the-global-packages-and-cache-folders.md)açıklandığı gibi *genel paketleri* ve önbellek klasörlerini temizlemek için komut satırından kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="a1f6f-161">Kaynak denetiminden proje alırken, proje klasörleriniz salt okunur olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="a1f6f-162">Klasör izinlerini değiştirin ve paketleri yeniden geri geri getirmeye çalışın.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="a1f6f-163">NuGet'in eski bir sürümünü kullanıyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="a1f6f-164">En son önerilen sürümler için [nuget.org/downloads](https://www.nuget.org/downloads) kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="a1f6f-165">Visual Studio 2015 için 3.6.0'ı öneriyoruz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="a1f6f-166">Başka sorunlarla karşılaşırsanız, sizden daha fazla ayrıntı alabilmemiz için [GitHub'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) dosyalayAbilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1f6f-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
