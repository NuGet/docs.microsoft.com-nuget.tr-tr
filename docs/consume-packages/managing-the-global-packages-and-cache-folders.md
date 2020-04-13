---
title: NuGet'deki küresel paketleri, önbellekleri, geçici klasörleri nasıl yönetebilirsiniz?
description: Paketleri yüklerken, geri yüklerken ve güncellerken kullanılan genel paket yükleme klasörünü, paket önbelleğini ve bilgisayarda bulunan geçici klasörleri nasıl yönetiriz?
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428970"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="d7931-103">Genel paketleri, önbelleği ve geçici klasörleri yönetme</span><span class="sxs-lookup"><span data-stu-id="d7931-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="d7931-104">Bir paketi yüklediğinizde, güncellediğinizde veya geri yüklediğinizde, NuGet paketleri ve paket bilgilerini proje yapınızın dışındaki çeşitli klasörlerde yönetir:</span><span class="sxs-lookup"><span data-stu-id="d7931-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="d7931-105">Adı</span><span class="sxs-lookup"><span data-stu-id="d7931-105">Name</span></span> | <span data-ttu-id="d7931-106">Açıklama ve Konum (kullanıcı başına)</span><span class="sxs-lookup"><span data-stu-id="d7931-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="d7931-107">küresel&#8209;paketleri</span><span class="sxs-lookup"><span data-stu-id="d7931-107">global&#8209;packages</span></span> | <span data-ttu-id="d7931-108">*Genel paketler* klasörü, NuGet'in indirilen herhangi bir paketi yüklendiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="d7931-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="d7931-109">Her paket, paket tanımlayıcısı ve sürüm numarasıyla eşleşen bir alt klasöre tamamen genişletilir.</span><span class="sxs-lookup"><span data-stu-id="d7931-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="d7931-110">[PackageReference](package-references-in-project-files.md) biçimini kullanan projeler her zaman paketleri doğrudan bu klasörden kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7931-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="d7931-111">[packages.config,](../reference/packages-config.md)paketleri kullanırken *genel paketler* klasörüne yüklenir ve proje `packages` klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="d7931-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="d7931-112">Windows:`%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="d7931-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="d7931-113">Mac/Linux:`~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="d7931-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="d7931-114">NUGET_PACKAGES ortam `globalPackagesFolder` değişkenini, `repositoryPath` veya yapılandırma [ayarlarını](../reference/nuget-config-file.md#config-section) (Sırasıyla PackageReference ve `RestorePackagesPath` `packages.config`MSBuild özelliğini kullanırken) veya MSBuild özelliğini (yalnızca MSBuild) kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="d7931-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="d7931-115">Ortam değişkeni yapılandırma ayarından önce gelir.</span><span class="sxs-lookup"><span data-stu-id="d7931-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="d7931-116">http&#8209;önbellek</span><span class="sxs-lookup"><span data-stu-id="d7931-116">http&#8209;cache</span></span> | <span data-ttu-id="d7931-117">Visual Studio Package Manager (NuGet 3.x+) ve `dotnet` araç, indirilen paketlerin kopyalarını `.dat` bu önbellekte (dosya olarak kaydedilir) her paket kaynağı için alt klasörler halinde düzenler.</span><span class="sxs-lookup"><span data-stu-id="d7931-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="d7931-118">Paketler genişletilmez ve önbelleğin son kullanma süresi 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="d7931-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="d7931-119">Windows:`%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="d7931-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="d7931-120">Mac/Linux:`~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="d7931-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="d7931-121">NUGET_HTTP_CACHE_PATH ortamı değişkenini kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="d7931-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="d7931-122">Temp</span><span class="sxs-lookup"><span data-stu-id="d7931-122">temp</span></span> | <span data-ttu-id="d7931-123">NuGet'in çeşitli işlemleri sırasında geçici dosyaları depoladığı klasör.</span><span class="sxs-lookup"><span data-stu-id="d7931-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="d7931-124">Windows:`%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="d7931-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="d7931-125">Mac/Linux:`/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="d7931-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="d7931-126">eklentileri-önbellek **4.8+**</span><span class="sxs-lookup"><span data-stu-id="d7931-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="d7931-127">NuGet'in operasyon talepleri isteğinin sonuçlarını depoladığı klasör.</span><span class="sxs-lookup"><span data-stu-id="d7931-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="d7931-128">Windows:`%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="d7931-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="d7931-129">Mac/Linux:`~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="d7931-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="d7931-130">NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="d7931-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="d7931-131">NuGet 3.5 ve önceki *paketler-önbellek* yerine *http-önbellek*kullanır `%localappdata%\NuGet\Cache`, hangi bulunur .</span><span class="sxs-lookup"><span data-stu-id="d7931-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="d7931-132">Önbellek ve *genel paketler* klasörlerini kullanarak NuGet genellikle bilgisayarda zaten var olan paketleri karşıdan yükler, yükleme, güncelleştirme ve geri yükleme işlemlerinin performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="d7931-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="d7931-133">PackageReference'ı kullanırken, *genel paketler* klasörü indirilen paketleri, yanlışlıkla kaynak denetimine eklenebilecekleri proje klasörlerinde tutmayı da önler ve NuGet'in bilgisayar depolama üzerindeki genel etkisini azaltır.</span><span class="sxs-lookup"><span data-stu-id="d7931-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="d7931-134">Bir paket almak istendiğinde, NuGet ilk olarak *genel paketler* klasörüne bakar.</span><span class="sxs-lookup"><span data-stu-id="d7931-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="d7931-135">Paketin tam sürümü yoksa, NuGet http olmayan tüm paket kaynaklarını denetler.</span><span class="sxs-lookup"><span data-stu-id="d7931-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="d7931-136">Paket hala bulunamazsa, `dotnet.exe` komutlarla `-NoCache` veya `nuget.exe` komutlarla belirtmediğiniz `--no-cache` sürece NuGet paketi http *önbelleğinde* arar.</span><span class="sxs-lookup"><span data-stu-id="d7931-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="d7931-137">Paket önbellekte değilse veya önbellek kullanılmamışsa, NuGet paketi HTTP üzerinden alır.</span><span class="sxs-lookup"><span data-stu-id="d7931-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="d7931-138">Daha fazla bilgi için [bkz.](../concepts/package-installation-process.md)</span><span class="sxs-lookup"><span data-stu-id="d7931-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="d7931-139">Klasör konumlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d7931-139">Viewing folder locations</span></span>

