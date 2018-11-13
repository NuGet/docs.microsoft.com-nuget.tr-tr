---
title: Visual Studio'da NuGet paket geri yükleme sorunlarını giderme
description: Visual Studio ve bunları nasıl giderebileceğinizden hatalar ortak NuGet açıklamasını geri yükleyin.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 51dd78ef7cc427232982df15657d76d117146853
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580363"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="2ebb1-103">Paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="2ebb1-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="2ebb1-104">Bu makalede, paketleri ve bunların çözülmesine yönelik adımları geri yüklerken ortak hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="2ebb1-105">Paketleri geri yükleme ile ilgili tüm ayrıntılar için bkz. [paket geri yükleme](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="2ebb1-106">Buradaki yönergeleri sizin için işe yaramazsa [Lütfen Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece biz kendi senaryonuza daha dikkatli bir şekilde inceleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="2ebb1-107">"Is bu sayfa faydalı?" kullanmayın</span><span class="sxs-lookup"><span data-stu-id="2ebb1-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="2ebb1-108">Bize daha fazla bilgi için sizinle olanağı vermez çünkü bu sayfada görünebilir denetimi.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="2ebb1-109">Visual Studio kullanıcılar için daha hızlı çözüm</span><span class="sxs-lookup"><span data-stu-id="2ebb1-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="2ebb1-110">İlk paket geri yükleme Visual Studio kullanıyorsanız, şu şekilde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="2ebb1-111">Aksi takdirde, izleyen bölümlerde devam edin.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="2ebb1-112">Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="2ebb1-113">Her iki seçenekleri altında **paketi geri yüklemeyi**.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="2ebb1-114">Seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-114">Select **OK**.</span></span>
1. <span data-ttu-id="2ebb1-115">Projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-115">Build your project again.</span></span>

![NuGet paket geri yükleme araç/seçenekler içinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="2ebb1-117">Bu ayarlar da içinde değiştirilebilir, `NuGet.config` bakın; dosyası [onay](#consent) bölümü.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="2ebb1-118">Bu proje, bu bilgisayarda eksik olan NuGet paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="2ebb1-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="2ebb1-119">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="2ebb1-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="2ebb1-120">Bir veya daha fazla NuGet paket başvuruları içeren bir projeyi açmaya çalıştığında bu hata oluşur, ancak bu paketleri şu anda bilgisayarınızda veya projeyi yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-120">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="2ebb1-121">PackageReference yönetim biçimi kullanılırken, paketin içinde yüklü değil hatası anlamına gelir *genel paketleri* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="2ebb1-122">Kullanırken `packages.config`, paket içinde yüklü değil hatası anlamına gelir `packages` çözüm kök klasör.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="2ebb1-123">Bu durum genellikle kaynak denetimi veya başka bir yükleme projenin kaynak kodunu edinmek oluşur.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="2ebb1-124">Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri paket akışları nuget.org gibi gelen döndürülebilir olduğundan (bkz [paketleri ve kaynak denetimi](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="2ebb1-125">Bunları da dahil olmak üzere Aksi halde depoyu Şişirme veya gereksiz derecede büyük .zip dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="2ebb1-126">Hata, proje dosyanızı içeren paket konumlara mutlak yollar ve proje taşıyorsanız de oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-126">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="2ebb1-127">Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="2ebb1-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="2ebb1-128">Proje dosyası taşıdıysanız, doğrudan paket başvuruları güncelleştirileceği dosyayı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-128">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="2ebb1-129">Visual Studio'da paket geri yükleme seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu, her iki çalışma seçeneklerde ayarlama **paketi geri yüklemeyi**, seçerek **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-129">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="2ebb1-130">Daha sonra çözümü yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-130">Then build the solution again.</span></span>
- <span data-ttu-id="2ebb1-131">.NET Core projeleri için çalıştırma `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-131">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="2ebb1-132">Komut satırında çalıştırın `nuget restore` (ile oluşturulan projeleri hariç `dotnet`, bu durumda kullanın `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-132">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="2ebb1-133">PackageReference biçimini kullanarak projeleri ile komut satırında çalıştırın `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-133">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="2ebb1-134">Paket başarılı bir geri yüklemeden sonra mevcut olmalıdır *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-134">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="2ebb1-135">PackageReference'ı kullanarak projeleri için bir geri yükleme yeniden oluşturmanız gerekir `obj/project.assets.json` dosya; kullanarak projeleri için `packages.config`, paket projesinin görünmelidir `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-135">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="2ebb1-136">Şimdi, projeyi başarıyla oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-136">The project should now build successfully.</span></span> <span data-ttu-id="2ebb1-137">Aksi halde [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz size izleyecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-137">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="2ebb1-138">Varlıklar dosya project.assets.json bulunamadı</span><span class="sxs-lookup"><span data-stu-id="2ebb1-138">Assets file project.assets.json not found</span></span>

<span data-ttu-id="2ebb1-139">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="2ebb1-139">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="2ebb1-140">`project.assets.json` Dosyası, bilgisayarda gerekli tüm paketleri yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimi kullanılırken bir projenin bağımlılık grafiği tutar.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-140">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="2ebb1-141">Bu dosya paket geri yükleme ile dinamik olarak oluşturulmuş olduğu için kaynak denetimine genellikle eklenmez.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-141">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="2ebb1-142">Sonuç olarak, bir aracı ile proje gibi oluştururken bu hata oluşur `msbuild` , otomatik olarak paketleri geri yüklemez.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-142">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="2ebb1-143">Bu durumda, çalıştırma `msbuild /t:restore` ardından `msbuild`, veya `dotnet build` (hangi yükler paketleri otomatik olarak).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-143">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="2ebb1-144">İçinde paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz [önceki bölümde](#missing).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-144">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="2ebb1-145">Bir veya daha fazla NuGet paketlerini geri yüklenmesi gerekir, ancak izin verilmedi olduğundan kaldırılamadı</span><span class="sxs-lookup"><span data-stu-id="2ebb1-145">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="2ebb1-146">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="2ebb1-146">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="2ebb1-147">Bu hata, bu paket geri yükleme, NuGet yapılandırmasında devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-147">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="2ebb1-148">Visual Studio'da geçerli ayarlar altında daha önce açıklandığı gibi değiştirebilirsiniz [hızlı çözüm için Visual Studio kullanıcılarına](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-148">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="2ebb1-149">Bu ayarları doğrudan geçerli da düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows üzerinde ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-149">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="2ebb1-150">Emin `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2ebb1-150">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="2ebb1-151">Düzenlediyseniz `packageRestore` ayarları doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir, böylece Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="2ebb1-152">Diğer olası koşulları</span><span class="sxs-lookup"><span data-stu-id="2ebb1-152">Other potential conditions</span></span>

- <span data-ttu-id="2ebb1-153">Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet geri yükleme kullanmak bildiren bir ileti ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-153">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="2ebb1-154">Ancak, bir geri yükleme devam varsayalım, "tüm paketler zaten yüklü ve geri yüklemek için bir şey yok."</span><span class="sxs-lookup"><span data-stu-id="2ebb1-154">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="2ebb1-155">Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-155">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="2ebb1-156">Hatanın hala devam ederse `nuget locals all -clear` veya `dotnet locals all --clear` temizlemek için komut satırından *genel paketleri* ve klasörler üzerinde açıklandığı gibi önbelleğe [genel paketleri ve önbellek klasörleriniyönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2ebb1-156">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="2ebb1-157">Bir projeyi kaynak denetiminden edinirken, proje klasörleri salt okunur ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-157">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="2ebb1-158">Klasör izinleri ve paketleri yeniden geri yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-158">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="2ebb1-159">NuGet'ın eski bir sürümünü kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-159">You may be using an old version of NuGet.</span></span> <span data-ttu-id="2ebb1-160">Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-160">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="2ebb1-161">Visual Studio 2015 için 3.6.0 öneririz.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-161">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="2ebb1-162">Diğer sorunlarla karşılaşırsanız [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ebb1-162">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
