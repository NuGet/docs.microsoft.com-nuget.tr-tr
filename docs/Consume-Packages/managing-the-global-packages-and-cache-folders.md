---
title: Genel paketler, önbellek NuGet geçici klasörlerde yönetmek nasıl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Genel paket yükleme klasörü, paket önbellek ve yüklenirken kullanılan bir bilgisayar, geri yükleme ve güncelleştirme paketlerini mevcut geçici klasör yönetmek nasıl.
keywords: Önbellekleri, NuGet yerel önbelleği, genel NuGet önbelleği, NuGet Yereller komutu, bir önbellek temizleme yönetme klasörü, NuGet paketi önbelleği, paketi önbelleğe alma, paket yükleme klasörü, NuGet önbellekleri genel NuGet paketleri
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="33f57-104">Genel paketler, önbellek ve geçici klasörleri yönetme</span><span class="sxs-lookup"><span data-stu-id="33f57-104">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="33f57-105">Yüklediğinizde, güncelleştirme veya bir paket geri yükleme her NuGet paketleri ve proje yapınızı dışında birkaç klasörlerde paket bilgilerini yönetir:</span><span class="sxs-lookup"><span data-stu-id="33f57-105">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="33f57-106">Ad</span><span class="sxs-lookup"><span data-stu-id="33f57-106">Name</span></span> | <span data-ttu-id="33f57-107">Açıklama ve konumu (her bir kullanıcı)</span><span class="sxs-lookup"><span data-stu-id="33f57-107">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="33f57-108">Genel&#8209;paketleri</span><span class="sxs-lookup"><span data-stu-id="33f57-108">global&#8209;packages</span></span> | <span data-ttu-id="33f57-109">*Paketleri genel* klasördür nerede NuGet herhangi indirilen paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="33f57-109">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="33f57-110">Her paket sürüm numarası ve paket tanımlayıcısı ile eşleşen bir alt klasör içine tümüyle genişletilemiyor.</span><span class="sxs-lookup"><span data-stu-id="33f57-110">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="33f57-111">PackageReference kullanarak projeleri her zaman bu klasörden doğrudan kullanım paketleri biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="33f57-111">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="33f57-112">Kullanırken `packages.config`, paketleri yüklenir *paketleri genel* projenin kopyaladığınız klasörü `packages` klasörü.</span><span class="sxs-lookup"><span data-stu-id="33f57-112">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="33f57-113">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="33f57-113">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="33f57-114">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="33f57-114">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="33f57-115">NUGET_PACKAGES ortam değişkeni kullanarak geçersiz kılma `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (PackageReference kullanırken ve `packages.config`sırasıyla), veya `RestorePackagesPath` MSBuild özelliği (MSBuild yalnızca).</span><span class="sxs-lookup"><span data-stu-id="33f57-115">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="33f57-116">Ortam değişkeni üzerinden yapılandırma ayarı öncelik alır.</span><span class="sxs-lookup"><span data-stu-id="33f57-116">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="33f57-117">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="33f57-117">http&#8209;cache</span></span> | <span data-ttu-id="33f57-118">Visual Studio Paket Yöneticisi (NuGet 3.x+) ve `dotnet` aracı bu önbellekteki indirilen paketleri deposu kopyalarını (olarak kaydedilen `.dat` dosyaları), her bir paket kaynağı için alt klasörler halinde düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="33f57-118">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="33f57-119">Paketleri genişletilmemiş ve 30 dakikalık zaman aşımı değeri bir önbelleğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="33f57-119">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="33f57-120">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="33f57-120">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="33f57-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="33f57-121">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="33f57-122">NUGET_HTTP_CACHE_PATH ortam değişkeni kullanarak geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="33f57-122">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="33f57-123">Temp</span><span class="sxs-lookup"><span data-stu-id="33f57-123">temp</span></span> | <span data-ttu-id="33f57-124">NuGet, çeşitli işlemleri sırasında geçici dosyaları depoladığı bir klasör.</span><span class="sxs-lookup"><span data-stu-id="33f57-124">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="33f57-125">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="33f57-125">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="33f57-126">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="33f57-126">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="33f57-127">NuGet 3.5 ve önceki kullanır *paketleri önbellek* yerine *http önbellek*, bulunan `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="33f57-127">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="33f57-128">Önbellek kullanarak ve *paketleri genel* klasörler, NuGet genellikle önler bilgisayarda zaten mevcut paketleri indirme, yükleme performansını iyileştirme, güncelleştirme ve geri yükleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="33f57-128">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="33f57-129">PackageReference, kullanırken *paketleri genel* klasörü ayrıca burada bunlar yanlışlıkla eklenmesi için kaynak denetimi, proje klasör içinde indirilen tutma paketleri engeller ve NuGet genel bilgisayar etkisini azaltır depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="33f57-129">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="33f57-130">Bir paket almak için sorulduğunda, NuGet ilk görünür *paketleri genel* klasör.</span><span class="sxs-lookup"><span data-stu-id="33f57-130">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="33f57-131">Paket'ün tam sürümünü yoksa, NuGet tüm HTTP olmayan paket kaynaklarını denetler.</span><span class="sxs-lookup"><span data-stu-id="33f57-131">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="33f57-132">Paket yine bulunamazsa, NuGet paketi arar *http önbellek* belirtmediğiniz sürece `--no-cache` ile `dotnet.exe` komutları veya `-NoCache` ile `nuget.exe` komutları.</span><span class="sxs-lookup"><span data-stu-id="33f57-132">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="33f57-133">Paketi önbellekte değil veya önbelleği kullanılmaz, NuGet paketi HTTP üzerinden sonra alır.</span><span class="sxs-lookup"><span data-stu-id="33f57-133">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="33f57-134">Daha fazla bilgi için bkz: [bir paket yüklendiğinde ne olacağını](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="33f57-134">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="33f57-135">Klasör konumlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="33f57-135">Viewing folder locations</span></span>

