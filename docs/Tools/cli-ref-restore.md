---
title: NuGet CLI restore komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Reference for the nuget.exe restore command
keywords: "nuget başvuru geri yüklemek için restore paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ad5156a065e20dfced99da6b2e2860dbd748ad5
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="f052d-104">Restore komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f052d-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="f052d-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="f052d-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="f052d-106">İndirir ve gelen eksik paketleri yükler `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="f052d-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="f052d-107">NuGet 4.0 + ve PackageReference biçimi ile kullanıldığında, oluşturan bir `<project>.nuget.props` , gerekirse, dosya `obj` klasör.</span><span class="sxs-lookup"><span data-stu-id="f052d-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="f052d-108">(Dosyası kaynak denetiminden atlanabilir.)</span><span class="sxs-lookup"><span data-stu-id="f052d-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="f052d-109">Mac OSX ve Linux Mono üzerinde CLI ile paketleri geri PackageReference ile desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f052d-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="f052d-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="f052d-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="f052d-111">Burada `<projectPath>` bir çözüm konumunu belirtir veya `packages.config` dosyası.</span><span class="sxs-lookup"><span data-stu-id="f052d-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="f052d-112">Bkz: [açıklamalar](#remarks) aşağıda davranış Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="f052d-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="f052d-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="f052d-113">Options</span></span>

| <span data-ttu-id="f052d-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="f052d-114">Option</span></span> | <span data-ttu-id="f052d-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f052d-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f052d-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f052d-116">ConfigFile</span></span> | <span data-ttu-id="f052d-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="f052d-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f052d-118">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f052d-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f052d-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="f052d-119">DirectDownload</span></span> | <span data-ttu-id="f052d-120">*(4.0 +)*  Doğrudan önbellekleri herhangi bir ikili dosyaları veya meta veri ile doldurma olmadan paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="f052d-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="f052d-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="f052d-121">DisableParallelProcessing</span></span> | <span data-ttu-id="f052d-122">Paralel olarak birden çok paket geri yükleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="f052d-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="f052d-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="f052d-123">FallbackSource</span></span> | <span data-ttu-id="f052d-124">*(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak.</span><span class="sxs-lookup"><span data-stu-id="f052d-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="f052d-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f052d-125">ForceEnglishOutput</span></span> | <span data-ttu-id="f052d-126">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="f052d-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f052d-127">Yardım</span><span class="sxs-lookup"><span data-stu-id="f052d-127">Help</span></span> | <span data-ttu-id="f052d-128">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f052d-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="f052d-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="f052d-129">MSBuildPath</span></span> | <span data-ttu-id="f052d-130">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="f052d-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="f052d-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="f052d-131">MSBuildVersion</span></span> | <span data-ttu-id="f052d-132">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f052d-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="f052d-133">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f052d-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="f052d-134">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="f052d-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="f052d-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="f052d-135">NoCache</span></span> | <span data-ttu-id="f052d-136">NuGet paketleri yerel makine önbellekleri kullanmalarını engeller.</span><span class="sxs-lookup"><span data-stu-id="f052d-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="f052d-137">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="f052d-137">NonInteractive</span></span> | <span data-ttu-id="f052d-138">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="f052d-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f052d-139">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="f052d-139">OutputDirectory</span></span> | <span data-ttu-id="f052d-140">Paketleri yüklendiği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f052d-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="f052d-141">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f052d-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f052d-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="f052d-142">PackageSaveMode</span></span> | <span data-ttu-id="f052d-143">Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f052d-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="f052d-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="f052d-144">PackagesDirectory</span></span> | <span data-ttu-id="f052d-145">Aynı `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="f052d-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="f052d-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="f052d-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="f052d-147">Proje proje başvurularını çözümlemek için saniye cinsinden zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="f052d-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="f052d-148">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="f052d-148">Recursive</span></span> | <span data-ttu-id="f052d-149">*(4.0 +)*  UWP ve .NET Core projeleri için tüm başvurular projeleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="f052d-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="f052d-150">Kullanarak projeleri için geçerli değildir `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f052d-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="f052d-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="f052d-151">RequireConsent</span></span> | <span data-ttu-id="f052d-152">Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="f052d-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="f052d-153">Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f052d-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="f052d-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="f052d-154">SolutionDirectory</span></span> | <span data-ttu-id="f052d-155">Çözüm klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f052d-155">Specifies the solution folder.</span></span> <span data-ttu-id="f052d-156">Bir çözüm için paketleri geri yüklenirken geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="f052d-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="f052d-157">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f052d-157">Source</span></span> | <span data-ttu-id="f052d-158">Paket kaynaklarını listesini geri yüklemek için kullanılacak (URL'ler olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="f052d-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="f052d-159">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f052d-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f052d-160">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="f052d-160">Verbosity</span></span> |<span data-ttu-id="f052d-161">> çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="f052d-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f052d-162">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f052d-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="f052d-163">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="f052d-163">Remarks</span></span>

