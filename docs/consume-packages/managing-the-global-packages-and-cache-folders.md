---
title: NuGet 'de küresel paketleri, önbelleği, temp klasörlerini yönetme
description: Paket yükleme, geri yükleme ve güncelleştirme sırasında kullanılan genel paket yükleme klasörünü, paket önbelleğini ve bir bilgisayarda bulunan temp klasörlerini yönetme.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e5585267d4ce2563d77ff30ec5c31e196d98686a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774793"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="4e815-103">Küresel paketleri, önbelleği ve temp klasörlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="4e815-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="4e815-104">Bir paketi yüklediğinizde, güncelleştirdiğinizde veya geri yükledikten sonra, NuGet paketleri ve paket bilgilerini proje yapınız dışında çeşitli klasörlerde yönetir:</span><span class="sxs-lookup"><span data-stu-id="4e815-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="4e815-105">Name</span><span class="sxs-lookup"><span data-stu-id="4e815-105">Name</span></span> | <span data-ttu-id="4e815-106">Açıklama ve konum (Kullanıcı başına)</span><span class="sxs-lookup"><span data-stu-id="4e815-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="4e815-107">Genel&#8209;paketleri</span><span class="sxs-lookup"><span data-stu-id="4e815-107">global&#8209;packages</span></span> | <span data-ttu-id="4e815-108">*Genel paketler* klasörü, NuGet 'in indirilen tüm paketleri yüklediği yerdir.</span><span class="sxs-lookup"><span data-stu-id="4e815-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="4e815-109">Her paket, paket tanımlayıcısı ve sürüm numarasıyla eşleşen bir alt klasöre tamamen genişletilir.</span><span class="sxs-lookup"><span data-stu-id="4e815-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="4e815-110">[Packagereference](package-references-in-project-files.md) biçimini kullanan projeler her zaman paketleri doğrudan bu klasörden kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e815-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="4e815-111">[packages.config](../reference/packages-config.md)kullanılırken, paketler *genel paketler* klasörüne yüklenir ve ardından projenin `packages` klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4e815-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="4e815-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="4e815-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="4e815-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="4e815-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="4e815-114">NUGET_PACKAGES ortam değişkenini, `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (, packagereference ve `packages.config` sırasıyla) veya `RestorePackagesPath` MSBuild özelliğini (yalnızca MSBuild) kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="4e815-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="4e815-115">Ortam değişkeni yapılandırma ayarından önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="4e815-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="4e815-116">http&#8209;önbelleği</span><span class="sxs-lookup"><span data-stu-id="4e815-116">http&#8209;cache</span></span> | <span data-ttu-id="4e815-117">Visual Studio Paket Yöneticisi (NuGet 3. x +) ve araç, `dotnet` indirilen paketlerin kopyalarını `.dat` , her bir paket kaynağı için alt klasörlere düzenlenmiş bu önbellekte (dosya olarak kaydedilir) depolar.</span><span class="sxs-lookup"><span data-stu-id="4e815-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="4e815-118">Paketler genişletilmez ve önbellekte 30 dakikalık bir sona erme saati bulunur.</span><span class="sxs-lookup"><span data-stu-id="4e815-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="4e815-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="4e815-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="4e815-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="4e815-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="4e815-121">NUGET_HTTP_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="4e815-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="4e815-122">temp</span><span class="sxs-lookup"><span data-stu-id="4e815-122">temp</span></span> | <span data-ttu-id="4e815-123">NuGet 'in farklı işlemleri sırasında geçici dosyaları depoladığı bir klasör.</span><span class="sxs-lookup"><span data-stu-id="4e815-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="4e815-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="4e815-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="4e815-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="4e815-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="4e815-126">Eklentiler-önbellek **4.8 +**</span><span class="sxs-lookup"><span data-stu-id="4e815-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="4e815-127">NuGet 'in işlem talep isteğinden sonuçları depoladığı bir klasör.</span><span class="sxs-lookup"><span data-stu-id="4e815-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="4e815-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="4e815-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="4e815-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="4e815-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="4e815-130">NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="4e815-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="4e815-131">NuGet 3,5 ve önceki sürümleri, ' de bulunan *http önbelleği* yerine *paketler-önbellek* kullanır `%localappdata%\NuGet\Cache` .</span><span class="sxs-lookup"><span data-stu-id="4e815-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="4e815-132">NuGet, önbellek ve *küresel paketler* klasörlerini kullanarak, yükleme, güncelleştirme ve geri yükleme işlemlerinin performansını artırarak, genellikle bilgisayarda zaten mevcut olan paketleri indirmeyi önler.</span><span class="sxs-lookup"><span data-stu-id="4e815-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="4e815-133">PackageReference kullanılırken, *genel paketler* klasörü, karşıdan yüklenen paketlerin proje klasörleri içinde tutulmasını önler. Bu dosyalar, yanlışlıkla kaynak denetimine eklenmiş olabilir ve NuGet 'in bilgisayar depolamada genel etkisini azaltır.</span><span class="sxs-lookup"><span data-stu-id="4e815-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="4e815-134">Bir paketi almak isteyip istemediğiniz sorulduğunda, NuGet ilk olarak *genel paketler* klasörüne bakar.</span><span class="sxs-lookup"><span data-stu-id="4e815-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="4e815-135">Paketin tam sürümü orada yoksa NuGet, HTTP olmayan tüm paket kaynaklarını denetler.</span><span class="sxs-lookup"><span data-stu-id="4e815-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="4e815-136">Paket hala bulunamazsa NuGet, komutlarla veya komutlarla belirtmediğiniz takdirde, paketi *http önbelleğinde* arar `--no-cache` `dotnet.exe` `-NoCache` `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="4e815-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="4e815-137">Paket önbellekte değilse veya önbellek kullanılmıyorsa, NuGet paketi HTTP üzerinden alır.</span><span class="sxs-lookup"><span data-stu-id="4e815-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="4e815-138">Daha fazla bilgi için bkz. [bir paket yüklendiğinde ne olur?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="4e815-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="4e815-139">Klasör konumlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="4e815-139">Viewing folder locations</span></span>