<span data-ttu-id="33f57-136">Klasör konumlarını kullanarak görüntüleyebileceğiniz [dotnet nuget Yereller komutu](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="33f57-136">You can view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="33f57-137">Tipik çıkış (Mac/Linux; "user1" olan geçerli kullanıcı adı):</span><span class="sxs-lookup"><span data-stu-id="33f57-137">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

<span data-ttu-id="33f57-138">Tek bir klasör konumunu görüntülemek için kullanın `http-cache`, `global-packages`, veya `temp` yerine `all`.</span><span class="sxs-lookup"><span data-stu-id="33f57-138">To display the location of a single folder, use `http-cache`, `global-packages`, or `temp` instead of `all`.</span></span> 

<span data-ttu-id="33f57-139">Ayrıca konumlardaki görüntülemek [nuget Yereller komutu](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="33f57-139">You also view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

<span data-ttu-id="33f57-140">Tipik çıkış (Windows; "user1" olan geçerli kullanıcı adı):</span><span class="sxs-lookup"><span data-stu-id="33f57-140">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

<span data-ttu-id="33f57-141">(`package-cache` NuGet içinde kullanılan 2.x ve NuGet 3.5 ve daha önce görünür.)</span><span class="sxs-lookup"><span data-stu-id="33f57-141">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="33f57-142">Yerel klasörleri temizleme</span><span class="sxs-lookup"><span data-stu-id="33f57-142">Clearing local folders</span></span>

<span data-ttu-id="33f57-143">Paket yükleme sorunlarla veya aksi takdirde uzaktan galerisinden, kullanım paketleri yüklüyorsanız sağlamak istiyorsanız `locals --clear` seçeneği (dotnet.exe) veya `locals -clear` (nuget.exe) temizlemek için klasörü belirtme veya `all` için tüm klasörleri temizleyin:</span><span class="sxs-lookup"><span data-stu-id="33f57-143">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="33f57-144">Visual Studio şu anda açık olan projeler tarafından kullanılan herhangi bir paket gelen temizlenmez *paketleri genel* klasör.</span><span class="sxs-lookup"><span data-stu-id="33f57-144">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="33f57-145">Visual Studio'da kullanın **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutunu ve ardından **Temizle tüm NuGet önbellekler**.</span><span class="sxs-lookup"><span data-stu-id="33f57-145">In Visual Studio, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="33f57-146">Önbellek yönetme, Paket Yöneticisi konsolu aracılığıyla şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="33f57-146">Managing the cache isn't presently available through the Package Manager Console.</span></span>

![Önbellekleri temizlemek için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="33f57-148">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="33f57-148">Troubleshooting errors</span></span>

<span data-ttu-id="33f57-149">Kullanırken aşağıdaki hatalar oluşabilir `nuget locals` veya `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="33f57-149">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="33f57-150">*Hata: İşlem dosyasına erişemiyor <package> başka bir işlem tarafından kullanıldığından* veya *yerel kaynakları temizleme başarısız oldu: bir veya daha fazla dosya silinemiyor*</span><span class="sxs-lookup"><span data-stu-id="33f57-150">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="33f57-151">Bir veya daha fazla dosya klasöründe başka bir işlem tarafından kullanılıyor; Örneğin, bir Visual Studio projesi paketlerinde başvurduğu açık olduğu *paketleri genel* klasör.</span><span class="sxs-lookup"><span data-stu-id="33f57-151">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="33f57-152">Bu işlemleri kapatın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="33f57-152">Close those processes and try again.</span></span>

- <span data-ttu-id="33f57-153">*Hata: Erişim yolunu <path> reddedildi* veya *dizini boş değil*</span><span class="sxs-lookup"><span data-stu-id="33f57-153">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="33f57-154">Önbellekteki dosyaları silmek için izniniz yok.</span><span class="sxs-lookup"><span data-stu-id="33f57-154">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="33f57-155">Mümkünse, klasör izinlerini değiştirin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="33f57-155">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="33f57-156">Aksi takdirde, sistem yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="33f57-156">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="33f57-157">*Hata: Belirtilen yolun, dosya adı veya her ikisini birden çok uzun. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden kısa olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="33f57-157">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="33f57-158">Klasör adları kısaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="33f57-158">Shorten the folder names and try again.</span></span>
