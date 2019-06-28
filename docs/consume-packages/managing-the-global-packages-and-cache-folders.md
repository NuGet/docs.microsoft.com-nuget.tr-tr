---
title: Genel paketleri, önbellek NuGet geçici klasörlere yönetmek nasıl
description: Genel paket yükleme klasörü, paket önbelleğini ve yüklenirken kullanılan bir bilgisayar, geri yükleme ve güncelleştirme paketlerini mevcut geçici klasör yönetmek nasıl.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 4b365488c8dd0e081449552b06451e7b40b5223b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426621"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="82358-103">Genel paketleri, önbellek ve geçici klasör yönetme</span><span class="sxs-lookup"><span data-stu-id="82358-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="82358-104">Yüklemek, güncelleştirmek ya da bir paket geri yükleme olduğunda, NuGet paketleri ve Proje yapısı dışında birçok klasörlerdeki paket bilgilerini yönetir:</span><span class="sxs-lookup"><span data-stu-id="82358-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="82358-105">Ad</span><span class="sxs-lookup"><span data-stu-id="82358-105">Name</span></span> | <span data-ttu-id="82358-106">Açıklama ve konumu (kullanıcı başına)</span><span class="sxs-lookup"><span data-stu-id="82358-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="82358-107">Genel&#8209;paketleri</span><span class="sxs-lookup"><span data-stu-id="82358-107">global&#8209;packages</span></span> | <span data-ttu-id="82358-108">*Genel paketleri* klasördür burada NuGet herhangi indirilen paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="82358-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="82358-109">Her paket tam sürüm numarası ve paket tanımlayıcısı ile eşleşen bir alt klasör içine genişletilir.</span><span class="sxs-lookup"><span data-stu-id="82358-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="82358-110">PackageReference'ı kullanarak projeleri, her zaman kullan paketlerini doğrudan bu klasörden biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="82358-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="82358-111">Kullanırken `packages.config`, için yüklü paketleri *genel paketleri* klasörü, ardından projenin kopyalanır `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="82358-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="82358-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="82358-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="82358-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="82358-114">Geçersiz kılma NUGET_PACKAGES ortam değişkenini kullanarak `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (PackageReference kullanırken ve `packages.config`sırasıyla), veya `RestorePackagesPath` MSBuild özellik (yalnızca MSBuild).</span><span class="sxs-lookup"><span data-stu-id="82358-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="82358-115">Ortam değişkenini üzerinden yapılandırma ayarı önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="82358-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="82358-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="82358-116">http&#8209;cache</span></span> | <span data-ttu-id="82358-117">Visual Studio Paket Yöneticisi'ni (NuGet 3.x+) ve `dotnet` aracı bu önbellek içinde indirilen paketler deposu kopyalarını (olarak kaydedilen `.dat` dosyaları), her paket kaynağı için alt klasörler halinde düzenlenmiş.</span><span class="sxs-lookup"><span data-stu-id="82358-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="82358-118">Paketleri genişletilmemiş ve sona erme süresini 30 dakika bir önbelleğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="82358-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="82358-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="82358-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="82358-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="82358-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="82358-121">NUGET_HTTP_CACHE_PATH ortam değişkenini kullanarak geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="82358-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="82358-122">Temp</span><span class="sxs-lookup"><span data-stu-id="82358-122">temp</span></span> | <span data-ttu-id="82358-123">NuGet, çeşitli işlemleri sırasında geçici dosyaları depoladığı bir klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="82358-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="82358-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="82358-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="82358-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="82358-126">Eklentileri önbellek **4.8 +**</span><span class="sxs-lookup"><span data-stu-id="82358-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="82358-127">NuGet işlem talepleri isteği sonuçlardan depoladığı bir klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="82358-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="82358-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="82358-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="82358-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="82358-130">NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="82358-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="82358-131">NuGet 3.5 ve önceki kullanımlar *paketleri önbellek* yerine *http önbellek*, bulunan `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="82358-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="82358-132">Önbellek kullanarak ve *genel paketleri* klasörleri NuGet genellikle önler bilgisayarda zaten mevcut olan paketleri indirme, yükleme performansını iyileştirme, güncelleştirme ve geri yükleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="82358-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="82358-133">PackageReference, kullanırken *genel paketleri* klasör ayrıca tutma indirilen paketler nerede bunlar yanlışlıkla eklenmesi için kaynak denetimi, proje klasörleri içindeki önler ve bilgisayar NuGet'ın genel etkisini azaltır depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="82358-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="82358-134">Bir paket almaya isteyip istemediğiniz sorulduğunda NuGet ilk baktığı *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="82358-135">Paket'ün tam sürümünü yoksa, NuGet HTTP olmayan paket kaynaklarının tümüne denetler.</span><span class="sxs-lookup"><span data-stu-id="82358-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="82358-136">Paket hala bulunamıyorsa, NuGet paketi arar *http önbellek* belirtmediğiniz sürece `--no-cache` ile `dotnet.exe` komutları veya `-NoCache` ile `nuget.exe` komutları.</span><span class="sxs-lookup"><span data-stu-id="82358-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="82358-137">Paket önbellekte değil ya da önbelleği kullanılmaz, NuGet paketi ardından HTTP üzerinden alır.</span><span class="sxs-lookup"><span data-stu-id="82358-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="82358-138">Daha fazla bilgi için [bir paket yüklendikten sonra ne olur?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="82358-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="82358-139">Klasör konumlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="82358-139">Viewing folder locations</span></span>