<span data-ttu-id="f052d-164">Restore komutu aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f052d-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="f052d-165">Restore komutu, işlem modunu belirler.</span><span class="sxs-lookup"><span data-stu-id="f052d-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="f052d-166">projectPath dosya türü</span><span class="sxs-lookup"><span data-stu-id="f052d-166">projectPath file type</span></span> | <span data-ttu-id="f052d-167">Davranış</span><span class="sxs-lookup"><span data-stu-id="f052d-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="f052d-168">Çözüm (klasör)</span><span class="sxs-lookup"><span data-stu-id="f052d-168">Solution (folder)</span></span> | <span data-ttu-id="f052d-169">NuGet arar bir `.sln` dosya ve aksi takdirde bir hata verir kullanır.</span><span class="sxs-lookup"><span data-stu-id="f052d-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="f052d-170">`(SolutionDir)\.nuget` Başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f052d-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="f052d-171">`.sln` Dosya</span><span class="sxs-lookup"><span data-stu-id="f052d-171">`.sln` file</span></span> | <span data-ttu-id="f052d-172">Çözümü tarafından tanımlanan paketler geri; bir hata durumunda verir `-SolutionDirectory` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f052d-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="f052d-173">`$(SolutionDir)\.nuget` Başlangıç klasörü olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f052d-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="f052d-174">`packages.config` ya da proje dosyası</span><span class="sxs-lookup"><span data-stu-id="f052d-174">`packages.config` or project file</span></span> | <span data-ttu-id="f052d-175">Çözümleme ve bağımlılıkları yükleme dosyasında listelenen paketler geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f052d-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="f052d-176">Başka bir dosya türü</span><span class="sxs-lookup"><span data-stu-id="f052d-176">Other file type</span></span> | <span data-ttu-id="f052d-177">Dosya olduğu varsayılır bir `.sln` dosya olarak yukarıdaki; yoksa bir çözüm, bir hata NuGet sağlar.</span><span class="sxs-lookup"><span data-stu-id="f052d-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="f052d-178">(belirtilmezse projectPath)</span><span class="sxs-lookup"><span data-stu-id="f052d-178">(projectPath not specified)</span></span> | <span data-ttu-id="f052d-179">-NuGet geçerli klasörde çözüm dosyalarını arar.</span><span class="sxs-lookup"><span data-stu-id="f052d-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="f052d-180">Tek bir dosyada bulunursa, bir paketlerini geri yüklemek için kullanılır; birden çok çözüm bulunursa, NuGet hata verir.</span><span class="sxs-lookup"><span data-stu-id="f052d-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="f052d-181">-Hiçbir çözüm dosya varsa, NuGet arayan bir `packages.config` ve bunu paketlerini geri yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f052d-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="f052d-182">-Çözüm Eğer veya `packages.config` dosya bulunduğunda, NuGet hata verir.</span><span class="sxs-lookup"><span data-stu-id="f052d-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="f052d-183">(Hiçbiri bu klasörlerin bulunmazsa NuGet hata verir) aşağıdaki öncelik sırasını kullanarak paketler klasörü belirleyin:</span><span class="sxs-lookup"><span data-stu-id="f052d-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="f052d-184">İle belirtilen klasör `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="f052d-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="f052d-185">`repositoryPath` Hyperlink içinde `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="f052d-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="f052d-186">İle belirtilen klasör `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="f052d-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="f052d-187">Bir çözüm için paketleri geri yüklenirken NuGet şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="f052d-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="f052d-188">Çözüm dosyasını yükler.</span><span class="sxs-lookup"><span data-stu-id="f052d-188">Loads the solution file.</span></span>
    - <span data-ttu-id="f052d-189">Listelenen çözüm düzeyi paketlerini yükler `$(SolutionDir)\.nuget\packages.config` içine `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="f052d-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="f052d-190">Listelenen paketler geri `$(ProjectDir)\packages.config` içine `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="f052d-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="f052d-191">Belirtilen her paket için paket paralel sürece geri `-DisableParallelProcessing` belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f052d-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="f052d-192">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f052d-192">Examples</span></span>

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
