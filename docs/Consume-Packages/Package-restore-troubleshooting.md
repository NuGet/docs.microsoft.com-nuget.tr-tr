---
title: "Geri yükleme Visual Studio'da NuGet paketi sorunlarını giderme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio ve bunları gidermek nasıl hatalar geri yükleme ortak NuGet açıklaması."
keywords: "NuGet paket geri yüklemesi, geri yükleme paketleri, sorun giderme, sorun giderme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="5f12e-104">Paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="5f12e-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="5f12e-105">Bu makalede, paketleri ve bunları gidermek için adımları geri yüklerken ortak hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5f12e-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="5f12e-106">Paketler geri yükleme ile ilgili tam Ayrıntılar için bkz: [paket geri yüklemesi](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="5f12e-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="5f12e-107">Buradaki yönergeleri, işe yaramazsa [Lütfen bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece senaryonuz daha dikkatlice inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5f12e-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="5f12e-108">"Yararlıdır bu sayfayı?" kullanmayın</span><span class="sxs-lookup"><span data-stu-id="5f12e-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="5f12e-109">Bunu bize daha fazla bilgi için sizinle vermek değil çünkü bu sayfada görünebilir denetim.</span><span class="sxs-lookup"><span data-stu-id="5f12e-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="5f12e-110">Visual Studio kullanıcılar için hızlı çözümü</span><span class="sxs-lookup"><span data-stu-id="5f12e-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="5f12e-111">İlk paket geri yüklemesi Visual Studio kullanıyorsanız, aşağıdaki gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5f12e-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="5f12e-112">Aksi durumda bölümlerde için devam edin.</span><span class="sxs-lookup"><span data-stu-id="5f12e-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="5f12e-113">Seçin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="5f12e-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="5f12e-114">Her iki seçenekleri altında **paketi geri yüklemesi**.</span><span class="sxs-lookup"><span data-stu-id="5f12e-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="5f12e-115">Seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5f12e-115">Select **OK**.</span></span>
1. <span data-ttu-id="5f12e-116">Projenizi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f12e-116">Build your project again.</span></span>

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="5f12e-118">Bu ayarları da değiştirilebilir, `NuGet.config` bakın; dosyası [onayı](#consent) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5f12e-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="5f12e-119">Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru</span><span class="sxs-lookup"><span data-stu-id="5f12e-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="5f12e-120">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="5f12e-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="5f12e-121">Bu hata oluşur. bir veya daha fazla NuGet Paketlerine yönelik başvuruları içeren bir projeyi derleme çalışıldı, ancak bu paketleri şu anda projede önbelleğe alınmaz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="5f12e-122">(Paketler önbelleğe bir `packages` proje kullanıyorsa, çözüm kök klasör `packages.config`, veya `obj/project.assets.json` proje PackageReference biçimi kullanıyorsa, dosya.)</span><span class="sxs-lookup"><span data-stu-id="5f12e-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="5f12e-123">Bu durum, yaygın olarak kaynak denetimi veya başka bir yükleme projenin kaynak kodu elde oluşur.</span><span class="sxs-lookup"><span data-stu-id="5f12e-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="5f12e-124">Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri bunlar paket akışları nuget.org gibi geri yüklenebileceği olduğundan (bkz [paketler ve kaynak denetimi](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="5f12e-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="5f12e-125">Bunları dahil olmak üzere Aksi durumda depo Şişir veya gereksiz yere büyük .zip dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f12e-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="5f12e-126">Paketler geri yüklemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5f12e-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="5f12e-127">Visual Studio'da paket geri yüklemesi seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu, her iki seçenek altında ayarı **paketi geri yüklemesi**ve seçme **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5f12e-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="5f12e-128">Ardından çözümü yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f12e-128">Then build the solution again.</span></span>
- <span data-ttu-id="5f12e-129">.NET Core projelerde çalıştırmak `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).</span><span class="sxs-lookup"><span data-stu-id="5f12e-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="5f12e-130">Komut satırında çalıştırmak `nuget restore` (ile oluşturulmuş projelerde dışında `dotnet`, bu durumda kullanmak `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="5f12e-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="5f12e-131">PackageReference biçimi kullanarak projeleri ile komut satırında çalıştırmak `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="5f12e-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="5f12e-132">Başarılı bir geri yüklendikten sonra ya da görmeniz gerekir bir `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken).</span><span class="sxs-lookup"><span data-stu-id="5f12e-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="5f12e-133">Projeyi şimdi başarıyla oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="5f12e-133">The project should now build successfully.</span></span> <span data-ttu-id="5f12e-134">Aksi durumda, [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz sizinle izleyecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="5f12e-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="5f12e-135">Varlıklar bulunamadı project.assets.json dosya</span><span class="sxs-lookup"><span data-stu-id="5f12e-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="5f12e-136">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="5f12e-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="5f12e-137">Bu hata için aynı nedenden dolayı açıklandığı şekilde oluşur. [önceki bölümde](#missing), ve aynı çözümlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5f12e-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="5f12e-138">Örneğin, çalışan `msbuild` .NET Core üzerinde kaynak denetiminden elde edilen proje otomatik olarak paketler geri olmaz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="5f12e-139">Bu durumda, çalıştırmak `msbuild /t:restore` arkasından `msbuild`, veya `dotnet build` (hangi geri yükler paketleri otomatik olarak).</span><span class="sxs-lookup"><span data-stu-id="5f12e-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="5f12e-140">Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı</span><span class="sxs-lookup"><span data-stu-id="5f12e-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="5f12e-141">Tam hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="5f12e-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="5f12e-142">Bu hata, paket geri yükleme NuGet yapılandırmanızda devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f12e-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="5f12e-143">Visual Studio içindeki geçerli ayarları altında daha önce açıklandığı gibi değiştirebilirsiniz [Visual Studio kullanıcılar için hızlı çözüm](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="5f12e-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="5f12e-144">Bu ayarları doğrudan geçerli de düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows'da ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta).</span><span class="sxs-lookup"><span data-stu-id="5f12e-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="5f12e-145">Emin olun `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="5f12e-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="5f12e-146">Düzenlediğiniz gerçekleştiriyorsanız `packageRestore` ayarlarını doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir böylece Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5f12e-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="5f12e-147">Diğer olası koşulları</span><span class="sxs-lookup"><span data-stu-id="5f12e-147">Other potential conditions</span></span>

- <span data-ttu-id="5f12e-148">Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet restore kullanılacağını belirten bir ileti ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="5f12e-149">Ancak, bir geri yükleme çalıştıran söyleyin, "tüm paketler zaten yüklendi ve geri yüklenecek bir şey yok."</span><span class="sxs-lookup"><span data-stu-id="5f12e-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="5f12e-150">Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5f12e-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="5f12e-151">Bir proje kaynak denetiminden alırken, proje klasörlerinizi salt okunur ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="5f12e-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="5f12e-152">Klasör izinlerini değiştirin ve paketleri geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="5f12e-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="5f12e-153">NuGet'ın eski sürümünü kullanıyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="5f12e-154">Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="5f12e-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="5f12e-155">Visual Studio 2015 için 3.6.0 öneririz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="5f12e-156">Başka bir sorunla karşılaşırsanız [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f12e-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>