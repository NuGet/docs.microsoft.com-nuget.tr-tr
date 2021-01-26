---
title: NuGet CLı geri yükleme komutu
description: nuget.exe restore komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780030"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="918b2-103">restore komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="918b2-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="918b2-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="918b2-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="918b2-105">Klasörde eksik olan paketleri indirir ve yükler `packages` .</span><span class="sxs-lookup"><span data-stu-id="918b2-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="918b2-106">NuGet 4.0 + ve PackageReference biçimiyle kullanıldığında, `<project>.nuget.props` klasörde, gerekirse bir dosya oluşturur `obj` .</span><span class="sxs-lookup"><span data-stu-id="918b2-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="918b2-107">(Dosya kaynak denetiminden atlanabilir.)</span><span class="sxs-lookup"><span data-stu-id="918b2-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="918b2-108">Mac OSX ve Linux 'ta, mono üzerinde CLı ile, paketleri geri yükleme, PackageReference ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="918b2-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="918b2-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="918b2-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="918b2-110">`<projectPath>`bir çözümün veya dosyanın konumunu belirtir `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="918b2-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="918b2-111">Davranış ayrıntıları [için aşağıdaki açıklamalara](#remarks) bakın.</span><span class="sxs-lookup"><span data-stu-id="918b2-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="918b2-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="918b2-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="918b2-113">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="918b2-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="918b2-114">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="918b2-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="918b2-115">*(4.0 +)* Herhangi bir ikili dosya veya meta veri ile önbellekleri doldurmadan paketleri doğrudan indirir.</span><span class="sxs-lookup"><span data-stu-id="918b2-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="918b2-116">Birden çok paketin paralel olarak geri yüklenmesini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="918b2-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="918b2-117">*(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi.</span><span class="sxs-lookup"><span data-stu-id="918b2-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="918b2-118">Liste girdilerini ayırmak için noktalı virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="918b2-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="918b2-119">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="918b2-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="918b2-120">Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="918b2-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="918b2-121">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="918b2-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="918b2-122">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="918b2-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="918b2-123">Bir kilit dosyası zaten mevcut olsa bile, geri yüklemeyi tüm bağımlılıklara yeniden değerlendirmeye zorlar.</span><span class="sxs-lookup"><span data-stu-id="918b2-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="918b2-124">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="918b2-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="918b2-125">Proje kilit dosyasının yazıldığı çıkış konumu.</span><span class="sxs-lookup"><span data-stu-id="918b2-125">Output location where project lock file is written.</span></span> <span data-ttu-id="918b2-126">Bu, varsayılan olarak `PROJECT_ROOT\packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="918b2-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="918b2-127">Proje kilit dosyası güncelleştirilmeye izin verme.</span><span class="sxs-lookup"><span data-stu-id="918b2-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="918b2-128">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="918b2-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="918b2-129">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="918b2-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="918b2-130">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="918b2-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="918b2-131">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="918b2-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="918b2-132">NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="918b2-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="918b2-133">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="918b2-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="918b2-134">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="918b2-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="918b2-135">Paketlerin yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="918b2-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="918b2-136">Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="918b2-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="918b2-137">`packages.config` `PackagesDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `SolutionDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="918b2-138">Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec` ,, `nupkg` veya `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="918b2-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="918b2-139">Aynı `OutputDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="918b2-140">`packages.config` `OutputDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `SolutionDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="918b2-141">Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="918b2-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="918b2-142">*(4.0 +)* UWP ve .NET Core projeleri için tüm başvuru projelerini geri yükler.</span><span class="sxs-lookup"><span data-stu-id="918b2-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="918b2-143">Kullanılarak projeler için geçerlidir `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="918b2-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="918b2-144">Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="918b2-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="918b2-145">Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="918b2-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="918b2-146">Çözüm klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="918b2-146">Specifies the solution folder.</span></span> <span data-ttu-id="918b2-147">Bir çözümün paketleri geri yüklenirken geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="918b2-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="918b2-148">`packages.config` `PackagesDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `OutputDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="918b2-149">Geri yükleme için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="918b2-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="918b2-150">Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="918b2-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="918b2-151">Liste girdilerini ayırmak için noktalı virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="918b2-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="918b2-152">Proje kilitleme dosyasının oluşturulup geri yükleme ile kullanılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="918b2-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="918b2-153">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="918b2-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="918b2-154">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="918b2-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="918b2-155">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="918b2-155">Remarks</span></span>

