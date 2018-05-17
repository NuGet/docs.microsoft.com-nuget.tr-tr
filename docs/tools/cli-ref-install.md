---
title: NuGet CLI yükleme komutu
description: Nuget.exe yükleme komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1c6ec1181f2f619eb8a4f2d87f7910f25b98e0f4
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/16/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="7e06b-103">install komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7e06b-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="7e06b-104">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="7e06b-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7e06b-105">İndirir ve bir paket bir projeye geçerli klasörü belirtilen paket kaynaklarını kullanarak için varsayılan değer olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="7e06b-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="7e06b-106">Paket bir proje bağlamı dışında doğrudan indirmek için üzerinde paketin sayfasını ziyaret [nuget.org](https://www.nuget.org) seçip **karşıdan** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7e06b-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="7e06b-107">Herhangi bir kaynağa belirtilirse, listelenenler genel yapılandırma dosyasında `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7e06b-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="7e06b-108">Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md) ek ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="7e06b-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="7e06b-109">Özel paket belirtilirse, `install` projenin içinde listelenen tüm paketler yükler `packages.config` dosyasının benzer URL'ini [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7e06b-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="7e06b-110">`install` Komutu bir proje dosyası değiştirilmez veya `packages.config`; bu şekilde, benzer `restore` yalnızca diske paketleri ekler ancak bir projenin bağımlılıkları değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="7e06b-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="7e06b-111">Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden paket ekleme veya değiştirme `packages.config` ve ardından çalıştırın `install` veya `restore`.</span><span class="sxs-lookup"><span data-stu-id="7e06b-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="7e06b-112">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7e06b-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="7e06b-113">Burada `<packageID>` (en son sürümünü kullanarak), yüklenecek paketin adları veya `<configFilePath>` tanımlayan `packages.config` yüklenecek paketleri listeleyen dosya.</span><span class="sxs-lookup"><span data-stu-id="7e06b-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="7e06b-114">Belirli bir sürümle belirtebilir `-Version` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7e06b-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="7e06b-115">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="7e06b-115">Options</span></span>

| <span data-ttu-id="7e06b-116">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7e06b-116">Option</span></span> | <span data-ttu-id="7e06b-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7e06b-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e06b-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7e06b-118">ConfigFile</span></span> | <span data-ttu-id="7e06b-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="7e06b-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7e06b-120">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7e06b-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7e06b-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7e06b-121">DependencyVersion</span></span> | <span data-ttu-id="7e06b-122">*(4.4 +)*  Varsayılan bağımlılık çözümleme davranışı geçersiz kılma, belirli bir sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e06b-122">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="7e06b-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="7e06b-123">DisableParallelProcessing</span></span> | <span data-ttu-id="7e06b-124">Paralel olarak birden çok paket yüklemeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="7e06b-124">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="7e06b-125">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="7e06b-125">ExcludeVersion</span></span> | <span data-ttu-id="7e06b-126">Yalnızca paket adı ve sürüm numarası ile adlı bir klasöre paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="7e06b-126">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="7e06b-127">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="7e06b-127">FallbackSource</span></span> | <span data-ttu-id="7e06b-128">*(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="7e06b-128">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="7e06b-129">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7e06b-129">ForceEnglishOutput</span></span> | <span data-ttu-id="7e06b-130">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="7e06b-130">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7e06b-131">Framework</span><span class="sxs-lookup"><span data-stu-id="7e06b-131">Framework</span></span> | <span data-ttu-id="7e06b-132">*(4.4 +)*  Hedef framework bağımlılıkları seçmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7e06b-132">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="7e06b-133">Varsayılan olarak 'Any' belirtilmediği takdirde.</span><span class="sxs-lookup"><span data-stu-id="7e06b-133">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="7e06b-134">Yardım</span><span class="sxs-lookup"><span data-stu-id="7e06b-134">Help</span></span> | <span data-ttu-id="7e06b-135">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7e06b-135">Displays help information for the command.</span></span> |
| <span data-ttu-id="7e06b-136">NoCache</span><span class="sxs-lookup"><span data-stu-id="7e06b-136">NoCache</span></span> | <span data-ttu-id="7e06b-137">NuGet kullanarak önbelleğe alınmış paketleri engeller.</span><span class="sxs-lookup"><span data-stu-id="7e06b-137">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="7e06b-138">Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="7e06b-138">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7e06b-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7e06b-139">NonInteractive</span></span> | <span data-ttu-id="7e06b-140">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="7e06b-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7e06b-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="7e06b-141">OutputDirectory</span></span> | <span data-ttu-id="7e06b-142">Paketleri yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e06b-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="7e06b-143">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7e06b-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="7e06b-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="7e06b-144">PackageSaveMode</span></span> | <span data-ttu-id="7e06b-145">Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7e06b-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="7e06b-146">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="7e06b-146">PreRelease</span></span> | <span data-ttu-id="7e06b-147">Yayın öncesi paketlerin yüklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e06b-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="7e06b-148">Bu bayrak paketleri geri yüklenirken gerekli değil `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="7e06b-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="7e06b-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="7e06b-149">RequireConsent</span></span> | <span data-ttu-id="7e06b-150">Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="7e06b-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="7e06b-151">Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7e06b-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="7e06b-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="7e06b-152">SolutionDirectory</span></span> | <span data-ttu-id="7e06b-153">Paketler geri yükleneceği için çözümün kök klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e06b-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="7e06b-154">Kaynak</span><span class="sxs-lookup"><span data-stu-id="7e06b-154">Source</span></span> | <span data-ttu-id="7e06b-155">Paket kaynaklarını listesini kullanmak için (URL) belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e06b-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="7e06b-156">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7e06b-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="7e06b-157">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="7e06b-157">Verbosity</span></span> | <span data-ttu-id="7e06b-158">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="7e06b-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="7e06b-159">Sürüm</span><span class="sxs-lookup"><span data-stu-id="7e06b-159">Version</span></span> | <span data-ttu-id="7e06b-160">Yüklenecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e06b-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="7e06b-161">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7e06b-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7e06b-162">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7e06b-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
