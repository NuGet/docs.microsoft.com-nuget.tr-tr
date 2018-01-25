---
title: "NuGet CLI yükleme komutunu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe yükleme komut başvurusu"
keywords: "nuget başvuru yükleyin, yükleme paketi komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b77e0e6ce045d1a1e59b29f770b5aca13fc4e7e3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="ffbf5-104">Yükleme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ffbf5-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="ffbf5-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="ffbf5-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ffbf5-106">İndirir ve bir paket bir projeye geçerli klasörü belirtilen paket kaynaklarını kullanarak için varsayılan değer olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="ffbf5-107">Paket bir proje bağlamı dışında doğrudan indirmek için üzerinde paketin sayfasını ziyaret [nuget.org](https://www.nuget.org) seçip **karşıdan** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="ffbf5-108">Herhangi bir kaynağa belirtilirse, listelenenler genel yapılandırma dosyasında `%APPDATA%\NuGet\NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="ffbf5-109">Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md) ek ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="ffbf5-110">Özel paket belirtilirse, `install` projenin içinde listelenen tüm paketler yükler `packages.config` dosyasının benzer URL'ini [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ffbf5-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="ffbf5-111">`install` Komutu bir proje dosyası değiştirilmez veya `packages.config`; bu şekilde, benzer `restore` yalnızca diske paketleri ekler ancak bir projenin bağımlılıkları değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="ffbf5-112">Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden bir proje eklemek veya değiştirmek `packages.config` ve ardından çalıştırın `install` veya `restore`.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="ffbf5-113">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ffbf5-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="ffbf5-114">Burada `<packageID>` (en son sürümünü kullanarak), yüklenecek paketin adları veya `<configFilePath>` tanımlayan `packages.config` yüklenecek paketleri listeleyen dosya.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="ffbf5-115">Belirli bir sürümle belirtebilir `-Version` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="ffbf5-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ffbf5-116">Options</span></span>

| <span data-ttu-id="ffbf5-117">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ffbf5-117">Option</span></span> | <span data-ttu-id="ffbf5-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ffbf5-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffbf5-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ffbf5-119">ConfigFile</span></span> | <span data-ttu-id="ffbf5-120">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ffbf5-121">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ffbf5-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="ffbf5-122">DependencyVersion</span></span> | <span data-ttu-id="ffbf5-123">*(4.4 +)*  Varsayılan bağımlılık çözümleme davranışı geçersiz kılma, belirli bir sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="ffbf5-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="ffbf5-124">DisableParallelProcessing</span></span> | <span data-ttu-id="ffbf5-125">Paralel olarak birden çok paket yüklemeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="ffbf5-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="ffbf5-126">ExcludeVersion</span></span> | <span data-ttu-id="ffbf5-127">Yalnızca paket adı ve sürüm numarası ile adlı bir klasöre paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="ffbf5-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="ffbf5-128">FallbackSource</span></span> | <span data-ttu-id="ffbf5-129">*(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="ffbf5-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ffbf5-130">ForceEnglishOutput</span></span> | <span data-ttu-id="ffbf5-131">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ffbf5-132">Framework</span><span class="sxs-lookup"><span data-stu-id="ffbf5-132">Framework</span></span> | <span data-ttu-id="ffbf5-133">*(4.4 +)*  Hedef framework bağımlılıkları seçmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="ffbf5-134">Varsayılan olarak 'Any' belirtilmediği takdirde.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="ffbf5-135">Yardım</span><span class="sxs-lookup"><span data-stu-id="ffbf5-135">Help</span></span> | <span data-ttu-id="ffbf5-136">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="ffbf5-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="ffbf5-137">NoCache</span></span> | <span data-ttu-id="ffbf5-138">NuGet paketleri yerel makine önbellekleri kullanmalarını engeller.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ffbf5-139">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="ffbf5-139">NonInteractive</span></span> | <span data-ttu-id="ffbf5-140">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ffbf5-141">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="ffbf5-141">OutputDirectory</span></span> | <span data-ttu-id="ffbf5-142">Paketleri yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ffbf5-143">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ffbf5-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="ffbf5-144">PackageSaveMode</span></span> | <span data-ttu-id="ffbf5-145">Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="ffbf5-146">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="ffbf5-146">PreRelease</span></span> | <span data-ttu-id="ffbf5-147">Yayın öncesi paketlerin yüklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="ffbf5-148">Bu bayrak paketleri geri yüklenirken gerekli değil `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="ffbf5-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="ffbf5-149">RequireConsent</span></span> | <span data-ttu-id="ffbf5-150">Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ffbf5-151">Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ffbf5-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="ffbf5-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="ffbf5-152">SolutionDirectory</span></span> | <span data-ttu-id="ffbf5-153">Paketler geri yükleneceği için çözümün kök klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="ffbf5-154">Kaynak</span><span class="sxs-lookup"><span data-stu-id="ffbf5-154">Source</span></span> | <span data-ttu-id="ffbf5-155">Paket kaynaklarını listesini kullanmak için (URL) belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="ffbf5-156">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ffbf5-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="ffbf5-157">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="ffbf5-157">Verbosity</span></span> | <span data-ttu-id="ffbf5-158">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="ffbf5-159">Sürüm</span><span class="sxs-lookup"><span data-stu-id="ffbf5-159">Version</span></span> | <span data-ttu-id="ffbf5-160">Yüklenecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ffbf5-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="ffbf5-161">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ffbf5-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ffbf5-162">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ffbf5-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
