---
title: Visual Studio'da NuGet paket geri yükleme sorunlarını giderme
description: Visual Studio ve bunları gidermek nasıl hatalar geri yükleme ortak NuGet açıklaması.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c552941c896d1a7136310c0a8bc6755d5974809a
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="650e6-103">Paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="650e6-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="650e6-104">Bu makalede, paketleri ve bunları gidermek için adımları geri yüklerken ortak hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="650e6-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="650e6-105">Paketler geri yükleme ile ilgili tam Ayrıntılar için bkz: [paket geri yüklemesi](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="650e6-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="650e6-106">Buradaki yönergeleri, işe yaramazsa [Lütfen bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece senaryonuz daha dikkatlice inceleyin.</span><span class="sxs-lookup"><span data-stu-id="650e6-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="650e6-107">"Yararlıdır bu sayfayı?" kullanmayın</span><span class="sxs-lookup"><span data-stu-id="650e6-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="650e6-108">Bunu bize daha fazla bilgi için sizinle vermek değil çünkü bu sayfada görünebilir denetim.</span><span class="sxs-lookup"><span data-stu-id="650e6-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="650e6-109">Visual Studio kullanıcılar için hızlı çözümü</span><span class="sxs-lookup"><span data-stu-id="650e6-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="650e6-110">İlk paket geri yüklemesi Visual Studio kullanıyorsanız, aşağıdaki gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="650e6-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="650e6-111">Aksi durumda bölümlerde için devam edin.</span><span class="sxs-lookup"><span data-stu-id="650e6-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="650e6-112">Seçin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="650e6-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="650e6-113">Her iki seçenekleri altında **paketi geri yüklemesi**.</span><span class="sxs-lookup"><span data-stu-id="650e6-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="650e6-114">Seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="650e6-114">Select **OK**.</span></span>
1. <span data-ttu-id="650e6-115">Projenizi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="650e6-115">Build your project again.</span></span>

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="650e6-117">Bu ayarları da değiştirilebilir, `NuGet.config` bakın; dosyası [onayı](#consent) bölümü.</span><span class="sxs-lookup"><span data-stu-id="650e6-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="650e6-118">Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru</span><span class="sxs-lookup"><span data-stu-id="650e6-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="650e6-119">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="650e6-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="650e6-120">Bu hata oluşur. bir veya daha fazla NuGet Paketlerine yönelik başvuruları içeren bir projeyi derleme çalışıldı, ancak bu paketleri şu anda bilgisayarda veya projesinde yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="650e6-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="650e6-121">PackageReference yönetim biçimi kullanırken, paket içinde yüklenmedi hata anlamına gelir *paketleri genel* açıklandığı gibi açık açıklandığı gibi klasör [önbellek klasörvegenelpaketleriniyönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="650e6-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="650e6-122">Kullanırken `packages.config`, paket içinde yüklenmedi hata anlamına gelir `packages` çözüm kök klasör.</span><span class="sxs-lookup"><span data-stu-id="650e6-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="650e6-123">Bu durum, yaygın olarak kaynak denetimi veya başka bir yükleme projenin kaynak kodu elde oluşur.</span><span class="sxs-lookup"><span data-stu-id="650e6-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="650e6-124">Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri bunlar paket akışları nuget.org gibi geri yüklenebileceği olduğundan (bkz [paketler ve kaynak denetimi](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="650e6-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="650e6-125">Bunları dahil olmak üzere Aksi durumda depo Şişir veya gereksiz yere büyük .zip dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="650e6-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="650e6-126">Paketler geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="650e6-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="650e6-127">Visual Studio'da paket geri yüklemesi seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu, her iki seçenek altında ayarı **paketi geri yüklemesi**ve seçme **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="650e6-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="650e6-128">Ardından çözümü yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="650e6-128">Then build the solution again.</span></span>
- <span data-ttu-id="650e6-129">.NET Core projelerde çalıştırmak `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).</span><span class="sxs-lookup"><span data-stu-id="650e6-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="650e6-130">Komut satırında çalıştırmak `nuget restore` (ile oluşturulmuş projelerde dışında `dotnet`, bu durumda kullanmak `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="650e6-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="650e6-131">PackageReference biçimi kullanarak projeleri ile komut satırında çalıştırmak `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="650e6-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="650e6-132">Başarılı bir geri yüklendikten sonra paketi mevcut olmalıdır *paketleri genel* klasör.</span><span class="sxs-lookup"><span data-stu-id="650e6-132">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="650e6-133">PackageReference kullanarak projeleri için bir geri yükleme yeniden oluşturmanız gerekir `obj/project.assets.json` dosya; kullanarak projeleri için `packages.config`, paket projesinin görünmelidir `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="650e6-133">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="650e6-134">Projeyi şimdi başarıyla oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="650e6-134">The project should now build successfully.</span></span> <span data-ttu-id="650e6-135">Aksi durumda, [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz sizinle izleyecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="650e6-135">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="650e6-136">Varlıklar bulunamadı project.assets.json dosya</span><span class="sxs-lookup"><span data-stu-id="650e6-136">Assets file project.assets.json not found</span></span>

<span data-ttu-id="650e6-137">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="650e6-137">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="650e6-138">`project.assets.json` Dosyası, tüm gerekli paketleri bilgisayarda yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimi kullanırken bir projenin bağımlılık grafiğinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="650e6-138">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="650e6-139">Bu dosya paket geri yüklemesi dinamik olarak oluşturulduğundan, kaynak denetimine genellikle eklenmez.</span><span class="sxs-lookup"><span data-stu-id="650e6-139">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="650e6-140">Sonuç olarak, aşağıdaki gibi bir araçla proje oluşturma bu hata oluşur `msbuild` , otomatik olarak paketler geri yüklemez.</span><span class="sxs-lookup"><span data-stu-id="650e6-140">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="650e6-141">Bu durumda, çalıştırmak `msbuild /t:restore` arkasından `msbuild`, veya `dotnet build` (hangi geri yükler paketleri otomatik olarak).</span><span class="sxs-lookup"><span data-stu-id="650e6-141">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="650e6-142">Paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz [önceki bölümde](#missing).</span><span class="sxs-lookup"><span data-stu-id="650e6-142">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="650e6-143">Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı</span><span class="sxs-lookup"><span data-stu-id="650e6-143">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="650e6-144">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="650e6-144">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="650e6-145">Bu hata, paket geri yükleme NuGet yapılandırmanızda devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="650e6-145">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="650e6-146">Visual Studio içindeki geçerli ayarları altında daha önce açıklandığı gibi değiştirebilirsiniz [Visual Studio kullanıcılar için hızlı çözüm](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="650e6-146">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="650e6-147">Bu ayarları doğrudan geçerli de düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows'da ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta).</span><span class="sxs-lookup"><span data-stu-id="650e6-147">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="650e6-148">Emin olun `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="650e6-148">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="650e6-149">Düzenlediyseniz `packageRestore` ayarlarını doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir böylece Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="650e6-149">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="650e6-150">Diğer olası koşulları</span><span class="sxs-lookup"><span data-stu-id="650e6-150">Other potential conditions</span></span>

- <span data-ttu-id="650e6-151">Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet restore kullanılacağını belirten bir ileti ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="650e6-151">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="650e6-152">Ancak, bir geri yükleme çalıştıran söyleyin, "tüm paketler zaten yüklendi ve geri yüklenecek bir şey yok."</span><span class="sxs-lookup"><span data-stu-id="650e6-152">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="650e6-153">Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="650e6-153">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="650e6-154">Hata devam ederse kullanmak `nuget locals all -clear` veya `dotnet locals all --clear` temizlemek için komut satırından *paketleri genel* ve açıklandığı gibi klasör önbelleğe [önbellek klasörvegenelpaketleriniyönetme](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="650e6-154">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="650e6-155">Bir proje kaynak denetiminden alırken, proje klasörlerinizi salt okunur ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="650e6-155">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="650e6-156">Klasör izinlerini değiştirin ve paketleri geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="650e6-156">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="650e6-157">NuGet'ın eski sürümünü kullanıyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="650e6-157">You may be using an old version of NuGet.</span></span> <span data-ttu-id="650e6-158">Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="650e6-158">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="650e6-159">Visual Studio 2015 için 3.6.0 öneririz.</span><span class="sxs-lookup"><span data-stu-id="650e6-159">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="650e6-160">Başka bir sorunla karşılaşırsanız [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="650e6-160">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>