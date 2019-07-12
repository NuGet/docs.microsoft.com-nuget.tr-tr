---
title: Visual Studio'da NuGet paket geri yükleme sorunlarını giderme
description: Visual Studio ve bunları nasıl giderebileceğinizden hatalar ortak NuGet açıklamasını geri yükleyin.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 287237cf4041870c562a6a7f48f233d8fdc8ef33
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842378"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="e94bc-103">Paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="e94bc-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="e94bc-104">Bu makalede, paketleri ve bunların çözülmesine yönelik adımları geri yüklerken ortak hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e94bc-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="e94bc-105">Paketleri geri yükleme ile ilgili tüm ayrıntılar için bkz. [paket geri yükleme](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="e94bc-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="e94bc-106">Buradaki yönergeleri sizin için işe yaramazsa [Lütfen Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece biz kendi senaryonuza daha dikkatli bir şekilde inceleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e94bc-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="e94bc-107">"Is bu sayfa faydalı?" kullanmayın</span><span class="sxs-lookup"><span data-stu-id="e94bc-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="e94bc-108">Bize daha fazla bilgi için sizinle olanağı vermez çünkü bu sayfada görünebilir denetimi.</span><span class="sxs-lookup"><span data-stu-id="e94bc-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="e94bc-109">Visual Studio kullanıcılar için daha hızlı çözüm</span><span class="sxs-lookup"><span data-stu-id="e94bc-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="e94bc-110">İlk paket geri yükleme Visual Studio kullanıyorsanız, şu şekilde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="e94bc-111">Aksi takdirde, izleyen bölümlerde devam edin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="e94bc-112">Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="e94bc-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="e94bc-113">Her iki seçenekleri altında **paketi geri yüklemeyi**.</span><span class="sxs-lookup"><span data-stu-id="e94bc-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="e94bc-114">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-114">Select **OK**.</span></span>
1. <span data-ttu-id="e94bc-115">Projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-115">Build your project again.</span></span>

![NuGet paket geri yükleme araç/seçenekler içinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="e94bc-117">Bu ayarlar da içinde değiştirilebilir, `NuGet.config` bakın; dosyası [onay](#consent) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e94bc-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="e94bc-118">Projenizi MSBuild tümleşik paket geri yükleme kullanan eski bir proje üzerinde çalışıyorsanız gerekebilir [geçirme](package-restore.md#migrate-to-automatic-package-restore-visual-studio) otomatik paket geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="e94bc-118">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="e94bc-119">Bu proje, bu bilgisayarda eksik olan NuGet paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="e94bc-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="e94bc-120">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="e94bc-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="e94bc-121">Bir veya daha fazla NuGet paket başvuruları içeren bir projeyi açmaya çalıştığında bu hata oluşur, ancak bu paketleri şu anda bilgisayarınızda veya projeyi yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="e94bc-121">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="e94bc-122">PackageReference yönetim biçimi kullanılırken, paketin içinde yüklü değil hatası anlamına gelir *genel paketleri* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e94bc-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="e94bc-123">Kullanırken `packages.config`, paket içinde yüklü değil hatası anlamına gelir `packages` çözüm kök klasör.</span><span class="sxs-lookup"><span data-stu-id="e94bc-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="e94bc-124">Bu durum genellikle kaynak denetimi veya başka bir yükleme projenin kaynak kodunu edinmek oluşur.</span><span class="sxs-lookup"><span data-stu-id="e94bc-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="e94bc-125">Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri paket akışları nuget.org gibi gelen döndürülebilir olduğundan (bkz [paketleri ve kaynak denetimi](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="e94bc-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="e94bc-126">Bunları da dahil olmak üzere Aksi halde depoyu Şişirme veya gereksiz derecede büyük .zip dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e94bc-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="e94bc-127">Hata, proje dosyanızı içeren paket konumlara mutlak yollar ve proje taşıyorsanız de oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="e94bc-127">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="e94bc-128">Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="e94bc-128">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="e94bc-129">Proje dosyası taşıdıysanız, doğrudan paket başvuruları güncelleştirileceği dosyayı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-129">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="e94bc-130">(Visual Studio) Paket geri yükleme seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu, her iki çalışma seçeneklerde ayarlama **paketi geri yüklemeyi**, seçerek **Tamam** .</span><span class="sxs-lookup"><span data-stu-id="e94bc-130">(Visual Studio) Enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="e94bc-131">Daha sonra çözümü yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e94bc-131">Then build the solution again.</span></span>
- <span data-ttu-id="e94bc-132">(dotnet CLI) Komut satırı, projenizi içeren klasöre geçin ve ardından çalıştırın `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).</span><span class="sxs-lookup"><span data-stu-id="e94bc-132">(dotnet CLI) In the command line, switch to the folder that contains your project, and then run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="e94bc-133">(nuget.exe CLI) Komut satırı, projenizi içeren klasöre geçin ve ardından çalıştırın `nuget restore` (ile oluşturulan projeleri hariç `dotnet` hangi büyük/küçük harf kullanımıyla CLI `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="e94bc-133">(nuget.exe CLI) In the command line, switch to the folder that contains your project, and then run `nuget restore` (except for projects created with `dotnet` CLI, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="e94bc-134">(Projeleri Project.json'dan) Komut satırında çalıştırın `msbuild -t:restore`.</span><span class="sxs-lookup"><span data-stu-id="e94bc-134">(Projects migrated to PackageReference) On the command line, run `msbuild -t:restore`.</span></span>

<span data-ttu-id="e94bc-135">Paket başarılı bir geri yüklemeden sonra mevcut olmalıdır *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="e94bc-135">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="e94bc-136">PackageReference'ı kullanarak projeleri için bir geri yükleme yeniden oluşturmanız gerekir `obj/project.assets.json` dosya; kullanarak projeleri için `packages.config`, paket projesinin görünmelidir `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="e94bc-136">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="e94bc-137">Şimdi, projeyi başarıyla oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="e94bc-137">The project should now build successfully.</span></span> <span data-ttu-id="e94bc-138">Aksi halde [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz size izleyecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="e94bc-138">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="e94bc-139">Varlıklar dosya project.assets.json bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e94bc-139">Assets file project.assets.json not found</span></span>

<span data-ttu-id="e94bc-140">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="e94bc-140">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="e94bc-141">`project.assets.json` Dosyası, bilgisayarda gerekli tüm paketleri yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimi kullanılırken bir projenin bağımlılık grafiği tutar.</span><span class="sxs-lookup"><span data-stu-id="e94bc-141">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="e94bc-142">Bu dosya paket geri yükleme ile dinamik olarak oluşturulmuş olduğu için kaynak denetimine genellikle eklenmez.</span><span class="sxs-lookup"><span data-stu-id="e94bc-142">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="e94bc-143">Sonuç olarak, bir aracı ile proje gibi oluştururken bu hata oluşur `msbuild` , otomatik olarak paketleri geri yüklemez.</span><span class="sxs-lookup"><span data-stu-id="e94bc-143">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="e94bc-144">Bu durumda, çalıştırma `msbuild -t:restore` ardından `msbuild`, veya `dotnet build` (hangi yükler paketleri otomatik olarak).</span><span class="sxs-lookup"><span data-stu-id="e94bc-144">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="e94bc-145">İçinde paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz [önceki bölümde](#missing).</span><span class="sxs-lookup"><span data-stu-id="e94bc-145">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="e94bc-146">Bir veya daha fazla NuGet paketlerini geri yüklenmesi gerekir, ancak izin verilmedi olduğundan kaldırılamadı</span><span class="sxs-lookup"><span data-stu-id="e94bc-146">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="e94bc-147">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="e94bc-147">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="e94bc-148">Bu hata, bu paket geri yükleme, NuGet yapılandırmasında devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e94bc-148">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="e94bc-149">Visual Studio'da geçerli ayarlar altında daha önce açıklandığı gibi değiştirebilirsiniz [hızlı çözüm için Visual Studio kullanıcılarına](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="e94bc-149">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="e94bc-150">Bu ayarları doğrudan geçerli da düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows üzerinde ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde).</span><span class="sxs-lookup"><span data-stu-id="e94bc-150">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="e94bc-151">Emin `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e94bc-151">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="e94bc-152">Düzenlediyseniz `packageRestore` ayarları doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir, böylece Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e94bc-152">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="e94bc-153">Diğer olası koşulları</span><span class="sxs-lookup"><span data-stu-id="e94bc-153">Other potential conditions</span></span>

- <span data-ttu-id="e94bc-154">Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet geri yükleme kullanmak bildiren bir ileti ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e94bc-154">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="e94bc-155">Ancak, bir geri yükleme devam varsayalım, "tüm paketler zaten yüklü ve geri yüklemek için bir şey yok."</span><span class="sxs-lookup"><span data-stu-id="e94bc-155">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="e94bc-156">Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e94bc-156">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="e94bc-157">Hatanın hala devam ederse `nuget locals all -clear` veya `dotnet locals all --clear` temizlemek için komut satırından *genel paketleri* ve klasörler üzerinde açıklandığı gibi önbelleğe [genel paketleri ve önbellek klasörleriniyönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e94bc-157">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="e94bc-158">Bir projeyi kaynak denetiminden edinirken, proje klasörleri salt okunur ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="e94bc-158">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="e94bc-159">Klasör izinleri ve paketleri yeniden geri yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="e94bc-159">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="e94bc-160">NuGet'ın eski bir sürümünü kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="e94bc-160">You may be using an old version of NuGet.</span></span> <span data-ttu-id="e94bc-161">Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="e94bc-161">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="e94bc-162">Visual Studio 2015 için 3.6.0 öneririz.</span><span class="sxs-lookup"><span data-stu-id="e94bc-162">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="e94bc-163">Diğer sorunlarla karşılaşırsanız [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e94bc-163">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
