---
title: NuGet CLI paketi komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Nuget.exe paketi komut başvurusu"
keywords: "nuget paketi başvurusu, paketi komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 353d5d839d85c04bc315c3a0e9cfe274a361bd15
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="91be4-104">Paketi komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="91be4-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="91be4-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="91be4-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="91be4-106">Belirtilen temel bir NuGet paketi oluşturur `.nuspec` veya proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="91be4-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="91be4-107">`dotnet pack` Komutu (bkz [dotnet komutları](dotnet-Commands.md)) ve `msbuild /t:pack` (bkz [MSBuild hedefleri](../schema/msbuild-targets.md)) alternatifler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91be4-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="91be4-108">Mono altında bir proje dosyasından paket oluşturma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="91be4-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="91be4-109">Ayrıca yerel olmayan yollarında ayarlamak gereken `.nuspec` dosya UNIX stili yollara nuget.exe Windows yol adları kendisini Dönüştürülmeyen gibi.</span><span class="sxs-lookup"><span data-stu-id="91be4-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="91be4-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="91be4-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="91be4-111">Burada `<nuspecPath>` ve `<projectPath>` belirtin `.nuspec` veya proje dosyası, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="91be4-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="91be4-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="91be4-112">Options</span></span>

| <span data-ttu-id="91be4-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="91be4-113">Option</span></span> | <span data-ttu-id="91be4-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="91be4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91be4-115">Ana yolu</span><span class="sxs-lookup"><span data-stu-id="91be4-115">BasePath</span></span> | <span data-ttu-id="91be4-116">Tanımlanan dosyalarının temel yolunu ayarlar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="91be4-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="91be4-117">Derleme</span><span class="sxs-lookup"><span data-stu-id="91be4-117">Build</span></span> | <span data-ttu-id="91be4-118">Proje paket oluşturmadan önce oluşturulmalıdır belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="91be4-119">Hariç tutma</span><span class="sxs-lookup"><span data-stu-id="91be4-119">Exclude</span></span> | <span data-ttu-id="91be4-120">Bir paket oluştururken çıkarılacak bir veya daha fazla joker karakter düzenleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="91be4-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="91be4-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="91be4-122">Boş dizinleri dahil edilmesi paket oluştururken engeller.</span><span class="sxs-lookup"><span data-stu-id="91be4-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="91be4-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="91be4-123">ForceEnglishOutput</span></span> | <span data-ttu-id="91be4-124">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="91be4-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="91be4-125">Yardım</span><span class="sxs-lookup"><span data-stu-id="91be4-125">Help</span></span> | <span data-ttu-id="91be4-126">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91be4-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="91be4-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="91be4-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="91be4-128">Yerleşik paket bağımlılıkları veya paketinin bir parçası olarak başvurulan projeleri içermelidir gösterir.</span><span class="sxs-lookup"><span data-stu-id="91be4-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="91be4-129">Başvurulan bir projenin karşılık gelen varsa `.nuspec` başvurulan proje bağımlılık olarak eklendikten sonra proje aynı ada sahip dosya.</span><span class="sxs-lookup"><span data-stu-id="91be4-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="91be4-130">Aksi takdirde, başvurulan proje paketinin bir parçası eklenir.</span><span class="sxs-lookup"><span data-stu-id="91be4-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="91be4-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="91be4-131">MinClientVersion</span></span> | <span data-ttu-id="91be4-132">Ayarlama *minClientVersion* özniteliği için oluşturulan paketi.</span><span class="sxs-lookup"><span data-stu-id="91be4-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="91be4-133">Bu değer var olan değerini geçersiz kılar *minClientVersion* (varsa) özniteliğini `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="91be4-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="91be4-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="91be4-134">MSBuildPath</span></span> | <span data-ttu-id="91be4-135">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="91be4-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="91be4-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="91be4-136">MSBuildVersion</span></span> | <span data-ttu-id="91be4-137">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="91be4-138">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="91be4-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="91be4-139">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="91be4-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="91be4-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="91be4-140">NoDefaultExcludes</span></span> | <span data-ttu-id="91be4-141">Varsayılan dışlama olan NuGet engelleyen paket dosyaları, dosya ve klasörleri gibi bir noktayla başlayan `.svn` ve `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="91be4-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="91be4-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="91be4-142">NoPackageAnalysis</span></span> | <span data-ttu-id="91be4-143">Paketi paket analiz paketi oluşturduktan sonra çalışmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="91be4-144">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="91be4-144">OutputDirectory</span></span> | <span data-ttu-id="91be4-145">Oluşturulan paket depolandığı klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="91be4-146">Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="91be4-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="91be4-147">Özellikler</span><span class="sxs-lookup"><span data-stu-id="91be4-147">Properties</span></span> | <span data-ttu-id="91be4-148">Proje dosyasında değerleri geçersiz kılmak özellikler listesini belirtir; bkz: [yaygın MSBuild proje özellikleri](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) özellik adları.</span><span class="sxs-lookup"><span data-stu-id="91be4-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="91be4-149">Burada özellikleri bağımsız değişkeni bir belirteç listesidir noktalı virgülle ayrılmış değer çiftleri = burada her oluşumu `$token$` içinde `.nuspec` dosya verilen değer ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="91be4-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="91be4-150">Değerleri tırnak işaretleri içindeki dizeleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="91be4-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="91be4-151">"Hata ayıklama" "Yapılandırma" özelliği için varsayılan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="91be4-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="91be4-152">Bir yayın yapılandırmasını değiştirmek için kullanın `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="91be4-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="91be4-153">Son eki</span><span class="sxs-lookup"><span data-stu-id="91be4-153">Suffix</span></span> | <span data-ttu-id="91be4-154">*(3.4.4+)*  Genellikle yapı ya da diğer yayın öncesi tanımlayıcıları ekleme için kullanılan dahili olarak oluşturulan sürüm numarası bir sonek ekler.</span><span class="sxs-lookup"><span data-stu-id="91be4-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="91be4-155">Örneğin, kullanarak `-suffix nightly` ile bir sürüm numarası benzer bir paket oluşturacak `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="91be4-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="91be4-156">Sonekleri uyarılar, hatalar ve farklı sürümlerini NuGet ve NuGet Paket Yöneticisi ile olası uyumsuzlukları önlemek için bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="91be4-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="91be4-157">Simgeleri</span><span class="sxs-lookup"><span data-stu-id="91be4-157">Symbols</span></span> | <span data-ttu-id="91be4-158">Paket kaynaklarını ve simgeleri içerdiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="91be4-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="91be4-159">İle kullanıldığında bir `.nuspec` dosyası, bu bir normal NuGet paket dosyası oluşturur ve karşılık gelen paket simgeler.</span><span class="sxs-lookup"><span data-stu-id="91be4-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="91be4-160">Aracı</span><span class="sxs-lookup"><span data-stu-id="91be4-160">Tool</span></span> | <span data-ttu-id="91be4-161">Proje çıktı dosyalarını içinde yerleştirilmesi gerektiğini belirtir `tool` klasör.</span><span class="sxs-lookup"><span data-stu-id="91be4-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="91be4-162">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="91be4-162">Verbosity</span></span> | <span data-ttu-id="91be4-163">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="91be4-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="91be4-164">Sürüm</span><span class="sxs-lookup"><span data-stu-id="91be4-164">Version</span></span> | <span data-ttu-id="91be4-165">Sürüm numarasını geçersiz kılmaları `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="91be4-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="91be4-166">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="91be4-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="91be4-167">Hariç geliştirme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="91be4-167">Excluding development dependencies</span></span>

<span data-ttu-id="91be4-168">Bazı NuGet paketleri kendi kitaplığı yazma yardımcı olur, ancak mutlaka asıl Paket bağımlılıklar olarak gerekmeyen geliştirme bağımlılık faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="91be4-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="91be4-169">`pack` Komutu yoksayar `package` girişleri `packages.config` sahip `developmentDependency` özniteliği kümesine `true`.</span><span class="sxs-lookup"><span data-stu-id="91be4-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="91be4-170">Bu girişler değil dahil edilecek öğeleri bir bağımlılık olarak oluşturulan paketi.</span><span class="sxs-lookup"><span data-stu-id="91be4-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="91be4-171">Örneğin, aşağıdakileri göz önünde bulundurun `packages.config` kaynak proje dosyasında:</span><span class="sxs-lookup"><span data-stu-id="91be4-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="91be4-172">Bu proje için paket tarafından oluşturulan `nuget pack` bir bağımlılığa sahip olur `jQuery` ve `microsoft-web-helpers` ama `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="91be4-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="91be4-173">Örnekler</span><span class="sxs-lookup"><span data-stu-id="91be4-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
