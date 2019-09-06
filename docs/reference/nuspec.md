---
title: NuGet için. nuspec dosya başvurusu
description: . Nuspec dosyası, bir paket oluştururken ve paket tüketicilere bilgi sağlamak için kullanılan paket meta verilerini içerir.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ea40f80a482a290b7399e5a6abc69e0c6fe32b77
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384454"
---
# <a name="nuspec-reference"></a><span data-ttu-id="8fe29-103">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="8fe29-103">.nuspec reference</span></span>

<span data-ttu-id="8fe29-104">`.nuspec` Dosya, paket meta verilerini içeren bir XML bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="8fe29-105">Bu bildirim her ikisi de paketini derlemek ve tüketicilere bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="8fe29-106">Bildirim her zaman bir pakete dahildir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="8fe29-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="8fe29-107">In this topic:</span></span>

- [<span data-ttu-id="8fe29-108">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="8fe29-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="8fe29-109">[Değiştirme belirteçleri](#replacement-tokens) (bir Visual Studio projesiyle kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="8fe29-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="8fe29-110">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="8fe29-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="8fe29-111">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="8fe29-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="8fe29-112">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="8fe29-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="8fe29-113">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="8fe29-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="8fe29-114">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="8fe29-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="8fe29-115">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="8fe29-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="8fe29-116">Proje türü uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="8fe29-116">Project type compatibility</span></span>

- <span data-ttu-id="8fe29-117">Kullanan `.nuspec` SDK `nuget.exe pack` olmayan projeler`packages.config`için ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="8fe29-118">`.nuspec` [SDK stilindeki projelere](../resources/check-project-format.md) yönelik paketler oluşturmak için bir dosya gerekli değildir (genellikle .NET Core ve [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanan .NET Standard projeler).</span><span class="sxs-lookup"><span data-stu-id="8fe29-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="8fe29-119">(Paketi oluşturduğunuzda bir `.nuspec` ' nin oluşturulduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="8fe29-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="8fe29-120">Veya `dotnet.exe pack` kullanarak`msbuild pack target`bir paket oluşturuyorsanız, bunun yerine genellikle proje dosyasındaki `.nuspec` dosyada bulunan [tüm özellikleri dahil](../reference/msbuild-targets.md#pack-target) etmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="8fe29-121">Ancak, bunun yerine [veya `.nuspec` `dotnet.exe` `msbuild pack target`kullanarak paketbir dosya kullanmayı ](../reference/msbuild-targets.md#packing-using-a-nuspec)seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="8fe29-122">' Den `packages.config` [packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için, `.nuspec` paketi oluşturmak için bir dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="8fe29-123">Bunun yerine, [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="8fe29-124">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="8fe29-124">General form and schema</span></span>

<span data-ttu-id="8fe29-125">Geçerli `nuspec.xsd` şema dosyası [NuGet GitHub deposunda](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="8fe29-126">Bu şema içinde, bir `.nuspec` dosya aşağıdaki genel biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="8fe29-127">Şemanın net bir görsel temsili için, şema dosyasını Visual Studio 'da tasarım modunda açın ve **XML şema Gezgini** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="8fe29-128">Alternatif olarak, dosyayı kod olarak açın, düzenleyicide sağ tıklayın ve **XML şeması Gezginini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8fe29-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="8fe29-129">Aşağıdakilerden biri gibi bir görünüm alacağınız şekilde (çoğunlukla genişletilir):</span><span class="sxs-lookup"><span data-stu-id="8fe29-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Nuspec. xsd Open ile Visual Studio şema Gezgini](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="8fe29-131">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-131">Required metadata elements</span></span>

<span data-ttu-id="8fe29-132">Aşağıdaki öğeler bir paket için en düşük gereksinimlerdir, ancak geliştiricilerin paketinize sahip olduğu genel deneyimi geliştirmek için [isteğe bağlı meta veri öğelerini](#optional-metadata-elements) eklemeyi göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="8fe29-133">Bu öğelerin bir `<metadata>` öğesi içinde görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="8fe29-134">kimlik</span><span class="sxs-lookup"><span data-stu-id="8fe29-134">id</span></span> 
<span data-ttu-id="8fe29-135">Nuget.org genelinde benzersiz olması gereken büyük/küçük harf duyarsız paket tanımlayıcısı veya paketin bulunduğu Galeri.</span><span class="sxs-lookup"><span data-stu-id="8fe29-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="8fe29-136">Kimlikler, URL için geçerli olmayan boşluk veya karakterler içeremez ve genellikle .NET ad alanı kurallarını izler.</span><span class="sxs-lookup"><span data-stu-id="8fe29-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="8fe29-137">Bkz. rehberlik için [benzersiz bir paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="8fe29-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="8fe29-138">sürüm</span><span class="sxs-lookup"><span data-stu-id="8fe29-138">version</span></span>
<span data-ttu-id="8fe29-139">*Ana. Minor. Patch* deseninin ardından paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="8fe29-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="8fe29-140">Sürüm numaraları, [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions)bölümünde açıklandığı gibi bir ön sürüm son eki içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="8fe29-141">açıklama</span><span class="sxs-lookup"><span data-stu-id="8fe29-141">description</span></span>
<span data-ttu-id="8fe29-142">UI görüntüleme paketinin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="8fe29-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="8fe29-143">düzenliyor</span><span class="sxs-lookup"><span data-stu-id="8fe29-143">authors</span></span>
<span data-ttu-id="8fe29-144">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="8fe29-145">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="8fe29-146">lere</span><span class="sxs-lookup"><span data-stu-id="8fe29-146">owners</span></span>
<span data-ttu-id="8fe29-147">Nuget.org üzerindeki profil adlarını kullanan paket oluşturucularının virgülle ayrılmış listesi. Bu, genellikle ile aynı listeyle `authors`aynıdır ve paket NuGet.org 'e yüklenirken yok sayılır. Bkz. [NuGet.org üzerinde paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8fe29-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="8fe29-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="8fe29-148">projectUrl</span></span>
<span data-ttu-id="8fe29-149">Genellikle kullanıcı arabiriminde gösterildiği gibi, paketin ana sayfası için bir URL de nuget.org görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="8fe29-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="8fe29-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="8fe29-151">licenseUrl kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="8fe29-152">Bunun yerine lisans kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-152">Use license instead.</span></span>

<span data-ttu-id="8fe29-153">Genellikle Unuget.org gibi gösterilen paket lisansının URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="8fe29-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="8fe29-154">lisan</span><span class="sxs-lookup"><span data-stu-id="8fe29-154">license</span></span>
<span data-ttu-id="8fe29-155">Bir SPDX lisans ifadesi veya paket içindeki bir lisans dosyasının yolu, genellikle Usıs nuget.org gibidir. Paketi MıT veya BSD-2 yan tümcesi gibi ortak bir lisans altında lisansladıysanız, ilişkili [Spdx lisans tanımlayıcısını](https://spdx.org/licenses/)kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="8fe29-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="8fe29-157">NuGet.org yalnızca açık kaynak girişimi veya ücretsiz yazılım temeli tarafından onaylanan lisans ifadelerini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="8fe29-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="8fe29-158">Paketinizin birden çok ortak lisans kapsamında lisansı varsa, [Spdx Expression sözdizimi 2,0 sürümünü](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)kullanarak bileşik bir lisans belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="8fe29-159">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="8fe29-160">Lisans ifadeleri tarafından desteklenmeyen özel bir lisans kullanıyorsanız, lisans metniyle bir `.txt` veya `.md` dosyasını paketleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="8fe29-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-161">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="8fe29-162">MSBuild eşdeğeri için [Lisans ifadesi veya lisans dosyası paketleme](msbuild-targets.md#packing-a-license-expression-or-a-license-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="8fe29-163">NuGet 'in lisans ifadelerinin tam sözdizimi aşağıda, [Abnf](https://tools.ietf.org/html/rfc5234)' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="8fe29-164">Iurl</span><span class="sxs-lookup"><span data-stu-id="8fe29-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="8fe29-165">Iurl kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="8fe29-165">iconUrl is deprecated.</span></span> <span data-ttu-id="8fe29-166">Bunun yerine simgesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-166">Use icon instead.</span></span>

<span data-ttu-id="8fe29-167">Kullanıcı arabirimi görüntüsündeki paketin simgesi olarak kullanılacak saydam arka planlı bir 64x64 görüntüsünün URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="8fe29-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="8fe29-168">Bu öğenin, görüntüyü içeren bir Web sayfasının URL 'sini değil *doğrudan görüntü URL* 'sini içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8fe29-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="8fe29-169">Örneğin, GitHub 'dan bir görüntü kullanmak için, gibi <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>ham dosya URL 'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="8fe29-170">Simgesi</span><span class="sxs-lookup"><span data-stu-id="8fe29-170">icon</span></span>

<span data-ttu-id="8fe29-171">Paket içindeki bir görüntü dosyasının yoludur ve genellikle paket simgesi olarak nuget.org gibi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="8fe29-172">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="8fe29-173">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="8fe29-174">64x64 için bir görüntü resoulution önerilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-174">We recommend an image resoulution of 64x64.</span></span>

<span data-ttu-id="8fe29-175">Örneğin, NuGet. exe ' yi kullanarak bir paket oluştururken şunu nuspec ' e eklersiniz:</span><span class="sxs-lookup"><span data-stu-id="8fe29-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="8fe29-176">Paket simgesi nuspec örneği.</span><span class="sxs-lookup"><span data-stu-id="8fe29-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="8fe29-177">MSBuild eşdeğeri için, [bir simge görüntüsü dosyası paketleme](msbuild-targets.md#packing-an-icon-image-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="8fe29-178">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="8fe29-178">requireLicenseAcceptance</span></span>
<span data-ttu-id="8fe29-179">İstemcinin paketi yüklemeden önce, tüketicinin paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="8fe29-179">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="8fe29-180">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="8fe29-180">developmentDependency</span></span>
<span data-ttu-id="8fe29-181">*(2.8+)* Paket olup olmadığını belirten bir Boole değeri, bir geliştirme-yalnızca-paket bağımlılık diğer paketleri olarak eklenmesini engelleyen bağımlılık olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-181">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="8fe29-182">PackageReference (NuGet 4.8 +) ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-182">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="8fe29-183">[PackageReference için bkz. Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="8fe29-183">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="8fe29-184">özet</span><span class="sxs-lookup"><span data-stu-id="8fe29-184">summary</span></span>
> [!Important]
> <span data-ttu-id="8fe29-185">`summary`kullanım dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="8fe29-185">`summary` is being deprecated.</span></span> <span data-ttu-id="8fe29-186">Bunun yerine `description` kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-186">Use `description` instead.</span></span>

<span data-ttu-id="8fe29-187">UI görüntülemesi için paketin kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="8fe29-187">A short description of the package for UI display.</span></span> <span data-ttu-id="8fe29-188">Atlanırsa, kesilen bir sürümü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-188">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="8fe29-189">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="8fe29-189">releaseNotes</span></span>
<span data-ttu-id="8fe29-190">*(1.5+)* Kullanıcı arabiriminde gibi sık kullanılan paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesini, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine.</span><span class="sxs-lookup"><span data-stu-id="8fe29-190">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="8fe29-191">telif hakkı</span><span class="sxs-lookup"><span data-stu-id="8fe29-191">copyright</span></span>
<span data-ttu-id="8fe29-192">*(1.5+)* Ayrıntıları paketi için telif hakkı.</span><span class="sxs-lookup"><span data-stu-id="8fe29-192">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="8fe29-193">dil</span><span class="sxs-lookup"><span data-stu-id="8fe29-193">language</span></span>
<span data-ttu-id="8fe29-194">Paket için yerel ayar KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="8fe29-194">The locale ID for the package.</span></span> <span data-ttu-id="8fe29-195">Bkz. [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8fe29-195">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="8fe29-196">etiketler</span><span class="sxs-lookup"><span data-stu-id="8fe29-196">tags</span></span>
<span data-ttu-id="8fe29-197">Paketi tanımlayan ve arama ve filtreleme aracılığıyla paketlerin bulunabilirliğini sağlayan, boşlukla ayrılmış etiketlerin ve anahtar kelimelerin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="8fe29-197">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="8fe29-198">hizmet verebilir</span><span class="sxs-lookup"><span data-stu-id="8fe29-198">serviceable</span></span> 
<span data-ttu-id="8fe29-199">*(3.3+)* Yalnızca iç NuGet için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-199">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="8fe29-200">depo</span><span class="sxs-lookup"><span data-stu-id="8fe29-200">repository</span></span>
<span data-ttu-id="8fe29-201">Dört isteğe bağlı öznitelikten oluşan depo meta verileri `type` : `url` ve *(4.0 +)* ve `branch` ve `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="8fe29-201">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="8fe29-202">Bu öznitelikler, `.nupkg` kendisini oluşturan depoya eşlemenize olanak tanır. Bu, tek bir dal adı olarak daha ayrıntılı bir şekilde ele alınır ve/veya paketi oluşturan SHA-1 karmasını işleyin.</span><span class="sxs-lookup"><span data-stu-id="8fe29-202">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="8fe29-203">Bu, doğrudan bir sürüm denetim yazılımıyla çağrılabilen, genel olarak kullanılabilir bir URL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-203">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="8fe29-204">Bu, bilgisayar için amaçlanmış olduğu için bir HTML sayfası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-204">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="8fe29-205">Proje sayfasına bağlantı için, bunun yerine `projectUrl` alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-205">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="8fe29-206">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-206">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="8fe29-207">title</span><span class="sxs-lookup"><span data-stu-id="8fe29-207">title</span></span>
<span data-ttu-id="8fe29-208">Paketin bazı Kullanıcı arabiriminde kullanılabilen, okunabilir bir başlığı.</span><span class="sxs-lookup"><span data-stu-id="8fe29-208">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="8fe29-209">(nuget.org ve Visual Studio 'da Paket Yöneticisi başlık gösterme)</span><span class="sxs-lookup"><span data-stu-id="8fe29-209">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="8fe29-210">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-210">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="8fe29-211">packageTypes</span><span class="sxs-lookup"><span data-stu-id="8fe29-211">packageTypes</span></span>
<span data-ttu-id="8fe29-212">*(3,5 +)* Geleneksel bir bağımlılık paketi dışında paketin `<packageType>` türünü belirten sıfır veya daha fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-212">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="8fe29-213">Her packageType 'ın *ad* ve *Sürüm*öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-213">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="8fe29-214">Bkz. [paket türünü ayarlama](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="8fe29-214">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="8fe29-215">bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="8fe29-215">dependencies</span></span>
<span data-ttu-id="8fe29-216">Paketin bağımlılıklarını belirten sıfır veya daha `<dependency>` fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-216">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="8fe29-217">Her bağımlılığın *kimliği*, *sürümü*, *içerme* (3. x +) ve *exclude* (3. x +) öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-217">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="8fe29-218">Aşağıdaki [bağımlılıklara](#dependencies-element) bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-218">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="8fe29-219">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="8fe29-219">frameworkAssemblies</span></span>
<span data-ttu-id="8fe29-220">*(1.2 +)* Bu paketin gerektirdiği .NET Framework bütünleştirilmiş kod `<frameworkAssembly>` başvurularını tanımlayan sıfır veya daha fazla öğe koleksiyonu, bu, başvuruların paketi kullanan projelere eklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fe29-220">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="8fe29-221">Her frameworkAssembly *AssemblyName* ve *TargetFramework* öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-221">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="8fe29-222">Aşağıdaki [Framework derleme BAŞVURULARı GAC 'Yi belirtme](#specifying-framework-assembly-references-gac) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-222">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="8fe29-223">başvurular</span><span class="sxs-lookup"><span data-stu-id="8fe29-223">references</span></span>
<span data-ttu-id="8fe29-224">*(1,5 +)* Paket klasöründeki, proje başvuruları olarak `<reference>` eklenen derlemeleri adlandırarak sıfır veya daha fazla öğe koleksiyonu. `lib`</span><span class="sxs-lookup"><span data-stu-id="8fe29-224">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="8fe29-225">Her başvurunun bir *Dosya* özniteliği vardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-225">Each reference has a *file* attribute.</span></span> <span data-ttu-id="8fe29-226">`<references>`Ayrıca, öğeleri içeren `<group>` `<reference>` bir *TargetFramework* özniteliği içeren bir öğe içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-226">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="8fe29-227">Atlanırsa, içindeki `lib` tüm başvurular dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-227">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="8fe29-228">Aşağıda [Açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-228">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="8fe29-229">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8fe29-229">contentFiles</span></span>
<span data-ttu-id="8fe29-230">*(3.3 +)* Tüketim projesinde içerilecek `<files>` içerik dosyalarını tanımlayan öğelerin koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-230">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="8fe29-231">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-231">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="8fe29-232">Aşağıdaki [pakete dahil edilecek dosyaları belirtme](#specifying-files-to-include-in-the-package) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-232">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="8fe29-233">dosyaları</span><span class="sxs-lookup"><span data-stu-id="8fe29-233">files</span></span> 
<span data-ttu-id="8fe29-234">`<metadata>` `<files>` `<metadata>` `<contentFiles>` Düğüm, pakete dahil edilecek derleme ve içerik dosyalarını belirtmek için eşdüzey öğesi olarak bir düğüm ve altında bir alt öğe içerebilir. `<package>`</span><span class="sxs-lookup"><span data-stu-id="8fe29-234">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="8fe29-235">Ayrıntılar için bu konunun ilerleyen kısımlarında [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files) dahil etme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-235">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="8fe29-236">meta veri öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-236">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="8fe29-237">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="8fe29-237">minClientVersion</span></span>
<span data-ttu-id="8fe29-238">NuGet. exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yükleyesağlayan NuGet istemcisinin en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-238">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="8fe29-239">Bu, paket, NuGet istemcisinin belirli bir sürümünde eklenmiş olan `.nuspec` dosyanın belirli özelliklerine bağlı olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-239">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="8fe29-240">Örneğin, `developmentDependency` özniteliğini kullanan bir paket için `minClientVersion`"2,8" belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-240">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="8fe29-241">Benzer şekilde, `contentFiles` öğesini kullanan bir paket (sonraki bölüme bakın) "3,3" `minClientVersion` olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-241">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="8fe29-242">Ayrıca, 2,5 ' den önceki NuGet istemcileri bu bayrağı tanımadığı için, *her zaman* ne `minClientVersion` içermesi gerektiğine bakılmaksızın paketi yüklemeyi reddeder.</span><span class="sxs-lookup"><span data-stu-id="8fe29-242">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="8fe29-243">Değiştirme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-243">Replacement tokens</span></span>

<span data-ttu-id="8fe29-244">Bir paket oluştururken, `.nuspec` [ `nuget pack` komut](../reference/cli-reference/cli-ref-pack.md) dosyanın `<metadata>` düğümündeki $-Delimited belirteçlerini bir proje dosyasından veya `pack` komutun `-properties` anahtarından değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-244">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="8fe29-245">Komut satırında belirteç değerlerini ile `nuget pack -properties <name>=<value>;<name>=<value>`belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-245">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="8fe29-246">Örneğin, `$owners$` ve `$desc$` içinde `.nuspec` gibi bir belirteç kullanabilir ve değerlerini paketleme zamanında aşağıdaki şekilde sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8fe29-246">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="8fe29-247">Bir projeden değerleri kullanmak için, aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo, dosyanın `Properties` `AssemblyInfo.cs` veya `AssemblyInfo.vb`gibi).</span><span class="sxs-lookup"><span data-stu-id="8fe29-247">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="8fe29-248">Bu belirteçleri kullanmak için, `nuget pack` `.nuspec`yalnızca yerine proje dosyası ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-248">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="8fe29-249">Örneğin, `$id$` aşağıdaki komutu kullanırken, bir `.nuspec` dosyadaki ve `$version$` belirteçleri proje `AssemblyName` ve `AssemblyVersion` değerleriyle değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-249">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="8fe29-250">Genellikle, bir projeniz olduğunda, bu standart belirteçlerden bazılarını `.nuspec` otomatik olarak `nuget spec MyProject.csproj` içeren ilk kullanımı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-250">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="8fe29-251">Ancak, bir proje gerekli `.nuspec` öğeler için değerler eksikse `nuget pack` , başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8fe29-251">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="8fe29-252">Ayrıca, proje değerlerini değiştirirseniz, paketi oluşturmadan önce yeniden oluşturmayı unutmayın; Bu, paket komutunun `build` anahtarıyla kolayca yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-252">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="8fe29-253">Özel durumu `$configuration$`ile, projedeki değerler, komut satırında aynı belirtece atanmış herhangi bir tercih halinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-253">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="8fe29-254">Belirteç</span><span class="sxs-lookup"><span data-stu-id="8fe29-254">Token</span></span> | <span data-ttu-id="8fe29-255">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="8fe29-255">Value source</span></span> | <span data-ttu-id="8fe29-256">Değer</span><span class="sxs-lookup"><span data-stu-id="8fe29-256">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="8fe29-257">**$id $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-257">**$id$**</span></span> | <span data-ttu-id="8fe29-258">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="8fe29-258">Project file</span></span> | <span data-ttu-id="8fe29-259">Proje dosyasından AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="8fe29-259">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="8fe29-260">**$version $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-260">**$version$**</span></span> | <span data-ttu-id="8fe29-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8fe29-261">AssemblyInfo</span></span> | <span data-ttu-id="8fe29-262">Varsa Assemblyformationalversion, yoksa AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="8fe29-262">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="8fe29-263">**$author $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-263">**$author$**</span></span> | <span data-ttu-id="8fe29-264">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8fe29-264">AssemblyInfo</span></span> | <span data-ttu-id="8fe29-265">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="8fe29-265">AssemblyCompany</span></span> |
| <span data-ttu-id="8fe29-266">**$title $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-266">**$title$**</span></span> | <span data-ttu-id="8fe29-267">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8fe29-267">AssemblyInfo</span></span> | <span data-ttu-id="8fe29-268">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="8fe29-268">AssemblyTitle</span></span> |
| <span data-ttu-id="8fe29-269">**$description $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-269">**$description$**</span></span> | <span data-ttu-id="8fe29-270">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8fe29-270">AssemblyInfo</span></span> | <span data-ttu-id="8fe29-271">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="8fe29-271">AssemblyDescription</span></span> |
| <span data-ttu-id="8fe29-272">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-272">**$copyright$**</span></span> | <span data-ttu-id="8fe29-273">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8fe29-273">AssemblyInfo</span></span> | <span data-ttu-id="8fe29-274">Assemblytelif hakkı</span><span class="sxs-lookup"><span data-stu-id="8fe29-274">AssemblyCopyright</span></span> |
| <span data-ttu-id="8fe29-275">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="8fe29-275">**$configuration$**</span></span> | <span data-ttu-id="8fe29-276">Derleme DLL 'SI</span><span class="sxs-lookup"><span data-stu-id="8fe29-276">Assembly DLL</span></span> | <span data-ttu-id="8fe29-277">Derlemeyi oluşturmak için kullanılan yapılandırma, hata ayıklamayı varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="8fe29-277">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="8fe29-278">Yayın yapılandırması kullanarak bir paket oluşturmak için her zaman komut satırında ' ı kullanın `-properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="8fe29-278">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="8fe29-279">Belirteçler, [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files)dahil ettiğinizde yolları çözümlemek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-279">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="8fe29-280">Belirteçler, MSBuild özellikleriyle aynı adlara sahiptir ve geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyaları seçmenizi mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-280">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="8fe29-281">Örneğin, `.nuspec` dosyasında aşağıdaki belirteçleri kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="8fe29-281">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="8fe29-282">`AssemblyName` Ve MSBuild `LoggingLibrary` 'deyapılandırma`Release` ile olan bir derleme oluşturduğunuzda, paketteki dosyadakisonuççizgileriaşağıdakigibidir:`.nuspec`</span><span class="sxs-lookup"><span data-stu-id="8fe29-282">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="8fe29-283">Dependencies öğesi</span><span class="sxs-lookup"><span data-stu-id="8fe29-283">Dependencies element</span></span>

<span data-ttu-id="8fe29-284">`<dependency>` İçindeki `<dependencies>` öğesi,üstdüzeypaketinbağımlıolduğudiğerpaketleritanımlayanherhangibirsayıdaöğeiçerir.`<metadata>`</span><span class="sxs-lookup"><span data-stu-id="8fe29-284">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="8fe29-285">Her biri `<dependency>` için öznitelikleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-285">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="8fe29-286">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="8fe29-286">Attribute</span></span> | <span data-ttu-id="8fe29-287">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8fe29-287">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="8fe29-288">Istenir "EntityFramework" ve "NUnit" gibi bağımlılığın paket KIMLIĞI, nuget.org paketinin adı bir paket sayfasında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-288">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="8fe29-289">Istenir Bağımlılık olarak kabul edilebilir sürüm aralığı.</span><span class="sxs-lookup"><span data-stu-id="8fe29-289">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="8fe29-290">Tam sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges-and-wildcards) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-290">See [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="8fe29-291">Joker karakter (kayan) sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8fe29-291">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="8fe29-292">include</span><span class="sxs-lookup"><span data-stu-id="8fe29-292">include</span></span> | <span data-ttu-id="8fe29-293">Son pakete dahil edilecek bağımlılığı belirten, etiketleri ekle/çıkar (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="8fe29-293">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="8fe29-294">Varsayılan değer `all` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-294">The default value is `all`.</span></span> |
| <span data-ttu-id="8fe29-295">exclude</span><span class="sxs-lookup"><span data-stu-id="8fe29-295">exclude</span></span> | <span data-ttu-id="8fe29-296">Son pakette hariç tutulacak bağımlılığı belirten, etiketleri dahil et/hariç tut (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="8fe29-296">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="8fe29-297">Varsayılan değer `build,analyzers` , üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-297">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="8fe29-298">Ancak `content/ ContentFiles` , üzerine yazılabilir olmayan son pakette da örtük olarak hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="8fe29-298">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="8fe29-299">İle belirtilen Etiketler `exclude` , ile `include`belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-299">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="8fe29-300">Örneğin, `include="runtime, compile" exclude="compile"` ile `include="runtime"`aynıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-300">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="8fe29-301">Dahil etme/hariç tutma etiketi</span><span class="sxs-lookup"><span data-stu-id="8fe29-301">Include/Exclude tag</span></span> | <span data-ttu-id="8fe29-302">Hedefin etkilenen klasörleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-302">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="8fe29-303">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8fe29-303">contentFiles</span></span> | <span data-ttu-id="8fe29-304">İçerik</span><span class="sxs-lookup"><span data-stu-id="8fe29-304">Content</span></span> |
| <span data-ttu-id="8fe29-305">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="8fe29-305">runtime</span></span> | <span data-ttu-id="8fe29-306">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="8fe29-306">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="8fe29-307">se</span><span class="sxs-lookup"><span data-stu-id="8fe29-307">compile</span></span> | <span data-ttu-id="8fe29-308">LIB</span><span class="sxs-lookup"><span data-stu-id="8fe29-308">lib</span></span> |
| <span data-ttu-id="8fe29-309">derleme</span><span class="sxs-lookup"><span data-stu-id="8fe29-309">build</span></span> | <span data-ttu-id="8fe29-310">Build (MSBuild props ve targets)</span><span class="sxs-lookup"><span data-stu-id="8fe29-310">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="8fe29-311">yerel</span><span class="sxs-lookup"><span data-stu-id="8fe29-311">native</span></span> | <span data-ttu-id="8fe29-312">yerel</span><span class="sxs-lookup"><span data-stu-id="8fe29-312">native</span></span> |
| <span data-ttu-id="8fe29-313">yok</span><span class="sxs-lookup"><span data-stu-id="8fe29-313">none</span></span> | <span data-ttu-id="8fe29-314">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="8fe29-314">No folders</span></span> |
| <span data-ttu-id="8fe29-315">tüm</span><span class="sxs-lookup"><span data-stu-id="8fe29-315">all</span></span> | <span data-ttu-id="8fe29-316">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="8fe29-316">All folders</span></span> |

<span data-ttu-id="8fe29-317">Örneğin, aşağıdaki satırlar `PackageA` sürüm 1.1.0 veya üzeri ve `PackageB` sürüm 1. x bağımlılıklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-317">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="8fe29-318">Aşağıdaki satırlar aynı paketlere `contentFiles` `PackageA` `build` `PackageB`yönelik bağımlılıklarıgösterir,ancakveklasörlerininyanısıra,veklasörlerinindadahiledileceğinibelirtir.`native` `compile`</span><span class="sxs-lookup"><span data-stu-id="8fe29-318">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="8fe29-319">`.nuspec` Kullanarak `.nuspec` birprojedenoluştururken,buprojedevarolanbağımlılıklareldeedilendosyayaotomatikolarakeklenmez.`nuget spec`</span><span class="sxs-lookup"><span data-stu-id="8fe29-319">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="8fe29-320">Bunun yerine, `nuget pack myproject.csproj`öğesini kullanın ve oluşturulan *. nupkg* dosyasının içinden *. nuspec* dosyasını alın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-320">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="8fe29-321">Bu *. nuspec* , bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-321">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="8fe29-322">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="8fe29-322">Dependency groups</span></span>

<span data-ttu-id="8fe29-323">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="8fe29-323">*Version 2.0+*</span></span>

<span data-ttu-id="8fe29-324">Tek bir düz listeye alternatif olarak, bağımlılıklar içindeki `<group>` `<dependencies>`öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-324">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="8fe29-325">Her grup adlı `targetFramework` bir özniteliğe sahiptir ve sıfır veya daha fazla `<dependency>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-325">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="8fe29-326">Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-326">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8fe29-327">Özniteliği olmayan öğe, bağımlılıkların varsayılan veya geri dönüş listesi olarak kullanılır. `<group>` `targetFramework`</span><span class="sxs-lookup"><span data-stu-id="8fe29-327">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="8fe29-328">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe29-328">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8fe29-329">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-329">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8fe29-330">Aşağıdaki örnek, `<group>` öğesinin farklı çeşitlemelerini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-330">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="8fe29-331">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="8fe29-331">Explicit assembly references</span></span>

<span data-ttu-id="8fe29-332">Öğesi, paket kullanılırken hedef projenin başvurması `packages.config` gereken derlemeleri açıkça belirtmek için kullanan projeler tarafından kullanılır. `<references>`</span><span class="sxs-lookup"><span data-stu-id="8fe29-332">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="8fe29-333">Açık başvurular genellikle yalnızca tasarım zamanı derlemeler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-333">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="8fe29-334">Daha fazla bilgi için bkz. [projeler tarafından başvurulan derlemeleri seçme](../create-packages/select-assemblies-referenced-by-projects.md) hakkında daha fazla bilgi için bu sayfaya bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-334">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="8fe29-335">Örneğin, aşağıdaki `<references>` öğe, NuGet 'e `xunit.extensions.dll` yalnızca `xunit.dll` başvuru eklemesi için, pakette ek derlemeler olsa bile:</span><span class="sxs-lookup"><span data-stu-id="8fe29-335">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="8fe29-336">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="8fe29-336">Reference groups</span></span>

<span data-ttu-id="8fe29-337">Tek bir düz listeye alternatif olarak, başvurular, içindeki `<group>` `<references>`öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-337">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="8fe29-338">Her grup adlı `targetFramework` bir özniteliğe sahiptir ve sıfır veya daha fazla `<reference>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-338">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="8fe29-339">Hedef çerçeve projenin çerçeve profiliyle uyumluysa, bu başvurular bir projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-339">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8fe29-340">Özniteliği olmayan öğe, başvuru varsayılan veya geri dönüş listesi olarak kullanılır. `<group>` `targetFramework`</span><span class="sxs-lookup"><span data-stu-id="8fe29-340">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="8fe29-341">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe29-341">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8fe29-342">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="8fe29-342">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8fe29-343">Aşağıdaki örnek, `<group>` öğesinin farklı çeşitlemelerini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-343">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="8fe29-344">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="8fe29-344">Framework assembly references</span></span>

<span data-ttu-id="8fe29-345">Framework derlemeleri, .NET Framework 'ün bir parçası olan ve belirli bir makine için genel derleme önbelleğinde (GAC) olması gereken olanlardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-345">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="8fe29-346">Bir paket, `<frameworkAssemblies>` öğesi içindeki bu derlemeleri tanımlayarak, gerekli başvuruların projenin bu tür başvurularına sahip olmadığı olayda bir projeye eklendiğinden emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-346">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="8fe29-347">Kuşkusuz bu tür derlemeler doğrudan bir pakete dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="8fe29-347">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="8fe29-348">Öğesi, her biri aşağıdaki öznitelikleri `<frameworkAssembly>` belirten sıfır veya daha fazla öğe içeriyor: `<frameworkAssemblies>`</span><span class="sxs-lookup"><span data-stu-id="8fe29-348">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="8fe29-349">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="8fe29-349">Attribute</span></span> | <span data-ttu-id="8fe29-350">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8fe29-350">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fe29-351">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="8fe29-351">**assemblyName**</span></span> | <span data-ttu-id="8fe29-352">Istenir Tam nitelikli derleme adı.</span><span class="sxs-lookup"><span data-stu-id="8fe29-352">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="8fe29-353">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="8fe29-353">**targetFramework**</span></span> | <span data-ttu-id="8fe29-354">Seçim Bu başvurunun uygulandığı hedef çerçeveyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-354">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="8fe29-355">Atlanırsa, başvurunun tüm çerçeveler için geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-355">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="8fe29-356">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="8fe29-356">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="8fe29-357">Aşağıdaki örnekte, tüm hedef çerçeveler `System.Net` için bir başvuru ve yalnızca .NET Framework 4,0 `System.ServiceModel` için bir başvuru gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-357">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="8fe29-358">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="8fe29-358">Including assembly files</span></span>

<span data-ttu-id="8fe29-359">[Paket oluşturma](../create-packages/creating-a-package.md)bölümünde açıklanan kuralları izlerseniz, `.nuspec` dosyadaki dosyaların listesini açıkça belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8fe29-359">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="8fe29-360">Komut `nuget pack` , gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="8fe29-360">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="8fe29-361">Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'lerine derleme başvuruları `.resources.dll` *ekler, çünkü bu, yerelleştirilmiş* uydu derlemeleri oldukları varsayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-361">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="8fe29-362">Bu nedenle, başka bir şekilde `.resources.dll` temel paket kodu içeren dosyalar için kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="8fe29-362">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="8fe29-363">Bu otomatik davranışı atlamak ve bir pakete hangi dosyaların ekleneceğini açıkça denetlemek `<files>` için, bir öğeyi bir `<package>` alt öğesi `<metadata>`(ve eşdüzey) olarak yerleştirin ve her bir dosyayı ayrı `<file>` bir öğeyle tanımlayarak.</span><span class="sxs-lookup"><span data-stu-id="8fe29-363">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="8fe29-364">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-364">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="8fe29-365">NuGet 2. x ve öncesiyle ve kullanan `packages.config` `<files>` projelerde, bir paket yüklendiğinde değişmez içerik dosyalarını dahil etmek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-365">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="8fe29-366">NuGet 3.3 + ve projeleri packagereference ile, `<contentFiles>` bunun yerine öğesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-366">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="8fe29-367">Ayrıntılar için aşağıdaki [içerik dosyalarını ekleme](#including-content-files) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8fe29-367">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="8fe29-368">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="8fe29-368">File element attributes</span></span>

<span data-ttu-id="8fe29-369">Her `<file>` öğe aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-369">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="8fe29-370">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="8fe29-370">Attribute</span></span> | <span data-ttu-id="8fe29-371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8fe29-371">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fe29-372">**YN**</span><span class="sxs-lookup"><span data-stu-id="8fe29-372">**src**</span></span> | <span data-ttu-id="8fe29-373">`exclude` Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-373">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8fe29-374">Mutlak bir yol belirtilmediği takdirde yol `.nuspec` dosyayla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-374">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="8fe29-375">Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-375">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8fe29-376">**hedef**</span><span class="sxs-lookup"><span data-stu-id="8fe29-376">**target**</span></span> | <span data-ttu-id="8fe29-377">Kaynak dosyaların yerleştirildiği,, `lib`, veya `tools`ile `content` `build`başlaması gereken paket içindeki klasörün göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-377">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="8fe29-378">Bkz. [kural tabanlı çalışma dizininden. nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="8fe29-378">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="8fe29-379">**amaz**</span><span class="sxs-lookup"><span data-stu-id="8fe29-379">**exclude**</span></span> | <span data-ttu-id="8fe29-380">`src` Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="8fe29-380">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8fe29-381">Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-381">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="8fe29-382">Örnekler</span><span class="sxs-lookup"><span data-stu-id="8fe29-382">Examples</span></span>

<span data-ttu-id="8fe29-383">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="8fe29-383">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="8fe29-384">**Hedef çerçeveye özgü tek bütünleştirilmiş kod**</span><span class="sxs-lookup"><span data-stu-id="8fe29-384">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="8fe29-385">**Joker karakter kullanan DLL 'Ler kümesi**</span><span class="sxs-lookup"><span data-stu-id="8fe29-385">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="8fe29-386">**Farklı çerçeveler için dll 'Ler**</span><span class="sxs-lookup"><span data-stu-id="8fe29-386">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="8fe29-387">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="8fe29-387">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="8fe29-388">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="8fe29-388">Including content files</span></span>

<span data-ttu-id="8fe29-389">İçerik dosyaları, bir paketin bir projeye eklemesi gereken sabit dosyalardır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-389">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="8fe29-390">Sabit olması, tüketim projesi tarafından değiştirilmeleri amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-390">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="8fe29-391">Örnek içerik dosyaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8fe29-391">Example content files include:</span></span>

- <span data-ttu-id="8fe29-392">Kaynak olarak gömülü görüntüler</span><span class="sxs-lookup"><span data-stu-id="8fe29-392">Images that are embedded as resources</span></span>
- <span data-ttu-id="8fe29-393">Zaten derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="8fe29-393">Source files that are already compiled</span></span>
- <span data-ttu-id="8fe29-394">Projenin derleme çıktısına dahil olması gereken betikler</span><span class="sxs-lookup"><span data-stu-id="8fe29-394">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="8fe29-395">Projeye dahil olması gereken ancak projeye özgü değişikliklere gerek gerektirmeyen paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="8fe29-395">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="8fe29-396">İçerik dosyaları, `<files>` `target` özniteliğinde `content` klasörü belirtilerek öğesini kullanarak bir pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-396">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="8fe29-397">Ancak, bu tür dosyalar, bir paket bir projeye yüklendiğinde, bunun yerine `<contentFiles>` öğesini kullanarak yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-397">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="8fe29-398">Tüketen projelerle maksimum uyumluluk için, her iki öğe içinde içerik dosyalarını ideal bir paket belirler.</span><span class="sxs-lookup"><span data-stu-id="8fe29-398">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="8fe29-399">İçerik dosyaları için Files öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="8fe29-399">Using the files element for content files</span></span>

<span data-ttu-id="8fe29-400">İçerik dosyaları için yalnızca derleme dosyaları için aynı biçimi kullanın, ancak aşağıdaki örneklerde gösterildiği gibi `content` `target` özniteliğinde temel klasör olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="8fe29-400">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="8fe29-401">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="8fe29-401">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="8fe29-402">**Dizin yapısıyla içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="8fe29-402">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="8fe29-403">**Hedef çerçeveye özgü içerik dosyası**</span><span class="sxs-lookup"><span data-stu-id="8fe29-403">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="8fe29-404">**İçerik dosyası ada sahip bir klasöre kopyalanmış**</span><span class="sxs-lookup"><span data-stu-id="8fe29-404">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="8fe29-405">Bu durumda, ' deki uzantının `target` içindeki `src` uzantıyla eşleşmediği ve bu nedenle adın bu `target` bölümünü bir klasör olarak değerlendirmiş olduğunu görür:</span><span class="sxs-lookup"><span data-stu-id="8fe29-405">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="8fe29-406">**Uzantısız içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="8fe29-406">**Content files without extensions**</span></span>

<span data-ttu-id="8fe29-407">Uzantısı olmayan dosyaları dahil etmek için, `*` veya `**` joker karakterleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fe29-407">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="8fe29-408">**Derin yolu ve derin hedefi olan içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="8fe29-408">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="8fe29-409">Bu durumda, kaynak ve hedef için dosya uzantıları eşleştiğinden, NuGet hedefin bir klasör değil bir dosya adı olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="8fe29-409">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="8fe29-410">**Paketteki bir içerik dosyasını yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="8fe29-410">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="8fe29-411">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="8fe29-411">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="8fe29-412">İçerik dosyaları için contentFiles öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="8fe29-412">Using the contentFiles element for content files</span></span>

<span data-ttu-id="8fe29-413">*PackageReference ile NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="8fe29-413">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="8fe29-414">Varsayılan olarak, bir paket içeriği bir `contentFiles` klasöre koyar (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-414">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="8fe29-415">Bu durumda, `contentFiles` `.nuspec` ' a bir düğüm eklemek gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-415">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="8fe29-416">Hangi dosyaların ekleneceğini denetlemek için, `<contentFiles>` öğesi, tam dosyaları içeren `<files>` öğelerin bir koleksiyonu olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="8fe29-416">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="8fe29-417">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-417">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="8fe29-418">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="8fe29-418">Attribute</span></span> | <span data-ttu-id="8fe29-419">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8fe29-419">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fe29-420">**include**</span><span class="sxs-lookup"><span data-stu-id="8fe29-420">**include**</span></span> | <span data-ttu-id="8fe29-421">Istenir `exclude` Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu.</span><span class="sxs-lookup"><span data-stu-id="8fe29-421">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8fe29-422">Mutlak bir yol belirtilmediği takdirde yol `contentFiles` klasöre göre değişir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-422">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="8fe29-423">Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-423">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8fe29-424">**amaz**</span><span class="sxs-lookup"><span data-stu-id="8fe29-424">**exclude**</span></span> | <span data-ttu-id="8fe29-425">`src` Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="8fe29-425">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8fe29-426">Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-426">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8fe29-427">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="8fe29-427">**buildAction**</span></span> | <span data-ttu-id="8fe29-428">,,, `Content`Vb. gibi MSBuild `None` `Embedded Resource` `Compile`için içerik öğesine atanacak yapı eylemi. Varsayılan, `Compile` değeridir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-428">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="8fe29-429">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="8fe29-429">**copyToOutput**</span></span> | <span data-ttu-id="8fe29-430">İçerik öğelerinin derleme (veya yayımlama) çıkış klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="8fe29-430">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="8fe29-431">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-431">The default is false.</span></span> |
| <span data-ttu-id="8fe29-432">**flatten**</span><span class="sxs-lookup"><span data-stu-id="8fe29-432">**flatten**</span></span> | <span data-ttu-id="8fe29-433">İçerik öğelerinin derleme çıkışında tek bir klasöre mi kopyalanacağını (true) veya paketteki klasör yapısını korumayı (false) gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="8fe29-433">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="8fe29-434">Bu bayrak yalnızca copyToOutput bayrağı true olarak ayarlandığında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-434">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="8fe29-435">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-435">The default is false.</span></span> |

<span data-ttu-id="8fe29-436">Bir paket yüklenirken NuGet, alt öğelerini `<contentFiles>` yukarıdan aşağıya uygular.</span><span class="sxs-lookup"><span data-stu-id="8fe29-436">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="8fe29-437">Aynı dosyayla birden çok giriş eşleşiyorsa, tüm girişler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8fe29-437">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="8fe29-438">Aynı öznitelik için bir çakışma varsa en üstteki girdi alt girişleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="8fe29-438">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="8fe29-439">Paket klasörü yapısı</span><span class="sxs-lookup"><span data-stu-id="8fe29-439">Package folder structure</span></span>

<span data-ttu-id="8fe29-440">Paket projesi, aşağıdaki kalıbı kullanarak içerik yapısını almalıdır:</span><span class="sxs-lookup"><span data-stu-id="8fe29-440">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="8fe29-441">`codeLanguages`,,, veya belirli bir `cs` `vb` `fs` `any``$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="8fe29-441">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="8fe29-442">`TxM`NuGet tarafından desteklenen geçerli bir hedef çerçeve adıdır (bkz. [hedef çerçeveler](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="8fe29-442">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="8fe29-443">Bu söz dizimi sonuna herhangi bir klasör yapısı eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe29-443">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="8fe29-444">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-444">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="8fe29-445">Boş klasörler `.` , belirli dil birleşimleri ve TXM için içerik sağlamayı devre dışı bırakmak için kullanılabilir. Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8fe29-445">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="8fe29-446">Örnek contentFiles bölümü</span><span class="sxs-lookup"><span data-stu-id="8fe29-446">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="8fe29-447">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="8fe29-447">Example nuspec files</span></span>

<span data-ttu-id="8fe29-448">**Bağımlılıklar veya `.nuspec` dosyalar belirtmeyen bir basit**</span><span class="sxs-lookup"><span data-stu-id="8fe29-448">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="8fe29-449">**Bağımlılıkları `.nuspec` olan A**</span><span class="sxs-lookup"><span data-stu-id="8fe29-449">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="8fe29-450">**Dosyalarla `.nuspec` birlikte**</span><span class="sxs-lookup"><span data-stu-id="8fe29-450">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="8fe29-451">**Bir `.nuspec` Framework Derlemeleriyle**</span><span class="sxs-lookup"><span data-stu-id="8fe29-451">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="8fe29-452">Bu örnekte, belirli proje hedefleri için aşağıdakiler yüklenir:</span><span class="sxs-lookup"><span data-stu-id="8fe29-452">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="8fe29-453">. NET4-> `System.Web`,`System.Net`</span><span class="sxs-lookup"><span data-stu-id="8fe29-453">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="8fe29-454">. NET4 Istemci profili->`System.Net`</span><span class="sxs-lookup"><span data-stu-id="8fe29-454">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="8fe29-455">Silverlight 3->`System.Json`</span><span class="sxs-lookup"><span data-stu-id="8fe29-455">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="8fe29-456">WindowsPhone->`Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="8fe29-456">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
