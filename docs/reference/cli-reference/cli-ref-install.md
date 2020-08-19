---
title: NuGet CLı install komutu
description: nuget.exe install komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623103"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="0963b-103">Install komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="0963b-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="0963b-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="0963b-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0963b-105">Belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="0963b-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="0963b-106">Bir paketi doğrudan bir proje bağlamı dışında indirmek için, [NuGet.org](https://www.nuget.org) adresindeki paketin sayfasını ziyaret edin ve **indirme** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="0963b-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="0963b-107">Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) listelenenler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0963b-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="0963b-108">Daha fazla bilgi için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="0963b-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="0963b-109">Belirli bir paket belirtilmemişse, `install` projenin dosyasında listelenen tüm paketleri `packages.config` ' a benzer hale getirir [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="0963b-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="0963b-110">`install`Komut, bir proje dosyası veya `packages.config` ; Bu şekilde, `restore` yalnızca paketleri diske eklemektedir ancak projenin bağımlılıklarını değiştirmediğinden buna benzer.</span><span class="sxs-lookup"><span data-stu-id="0963b-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="0963b-111">Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin ya da `packages.config` veya öğesini değiştirip `install` veya çalıştırın `restore` .</span><span class="sxs-lookup"><span data-stu-id="0963b-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="0963b-112">Kullanım</span><span class="sxs-lookup"><span data-stu-id="0963b-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="0963b-113">`<packageID>`, Yüklenecek paketin adını (en son sürümü kullanarak) veya `<configFilePath>` `packages.config` yüklenecek paketleri listeleyen dosyayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0963b-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="0963b-114">Seçeneğiyle belirli bir sürümü belirtebilirsiniz `-Version` .</span><span class="sxs-lookup"><span data-stu-id="0963b-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="0963b-115">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="0963b-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="0963b-116">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="0963b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0963b-117">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0963b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="0963b-118">*(4.4 +)* Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="0963b-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="0963b-119">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="0963b-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="0963b-120">*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="0963b-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="0963b-121">*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="0963b-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="0963b-122">*En yüksek*: en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="0963b-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="0963b-123">*Yoksay*: bağımlılık paketleri kullanılmayacak</span><span class="sxs-lookup"><span data-stu-id="0963b-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="0963b-124">Meta veri veya ikili dosyaları olan herhangi bir önbelleği doldurmadan doğrudan indirin.</span><span class="sxs-lookup"><span data-stu-id="0963b-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="0963b-125">Birden çok paketi paralel olarak yüklemeyi devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="0963b-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="0963b-126">Paketi, sürüm numarasını değil yalnızca paket adı ile adlandırılan bir klasöre yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0963b-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="0963b-127">*(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi.</span><span class="sxs-lookup"><span data-stu-id="0963b-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="0963b-128">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="0963b-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="0963b-129">*(4.4 +)* Bağımlılıkları seçmek için kullanılan hedef çerçeve.</span><span class="sxs-lookup"><span data-stu-id="0963b-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="0963b-130">Belirtilmemişse, varsayılan olarak ' any ' olur.</span><span class="sxs-lookup"><span data-stu-id="0963b-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0963b-131">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0963b-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="0963b-132">NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="0963b-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="0963b-133">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0963b-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0963b-134">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="0963b-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="0963b-135">Paketlerin yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0963b-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="0963b-136">Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0963b-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="0963b-137">Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec` ,, `nupkg` veya `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="0963b-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="0963b-138">Ön sürüm paketlerinin yüklenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="0963b-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="0963b-139">Paketleri ile geri yüklenirken bu bayrak gerekli değildir `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="0963b-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="0963b-140">Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="0963b-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="0963b-141">Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="0963b-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="0963b-142">Paketlerin geri yükleneceği çözümün kök klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0963b-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="0963b-143">Kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0963b-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="0963b-144">Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0963b-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0963b-145">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0963b-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="0963b-146">Yüklenecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0963b-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="0963b-147">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0963b-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0963b-148">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0963b-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
