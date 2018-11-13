---
title: CLI NuGet Paketi komutu
description: Nuget.exe paketi komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 826316bdbce881836836f2a667cfa5297996d14f
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580317"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="c6b93-103">Paketi komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c6b93-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="c6b93-104">**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="c6b93-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="c6b93-105">Belirtilen temel bir NuGet paketi oluşturur `.nuspec` ya da proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="c6b93-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="c6b93-106">`dotnet pack` Komut (bkz [dotnet komutları](dotnet-Commands.md)) ve `msbuild /t:pack` (bkz [MSBuild hedefleri](../reference/msbuild-targets.md)) alternatifler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="c6b93-107">Mono altında bir proje dosyasından paket oluşturma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c6b93-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="c6b93-108">Ayrıca yerel olmayan yollarında ayarlamanız gereken `.nuspec` nuget.exe Windows yol adlarını kendi Dönüştürülmeyen olarak UNIX stili yollara, dosya.</span><span class="sxs-lookup"><span data-stu-id="c6b93-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="c6b93-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c6b93-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="c6b93-110">Burada `<nuspecPath>` ve `<projectPath>` belirtin `.nuspec` veya proje dosyası, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="c6b93-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c6b93-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="c6b93-111">Options</span></span>

| <span data-ttu-id="c6b93-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="c6b93-112">Option</span></span> | <span data-ttu-id="c6b93-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c6b93-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6b93-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="c6b93-114">BasePath</span></span> | <span data-ttu-id="c6b93-115">Temel yol içinde tanımlanan tüm dosyaların ayarlar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="c6b93-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c6b93-116">Derleme</span><span class="sxs-lookup"><span data-stu-id="c6b93-116">Build</span></span> | <span data-ttu-id="c6b93-117">Projenin paket oluşturulmadan önce oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="c6b93-118">Hariç tutma</span><span class="sxs-lookup"><span data-stu-id="c6b93-118">Exclude</span></span> | <span data-ttu-id="c6b93-119">Bir paket oluştururken hariç tutmak için bir veya daha fazla joker karakter düzeni belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="c6b93-120">Birden fazla düzenini belirtmek için yineleyin Exclude bayrağı.</span><span class="sxs-lookup"><span data-stu-id="c6b93-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="c6b93-121">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="c6b93-121">See example below.</span></span> |
| <span data-ttu-id="c6b93-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="c6b93-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="c6b93-123">Boş dizinleri dahil edilmesi, paket oluştururken engeller.</span><span class="sxs-lookup"><span data-stu-id="c6b93-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="c6b93-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c6b93-124">ForceEnglishOutput</span></span> | <span data-ttu-id="c6b93-125">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="c6b93-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c6b93-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c6b93-126">ConfigFile</span></span> | <span data-ttu-id="c6b93-127">Paketi komut için yapılandırma dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="c6b93-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="c6b93-128">Yardım</span><span class="sxs-lookup"><span data-stu-id="c6b93-128">Help</span></span> | <span data-ttu-id="c6b93-129">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c6b93-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="c6b93-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="c6b93-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="c6b93-131">Yerleşik paket bağımlılıkları veya paketinin bir parçası olarak başvurulan projeler içermelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="c6b93-132">Başvurulan projenin karşılık gelen varsa `.nuspec` başvurulan proje bir bağımlılık olarak eklendikten sonra proje ile aynı ada sahip bir dosya.</span><span class="sxs-lookup"><span data-stu-id="c6b93-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="c6b93-133">Aksi takdirde, başvurulan projenin paketinin bir parçası eklenir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="c6b93-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c6b93-134">MinClientVersion</span></span> | <span data-ttu-id="c6b93-135">Ayarlama *minClientVersion* oluşturulan bir paket için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="c6b93-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="c6b93-136">Bu değer mevcut değerini geçersiz kılar *minClientVersion* (varsa) özniteliğini `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="c6b93-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="c6b93-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c6b93-137">MSBuildPath</span></span> | <span data-ttu-id="c6b93-138">*(4.0 +)*  Önceliği alma komutu ile kullanılacak MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c6b93-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c6b93-139">MSBuildVersion</span></span> | <span data-ttu-id="c6b93-140">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c6b93-141">Desteklenen değerler şunlardır: 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="c6b93-141">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c6b93-142">Yolunuza Msbuild'de çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="c6b93-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c6b93-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="c6b93-143">NoDefaultExcludes</span></span> | <span data-ttu-id="c6b93-144">Varsayılan dışlama nuget engelleyen paket dosyalarını ve dosya ve klasörleri gibi bir noktayla başlayan `.svn` ve `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="c6b93-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c6b93-145">NoPackageAnalysis</span></span> | <span data-ttu-id="c6b93-146">Paketi paket analiz paketini oluşturduktan sonra çalışmaması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="c6b93-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="c6b93-147">OutputDirectory</span></span> | <span data-ttu-id="c6b93-148">Oluşturulan bir paket depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="c6b93-149">Klasör belirtilirse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c6b93-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="c6b93-150">Özellikler</span><span class="sxs-lookup"><span data-stu-id="c6b93-150">Properties</span></span> | <span data-ttu-id="c6b93-151">Diğer seçeneklerden sonra komut satırında son görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="c6b93-152">Geçersiz kılma değerleri proje dosyasında özelliklerin bir listesini belirtir. bkz: [yaygın MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) özellik adları.</span><span class="sxs-lookup"><span data-stu-id="c6b93-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="c6b93-153">Burada özellikleri bağımsız değişkeni bir belirteç listesidir. = değer çiftleri noktalı virgülle ayrılmış, burada her geçtiği `$token$` içinde `.nuspec` dosya verilen değer ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="c6b93-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="c6b93-154">Dizeleri tırnak işaretleri içindeki değerleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="c6b93-155">"Debug" "Yapılandırma" özelliği için varsayılan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c6b93-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="c6b93-156">Bir yayın yapılandırmasına değiştirmek için kullanın `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="c6b93-157">Son eki</span><span class="sxs-lookup"><span data-stu-id="c6b93-157">Suffix</span></span> | <span data-ttu-id="c6b93-158">*(3.4.4+)*  Genellikle derleme veya diğer yayın öncesi tanımlayıcıları ekleme için kullanılan dahili olarak oluşturulan sürüm numarası, bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="c6b93-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="c6b93-159">Örneğin, kullanarak `-suffix nightly` ile bir sürüm numarası benzer bir paket oluşturacak `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="c6b93-160">Sonekleri uyarılar, hatalar ve farklı sürümlerini NuGet ve NuGet Paket Yöneticisi ile olası uyumsuzluklar önlemek için bir harf ile başlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="c6b93-161">Simgeleri</span><span class="sxs-lookup"><span data-stu-id="c6b93-161">Symbols</span></span> | <span data-ttu-id="c6b93-162">Paket kaynakları ve semboller içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6b93-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="c6b93-163">İle kullanıldığında bir `.nuspec` dosyası bu oluşturur normal bir NuGet paketi dosyası ve karşılık gelen paket simgeleri.</span><span class="sxs-lookup"><span data-stu-id="c6b93-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="c6b93-164">Varsayılan olarak oluşturduğu bir [eski sembol paketi](../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="c6b93-164">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="c6b93-165">Sembol paketleri yeni Önerilen biçimi .snupkg değil.</span><span class="sxs-lookup"><span data-stu-id="c6b93-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="c6b93-166">Bkz: [sembol paketleri (.snupkg) oluşturma](../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="c6b93-166">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="c6b93-167">Aracı</span><span class="sxs-lookup"><span data-stu-id="c6b93-167">Tool</span></span> | <span data-ttu-id="c6b93-168">Projenin çıkış dosyalarının içinde yerleştirilmesi gerektiğini belirtir `tool` klasör.</span><span class="sxs-lookup"><span data-stu-id="c6b93-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="c6b93-169">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="c6b93-169">Verbosity</span></span> | <span data-ttu-id="c6b93-170">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="c6b93-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="c6b93-171">Sürüm</span><span class="sxs-lookup"><span data-stu-id="c6b93-171">Version</span></span> | <span data-ttu-id="c6b93-172">Sürüm numarasını geçersiz kılmalar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="c6b93-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="c6b93-173">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c6b93-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="c6b93-174">Geliştirme bağımlılıkları hariç</span><span class="sxs-lookup"><span data-stu-id="c6b93-174">Excluding development dependencies</span></span>

<span data-ttu-id="c6b93-175">NuGet paketlerinden bazıları kendi kitaplığı yazma yardımcı, ancak mutlaka asıl Paket bağımlılıkları olarak gerekmeyen geliştirme bağımlılık olarak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c6b93-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="c6b93-176">`pack` Komut yoksayar `package` girişleri `packages.config` sahip `developmentDependency` özniteliğini `true`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="c6b93-177">Bu girişler değil dahil edilecek öğeleri oluşturulan paketi bir bağımlılık olarak.</span><span class="sxs-lookup"><span data-stu-id="c6b93-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="c6b93-178">Örneğin, aşağıdakileri dikkate alın `packages.config` kaynak proje dosyasında:</span><span class="sxs-lookup"><span data-stu-id="c6b93-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="c6b93-179">Bu proje için paket tarafından oluşturulan `nuget pack` bağımlılığa sahip `jQuery` ve `microsoft-web-helpers` ama `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="c6b93-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="c6b93-180">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c6b93-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
