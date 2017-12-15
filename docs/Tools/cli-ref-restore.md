---
title: NuGet CLI restore komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe restore komutu için başvurusu"
keywords: "nuget başvuru geri yüklemek için restore paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="b336f-104">Restore komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b336f-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="b336f-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="b336f-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="b336f-106">NuGet 2.7 +: İndirir ve gelen eksik paketleri yükler `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="b336f-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="b336f-107">NuGet 3.3 + kullanarak projeleri ile `project.json`: oluşturan bir `project.lock.json` dosyası ve bir `<project>.nuget.props` gerekirse, dosya.</span><span class="sxs-lookup"><span data-stu-id="b336f-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="b336f-108">(Her iki dosyası kaynak denetiminden atlanabilir.)</span><span class="sxs-lookup"><span data-stu-id="b336f-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="b336f-109">NuGet 4.0 + hangi başvuruları paketindeki proje dosyasında doğrudan projeyle: oluşturur bir `<project>.nuget.props` , gerekirse, dosya `obj` klasör.</span><span class="sxs-lookup"><span data-stu-id="b336f-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="b336f-110">(Dosyası kaynak denetiminden atlanabilir.)</span><span class="sxs-lookup"><span data-stu-id="b336f-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="b336f-111">Mac OSX ve Linux Mono üzerinde CLI ile paketleri geri PackageReference biçimiyle desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b336f-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="b336f-112">Kullanım</span><span class="sxs-lookup"><span data-stu-id="b336f-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="b336f-113">Burada `<projectPath>` bir çözüm konumunu belirten bir `packages.config` dosya, veya bir `project.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="b336f-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="b336f-114">Bkz: [açıklamalar](#remarks) aşağıda davranış Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="b336f-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="b336f-115">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b336f-115">Options</span></span>

| <span data-ttu-id="b336f-116">Seçenek</span><span class="sxs-lookup"><span data-stu-id="b336f-116">Option</span></span> | <span data-ttu-id="b336f-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b336f-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b336f-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b336f-118">ConfigFile</span></span> | <span data-ttu-id="b336f-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="b336f-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b336f-120">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b336f-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b336f-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="b336f-121">DirectDownload</span></span> | <span data-ttu-id="b336f-122">*(4.0 +)*  Doğrudan önbellekleri herhangi bir ikili dosyaları veya meta veri ile doldurma olmadan paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="b336f-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="b336f-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="b336f-123">DisableParallelProcessing</span></span> | <span data-ttu-id="b336f-124">Paralel olarak birden çok paket geri yükleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="b336f-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="b336f-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="b336f-125">FallbackSource</span></span> | <span data-ttu-id="b336f-126">*(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="b336f-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="b336f-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b336f-127">ForceEnglishOutput</span></span> | <span data-ttu-id="b336f-128">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="b336f-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b336f-129">Yardım</span><span class="sxs-lookup"><span data-stu-id="b336f-129">Help</span></span> | <span data-ttu-id="b336f-130">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b336f-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="b336f-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="b336f-131">MSBuildPath</span></span> | <span data-ttu-id="b336f-132">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="b336f-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="b336f-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="b336f-133">MSBuildVersion</span></span> | <span data-ttu-id="b336f-134">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b336f-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b336f-135">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b336f-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="b336f-136">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="b336f-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="b336f-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="b336f-137">NoCache</span></span> | <span data-ttu-id="b336f-138">NuGet paketleri yerel makine önbellekleri kullanmalarını engeller.</span><span class="sxs-lookup"><span data-stu-id="b336f-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="b336f-139">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="b336f-139">NonInteractive</span></span> | <span data-ttu-id="b336f-140">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="b336f-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b336f-141">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="b336f-141">OutputDirectory</span></span> | <span data-ttu-id="b336f-142">Paketleri yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b336f-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="b336f-143">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b336f-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="b336f-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="b336f-144">PackageSaveMode</span></span> | <span data-ttu-id="b336f-145">Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b336f-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="b336f-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="b336f-146">PackagesDirectory</span></span> | <span data-ttu-id="b336f-147">Aynı `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="b336f-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="b336f-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="b336f-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="b336f-149">Proje proje başvurularını çözümlemek için saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="b336f-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="b336f-150">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="b336f-150">Recursive</span></span> | <span data-ttu-id="b336f-151">*(4.0 +)*  UWP ve .NET Core projeleri için tüm başvurular projeleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="b336f-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="b336f-152">Kullanarak projeleri için geçerli değildir `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="b336f-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="b336f-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="b336f-153">RequireConsent</span></span> | <span data-ttu-id="b336f-154">Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="b336f-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="b336f-155">Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="b336f-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="b336f-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="b336f-156">SolutionDirectory</span></span> | <span data-ttu-id="b336f-157">Çözüm klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b336f-157">Specifies the solution folder.</span></span> <span data-ttu-id="b336f-158">Bir çözüm için paketleri geri yüklenirken geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="b336f-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="b336f-159">Kaynak</span><span class="sxs-lookup"><span data-stu-id="b336f-159">Source</span></span> | <span data-ttu-id="b336f-160">Paket kaynaklarını listesini geri yüklemek için kullanılacak (URL'ler olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="b336f-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="b336f-161">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b336f-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="b336f-162">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="b336f-162">Verbosity</span></span> |<span data-ttu-id="b336f-163">> çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="b336f-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="b336f-164">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b336f-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="b336f-165">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="b336f-165">Remarks</span></span>

<span data-ttu-id="b336f-166">Restore komutu aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="b336f-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="b336f-167">Restore komutu, işlem modunu belirler.</span><span class="sxs-lookup"><span data-stu-id="b336f-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="b336f-168">projectPath dosya türü</span><span class="sxs-lookup"><span data-stu-id="b336f-168">projectPath file type</span></span> | <span data-ttu-id="b336f-169">Davranış</span><span class="sxs-lookup"><span data-stu-id="b336f-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="b336f-170">Çözüm (klasör)</span><span class="sxs-lookup"><span data-stu-id="b336f-170">Solution (folder)</span></span> | <span data-ttu-id="b336f-171">NuGet arar bir `.sln` dosya ve aksi takdirde bir hata verir kullanır.</span><span class="sxs-lookup"><span data-stu-id="b336f-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="b336f-172">`(SolutionDir)\.nuget`Başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b336f-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="b336f-173">`.sln`Dosya</span><span class="sxs-lookup"><span data-stu-id="b336f-173">`.sln` file</span></span> | <span data-ttu-id="b336f-174">Çözümü tarafından tanımlanan paketler geri; bir hata durumunda verir `-SolutionDirectory` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b336f-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="b336f-175">`$(SolutionDir)\.nuget`Başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b336f-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="b336f-176">`packages.config`, `project.json`, ya da proje dosyası</span><span class="sxs-lookup"><span data-stu-id="b336f-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="b336f-177">Çözümleme ve bağımlılıkları yükleme dosyasında listelenen paketler geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b336f-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="b336f-178">Başka bir dosya türü</span><span class="sxs-lookup"><span data-stu-id="b336f-178">Other file type</span></span> | <span data-ttu-id="b336f-179">Dosya olduğu varsayılır bir `.sln` dosya olarak yukarıdaki; yoksa bir çözüm, bir hata NuGet sağlar.</span><span class="sxs-lookup"><span data-stu-id="b336f-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="b336f-180">(belirtilmezse projectPath)</span><span class="sxs-lookup"><span data-stu-id="b336f-180">(projectPath not specified)</span></span> | <span data-ttu-id="b336f-181">-NuGet geçerli klasörde çözüm dosyalarını arar.</span><span class="sxs-lookup"><span data-stu-id="b336f-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="b336f-182">Tek bir dosyada bulunursa, bir paketlerini geri yüklemek için kullanılır; birden çok çözüm bulunursa, NuGet hata verir.</span><span class="sxs-lookup"><span data-stu-id="b336f-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="b336f-183">-Hiçbir çözüm dosya varsa, NuGet arayan bir `packages.config` veya `project.json` ve bunu paketlerini geri yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b336f-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="b336f-184">-Çözüm dosyası yok varsa, `packages.config`, veya `project.json` bulunduğunda NuGet hata verir.</span><span class="sxs-lookup"><span data-stu-id="b336f-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="b336f-185">(Hiçbiri bu klasörlerin bulunmazsa NuGet hata verir) aşağıdaki öncelik sırasını kullanarak paketler klasörü belirleyin:</span><span class="sxs-lookup"><span data-stu-id="b336f-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="b336f-186">`%userprofile%\.nuget\packages` Değeri `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b336f-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="b336f-187">İle belirtilen klasör `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="b336f-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="b336f-188">`repositoryPath` Hyperlink içinde`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="b336f-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="b336f-189">İle belirtilen klasör`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="b336f-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="b336f-190">Bir çözüm için paketleri geri yüklenirken NuGet şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="b336f-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="b336f-191">Çözüm dosyasını yükler.</span><span class="sxs-lookup"><span data-stu-id="b336f-191">Loads the solution file.</span></span>
    - <span data-ttu-id="b336f-192">Listelenen çözüm düzeyi paketlerini yükler `$(SolutionDir)\.nuget\packages.config` içine `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="b336f-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="b336f-193">Listelenen paketler geri `$(ProjectDir)\packages.config` içine `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="b336f-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="b336f-194">Belirtilen her paket için paket paralel sürece geri `-DisableParallelProcessing` belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b336f-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="b336f-195">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b336f-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
