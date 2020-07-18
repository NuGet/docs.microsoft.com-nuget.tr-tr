---
title: NuGet CLı paketi komutu
description: nuget.exe Pack komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 649c440d868c89068a069a396919b58b999369e5
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451144"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="9605b-103">Pack komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="9605b-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="9605b-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="9605b-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="9605b-105">Belirtilen [. nuspec](../nuspec.md) veya proje dosyasını temel alan bir NuGet paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9605b-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="9605b-106">`dotnet pack`Komut (bkz. [DotNet komutları](../dotnet-Commands.md)) ve `msbuild -t:pack` (bkz. [MSBuild hedefleri](../msbuild-targets.md)), alternatifler olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9605b-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="9605b-107">[`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) [Packagereference](../../consume-packages/package-references-in-project-files.md) tabanlı projeler için veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="9605b-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="9605b-108">Mono bölümünde proje dosyasından bir paket oluşturmak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9605b-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="9605b-109">Ayrıca `.nuspec` , nuget.exe Windows yol adları 'in kendisini dönüştürmediği için, dosyadaki yerel olmayan yolları UNIX stili yollara ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9605b-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="9605b-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="9605b-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="9605b-111">Burada `<nuspecPath>` `<projectPath>` `.nuspec` veya proje dosyasını sırasıyla belirtin.</span><span class="sxs-lookup"><span data-stu-id="9605b-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="9605b-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="9605b-112">Options</span></span>

| <span data-ttu-id="9605b-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="9605b-113">Option</span></span> | <span data-ttu-id="9605b-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9605b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9605b-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="9605b-115">BasePath</span></span> | <span data-ttu-id="9605b-116">[. Nuspec](../nuspec.md) dosyasında tanımlanan dosyaların temel yolunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9605b-116">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="9605b-117">Yapı</span><span class="sxs-lookup"><span data-stu-id="9605b-117">Build</span></span> | <span data-ttu-id="9605b-118">Paketi oluşturmadan önce projenin oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9605b-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="9605b-119">Exclude</span><span class="sxs-lookup"><span data-stu-id="9605b-119">Exclude</span></span> | <span data-ttu-id="9605b-120">Bir paket oluştururken dışlanacak bir veya daha fazla joker karakter deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="9605b-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="9605b-121">Birden fazla model belirtmek için-exclude bayrağını tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="9605b-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="9605b-122">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="9605b-122">See example below.</span></span> |
| <span data-ttu-id="9605b-123">Excludeemptydizinler</span><span class="sxs-lookup"><span data-stu-id="9605b-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="9605b-124">Paketi oluştururken boş dizinlerin eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="9605b-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="9605b-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9605b-125">ForceEnglishOutput</span></span> | <span data-ttu-id="9605b-126">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="9605b-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9605b-127">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9605b-127">ConfigFile</span></span> | <span data-ttu-id="9605b-128">Paket komutu için yapılandırma dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9605b-128">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="9605b-129">Help (Yardım)</span><span class="sxs-lookup"><span data-stu-id="9605b-129">Help</span></span> | <span data-ttu-id="9605b-130">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9605b-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="9605b-131">Includprojelere başvuru</span><span class="sxs-lookup"><span data-stu-id="9605b-131">IncludeReferencedProjects</span></span> | <span data-ttu-id="9605b-132">Oluşturulan paketin, bağımlılık olarak veya paketin parçası olarak başvurulan projeleri içermesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9605b-132">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="9605b-133">Başvurulan bir proje, `.nuspec` projeyle aynı ada sahip karşılık gelen bir dosya içeriyorsa, bu başvurulan proje bir bağımlılık olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="9605b-133">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="9605b-134">Aksi takdirde, başvurulan proje, paketin parçası olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="9605b-134">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="9605b-135">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="9605b-135">MinClientVersion</span></span> | <span data-ttu-id="9605b-136">Oluşturulan paket için *Minclientversion* özniteliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9605b-136">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="9605b-137">Bu değer, dosyadaki var olan *Minclientversion* özniteliğinin (varsa) değerini geçersiz kılar `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="9605b-137">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="9605b-138">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="9605b-138">MSBuildPath</span></span> | <span data-ttu-id="9605b-139">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="9605b-139">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="9605b-140">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="9605b-140">MSBuildVersion</span></span> | <span data-ttu-id="9605b-141">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9605b-141">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="9605b-142">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="9605b-142">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="9605b-143">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9605b-143">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="9605b-144">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="9605b-144">NoDefaultExcludes</span></span> | <span data-ttu-id="9605b-145">, Ve gibi bir noktayla başlayan NuGet paket dosyalarının ve dosyalarının ve klasörlerinin varsayılan dışlamasını engeller `.svn` `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="9605b-145">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="9605b-146">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="9605b-146">NoPackageAnalysis</span></span> | <span data-ttu-id="9605b-147">Paketi derlemeden sonra paketin paket analizini çalıştırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9605b-147">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="9605b-148">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="9605b-148">OutputDirectory</span></span> | <span data-ttu-id="9605b-149">Oluşturulan Paketin depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9605b-149">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="9605b-150">Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9605b-150">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="9605b-151">Özellikler</span><span class="sxs-lookup"><span data-stu-id="9605b-151">Properties</span></span> | <span data-ttu-id="9605b-152">Diğer seçeneklerden sonra komut satırında son olarak görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="9605b-152">Should appear last on the command line after other options.</span></span> <span data-ttu-id="9605b-153">Proje dosyasındaki değerleri geçersiz kılan özelliklerin bir listesini belirtir; Özellik adları için bkz. [Ortak MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="9605b-153">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="9605b-154">Burada bulunan Properties bağımsız değişkeni, noktalı virgülle ayrılmış bir belirteç = değer çiftleri listesi ve dosyadaki her oluşumun `$token$` `.nuspec` verilen değer ile değiştirilmesidir.</span><span class="sxs-lookup"><span data-stu-id="9605b-154">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="9605b-155">Değerler, tırnak işaretleri içinde dizeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9605b-155">Values can be strings in quotation marks.</span></span> <span data-ttu-id="9605b-156">"Yapılandırma" özelliği için varsayılan "hata ayıkla" dır.</span><span class="sxs-lookup"><span data-stu-id="9605b-156">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="9605b-157">Bir sürüm yapılandırmasına geçiş yapmak için kullanın `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="9605b-157">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="9605b-158">**Genel**olarak, alışılmadık davranışları önlemek için ilgili proje derlemesi sırasında kullanılan özellikler aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9605b-158">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span> |
| <span data-ttu-id="9605b-159">Önekini</span><span class="sxs-lookup"><span data-stu-id="9605b-159">Suffix</span></span> | <span data-ttu-id="9605b-160">*(3.4.4 +)* Genellikle derleme veya diğer yayın öncesi tanımlayıcıları eklemek için kullanılan, dahili olarak oluşturulan sürüm numarasına bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="9605b-160">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="9605b-161">Örneğin, kullanmak `-suffix nightly` gibi sürüm numarasına sahip bir paket oluşturur `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="9605b-161">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="9605b-162">Farklı NuGet ve NuGet Paket Yöneticisi sürümleriyle uyarı, hata ve potansiyel uyumsuzluktan kaçınmak için son ekler bir harfle başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9605b-162">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="9605b-163">Simgeleri</span><span class="sxs-lookup"><span data-stu-id="9605b-163">Symbols</span></span> | <span data-ttu-id="9605b-164">Paketin kaynakları ve sembolleri içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9605b-164">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="9605b-165">Bir dosya ile kullanıldığında `.nuspec` , bu, normal bir NuGet paket dosyası ve ilgili semboller paketini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9605b-165">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="9605b-166">Varsayılan olarak, eski bir [sembol paketi](../../create-packages/Symbol-Packages.md)oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9605b-166">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="9605b-167">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="9605b-167">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="9605b-168">Bkz. [sembol paketleri oluşturma (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="9605b-168">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="9605b-169">Araç</span><span class="sxs-lookup"><span data-stu-id="9605b-169">Tool</span></span> | <span data-ttu-id="9605b-170">Projenin çıkış dosyalarının klasöre yerleştirilmesi gerektiğini belirtir `tool` .</span><span class="sxs-lookup"><span data-stu-id="9605b-170">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="9605b-171">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="9605b-171">Verbosity</span></span> | <span data-ttu-id="9605b-172">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="9605b-172">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="9605b-173">Sürüm</span><span class="sxs-lookup"><span data-stu-id="9605b-173">Version</span></span> | <span data-ttu-id="9605b-174">Dosyadaki sürüm numarasını geçersiz kılar `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="9605b-174">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="9605b-175">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9605b-175">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="9605b-176">Geliştirme bağımlılıklarını hariç tutma</span><span class="sxs-lookup"><span data-stu-id="9605b-176">Excluding development dependencies</span></span>

<span data-ttu-id="9605b-177">Bazı NuGet paketleri geliştirme bağımlılıkları olarak faydalıdır, bu da kendi kitaplığınızı yazmanıza yardımcı olur, ancak gerçek paket bağımlılıkları olarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9605b-177">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="9605b-178">`pack`Komutu, `package` `packages.config` `developmentDependency` özniteliği olarak ayarlanmış olan içindeki girişleri yoksayar `true` .</span><span class="sxs-lookup"><span data-stu-id="9605b-178">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="9605b-179">Bu girişler oluşturulan pakette bir bağımlılık olarak dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="9605b-179">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="9605b-180">Örneğin, kaynak projede aşağıdaki dosyayı göz önünde bulundurun `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="9605b-180">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="9605b-181">Bu proje için tarafından oluşturulan paketin `nuget pack` bağımlılığı olur, `jQuery` `microsoft-web-helpers` ancak uygulanmaz `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="9605b-181">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="9605b-182">Paket uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="9605b-182">Suppressing pack warnings</span></span>

<span data-ttu-id="9605b-183">Paket işlemlerinizin sırasında tüm NuGet uyarılarını çözmeniz önerilir, ancak bazı durumlarda bunların garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="9605b-183">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="9605b-184">Bunu aşağıdaki şekilde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9605b-184">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="9605b-185">nuget.exe paketi paketi. nuspec-Özellikler NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="9605b-185">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="9605b-186">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9605b-186">Examples</span></span>

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
