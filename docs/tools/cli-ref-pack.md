---
title: NuGet CLI Paketi komutu
description: Nuget.exe paketi komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="371c0-103">pack komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="371c0-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="371c0-104">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="371c0-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="371c0-105">Belirtilen temel bir NuGet paketi oluşturur `.nuspec` veya proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="371c0-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="371c0-106">`dotnet pack` Komutu (bkz [dotnet komutları](dotnet-Commands.md)) ve `msbuild /t:pack` (bkz [MSBuild hedefleri](../reference/msbuild-targets.md)) alternatifler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="371c0-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="371c0-107">Mono altında bir proje dosyasından paket oluşturma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="371c0-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="371c0-108">Ayrıca yerel olmayan yollarında ayarlamak gereken `.nuspec` dosya UNIX stili yollara nuget.exe Windows yol adları kendisini Dönüştürülmeyen gibi.</span><span class="sxs-lookup"><span data-stu-id="371c0-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="371c0-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="371c0-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="371c0-110">Burada `<nuspecPath>` ve `<projectPath>` belirtin `.nuspec` veya proje dosyası, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="371c0-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="371c0-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="371c0-111">Options</span></span>

| <span data-ttu-id="371c0-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="371c0-112">Option</span></span> | <span data-ttu-id="371c0-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="371c0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="371c0-114">Ana yolu</span><span class="sxs-lookup"><span data-stu-id="371c0-114">BasePath</span></span> | <span data-ttu-id="371c0-115">Tanımlanan dosyalarının temel yolunu ayarlar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="371c0-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="371c0-116">Derleme</span><span class="sxs-lookup"><span data-stu-id="371c0-116">Build</span></span> | <span data-ttu-id="371c0-117">Proje paket oluşturmadan önce oluşturulmalıdır belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="371c0-118">Hariç tutma</span><span class="sxs-lookup"><span data-stu-id="371c0-118">Exclude</span></span> | <span data-ttu-id="371c0-119">Bir paket oluştururken çıkarılacak bir veya daha fazla joker karakter düzenleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="371c0-120">Birden fazla desen belirtmek için yineleyin Exclude bayrağı.</span><span class="sxs-lookup"><span data-stu-id="371c0-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="371c0-121">Aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="371c0-121">See example below.</span></span> |
| <span data-ttu-id="371c0-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="371c0-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="371c0-123">Boş dizinleri dahil edilmesi paket oluştururken engeller.</span><span class="sxs-lookup"><span data-stu-id="371c0-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="371c0-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="371c0-124">ForceEnglishOutput</span></span> | <span data-ttu-id="371c0-125">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="371c0-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="371c0-126">Yardım</span><span class="sxs-lookup"><span data-stu-id="371c0-126">Help</span></span> | <span data-ttu-id="371c0-127">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="371c0-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="371c0-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="371c0-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="371c0-129">Yerleşik paket bağımlılıkları veya paketinin bir parçası olarak başvurulan projeleri içermelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="371c0-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="371c0-130">Başvurulan bir projenin karşılık gelen varsa `.nuspec` başvurulan proje bağımlılık olarak eklendikten sonra proje aynı ada sahip dosya.</span><span class="sxs-lookup"><span data-stu-id="371c0-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="371c0-131">Aksi takdirde, başvurulan proje paketinin bir parçası eklenir.</span><span class="sxs-lookup"><span data-stu-id="371c0-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="371c0-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="371c0-132">MinClientVersion</span></span> | <span data-ttu-id="371c0-133">Ayarlama *minClientVersion* özniteliği için oluşturulan paketi.</span><span class="sxs-lookup"><span data-stu-id="371c0-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="371c0-134">Bu değer var olan değerini geçersiz kılar *minClientVersion* (varsa) özniteliğini `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="371c0-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="371c0-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="371c0-135">MSBuildPath</span></span> | <span data-ttu-id="371c0-136">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="371c0-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="371c0-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="371c0-137">MSBuildVersion</span></span> | <span data-ttu-id="371c0-138">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="371c0-139">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="371c0-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="371c0-140">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="371c0-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="371c0-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="371c0-141">NoDefaultExcludes</span></span> | <span data-ttu-id="371c0-142">Varsayılan dışlama olan NuGet engelleyen paket dosyaları, dosya ve klasörleri gibi bir noktayla başlayan `.svn` ve `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="371c0-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="371c0-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="371c0-143">NoPackageAnalysis</span></span> | <span data-ttu-id="371c0-144">Paketi paket analiz paketi oluşturduktan sonra çalışmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="371c0-145">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="371c0-145">OutputDirectory</span></span> | <span data-ttu-id="371c0-146">Oluşturulan paket depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="371c0-147">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="371c0-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="371c0-148">Özellikler</span><span class="sxs-lookup"><span data-stu-id="371c0-148">Properties</span></span> | <span data-ttu-id="371c0-149">Diğer Seçenekler sonra komut satırında son görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="371c0-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="371c0-150">Proje dosyasında değerleri geçersiz kılmak özellikler listesini belirtir; bkz: [yaygın MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) özellik adları.</span><span class="sxs-lookup"><span data-stu-id="371c0-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="371c0-151">Burada özellikleri bağımsız değişkeni bir belirteç listesidir noktalı virgülle ayrılmış değer çiftleri = burada her oluşumu `$token$` içinde `.nuspec` dosya verilen değer ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="371c0-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="371c0-152">Değerleri tırnak işaretleri içindeki dizeleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="371c0-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="371c0-153">"Hata ayıklama" "Yapılandırma" özelliği için varsayılan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="371c0-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="371c0-154">Bir yayın yapılandırmasını değiştirmek için kullanın `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="371c0-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="371c0-155">Son eki</span><span class="sxs-lookup"><span data-stu-id="371c0-155">Suffix</span></span> | <span data-ttu-id="371c0-156">*(3.4.4+)*  Genellikle yapı ya da diğer yayın öncesi tanımlayıcıları ekleme için kullanılan dahili olarak oluşturulan sürüm numarası bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="371c0-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="371c0-157">Örneğin, kullanarak `-suffix nightly` ile bir sürüm numarası benzer bir paket oluşturacak `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="371c0-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="371c0-158">Sonekleri uyarılar, hatalar ve farklı sürümlerini NuGet ve NuGet Paket Yöneticisi ile olası uyumsuzlukları önlemek için bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="371c0-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="371c0-159">Simgeleri</span><span class="sxs-lookup"><span data-stu-id="371c0-159">Symbols</span></span> | <span data-ttu-id="371c0-160">Paket kaynaklarını ve simgeleri içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="371c0-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="371c0-161">İle kullanıldığında bir `.nuspec` dosyası, bu bir normal NuGet paket dosyası oluşturur ve karşılık gelen paket simgeler.</span><span class="sxs-lookup"><span data-stu-id="371c0-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="371c0-162">Aracı</span><span class="sxs-lookup"><span data-stu-id="371c0-162">Tool</span></span> | <span data-ttu-id="371c0-163">Proje çıktı dosyalarını içinde yerleştirilmesi gerektiğini belirtir `tool` klasör.</span><span class="sxs-lookup"><span data-stu-id="371c0-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="371c0-164">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="371c0-164">Verbosity</span></span> | <span data-ttu-id="371c0-165">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="371c0-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="371c0-166">Sürüm</span><span class="sxs-lookup"><span data-stu-id="371c0-166">Version</span></span> | <span data-ttu-id="371c0-167">Sürüm numarasını geçersiz kılmaları `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="371c0-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="371c0-168">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="371c0-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="371c0-169">Hariç geliştirme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="371c0-169">Excluding development dependencies</span></span>

<span data-ttu-id="371c0-170">Bazı NuGet paketleri kendi kitaplığı yazma yardımcı olur, ancak mutlaka asıl Paket bağımlılıklar olarak gerekmeyen geliştirme bağımlılık faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="371c0-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="371c0-171">`pack` Komutu yoksayar `package` girişleri `packages.config` sahip `developmentDependency` özniteliği kümesine `true`.</span><span class="sxs-lookup"><span data-stu-id="371c0-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="371c0-172">Bu girişler değil dahil edilecek öğeleri bir bağımlılık olarak oluşturulan paketi.</span><span class="sxs-lookup"><span data-stu-id="371c0-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="371c0-173">Örneğin, aşağıdakileri göz önünde bulundurun `packages.config` kaynak proje dosyasında:</span><span class="sxs-lookup"><span data-stu-id="371c0-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="371c0-174">Bu proje için paket tarafından oluşturulan `nuget pack` bir bağımlılığa sahip olur `jQuery` ve `microsoft-web-helpers` ama `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="371c0-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="371c0-175">Örnekler</span><span class="sxs-lookup"><span data-stu-id="371c0-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
