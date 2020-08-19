---
title: NuGet CLı paketi komutu
description: nuget.exe Pack komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622960"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="b30d8-103">Pack komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="b30d8-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="b30d8-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="b30d8-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="b30d8-105">Belirtilen [. nuspec](../nuspec.md) veya proje dosyasını temel alan bir NuGet paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b30d8-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="b30d8-106">`dotnet pack`Komut (bkz. [DotNet komutları](../dotnet-Commands.md)) ve `msbuild -t:pack` (bkz. [MSBuild hedefleri](../msbuild-targets.md)), alternatifler olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="b30d8-107">[`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) [Packagereference](../../consume-packages/package-references-in-project-files.md) tabanlı projeler için veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="b30d8-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="b30d8-108">Mono bölümünde proje dosyasından bir paket oluşturmak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b30d8-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="b30d8-109">Ayrıca `.nuspec` , nuget.exe Windows yol adları 'in kendisini dönüştürmediği için, dosyadaki yerel olmayan yolları UNIX stili yollara ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="b30d8-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="b30d8-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="b30d8-111">Burada `<nuspecPath>` `<projectPath>` `.nuspec` veya proje dosyasını sırasıyla belirtin.</span><span class="sxs-lookup"><span data-stu-id="b30d8-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="b30d8-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b30d8-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="b30d8-113">[. Nuspec](../nuspec.md) dosyasında tanımlanan dosyaların temel yolunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b30d8-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="b30d8-114">Paketi oluşturmadan önce projenin oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b30d8-115">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="b30d8-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b30d8-116">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="b30d8-117">Bir paket oluştururken dışlanacak bir veya daha fazla joker karakter deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="b30d8-118">Birden fazla model belirtmek için-exclude bayrağını tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="b30d8-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="b30d8-119">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="b30d8-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="b30d8-120">Paketi oluştururken boş dizinlerin eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="b30d8-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b30d8-121">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="b30d8-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b30d8-122">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b30d8-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="b30d8-123">Oluşturulan paketin, bağımlılık olarak veya paketin parçası olarak başvurulan projeleri içermesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="b30d8-124">Başvurulan bir proje, `.nuspec` projeyle aynı ada sahip karşılık gelen bir dosya içeriyorsa, bu başvurulan proje bir bağımlılık olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="b30d8-125">Aksi takdirde, başvurulan proje, paketin parçası olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="b30d8-126">Komutun, paylaşılan akışı desteklemek için paket çıkış dizinini hazırlaması gerekip gerekmediğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b30d8-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="b30d8-127">Oluşturulan paket için *Minclientversion* özniteliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b30d8-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="b30d8-128">Bu değer, dosyadaki var olan *Minclientversion* özniteliğinin (varsa) değerini geçersiz kılar `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="b30d8-129">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="b30d8-130">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b30d8-131">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="b30d8-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="b30d8-132">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="b30d8-133">, Ve gibi bir noktayla başlayan NuGet paket dosyalarının ve dosyalarının ve klasörlerinin varsayılan dışlamasını engeller `.svn` `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b30d8-134">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="b30d8-135">Paketi derlemeden sonra paketin paket analizini çalıştırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="b30d8-136">Oluşturulan Paketin depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="b30d8-137">Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="b30d8-138">Komutun paket çıkış adını sürüm olmadan hazırlaması gerekip gerekmediğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b30d8-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="b30d8-139">Paketler klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="b30d8-140">Diğer seçeneklerden sonra komut satırında son olarak görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="b30d8-141">Proje dosyasındaki değerleri geçersiz kılan özelliklerin bir listesini belirtir; Özellik adları için bkz. [Ortak MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="b30d8-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="b30d8-142">Burada bulunan Properties bağımsız değişkeni, noktalı virgülle ayrılmış bir belirteç = değer çiftleri listesi ve dosyadaki her oluşumun `$token$` `.nuspec` verilen değer ile değiştirilmesidir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="b30d8-143">Değerler, tırnak işaretleri içinde dizeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="b30d8-144">"Yapılandırma" özelliği için varsayılan "hata ayıkla" dır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="b30d8-145">Bir sürüm yapılandırmasına geçiş yapmak için kullanın `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="b30d8-146">**Genel**olarak, alışılmadık davranışları önlemek için ilgili proje derlemesi sırasında kullanılan özellikler aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="b30d8-147">Çözüm dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="b30d8-148">*(3.4.4 +)* Genellikle derleme veya diğer yayın öncesi tanımlayıcıları eklemek için kullanılan, dahili olarak oluşturulan sürüm numarasına bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="b30d8-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="b30d8-149">Örneğin, kullanmak `-suffix nightly` gibi sürüm numarasına sahip bir paket oluşturur `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="b30d8-150">Farklı NuGet ve NuGet Paket Yöneticisi sürümleriyle uyarı, hata ve potansiyel uyumsuzluktan kaçınmak için son ekler bir harfle başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b30d8-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="b30d8-151">Bir semboller paketi oluştururken, ve biçimi arasında seçim yapılmasına izin `snupkg` verir `symbols.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="b30d8-152">Paketin kaynakları ve sembolleri içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="b30d8-153">Bir dosya ile kullanıldığında `.nuspec` , bu, normal bir NuGet paket dosyası ve ilgili semboller paketini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b30d8-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="b30d8-154">Varsayılan olarak, eski bir [sembol paketi](../../create-packages/Symbol-Packages.md)oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b30d8-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="b30d8-155">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="b30d8-156">Bkz. [sembol paketleri oluşturma (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="b30d8-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="b30d8-157">Projenin çıkış dosyalarının klasöre yerleştirilmesi gerektiğini belirtir `tool` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b30d8-158">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="b30d8-159">Dosyadaki sürüm numarasını geçersiz kılar `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="b30d8-160">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b30d8-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="b30d8-161">Geliştirme bağımlılıklarını hariç tutma</span><span class="sxs-lookup"><span data-stu-id="b30d8-161">Excluding development dependencies</span></span>

<span data-ttu-id="b30d8-162">Bazı NuGet paketleri geliştirme bağımlılıkları olarak faydalıdır, bu da kendi kitaplığınızı yazmanıza yardımcı olur, ancak gerçek paket bağımlılıkları olarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="b30d8-163">`pack`Komutu, `package` `packages.config` `developmentDependency` özniteliği olarak ayarlanmış olan içindeki girişleri yoksayar `true` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="b30d8-164">Bu girişler oluşturulan pakette bir bağımlılık olarak dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="b30d8-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="b30d8-165">Örneğin, kaynak projede aşağıdaki dosyayı göz önünde bulundurun `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="b30d8-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="b30d8-166">Bu proje için tarafından oluşturulan paketin `nuget pack` bağımlılığı olur, `jQuery` `microsoft-web-helpers` ancak uygulanmaz `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="b30d8-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="b30d8-167">Paket uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="b30d8-167">Suppressing pack warnings</span></span>

<span data-ttu-id="b30d8-168">Paket işlemlerinizin sırasında tüm NuGet uyarılarını çözmeniz önerilir, ancak bazı durumlarda bunların garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="b30d8-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="b30d8-169">Bunu aşağıdaki şekilde yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b30d8-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="b30d8-170">nuget.exe paketi paketi. nuspec-Özellikler NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="b30d8-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="b30d8-171">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b30d8-171">Examples</span></span>

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