<span data-ttu-id="d7931-140">[Nuget locals komutunu](../reference/cli-reference/cli-ref-locals.md)kullanarak konumları görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7931-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="d7931-141">Tipik çıktı (Windows; "user1" geçerli kullanıcı adıdır:</span><span class="sxs-lookup"><span data-stu-id="d7931-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="d7931-142">(`package-cache` NuGet 2.x'te kullanılır ve NuGet 3.5 ve daha önce siyle birlikte görünür.)</span><span class="sxs-lookup"><span data-stu-id="d7931-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="d7931-143">Ayrıca [noktanu nuget yerel komutunu](/dotnet/core/tools/dotnet-nuget-locals)kullanarak klasör konumlarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7931-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="d7931-144">Tipik çıktı (Mac/Linux; "user1" geçerli kullanıcı adıdır:</span><span class="sxs-lookup"><span data-stu-id="d7931-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="d7931-145">Tek bir klasörün konumunu görüntülemek `http-cache` `global-packages`için `temp`, `plugins-cache` , `all`, veya yerine .</span><span class="sxs-lookup"><span data-stu-id="d7931-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="d7931-146">Yerel klasörleri temizleme</span><span class="sxs-lookup"><span data-stu-id="d7931-146">Clearing local folders</span></span>

<span data-ttu-id="d7931-147">Paket yükleme sorunlarıyla karşılaşırsanız veya uzak bir galeriden paket yüklediğinizden `locals --clear` emin olmak istiyorsanız, klasörü `locals -clear` temizlemek veya `all` temizlemek için klasörü belirterek seçeneği (dotnet.exe) veya (nuget.exe) kullanın:</span><span class="sxs-lookup"><span data-stu-id="d7931-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="d7931-148">Visual Studio'da şu anda açık olan projeler tarafından kullanılan paketler *genel paketler* klasöründen temizlenmez.</span><span class="sxs-lookup"><span data-stu-id="d7931-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="d7931-149">Visual Studio 2017'den **itibaren, NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutunu > Araçlar'ı kullanın ve ardından Tüm **NuGet Önbelleğini(ler) temizle'yi**seçin.</span><span class="sxs-lookup"><span data-stu-id="d7931-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="d7931-150">Önbelleği yönetmek şu anda Paket Yöneticisi Konsolu aracılığıyla kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="d7931-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="d7931-151">Visual Studio 2015'te cli komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7931-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Önbellekleri temizlemek için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="d7931-153">Hatalarda sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d7931-153">Troubleshooting errors</span></span>

<span data-ttu-id="d7931-154">Aşağıdaki hatalar kullanırken `nuget locals` oluşabilir `dotnet nuget locals`veya:</span><span class="sxs-lookup"><span data-stu-id="d7931-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="d7931-155">*Hata: İşlem, <package> başka bir işlem tarafından kullanıldığından* veya yerel kaynakları temizlemeden dosyaya erişemiyor: *Bir veya daha fazla dosya silinemiyor*</span><span class="sxs-lookup"><span data-stu-id="d7931-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="d7931-156">Klasördeki bir veya daha fazla dosya başka bir işlem tarafından kullanılıyor; örneğin, *genel paketler* klasöründeki paketleri ifade eden bir Visual Studio projesi açıktır.</span><span class="sxs-lookup"><span data-stu-id="d7931-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="d7931-157">Bu işlemleri kapatın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d7931-157">Close those processes and try again.</span></span>

- <span data-ttu-id="d7931-158">*Hata: Yola <path> erişim reddedildi* veya *dizin boş değil*</span><span class="sxs-lookup"><span data-stu-id="d7931-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="d7931-159">Önbellekteki dosyaları silme izniniz yok.</span><span class="sxs-lookup"><span data-stu-id="d7931-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="d7931-160">Mümkünse klasör izinlerini değiştirin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d7931-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="d7931-161">Aksi takdirde, sistem yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="d7931-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="d7931-162">*Hata: Belirtilen yol, dosya adı veya her ikisi de çok uzun. Tam nitelikli dosya adı 260 karakterden az olmalı ve dizin adı 248 karakterden az olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="d7931-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="d7931-163">Klasör adlarını kısaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d7931-163">Shorten the folder names and try again.</span></span>