<span data-ttu-id="82358-140">Konumları kullanarak görüntüleyebileceğiniz [nuget Yereller komutu](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="82358-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="82358-141">Tipik çıkış (Windows; "user1" olan geçerli kullanıcı adı):</span><span class="sxs-lookup"><span data-stu-id="82358-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="82358-142">(`package-cache` Nuget'te kullanılan 2.x ve NuGet 3.5 ve önceki sürümleri görüntülenir.)</span><span class="sxs-lookup"><span data-stu-id="82358-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="82358-143">Klasör konumlarını kullanarak da görüntüleyebilirsiniz [dotnet nuget Yereller komutu](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="82358-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="82358-144">Tipik çıkış (Mac/Linux; "user1" olan geçerli kullanıcı adı):</span><span class="sxs-lookup"><span data-stu-id="82358-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="82358-145">Tek bir klasör konumunu görüntülemek için kullanın `http-cache`, `global-packages`, `temp`, veya `plugins-cache` yerine `all`.</span><span class="sxs-lookup"><span data-stu-id="82358-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="82358-146">Yerel klasörler temizleme</span><span class="sxs-lookup"><span data-stu-id="82358-146">Clearing local folders</span></span>

<span data-ttu-id="82358-147">Paket yükleme sorunlarla veya aksi halde uzak galerisinden, kullanım paketleri güvenilirliğinden emin olmak isterseniz `locals --clear` seçeneği (dotnet.exe) veya `locals -clear` (nuget.exe) temizlemek için bir klasör belirterek veya `all` için tüm klasörleri temizleyin:</span><span class="sxs-lookup"><span data-stu-id="82358-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="82358-148">Visual Studio'da açık olan projeler tarafından kullanılan tüm paketler gelen temizlenmez *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="82358-149">Visual Studio 2017'den itibaren kullanın **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutunu ve ardından **Temizle tüm NuGet önbellekler**.</span><span class="sxs-lookup"><span data-stu-id="82358-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="82358-150">Önbellek Yönetimi, Paket Yöneticisi konsolu aracılığıyla şu anda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="82358-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="82358-151">Visual Studio 2015'te, bunun yerine CLI komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="82358-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Önbellek Temizleme için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="82358-153">Sorun giderme hataları</span><span class="sxs-lookup"><span data-stu-id="82358-153">Troubleshooting errors</span></span>

<span data-ttu-id="82358-154">Kullanırken aşağıdaki hatalar oluşabilir `nuget locals` veya `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="82358-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="82358-155">*Hata: İşlem dosyaya erişemiyor <package> başka bir işlem tarafından kullanıldığından* veya *yerel kaynakları temizleme başarısız oldu: Bir veya daha fazla dosya silinemedi*</span><span class="sxs-lookup"><span data-stu-id="82358-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="82358-156">Bir veya daha fazla dosya klasörüne başka bir işlem tarafından kullanılıyor; Örneğin, Visual Studio projesi paketlerine başvuran açık olan *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="82358-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="82358-157">Bu işlemleri kapatın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="82358-157">Close those processes and try again.</span></span>

- <span data-ttu-id="82358-158">*Hata: Yoluna erişim <path> reddedildi* veya *dizini boş değil*</span><span class="sxs-lookup"><span data-stu-id="82358-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="82358-159">Önbellekteki dosyaları silmek için izniniz yok.</span><span class="sxs-lookup"><span data-stu-id="82358-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="82358-160">Mümkünse, klasör izinlerini değiştirin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="82358-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="82358-161">Aksi takdirde, sistem yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="82358-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="82358-162">*Hata: Belirtilen yol, dosya adı veya her ikisi çok uzun olabilir. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden kısa olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="82358-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="82358-163">Klasör adları kısaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="82358-163">Shorten the folder names and try again.</span></span>