<span data-ttu-id="4e815-140">[NuGet Yereller komutunu](../reference/cli-reference/cli-ref-locals.md)kullanarak konumları görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4e815-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="4e815-141">Tipik çıkış (Windows; "kullanıcı1" geçerli kullanıcı adıdır):</span><span class="sxs-lookup"><span data-stu-id="4e815-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="4e815-142">( `package-cache` NuGet 2. x içinde kullanılır ve nuget 3,5 ve önceki sürümlerde görüntülenir.)</span><span class="sxs-lookup"><span data-stu-id="4e815-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="4e815-143">Ayrıca, [DotNet NuGet Yereller komutunu](/dotnet/core/tools/dotnet-nuget-locals)kullanarak klasör konumlarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4e815-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="4e815-144">Tipik çıkış (Mac/Linux; "kullanıcı1" geçerli kullanıcı adıdır):</span><span class="sxs-lookup"><span data-stu-id="4e815-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="4e815-145">Tek bir klasörün konumunu görüntüleme,,, `http-cache` `global-packages` `temp` veya `plugins-cache` yerine kullanın `all` .</span><span class="sxs-lookup"><span data-stu-id="4e815-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="4e815-146">Yerel klasörleri Temizleme</span><span class="sxs-lookup"><span data-stu-id="4e815-146">Clearing local folders</span></span>

<span data-ttu-id="4e815-147">Paket yükleme sorunlarıyla karşılaşırsanız veya uzak bir galeriden paket yüklediğinizden emin olmak istiyorsanız, `locals --clear` (dotnet.exe) veya `locals -clear` (nuget.exe) seçeneğini kullanın, temizlenecek klasörü belirterek veya `all` tüm klasörleri temizleyin:</span><span class="sxs-lookup"><span data-stu-id="4e815-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="4e815-148">Visual Studio 'da Şu anda açık olan projeler tarafından kullanılan tüm paketler, *genel paketler* klasöründen silinmez.</span><span class="sxs-lookup"><span data-stu-id="4e815-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="4e815-149">Visual Studio 2017 ' den başlayarak, **araç > NuGet paket yöneticisi > Paket Yöneticisi ayarları** menü komutunu kullanın ve **Tüm NuGet önbelleklerini temizle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="4e815-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="4e815-150">Önbelleğin yönetilmesi, şu anda Paket Yöneticisi konsolu aracılığıyla kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="4e815-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="4e815-151">Visual Studio 2015 ' de, bunun yerine CLı komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e815-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Önbellekleri temizlemek için NuGet seçenek komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="4e815-153">Hatalarda sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4e815-153">Troubleshooting errors</span></span>

<span data-ttu-id="4e815-154">Veya kullanırken aşağıdaki hatalar oluşabilir `nuget locals` `dotnet nuget locals` :</span><span class="sxs-lookup"><span data-stu-id="4e815-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="4e815-155">*Hata: <package> başka bir işlem tarafından kullanıldığı* veya *yerel kaynakları temizleyemedi, işlem dosyaya erişemiyor: bir veya daha fazla dosya silinemiyor*</span><span class="sxs-lookup"><span data-stu-id="4e815-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="4e815-156">Klasördeki bir veya daha fazla dosya başka bir işlem tarafından kullanılıyor; Örneğin, *genel paketler* klasöründeki paketlere başvuran bir Visual Studio projesi açıktır.</span><span class="sxs-lookup"><span data-stu-id="4e815-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="4e815-157">Bu işlemi kapatın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4e815-157">Close those processes and try again.</span></span>

- <span data-ttu-id="4e815-158">*Hata: yola erişim <path> engellendi* veya *Dizin boş değil*</span><span class="sxs-lookup"><span data-stu-id="4e815-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="4e815-159">Önbellekteki dosyaları silme izniniz yok.</span><span class="sxs-lookup"><span data-stu-id="4e815-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="4e815-160">Mümkünse klasör izinlerini değiştirip yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4e815-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="4e815-161">Aksi takdirde, sistem yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="4e815-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="4e815-162">*Hata: belirtilen yol, dosya adı veya her ikisi çok uzun. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden az olmalıdır.*</span><span class="sxs-lookup"><span data-stu-id="4e815-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="4e815-163">Klasör adlarını kısaltın ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4e815-163">Shorten the folder names and try again.</span></span>
