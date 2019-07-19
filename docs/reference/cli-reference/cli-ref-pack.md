---
title: NuGet CLı paketi komutu
description: NuGet. exe paketi komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e12944bdd5d43b8b9e84908be480a5249dd924f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328302"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="ea4cc-103">Pack komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="ea4cc-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="ea4cc-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="ea4cc-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="ea4cc-105">Belirtilen `.nuspec` veya proje dosyasını temel alan bir NuGet paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="ea4cc-106">Komut (bkz. [DotNet komutları](../dotnet-Commands.md)) ve `msbuild -t:pack` (bkz. [MSBuild hedefleri](../msbuild-targets.md)), alternatifler olarak kullanılabilir. `dotnet pack`</span><span class="sxs-lookup"><span data-stu-id="ea4cc-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="ea4cc-107">Mono bölümünde proje dosyasından bir paket oluşturmak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="ea4cc-108">NuGet. exe Windows yol adları 'in kendisini dönüştürmediğinden, `.nuspec` dosyadaki yerel olmayan yolları UNIX stili yollarla da ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="ea4cc-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ea4cc-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="ea4cc-110">Burada `<nuspecPath>` veya proje dosyasını sırasıyla belirtin.`<projectPath>` `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="ea4cc-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ea4cc-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ea4cc-111">Options</span></span>

| <span data-ttu-id="ea4cc-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ea4cc-112">Option</span></span> | <span data-ttu-id="ea4cc-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ea4cc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea4cc-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="ea4cc-114">BasePath</span></span> | <span data-ttu-id="ea4cc-115">`.nuspec` Dosyada tanımlanan dosyaların temel yolunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="ea4cc-116">Yapı</span><span class="sxs-lookup"><span data-stu-id="ea4cc-116">Build</span></span> | <span data-ttu-id="ea4cc-117">Paketi oluşturmadan önce projenin oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="ea4cc-118">Amaz</span><span class="sxs-lookup"><span data-stu-id="ea4cc-118">Exclude</span></span> | <span data-ttu-id="ea4cc-119">Bir paket oluştururken dışlanacak bir veya daha fazla joker karakter deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="ea4cc-120">Birden fazla model belirtmek için-exclude bayrağını tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="ea4cc-121">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-121">See example below.</span></span> |
| <span data-ttu-id="ea4cc-122">Excludeemptydizinler</span><span class="sxs-lookup"><span data-stu-id="ea4cc-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="ea4cc-123">Paketi oluştururken boş dizinlerin eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="ea4cc-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ea4cc-124">ForceEnglishOutput</span></span> | <span data-ttu-id="ea4cc-125">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ea4cc-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ea4cc-126">ConfigFile</span></span> | <span data-ttu-id="ea4cc-127">Paket komutu için yapılandırma dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="ea4cc-128">Help</span><span class="sxs-lookup"><span data-stu-id="ea4cc-128">Help</span></span> | <span data-ttu-id="ea4cc-129">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="ea4cc-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="ea4cc-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="ea4cc-131">Oluşturulan paketin, bağımlılık olarak veya paketin parçası olarak başvurulan projeleri içermesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="ea4cc-132">Başvurulan bir proje, projeyle aynı ada `.nuspec` sahip karşılık gelen bir dosya içeriyorsa, bu başvurulan proje bir bağımlılık olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="ea4cc-133">Aksi takdirde, başvurulan proje, paketin parçası olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="ea4cc-134">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="ea4cc-134">MinClientVersion</span></span> | <span data-ttu-id="ea4cc-135">Oluşturulan paket için *Minclientversion* özniteliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="ea4cc-136">Bu değer, `.nuspec` dosyadaki var olan *minclientversion* özniteliğinin (varsa) değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="ea4cc-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ea4cc-137">MSBuildPath</span></span> | <span data-ttu-id="ea4cc-138">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ea4cc-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ea4cc-139">MSBuildVersion</span></span> | <span data-ttu-id="ea4cc-140">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ea4cc-141">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ea4cc-142">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ea4cc-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="ea4cc-143">NoDefaultExcludes</span></span> | <span data-ttu-id="ea4cc-144">, `.svn` Ve`.gitignore`gibi bir noktayla başlayan NuGet paket dosyalarının ve dosyalarının ve klasörlerinin varsayılan dışlamasını engeller.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="ea4cc-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="ea4cc-145">NoPackageAnalysis</span></span> | <span data-ttu-id="ea4cc-146">Paketi derlemeden sonra paketin paket analizini çalıştırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="ea4cc-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="ea4cc-147">OutputDirectory</span></span> | <span data-ttu-id="ea4cc-148">Oluşturulan Paketin depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="ea4cc-149">Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ea4cc-150">Özellikler</span><span class="sxs-lookup"><span data-stu-id="ea4cc-150">Properties</span></span> | <span data-ttu-id="ea4cc-151">Diğer seçeneklerden sonra komut satırında son olarak görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="ea4cc-152">Proje dosyasındaki değerleri geçersiz kılan özelliklerin bir listesini belirtir; Özellik adları için bkz. [Ortak MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="ea4cc-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="ea4cc-153">Burada bulunan Properties bağımsız değişkeni, noktalı virgülle ayrılmış bir belirteç = değer çiftleri listesi ve `$token$` `.nuspec` dosyadaki her oluşumun verilen değer ile değiştirilmesidir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="ea4cc-154">Değerler, tırnak işaretleri içinde dizeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="ea4cc-155">"Yapılandırma" özelliği için varsayılan "hata ayıkla" dır.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="ea4cc-156">Bir sürüm yapılandırmasına geçiş yapmak için kullanın `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="ea4cc-157">Önekini</span><span class="sxs-lookup"><span data-stu-id="ea4cc-157">Suffix</span></span> | <span data-ttu-id="ea4cc-158">*(3.4.4 +)* Genellikle derleme veya diğer yayın öncesi tanımlayıcıları eklemek için kullanılan, dahili olarak oluşturulan sürüm numarasına bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="ea4cc-159">Örneğin, kullanmak `-suffix nightly` gibi `1.2.3-nightly`sürüm numarasına sahip bir paket oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="ea4cc-160">Farklı NuGet ve NuGet Paket Yöneticisi sürümleriyle uyarı, hata ve potansiyel uyumsuzluktan kaçınmak için son ekler bir harfle başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="ea4cc-161">Simgeleri</span><span class="sxs-lookup"><span data-stu-id="ea4cc-161">Symbols</span></span> | <span data-ttu-id="ea4cc-162">Paketin kaynakları ve sembolleri içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="ea4cc-163">Bir `.nuspec` dosya ile kullanıldığında, bu, normal bir NuGet paket dosyası ve ilgili semboller paketini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="ea4cc-164">Varsayılan olarak, eski bir [sembol paketi](../../create-packages/Symbol-Packages.md)oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="ea4cc-165">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="ea4cc-166">Bkz. [sembol paketleri oluşturma (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="ea4cc-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="ea4cc-167">Aracı</span><span class="sxs-lookup"><span data-stu-id="ea4cc-167">Tool</span></span> | <span data-ttu-id="ea4cc-168">Projenin çıkış dosyalarının `tool` klasöre yerleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="ea4cc-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ea4cc-169">Verbosity</span></span> | <span data-ttu-id="ea4cc-170">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="ea4cc-171">Sürüm</span><span class="sxs-lookup"><span data-stu-id="ea4cc-171">Version</span></span> | <span data-ttu-id="ea4cc-172">`.nuspec` Dosyadaki sürüm numarasını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="ea4cc-173">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ea4cc-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="ea4cc-174">Geliştirme bağımlılıklarını hariç tutma</span><span class="sxs-lookup"><span data-stu-id="ea4cc-174">Excluding development dependencies</span></span>

<span data-ttu-id="ea4cc-175">Bazı NuGet paketleri geliştirme bağımlılıkları olarak faydalıdır, bu da kendi kitaplığınızı yazmanıza yardımcı olur, ancak gerçek paket bağımlılıkları olarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="ea4cc-176">`developmentDependency` `packages.config` Komutu,`package` özniteliği olarak`true`ayarlanmış olan içindeki girişleri yoksayar. `pack`</span><span class="sxs-lookup"><span data-stu-id="ea4cc-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="ea4cc-177">Bu girişler oluşturulan pakette bir bağımlılık olarak dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="ea4cc-178">Örneğin, kaynak projede aşağıdaki `packages.config` dosyayı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="ea4cc-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="ea4cc-179">Bu `nuget pack` proje için tarafından oluşturulan paketin `jQuery` bağımlılığı `microsoft-web-helpers` olur, ancak uygulanmaz `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="ea4cc-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="ea4cc-180">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ea4cc-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
