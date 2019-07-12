---
title: NuGet için .nuspec dosyası başvurusu
description: Paket meta verileri bir paketi ve paket tüketicilere bilgi sağlamak için oluştururken kullanılan .nuspec dosyası içerir.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842407"
---
# <a name="nuspec-reference"></a><span data-ttu-id="0358a-103">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="0358a-103">.nuspec reference</span></span>

<span data-ttu-id="0358a-104">A `.nuspec` paket meta verileri içeren bir XML bildirimi dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="0358a-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="0358a-105">Bu bildirim, paket oluşturun ve tüketicilere bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="0358a-106">Bildirim her zaman bir paketine dahildir.</span><span class="sxs-lookup"><span data-stu-id="0358a-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="0358a-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="0358a-107">In this topic:</span></span>

- [<span data-ttu-id="0358a-108">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="0358a-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="0358a-109">[Belirteçleri değiştirme](#replacement-tokens) (Visual Studio projesi ile kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="0358a-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="0358a-110">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="0358a-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="0358a-111">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="0358a-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="0358a-112">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="0358a-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="0358a-113">Derleme dosyaları da dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="0358a-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="0358a-114">İçerik dosyaları dahil</span><span class="sxs-lookup"><span data-stu-id="0358a-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="0358a-115">Örneğin nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="0358a-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="0358a-116">Proje türü uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="0358a-116">Project type compatibility</span></span>

- <span data-ttu-id="0358a-117">Kullanma `.nuspec` ile `nuget.exe pack` kullanan olmayan-SDK-stili projeleri `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="0358a-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="0358a-118">A `.nuspec` dosya için paketler oluşturmak için gerekli değildir [SDK stili projeleri](../resources/check-project-format.md) (genellikle .NET Core ve .NET Standard projeleri [SDK özniteliği](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="0358a-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="0358a-119">(Unutmayın bir `.nuspec` paketi oluşturduğunuzda oluşturulur.)</span><span class="sxs-lookup"><span data-stu-id="0358a-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="0358a-120">Kullanarak bir paket oluşturuyorsanız `dotnet.exe pack` veya `msbuild pack target`, öneririz, [özellikleri içeren](../reference/msbuild-targets.md#pack-target) , genellikle `.nuspec` bunun yerine proje dosyasında dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="0358a-121">Ancak, bunun yerine seçebileceğiniz [kullanan bir `.nuspec` kullanarak paketi dosyaya `dotnet.exe` veya `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="0358a-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="0358a-122">Geçiş projeleri için `packages.config` için [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` dosya paketi oluşturmak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="0358a-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="0358a-123">Bunun yerine, [msbuild paketi](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="0358a-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="0358a-124">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="0358a-124">General form and schema</span></span>

<span data-ttu-id="0358a-125">Geçerli `nuspec.xsd` şema dosyası bulunabilir [NuGet GitHub deposu](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="0358a-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="0358a-126">Bu şema içinde bir `.nuspec` dosyası aşağıdaki genel form vardır:</span><span class="sxs-lookup"><span data-stu-id="0358a-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="0358a-127">Şema NET bir görsel bir temsili şema dosyasını Visual Studio'da Tasarım modunda açın ve tıklayarak **XML Şeması Gezgini** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="0358a-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="0358a-128">Alternatif olarak, kod olarak dosyasını açın, Düzenleyicisi'nde sağ tıklatın ve seçin **XML Şeması Gezgini Göster**.</span><span class="sxs-lookup"><span data-stu-id="0358a-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="0358a-129">Her iki şekilde (çoğunlukla genişletildiğinde) aşağıdaki gibi bir görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="0358a-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio şema Gezgini ile nuspec.xsd Aç](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="0358a-131">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="0358a-131">Required metadata elements</span></span>

<span data-ttu-id="0358a-132">Aşağıdaki öğeleri bir paket için en düşük gereksinimler olsa da, eklemeyi düşünmelidir [isteğe bağlı meta veri öğeleri](#optional-metadata-elements) genel deneyimini iyileştirmek için paketinizle birlikte geliştiricileri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0358a-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="0358a-133">Bu öğeleri içinde görünmelidir bir `<metadata>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0358a-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="0358a-134">kimlik</span><span class="sxs-lookup"><span data-stu-id="0358a-134">id</span></span> 
<span data-ttu-id="0358a-135">Nuget.org veya ne olursa olsun arasında benzersiz olması gereken büyük küçük harf duyarsız paket tanımlayıcısı galeri paketi bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="0358a-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="0358a-136">Kimlikleri değil boşluk ya da bir URL için geçerli olmayan karakterler içeren ve genellikle .NET ad alanı kuralları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0358a-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="0358a-137">Bkz: [benzersiz paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="0358a-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="0358a-138">sürüm</span><span class="sxs-lookup"><span data-stu-id="0358a-138">version</span></span>
<span data-ttu-id="0358a-139">Aşağıdaki Paket sürümü *ana.İkincil.yama* deseni.</span><span class="sxs-lookup"><span data-stu-id="0358a-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="0358a-140">Sürüm numaraları, yayın öncesi son içerebilir, açıklandığı [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="0358a-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="0358a-141">açıklama</span><span class="sxs-lookup"><span data-stu-id="0358a-141">description</span></span>
<span data-ttu-id="0358a-142">Kullanıcı Arabirimi ekranı için paketinin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="0358a-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="0358a-143">Yazarları</span><span class="sxs-lookup"><span data-stu-id="0358a-143">authors</span></span>
<span data-ttu-id="0358a-144">Nuget.org profil adları eşleşen paketleri yazar, virgülle ayrılmış listesi. Bunlar nuget.org NuGet galerisinde görüntülenir ve paketleri çapraz başvuru için aynı yazarları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="0358a-145">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="0358a-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="0358a-146">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="0358a-146">owners</span></span>
<span data-ttu-id="0358a-147">Nuget.org adresinden profil adları kullanarak paket creators virgülle ayrılmış listesi. Bu genellikle aynı liste olarak olur `authors`ve nuget.org için paket karşıya yüklenirken göz ardı edilir. Bkz: [yönetme paket sahipleri nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="0358a-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="0358a-148">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0358a-148">projectUrl</span></span>
<span data-ttu-id="0358a-149">Genellikle kullanıcı Arabiriminde gösterilir paketin giriş sayfası için bir URL yanı sıra nuget.org görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0358a-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="0358a-150">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0358a-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="0358a-151">licenseUrl kullanımdan kaldırılıyor.</span><span class="sxs-lookup"><span data-stu-id="0358a-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="0358a-152">Lisans kullanın.</span><span class="sxs-lookup"><span data-stu-id="0358a-152">Use license instead.</span></span>

<span data-ttu-id="0358a-153">Genellikle kullanıcı arabirimleri nuget.org gibi gösterilir, paketi lisansının URL'si.</span><span class="sxs-lookup"><span data-stu-id="0358a-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="0358a-154">Lisans</span><span class="sxs-lookup"><span data-stu-id="0358a-154">license</span></span>
<span data-ttu-id="0358a-155">SPDX lisans ifadesi veya genellikle nuget.org gibi kullanıcı arabirimleri gösterilen paket içindeki bir lisans dosyasının yolu. Paket MIT veya BSD-2-yan gibi ortak bir lisans kapsamında lisans ilişkili kullanırsanız [SPDX lisans tanımlayıcısı](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="0358a-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="0358a-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0358a-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="0358a-157">NuGet.org yalnızca açık kaynak girişim veya ücretsiz Software Foundation tarafından onaylanan lisans ifadeleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="0358a-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="0358a-158">Paketinizi altında birden çok ortak lisansları lisanslanmıştır, kullanarak bir bileşik lisans belirtebilirsiniz [SPDX ifadesi söz dizimi sürümü 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="0358a-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="0358a-159">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0358a-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="0358a-160">Lisans ifadeleri tarafından desteklenmeyen özel lisans kullanırsanız, paketleyebilir bir `.txt` veya `.md` Lisans'ın metin dosyası.</span><span class="sxs-lookup"><span data-stu-id="0358a-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="0358a-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0358a-161">For example:</span></span>

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

<span data-ttu-id="0358a-162">MSBuild eşdeğer için göz atın [lisans ifadesi veya bir lisans dosyası](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="0358a-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="0358a-163">NuGet'ın lisans ifadelerin söz dizimi aşağıda açıklanan [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="0358a-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="0358a-164">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0358a-164">iconUrl</span></span>
<span data-ttu-id="0358a-165">Kullanıcı Arabirimi ekranı pakette için simge olarak kullanılacak bir URL saydam arka plana sahip 64 x 64 görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="0358a-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="0358a-166">Bu öğe içerdiğinden emin olun *resim URL'si doğrudan* ve görüntü içeren bir web sayfasının URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="0358a-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="0358a-167">Örneğin, github'dan bir görüntüyü kullanmak için URL gibi ham dosyasını kullanın. <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="0358a-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="0358a-168">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0358a-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="0358a-169">İstemci paketi yüklemeden önce paket lisansını kabul etmek için tüketici sor olup olmadığını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0358a-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="0358a-170">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0358a-170">developmentDependency</span></span>
<span data-ttu-id="0358a-171">*(2.8+)* Paket olup olmadığını belirten bir Boole değeri, bir geliştirme-yalnızca-paket bağımlılık diğer paketleri olarak eklenmesini engelleyen bağımlılık olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="0358a-172">PackageReference (NuGet 4.8 +) bu bayrağı Ayrıca, derleme zamanı varlıklar derlemeden dışladığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0358a-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="0358a-173">Bkz: [PackageReference DevelopmentDependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="0358a-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="0358a-174">özet</span><span class="sxs-lookup"><span data-stu-id="0358a-174">summary</span></span>
<span data-ttu-id="0358a-175">Kullanıcı Arabirimi ekranı için paket kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="0358a-175">A short description of the package for UI display.</span></span> <span data-ttu-id="0358a-176">Atlanırsa, kesilmiş bir sürümünü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="0358a-177">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0358a-177">releaseNotes</span></span>
<span data-ttu-id="0358a-178">*(1.5+)* Kullanıcı arabiriminde gibi sık kullanılan paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesini, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine.</span><span class="sxs-lookup"><span data-stu-id="0358a-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="0358a-179">telif hakkı</span><span class="sxs-lookup"><span data-stu-id="0358a-179">copyright</span></span>
<span data-ttu-id="0358a-180">*(1.5+)* Ayrıntıları paketi için telif hakkı.</span><span class="sxs-lookup"><span data-stu-id="0358a-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="0358a-181">dil</span><span class="sxs-lookup"><span data-stu-id="0358a-181">language</span></span>
<span data-ttu-id="0358a-182">Paket için yerel ayar kimliği.</span><span class="sxs-lookup"><span data-stu-id="0358a-182">The locale ID for the package.</span></span> <span data-ttu-id="0358a-183">Bkz: [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0358a-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="0358a-184">etiketler</span><span class="sxs-lookup"><span data-stu-id="0358a-184">tags</span></span>
<span data-ttu-id="0358a-185">Etiketleri ve arama ve filtreleme yoluyla paketleri paket ve ürettiği bulunabilirliğini tanımlayan anahtar sözcükleri boşlukla ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="0358a-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="0358a-186">tutulabilmesi</span><span class="sxs-lookup"><span data-stu-id="0358a-186">serviceable</span></span> 
<span data-ttu-id="0358a-187">*(3.3+)* Yalnızca iç NuGet için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0358a-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="0358a-188">depo</span><span class="sxs-lookup"><span data-stu-id="0358a-188">repository</span></span>
<span data-ttu-id="0358a-189">Depo meta verileri, dört isteğe bağlı özniteliklerden oluşan: *türü* ve *url* *(4.0 +)* , ve *dal* ve  *işleme* *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="0358a-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="0358a-190">Bu öznitelikler, alma olasılığı ile oluşturulan depo .nupkg eşlemek izin tek tek bir dalı veya da paket yerleşik işleme olarak ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="0358a-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="0358a-191">Bu, doğrudan bir sürüm denetim yazılımı tarafından çağrılabilen genel kullanıma açık bir url olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0358a-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="0358a-192">Bu bilgisayar için tasarlanmıştır olarak html sayfasından olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0358a-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="0358a-193">Proje sayfasına bağlamak için kullanın `projectUrl` , bunun yerine alan.</span><span class="sxs-lookup"><span data-stu-id="0358a-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="0358a-194">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0358a-194">minClientVersion</span></span>
<span data-ttu-id="0358a-195">Nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yüklemek NuGet istemci en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0358a-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="0358a-196">Bu paket belirli özelliklere bağımlı olduğunda kullanılır `.nuspec` belirli bir NuGet istemcisi sürümünde eklenen dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="0358a-197">Örneğin, bir paketini kullanarak `developmentDependency` özniteliği için "2.8" belirtmelidir `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="0358a-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="0358a-198">Benzer şekilde, bir paketini kullanarak `contentFiles` öğesi (sonraki bölüme bakın) ayarlamalıdır `minClientVersion` "3.3" için.</span><span class="sxs-lookup"><span data-stu-id="0358a-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="0358a-199">Bu bayrak, 2.5 önce NuGet istemcileri algılanmadığı için de unutmayın bunlar *her zaman* ne olursa olsun paketi yüklemek Reddet `minClientVersion` içerir.</span><span class="sxs-lookup"><span data-stu-id="0358a-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="0358a-200">title</span><span class="sxs-lookup"><span data-stu-id="0358a-200">title</span></span>
<span data-ttu-id="0358a-201">Bazı kullanıcı Arabiriminde kullanılabilen paket İnsan dostu başlık görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="0358a-202">(nuget.org ve Visual Studio'da Paket Yöneticisi başlığını gösterme)</span><span class="sxs-lookup"><span data-stu-id="0358a-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="0358a-203">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="0358a-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="0358a-204">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0358a-204">packageTypes</span></span>
<span data-ttu-id="0358a-205">*(3.5 +)*  Sıfır veya daha fazla koleksiyonu `<packageType>` dışında geleneksel bağımlılık paket, paketin türünü belirleyen öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="0358a-206">Her bir packageType öznitelikleri *adı* ve *sürüm*.</span><span class="sxs-lookup"><span data-stu-id="0358a-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="0358a-207">Bkz: [ayar paket türü](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="0358a-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="0358a-208">bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="0358a-208">dependencies</span></span>
<span data-ttu-id="0358a-209">Sıfır veya daha fazla koleksiyonu `<dependency>` paket için bağımlılıkları belirtme öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="0358a-210">Her bir bağımlılığı özniteliklerini *kimliği*, *sürüm*, *dahil* (3.x+) ve *hariç* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="0358a-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="0358a-211">Bkz: [bağımlılıkları](#dependencies-element) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="0358a-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="0358a-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="0358a-212">frameworkAssemblies</span></span>
<span data-ttu-id="0358a-213">*(1.2 +)*  Sıfır veya daha fazla koleksiyonu `<frameworkAssembly>` öğeleri, bu paket gerekli .NET Framework derleme başvurularını tanımlamak da sağlar başvurular paketi kullanan projeler için eklenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="0358a-214">Her frameworkAssembly sahip *assemblyName* ve *targetFramework* öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="0358a-215">Bkz: [framework derlemesi belirterek başvuran GAC](#specifying-framework-assembly-references-gac) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="0358a-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="0358a-216">başvurular</span><span class="sxs-lookup"><span data-stu-id="0358a-216">references</span></span>
<span data-ttu-id="0358a-217">*(1.5 +)*  Sıfır veya daha fazla koleksiyonu `<reference>` paketin derlemelerde adlandırma öğeleri `lib` proje başvuru olarak eklediğiniz klasörü.</span><span class="sxs-lookup"><span data-stu-id="0358a-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="0358a-218">Her başvuru bir *dosya* özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0358a-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="0358a-219">`<references>` de içerebilir bir `<group>` öğesi ile bir *targetFramework* ardından içeren öznitelik `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="0358a-220">Atlanırsa, tüm başvuruları `lib` dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="0358a-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="0358a-221">Bkz: [açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="0358a-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="0358a-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="0358a-222">contentFiles</span></span>
<span data-ttu-id="0358a-223">*(3.3 +)*  Koleksiyonunu `<files>` alıcı projeye eklenecek içerik dosyaları tanımlayan öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="0358a-224">Bu dosyaları nasıl bunlar içinde proje sisteminin kullanılması gerektiğini açıklayan öznitelikler kümesi ile belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0358a-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="0358a-225">Bkz: [dosyalar paket içerisine dâhil etmek belirtme](#specifying-files-to-include-in-the-package) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="0358a-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="0358a-226">dosyaları</span><span class="sxs-lookup"><span data-stu-id="0358a-226">files</span></span> 
<span data-ttu-id="0358a-227">`<package>` Düğüm içerebilir bir `<files>` düğümü bir eşdüzeyi olarak `<metadata>`ve `<contentFiles>` altında alt `<metadata>`paket içerisine dâhil etmek hangi derleme ve içerik dosyaları belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="0358a-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="0358a-228">Bkz: [derleme dosyaları da dahil olmak üzere](#including-assembly-files) ve [içerik dosyaları dahil olmak üzere](#including-content-files) Ayrıntılar için bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0358a-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="0358a-229">Belirteçleri değiştirme</span><span class="sxs-lookup"><span data-stu-id="0358a-229">Replacement tokens</span></span>

<span data-ttu-id="0358a-230">Bir paket oluştururken [ `nuget pack` komut](../tools/cli-ref-pack.md) $ayrılmış belirteçler değiştirir `.nuspec` dosyanın `<metadata>` düğümü'nden ya da proje dosyası gelen değerlerle veya `pack` komutunun `-properties`geçin.</span><span class="sxs-lookup"><span data-stu-id="0358a-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="0358a-231">Komut satırında belirttiğiniz belirteci değerlerle `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="0358a-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="0358a-232">Örneğin, bir belirteç gibi kullanabileceğiniz `$owners$` ve `$desc$` içinde `.nuspec` ve saat gibi paketleme sırasında değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="0358a-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="0358a-233">Bir projeden değerleri kullanmak için aşağıdaki tabloda açıklanan belirteçleri belirtin (dosyasında başvurduğu AssemblyInfo `Properties` gibi `AssemblyInfo.cs` veya `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="0358a-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="0358a-234">Bu belirteçleri kullanmak için çalıştırın `nuget pack` proje dosyası yerine yalnızca `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0358a-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="0358a-235">Örneğin aşağıdaki komutu kullanarak, `$id$` ve `$version$` içinde belirteçleri bir `.nuspec` dosyası proje değiştirilmiş `AssemblyName` ve `AssemblyVersion` değerleri:</span><span class="sxs-lookup"><span data-stu-id="0358a-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="0358a-236">Genellikle, sahip olduğunuz bir proje oluşturduğunuzda `.nuspec` başlangıçta kullanarak `nuget spec MyProject.csproj` otomatik olarak içeren bazı standart bu belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="0358a-237">Ancak, bir proje için değerler yoksa gerekli `.nuspec` öğeleri, ardından `nuget pack` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0358a-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="0358a-238">Ayrıca, Proje değeri değiştirirseniz, paket oluşturmadan önce yeniden emin olun; Bu paketi komut ile kolayca yapılabilir `build` geçin.</span><span class="sxs-lookup"><span data-stu-id="0358a-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="0358a-239">Dışında `$configuration$`, projedeki değerleri herhangi bir komut satırında aynı belirtece atanan yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="0358a-240">Belirteç</span><span class="sxs-lookup"><span data-stu-id="0358a-240">Token</span></span> | <span data-ttu-id="0358a-241">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="0358a-241">Value source</span></span> | <span data-ttu-id="0358a-242">Değer</span><span class="sxs-lookup"><span data-stu-id="0358a-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="0358a-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="0358a-243">**$id$**</span></span> | <span data-ttu-id="0358a-244">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="0358a-244">Project file</span></span> | <span data-ttu-id="0358a-245">Proje dosyasında AssemblyName (başlık)</span><span class="sxs-lookup"><span data-stu-id="0358a-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="0358a-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="0358a-246">**$version$**</span></span> | <span data-ttu-id="0358a-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="0358a-247">AssemblyInfo</span></span> | <span data-ttu-id="0358a-248">AssemblyInformationalVersion varsa, aksi takdirde AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="0358a-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="0358a-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="0358a-249">**$author$**</span></span> | <span data-ttu-id="0358a-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="0358a-250">AssemblyInfo</span></span> | <span data-ttu-id="0358a-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="0358a-251">AssemblyCompany</span></span> |
| <span data-ttu-id="0358a-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="0358a-252">**$title$**</span></span> | <span data-ttu-id="0358a-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="0358a-253">AssemblyInfo</span></span> | <span data-ttu-id="0358a-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="0358a-254">AssemblyTitle</span></span> |
| <span data-ttu-id="0358a-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="0358a-255">**$description$**</span></span> | <span data-ttu-id="0358a-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="0358a-256">AssemblyInfo</span></span> | <span data-ttu-id="0358a-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="0358a-257">AssemblyDescription</span></span> |
| <span data-ttu-id="0358a-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="0358a-258">**$copyright$**</span></span> | <span data-ttu-id="0358a-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="0358a-259">AssemblyInfo</span></span> | <span data-ttu-id="0358a-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="0358a-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="0358a-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="0358a-261">**$configuration$**</span></span> | <span data-ttu-id="0358a-262">Derleme DLL</span><span class="sxs-lookup"><span data-stu-id="0358a-262">Assembly DLL</span></span> | <span data-ttu-id="0358a-263">Hata ayıklama için varsayılan olarak ayarlanıyor derlemesi oluşturmak için kullanılan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0358a-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="0358a-264">Yayın Yapılandırması'nı kullanarak bir paket oluşturmak için her zaman kullanmanız gerektiğini unutmayın `-properties Configuration=Release` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="0358a-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="0358a-265">Belirteçleri de kullanılabilir, eklediğinizde yolları çözümlemek için [derleme dosyaları](#including-assembly-files) ve [içerik dosyaları](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="0358a-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="0358a-266">Belirteçler, geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyalar seçmek edinerek MSBuild özellikleri olarak aynı ada sahip.</span><span class="sxs-lookup"><span data-stu-id="0358a-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="0358a-267">Örneğin, aşağıdaki belirteçler kullanırsanız `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0358a-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="0358a-268">Ve bir derleme, `AssemblyName` olduğu `LoggingLibrary` ile `Release` MSBuild, sonuçta elde edilen satırları yapılandırmasında `.nuspec` paket dosyasında aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0358a-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="0358a-269">Bağımlılıklar öğesi</span><span class="sxs-lookup"><span data-stu-id="0358a-269">Dependencies element</span></span>

<span data-ttu-id="0358a-270">`<dependencies>` Öğesiyle `<metadata>` içeren herhangi bir sayıda `<dependency>` en üst düzey paket olduğu diğer paketleri tanımlayan öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="0358a-271">Her öznitelik `<dependency>` aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0358a-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="0358a-272">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0358a-272">Attribute</span></span> | <span data-ttu-id="0358a-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0358a-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="0358a-274">(Gerekli) Bir paketi sayfasında "EntityFramework" ve paket nuget.org adı "NUnit" gibi bir bağımlılık, uygulamanın paket Kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0358a-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="0358a-275">(Gerekli) Sürümleri bağımlılık olarak kabul edilebilir aralık.</span><span class="sxs-lookup"><span data-stu-id="0358a-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="0358a-276">Bkz: [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards) için söz dizimi.</span><span class="sxs-lookup"><span data-stu-id="0358a-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="0358a-277">include</span><span class="sxs-lookup"><span data-stu-id="0358a-277">include</span></span> | <span data-ttu-id="0358a-278">İçerme/dışlama virgülle ayrılmış listesi (aşağıya bakın) son pakette eklenecek bağımlılığın gösteren etiketler.</span><span class="sxs-lookup"><span data-stu-id="0358a-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="0358a-279">Varsayılan değer `all` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="0358a-279">The default value is `all`.</span></span> |
| <span data-ttu-id="0358a-280">exclude</span><span class="sxs-lookup"><span data-stu-id="0358a-280">exclude</span></span> | <span data-ttu-id="0358a-281">İçerme/dışlama virgülle ayrılmış listesi (aşağıya bakın) son pakette dışlanacak bağımlılığın gösteren etiketler.</span><span class="sxs-lookup"><span data-stu-id="0358a-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="0358a-282">Varsayılan değer `build,analyzers` olabilen aşırı yazılmış.</span><span class="sxs-lookup"><span data-stu-id="0358a-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="0358a-283">Ancak `content/ ContentFiles` aşırı yazılı olamaz son pakette de örtülü olarak tutulur.</span><span class="sxs-lookup"><span data-stu-id="0358a-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="0358a-284">İle belirtilen etiketlere `exclude` ile belirtilenler üzerinde önceliklidir `include`.</span><span class="sxs-lookup"><span data-stu-id="0358a-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="0358a-285">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="0358a-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="0358a-286">Etiket Ekle/Dışla</span><span class="sxs-lookup"><span data-stu-id="0358a-286">Include/Exclude tag</span></span> | <span data-ttu-id="0358a-287">Etkilenen hedef klasör</span><span class="sxs-lookup"><span data-stu-id="0358a-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="0358a-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="0358a-288">contentFiles</span></span> | <span data-ttu-id="0358a-289">İçerik</span><span class="sxs-lookup"><span data-stu-id="0358a-289">Content</span></span> |
| <span data-ttu-id="0358a-290">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="0358a-290">runtime</span></span> | <span data-ttu-id="0358a-291">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="0358a-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="0358a-292">Derleme</span><span class="sxs-lookup"><span data-stu-id="0358a-292">compile</span></span> | <span data-ttu-id="0358a-293">lib</span><span class="sxs-lookup"><span data-stu-id="0358a-293">lib</span></span> |
| <span data-ttu-id="0358a-294">derleme</span><span class="sxs-lookup"><span data-stu-id="0358a-294">build</span></span> | <span data-ttu-id="0358a-295">derleme (MSBuild özellikler ve hedefler)</span><span class="sxs-lookup"><span data-stu-id="0358a-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="0358a-296">yerel</span><span class="sxs-lookup"><span data-stu-id="0358a-296">native</span></span> | <span data-ttu-id="0358a-297">yerel</span><span class="sxs-lookup"><span data-stu-id="0358a-297">native</span></span> |
| <span data-ttu-id="0358a-298">yok</span><span class="sxs-lookup"><span data-stu-id="0358a-298">none</span></span> | <span data-ttu-id="0358a-299">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="0358a-299">No folders</span></span> |
| <span data-ttu-id="0358a-300">tüm</span><span class="sxs-lookup"><span data-stu-id="0358a-300">all</span></span> | <span data-ttu-id="0358a-301">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="0358a-301">All folders</span></span> |

<span data-ttu-id="0358a-302">Örneğin, aşağıdaki satırları üzerinde bağımlılıkları göstermek `PackageA` 1.1.0 sürümü veya sonraki bir sürümünü ve `PackageB` sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="0358a-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="0358a-303">Aşağıdaki satırları aynı paket bağımlılıkları gösterir, ancak dahil edileceğini belirtin `contentFiles` ve `build` klasörleri `PackageA` ve her şeyi ancak `native` ve `compile` klasörleri `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="0358a-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="0358a-304">Not: Oluştururken bir `.nuspec` kullanarak proje `nuget spec`, o projede bağımlılıkları otomatik olarak dahil edilecek ortaya çıkan `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="0358a-305">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="0358a-305">Dependency groups</span></span>

<span data-ttu-id="0358a-306">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="0358a-306">*Version 2.0+*</span></span>

<span data-ttu-id="0358a-307">Tek bir düz liste alternatif, project kullanarak hedef framework profile göre bağımlılıklar belirtilebilir `<group>` öğeleri içinde `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="0358a-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="0358a-308">Her Grup adlı öznitelikle `targetFramework` ve sıfır veya daha fazlasını içeren `<dependency>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="0358a-309">Hedef Çerçeve proje framework profiliyle uyumlu olduğunda bu bağımlılıkların birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="0358a-310">`<group>` Öğe olmadan bir `targetFramework` özniteliği bağımlılıkları varsayılan ya da geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="0358a-311">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="0358a-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="0358a-312">Grubu biçimi karıştırılmış, düz bir liste ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0358a-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="0358a-313">Aşağıdaki örnek, farklı çeşitleri gösterir `<group>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="0358a-313">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="0358a-314">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="0358a-314">Explicit assembly references</span></span>

<span data-ttu-id="0358a-315">`<references>` Öğesi kullanarak projeleri tarafından kullanılan `packages.config` paket kullanırken hedef projeye başvurması gereken derlemelerin açıkça belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="0358a-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="0358a-316">Açık başvuruları genellikle yalnızca tasarım zamanı derlemeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="0358a-317">Daha fazla bilgi için sayfasına bakın [proje tarafından başvurulan derlemeleri seçerek](../create-packages/select-assemblies-referenced-by-projects.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="0358a-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="0358a-318">Örneğin, aşağıdaki `<references>` öğe bildirir yalnızca başvuruları eklemek için NuGet `xunit.dll` ve `xunit.extensions.dll` olsa bile ek derlemeler paketi:</span><span class="sxs-lookup"><span data-stu-id="0358a-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="0358a-319">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="0358a-319">Reference groups</span></span>

<span data-ttu-id="0358a-320">Tek bir düz liste alternatif, project kullanarak hedef framework profile göre başvuruları belirtilebilir `<group>` öğeleri içinde `<references>`.</span><span class="sxs-lookup"><span data-stu-id="0358a-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="0358a-321">Her Grup adlı öznitelikle `targetFramework` ve sıfır veya daha fazlasını içeren `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="0358a-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="0358a-322">Hedef Çerçeve proje framework profiliyle uyumlu olduğunda bu başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="0358a-323">`<group>` Öğe olmadan bir `targetFramework` özniteliği başvuruları varsayılan ya da geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="0358a-324">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="0358a-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="0358a-325">Grubu biçimi karıştırılmış, düz bir liste ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="0358a-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="0358a-326">Aşağıdaki örnek, farklı çeşitleri gösterir `<group>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="0358a-326">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="0358a-327">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="0358a-327">Framework assembly references</span></span>

<span data-ttu-id="0358a-328">Framework derlemeleri, .NET framework'ün bir parçasıdır ve herhangi bir makine için genel derleme önbelleğinde (GAC) olması izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="0358a-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="0358a-329">Bu bütünleştirilmiş kodlarında belirleme `<frameworkAssemblies>` öğesi, bir paket sağlayabilirsiniz projesinde bu tür başvurularını zaten yok olay, gerekli başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="0358a-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="0358a-330">Bu tür derlemeler, bir paket içinde doğrudan dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="0358a-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="0358a-331">`<frameworkAssemblies>` Sıfır veya daha fazla öğe içeriyor `<frameworkAssembly>` öğeleri, her biri aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="0358a-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="0358a-332">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0358a-332">Attribute</span></span> | <span data-ttu-id="0358a-333">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0358a-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0358a-334">**AssemblyName**</span><span class="sxs-lookup"><span data-stu-id="0358a-334">**assemblyName**</span></span> | <span data-ttu-id="0358a-335">(Gerekli) Tam derleme adı.</span><span class="sxs-lookup"><span data-stu-id="0358a-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="0358a-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="0358a-336">**targetFramework**</span></span> | <span data-ttu-id="0358a-337">(İsteğe bağlı) Bu başvuru uygulandığı hedef Framework'ü belirtir.</span><span class="sxs-lookup"><span data-stu-id="0358a-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="0358a-338">Atlanırsa, başvuru için tüm çerçeveleri geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0358a-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="0358a-339">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="0358a-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="0358a-340">Aşağıdaki örnek, bir başvuru gösterir `System.Net` için tüm çerçeveleri ve başvuru hedef `System.ServiceModel` yalnızca .NET Framework 4.0 için:</span><span class="sxs-lookup"><span data-stu-id="0358a-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="0358a-341">Derleme dosyaları da dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="0358a-341">Including assembly files</span></span>

<span data-ttu-id="0358a-342">Açıklanan kurallarını takip ederseniz [paket oluşturma](../create-packages/creating-a-package.md), dosyaların bir listesini açıkça belirtmeniz gerekmez `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="0358a-343">`nuget pack` Komutu, gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="0358a-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="0358a-344">Bir projeye bir paketi yüklendiğinde, NuGet paket DLL'leri derleme başvurularını otomatik olarak ekler. *hariç* adlandırılmış olanlar `.resources.dll` çünkü yerelleştirilmiş yardımcı derlemeler olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="0358a-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="0358a-345">Bu nedenle, kullanmaktan kaçının `.resources.dll` Aksi takdirde, gerekli paket kodu içeren dosyalar için.</span><span class="sxs-lookup"><span data-stu-id="0358a-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="0358a-346">Bu otomatik davranış atlayabilir ve hangi dosyaların bir paketine dahil edilen açıkça denetlemek için yerleştirin bir `<files>` öğesi alt öğesi olarak `<package>` (ve bir eşdüzeyi `<metadata>`), her dosyayı ayrı bir tanımlamak `<file>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0358a-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="0358a-347">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0358a-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="0358a-348">İle NuGet 2.x ve önceki sürümleri ve kullanarak projeleri `packages.config`, `<files>` öğesi bir paketi yüklendiğinde sabit içerik dosyalarını eklemek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="0358a-349">NuGet 3.3 + ve projeleri PackageReference, `<contentFiles>` öğe yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0358a-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="0358a-350">Bkz: [içerik dosyaları dahil olmak üzere](#including-content-files) altındaki ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="0358a-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="0358a-351">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="0358a-351">File element attributes</span></span>

<span data-ttu-id="0358a-352">Her `<file>` öğesi aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="0358a-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="0358a-353">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0358a-353">Attribute</span></span> | <span data-ttu-id="0358a-354">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0358a-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0358a-355">**src**</span><span class="sxs-lookup"><span data-stu-id="0358a-355">**src**</span></span> | <span data-ttu-id="0358a-356">Tarafından belirtilen dışlamaları tabi dahil edilecek dosyalar ve dosya konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0358a-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="0358a-357">Yolun göreli olduğu `.nuspec` mutlak bir yol belirtilmezse dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="0358a-358">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0358a-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="0358a-359">**Hedef**</span><span class="sxs-lookup"><span data-stu-id="0358a-359">**target**</span></span> | <span data-ttu-id="0358a-360">Klasörün başlamalıdır. burada kaynak dosyaları yerleştirilir, paket içindeki göreli yolu `lib`, `content`, `build`, veya `tools`.</span><span class="sxs-lookup"><span data-stu-id="0358a-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="0358a-361">Bkz: [kural tabanlı bir çalışma dizininden bir .nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="0358a-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="0358a-362">**Hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="0358a-362">**exclude**</span></span> | <span data-ttu-id="0358a-363">Dışlanacak dosya desenlerinin veya dosyaların noktalı virgülle ayrılmış listesi `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="0358a-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="0358a-364">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0358a-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="0358a-365">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0358a-365">Examples</span></span>

<span data-ttu-id="0358a-366">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="0358a-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="0358a-367">**Belirli bir hedef çerçeve için tek bir derleme**</span><span class="sxs-lookup"><span data-stu-id="0358a-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="0358a-368">**Joker karakter kullanarak DLL'leri kümesi**</span><span class="sxs-lookup"><span data-stu-id="0358a-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="0358a-369">**Farklı çerçeveler için DLL'leri**</span><span class="sxs-lookup"><span data-stu-id="0358a-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="0358a-370">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="0358a-370">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="0358a-371">İçerik dosyaları dahil</span><span class="sxs-lookup"><span data-stu-id="0358a-371">Including content files</span></span>

<span data-ttu-id="0358a-372">İçerik dosyaları bir proje eklemek için bir paket gereken sabit dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0358a-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="0358a-373">Sabit olduğundan, bunlar kullanan proje tarafından değiştirilmesi kullanılmaya yönelik değildir.</span><span class="sxs-lookup"><span data-stu-id="0358a-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="0358a-374">Örnek içerik dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="0358a-374">Example content files include:</span></span>

- <span data-ttu-id="0358a-375">Kaynak olarak gömülü görüntü</span><span class="sxs-lookup"><span data-stu-id="0358a-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="0358a-376">Önceden derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="0358a-376">Source files that are already compiled</span></span>
- <span data-ttu-id="0358a-377">Proje derleme çıktısı ile dahil edilmesi gereken komut</span><span class="sxs-lookup"><span data-stu-id="0358a-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="0358a-378">Projeye özgü herhangi bir değişiklik gerekmez ancak projeye dahil edilmesi gereken bir paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="0358a-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="0358a-379">İçerik paketini kullanarak dosyaları eklenir `<files>` öğesini belirterek `content` klasöründe `target` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0358a-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="0358a-380">Bunun yerine kullanan PackageReference kullanarak bir proje paketi yüklendiğinde, ancak bu tür dosyaları göz ardı edilir `<contentFiles>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0358a-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="0358a-381">Projeleri tüketen ile en fazla uyumluluk için bir paket içerik dosyalarını ideal olarak her iki öğeleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="0358a-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="0358a-382">Dosya öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="0358a-382">Using the files element for content files</span></span>

<span data-ttu-id="0358a-383">İçerik dosyaları için yalnızca derleme dosyalarında olduğu gibi aynı biçimi kullanır, ancak belirtin `content` temel klasör olarak `target` özniteliği aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="0358a-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="0358a-384">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0358a-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="0358a-385">**Dizin yapısı ile içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0358a-385">**Content files with directory structure**</span></span>

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

<span data-ttu-id="0358a-386">**İçerik dosyası için bir hedef çerçeve belirli**</span><span class="sxs-lookup"><span data-stu-id="0358a-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="0358a-387">**İçerik dosya adı nokta olan bir klasöre kopyalandı**</span><span class="sxs-lookup"><span data-stu-id="0358a-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="0358a-388">Bu durumda, NuGet görür uzantı `target` uzantı eşleşmiyor `src` ve bu nedenle bu bölümü adı değerlendirir `target` klasörü olarak:</span><span class="sxs-lookup"><span data-stu-id="0358a-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="0358a-389">**Uzantısız içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0358a-389">**Content files without extensions**</span></span>

<span data-ttu-id="0358a-390">Uzantısız dosyaları eklenip eklenmeyeceğini kullanın `*` veya `**` joker karakterleri:</span><span class="sxs-lookup"><span data-stu-id="0358a-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="0358a-391">**Ayrıntılı yolu ve ayrıntılı hedef içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0358a-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="0358a-392">Bu durumda, kaynak ve hedef dosya uzantılarını aynı gerektiğinden, NuGet hedef dosya adını ve bir klasör olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="0358a-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="0358a-393">**Paketteki içerik bir dosyayı yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="0358a-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="0358a-394">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="0358a-394">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="0358a-395">ContentFiles öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="0358a-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="0358a-396">*NuGet 4.0 + PackageReference ile*</span><span class="sxs-lookup"><span data-stu-id="0358a-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="0358a-397">Varsayılan olarak, bir paket içeriği yerleştirir bir `contentFiles` klasörü (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları dahil.</span><span class="sxs-lookup"><span data-stu-id="0358a-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="0358a-398">Bu durumda eklenmesi gerekli değil bir `contentFiles` düğümünde `.nuspec` hiç.</span><span class="sxs-lookup"><span data-stu-id="0358a-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="0358a-399">Hangi dosyaların dahil olduğunu denetlemek için `<contentFiles>` öğeyi belirten bir koleksiyonu `<files>` tam dosyaları tanımlayan öğeleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="0358a-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="0358a-400">Bu dosyaları nasıl bunlar içinde proje sisteminin kullanılması gerektiğini açıklayan öznitelikler kümesi ile belirtilir:</span><span class="sxs-lookup"><span data-stu-id="0358a-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="0358a-401">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="0358a-401">Attribute</span></span> | <span data-ttu-id="0358a-402">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0358a-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0358a-403">**include**</span><span class="sxs-lookup"><span data-stu-id="0358a-403">**include**</span></span> | <span data-ttu-id="0358a-404">(Gerekli) Tarafından belirtilen dışlamaları tabi dahil edilecek dosyalar ve dosya konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0358a-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="0358a-405">Yolun göreli olduğu `.nuspec` mutlak bir yol belirtilmezse dosya.</span><span class="sxs-lookup"><span data-stu-id="0358a-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="0358a-406">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0358a-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="0358a-407">**Hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="0358a-407">**exclude**</span></span> | <span data-ttu-id="0358a-408">Dışlanacak dosya desenlerinin veya dosyaların noktalı virgülle ayrılmış listesi `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="0358a-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="0358a-409">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0358a-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="0358a-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="0358a-410">**buildAction**</span></span> | <span data-ttu-id="0358a-411">Derleme eylemi gibi MSBuild için içerik öğesinin atanacağı `Content`, `None`, `Embedded Resource`, `Compile`vb. Varsayılan, `Compile` değeridir.</span><span class="sxs-lookup"><span data-stu-id="0358a-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="0358a-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="0358a-412">**copyToOutput**</span></span> | <span data-ttu-id="0358a-413">Çıkış klasörü yapı içerik öğeleri kopyalama (veya yayımlamak) belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0358a-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="0358a-414">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="0358a-414">The default is false.</span></span> |
| <span data-ttu-id="0358a-415">**flatten**</span><span class="sxs-lookup"><span data-stu-id="0358a-415">**flatten**</span></span> | <span data-ttu-id="0358a-416">İçerik öğeleri derleme çıktı (true) tek bir klasöre kopyalamak ya da klasör yapısını (false) paketindeki korumak için etkinleştirilip etkinleştirilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0358a-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="0358a-417">Bu bayrağı yalnızca copyToOutput bayrak ayarlandığında çalışır true.</span><span class="sxs-lookup"><span data-stu-id="0358a-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="0358a-418">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="0358a-418">The default is false.</span></span> |

<span data-ttu-id="0358a-419">Bir paketi yüklerken NuGet alt öğelerinin geçerlidir `<contentFiles>` yukarıdan.</span><span class="sxs-lookup"><span data-stu-id="0358a-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="0358a-420">Daha sonra aynı dosyanın birden çok girişi eşleşen tüm girişleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0358a-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="0358a-421">Aynı öznitelik için bir çakışma varsa, en üstteki girişe daha aşağıdaki girişler geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="0358a-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="0358a-422">Paket klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="0358a-422">Package folder structure</span></span>

<span data-ttu-id="0358a-423">Şu biçimi kullanarak içerik paketi Proje yapısı:</span><span class="sxs-lookup"><span data-stu-id="0358a-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="0358a-424">`codeLanguages` olabilir `cs`, `vb`, `fs`, `any`, ya da küçük harfli eşdeğeri bir verilen `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="0358a-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="0358a-425">`TxM` NuGet destekleyen herhangi bir geçerli hedef çerçeve adı olan (bkz [hedef çerçeveyi](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="0358a-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="0358a-426">Bu söz dizimi sonuna kadar herhangi bir klasör yapısının eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0358a-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="0358a-427">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0358a-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="0358a-428">Boş klasörler kullanabileceğiniz `.` örneğin dil ve TxM, belirli bir kombinasyonu için içerik sağlama dışında katılmak için:</span><span class="sxs-lookup"><span data-stu-id="0358a-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="0358a-429">Örnek contentFiles bölümünde</span><span class="sxs-lookup"><span data-stu-id="0358a-429">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="0358a-430">Örneğin nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="0358a-430">Example nuspec files</span></span>

<span data-ttu-id="0358a-431">**Basit bir `.nuspec` , bağımlılıklar veya dosyaları belirtmiyor**</span><span class="sxs-lookup"><span data-stu-id="0358a-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="0358a-432">**A `.nuspec` bağımlılıklar**</span><span class="sxs-lookup"><span data-stu-id="0358a-432">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="0358a-433">**A `.nuspec` dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0358a-433">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="0358a-434">**A `.nuspec` framework derlemeleri ile**</span><span class="sxs-lookup"><span data-stu-id="0358a-434">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="0358a-435">Bu örnekte, belirli proje hedefleri aşağıdaki yüklenir:</span><span class="sxs-lookup"><span data-stu-id="0358a-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="0358a-436">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="0358a-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="0358a-437">. NET4 İstemci profili -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="0358a-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="0358a-438">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="0358a-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="0358a-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="0358a-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