<span data-ttu-id="918b2-156">Restore komutu aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="918b2-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="918b2-157">Restore komutunun işlem modunu belirleme.</span><span class="sxs-lookup"><span data-stu-id="918b2-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="918b2-158">projectPath dosya türü</span><span class="sxs-lookup"><span data-stu-id="918b2-158">projectPath file type</span></span> | <span data-ttu-id="918b2-159">Davranış</span><span class="sxs-lookup"><span data-stu-id="918b2-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="918b2-160">Çözüm (klasör)</span><span class="sxs-lookup"><span data-stu-id="918b2-160">Solution (folder)</span></span> | <span data-ttu-id="918b2-161">NuGet bir dosya arar `.sln` ve bulursa kullanır; Aksi takdirde bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="918b2-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="918b2-162">`(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="918b2-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="918b2-163">`.sln` dosyasýný</span><span class="sxs-lookup"><span data-stu-id="918b2-163">`.sln` file</span></span> | <span data-ttu-id="918b2-164">Çözüm tarafından tanımlanan paketleri geri yükleme; kullanılıyorsa bir hata verir `-SolutionDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="918b2-165">`$(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="918b2-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="918b2-166">`packages.config` veya proje dosyası</span><span class="sxs-lookup"><span data-stu-id="918b2-166">`packages.config` or project file</span></span> | <span data-ttu-id="918b2-167">Dosyada listelenen paketleri geri yükleme, bağımlılıkları çözme ve yükleme.</span><span class="sxs-lookup"><span data-stu-id="918b2-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="918b2-168">Diğer dosya türü</span><span class="sxs-lookup"><span data-stu-id="918b2-168">Other file type</span></span> | <span data-ttu-id="918b2-169">Dosyanın `.sln` yukarıdaki gibi bir dosya olduğu varsayılır; bir çözüm değilse, NuGet bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="918b2-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="918b2-170">(projectPath belirtilmemiş)</span><span class="sxs-lookup"><span data-stu-id="918b2-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="918b2-171">NuGet, geçerli klasörde çözüm dosyalarını arar.</span><span class="sxs-lookup"><span data-stu-id="918b2-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="918b2-172">Tek bir dosya bulunursa, paket geri yüklemek için kullanılır; birden çok çözüm bulunursa NuGet bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="918b2-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="918b2-173">Çözüm dosyası yoksa, NuGet bir arar `packages.config` ve paketleri geri yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="918b2-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="918b2-174">Çözüm veya `packages.config` Dosya bulunamazsa, NuGet bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="918b2-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="918b2-175">Aşağıdaki öncelik sırasını kullanarak paketler klasörünü belirleme (NuGet, bu klasörlerden hiçbiri bulunmazsa bir hata verir):</span><span class="sxs-lookup"><span data-stu-id="918b2-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="918b2-176">İle belirtilen klasör `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="918b2-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="918b2-177">`repositoryPath`İçindeki değer`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="918b2-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="918b2-178">İle belirtilen klasör `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="918b2-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="918b2-179">Bir çözümün paketlerini geri yüklerken NuGet aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="918b2-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="918b2-180">Çözüm dosyasını yükler.</span><span class="sxs-lookup"><span data-stu-id="918b2-180">Loads the solution file.</span></span>
    - <span data-ttu-id="918b2-181">İçinde listelenen çözüm düzeyi paketleri `$(SolutionDir)\.nuget\packages.config` klasörüne geri yükler `packages` .</span><span class="sxs-lookup"><span data-stu-id="918b2-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="918b2-182">İçinde listelenen paketleri `$(ProjectDir)\packages.config` klasörüne geri yükleyin `packages` .</span><span class="sxs-lookup"><span data-stu-id="918b2-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="918b2-183">Belirtilen her paket için, belirtilmediği takdirde paketi paralel olarak geri yükleyin `-DisableParallelProcessing` .</span><span class="sxs-lookup"><span data-stu-id="918b2-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="918b2-184">Örnekler</span><span class="sxs-lookup"><span data-stu-id="918b2-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
