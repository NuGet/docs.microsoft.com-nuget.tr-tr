---
title: NuGet için. nuspec dosya başvurusu
description: . Nuspec dosyası, bir paket oluştururken ve paket tüketicilere bilgi sağlamak için kullanılan paket meta verilerini içerir.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: f91d47bdf9b957b512d3d83434693ee93de07afb
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623142"
---
# <a name="nuspec-reference"></a><span data-ttu-id="fef6a-103">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="fef6a-103">.nuspec reference</span></span>

<span data-ttu-id="fef6a-104">`.nuspec`Dosya, paket meta verilerini içeren BIR XML bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="fef6a-105">Bu bildirim her ikisi de paketini derlemek ve tüketicilere bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="fef6a-106">Bildirim her zaman bir pakete dahildir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="fef6a-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="fef6a-107">In this topic:</span></span>

- [<span data-ttu-id="fef6a-108">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="fef6a-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="fef6a-109">[Değiştirme belirteçleri](#replacement-tokens) (bir Visual Studio projesiyle kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="fef6a-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="fef6a-110">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="fef6a-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="fef6a-111">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="fef6a-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="fef6a-112">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="fef6a-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="fef6a-113">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="fef6a-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="fef6a-114">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="fef6a-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="fef6a-115">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="fef6a-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="fef6a-116">Proje türü uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="fef6a-116">Project type compatibility</span></span>

- <span data-ttu-id="fef6a-117">Kullanan `.nuspec` `nuget.exe pack` SDK olmayan projeler için ile kullanın `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="fef6a-118">`.nuspec` [SDK stilindeki projelere](../resources/check-project-format.md) yönelik paketler oluşturmak için bir dosya gerekli değildir (genellikle .NET Core ve [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanan .NET Standard projeler).</span><span class="sxs-lookup"><span data-stu-id="fef6a-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="fef6a-119">( `.nuspec` Paketi oluşturduğunuzda bir ' nin oluşturulduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="fef6a-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="fef6a-120">Veya kullanarak bir paket oluşturuyorsanız `dotnet.exe pack` `msbuild pack target` , bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri dahil](../reference/msbuild-targets.md#pack-target) etmenizi öneririz `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="fef6a-121">Ancak, bunun yerine [ `.nuspec` `dotnet.exe` `msbuild pack target` veya kullanarak paketbir dosya kullanmayı ](../reference/msbuild-targets.md#packing-using-a-nuspec)seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="fef6a-122">`packages.config`' Den [packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için, `.nuspec` paketi oluşturmak için bir dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="fef6a-123">Bunun yerine, [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="fef6a-124">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="fef6a-124">General form and schema</span></span>

<span data-ttu-id="fef6a-125">Geçerli `nuspec.xsd` şema dosyası [NuGet GitHub deposunda](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="fef6a-126">Bu şema içinde, bir `.nuspec` dosya aşağıdaki genel biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="fef6a-127">Şemanın net bir görsel temsili için, şema dosyasını Visual Studio 'da tasarım modunda açın ve **XML şema Gezgini** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="fef6a-128">Alternatif olarak, dosyayı kod olarak açın, düzenleyicide sağ tıklayın ve **XML şeması Gezginini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="fef6a-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="fef6a-129">Aşağıdakilerden biri gibi bir görünüm alacağınız şekilde (çoğunlukla genişletilir):</span><span class="sxs-lookup"><span data-stu-id="fef6a-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Nuspec. xsd Open ile Visual Studio şema Gezgini](media/SchemaExplorer.png)

<span data-ttu-id="fef6a-131">. Nuspec dosyasındaki tüm XML öğesi adları büyük/küçük harfe duyarlıdır, çünkü genel olarak XML için bu durumdur.</span><span class="sxs-lookup"><span data-stu-id="fef6a-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="fef6a-132">Örneğin, meta veri öğesinin kullanılması `<description>` doğru ve `<Description>` doğru değildir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="fef6a-133">Her öğe adı için uygun büyük küçük harf aşağıda belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="fef6a-134">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-134">Required metadata elements</span></span>

<span data-ttu-id="fef6a-135">Aşağıdaki öğeler bir paket için en düşük gereksinimlerdir, ancak geliştiricilerin paketinize sahip olduğu genel deneyimi geliştirmek için [isteğe bağlı meta veri öğelerini](#optional-metadata-elements) eklemeyi göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="fef6a-136">Bu öğelerin bir öğesi içinde görünmesi gerekir `<metadata>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="fef6a-137">kimlik</span><span class="sxs-lookup"><span data-stu-id="fef6a-137">id</span></span> 
<span data-ttu-id="fef6a-138">Nuget.org genelinde benzersiz olması gereken büyük/küçük harf duyarsız paket tanımlayıcısı veya paketin bulunduğu Galeri.</span><span class="sxs-lookup"><span data-stu-id="fef6a-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="fef6a-139">Kimlikler, URL için geçerli olmayan boşluk veya karakterler içeremez ve genellikle .NET ad alanı kurallarını izler.</span><span class="sxs-lookup"><span data-stu-id="fef6a-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="fef6a-140">Bkz. rehberlik için [benzersiz bir paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="fef6a-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="fef6a-141">Bir paketi nuget.org 'e yüklerken, `id` alan 128 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="fef6a-142">sürüm</span><span class="sxs-lookup"><span data-stu-id="fef6a-142">version</span></span>
<span data-ttu-id="fef6a-143">*Ana. Minor. Patch* deseninin ardından paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="fef6a-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="fef6a-144">Sürüm numaraları, [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions)bölümünde açıklandığı gibi bir ön sürüm son eki içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="fef6a-145">Bir paketi nuget.org 'e yüklerken, `version` alan 64 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="fef6a-146">açıklama</span><span class="sxs-lookup"><span data-stu-id="fef6a-146">description</span></span>
<span data-ttu-id="fef6a-147">UI görüntüleme paketinin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="fef6a-147">A description of the package for UI display.</span></span>

<span data-ttu-id="fef6a-148">Bir paketi nuget.org 'e yüklerken, `description` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="fef6a-149">düzenliyor</span><span class="sxs-lookup"><span data-stu-id="fef6a-149">authors</span></span>
<span data-ttu-id="fef6a-150">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="fef6a-151">Bir paketi nuget.org 'e yüklerken, `authors` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="fef6a-152">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="fef6a-153">lere</span><span class="sxs-lookup"><span data-stu-id="fef6a-153">owners</span></span>
<span data-ttu-id="fef6a-154">Nuget.org üzerindeki profil adlarını kullanan paket oluşturucularının virgülle ayrılmış listesi. Bu, genellikle ile aynı listeyle aynıdır `authors` ve paket NuGet.org 'e yüklenirken yok sayılır. Bkz. [NuGet.org üzerinde paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="fef6a-154">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="fef6a-155">projectUrl</span><span class="sxs-lookup"><span data-stu-id="fef6a-155">projectUrl</span></span>
<span data-ttu-id="fef6a-156">Genellikle kullanıcı arabiriminde gösterildiği gibi, paketin ana sayfası için bir URL de nuget.org görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-156">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="fef6a-157">Bir paketi nuget.org 'e yüklerken, `projectUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-157">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="fef6a-158">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="fef6a-158">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="fef6a-159">licenseUrl kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-159">licenseUrl is deprecated.</span></span> <span data-ttu-id="fef6a-160">Bunun yerine lisans kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-160">Use license instead.</span></span>

<span data-ttu-id="fef6a-161">Genellikle Unuget.org gibi gösterilen paket lisansının URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="fef6a-161">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="fef6a-162">Bir paketi nuget.org 'e yüklerken, `licenseUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-162">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="fef6a-163">lisans</span><span class="sxs-lookup"><span data-stu-id="fef6a-163">license</span></span>

<span data-ttu-id="fef6a-164">***NuGet 4.9.0** ve üzeri sürümlerde desteklenir*</span><span class="sxs-lookup"><span data-stu-id="fef6a-164">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="fef6a-165">Bir SPDX lisans ifadesi veya paket içindeki bir lisans dosyasının yolu, genellikle Usıs nuget.org gibidir. Paketi MıT veya BSD-2 yan tümcesi gibi ortak bir lisans altında lisansladıysanız, ilişkili [Spdx lisans tanımlayıcısını](https://spdx.org/licenses/)kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-165">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="fef6a-166">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-166">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="fef6a-167">NuGet.org yalnızca açık kaynak girişimi veya ücretsiz yazılım temeli tarafından onaylanan lisans ifadelerini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="fef6a-167">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="fef6a-168">Paketinizin birden çok ortak lisans kapsamında lisansı varsa, [Spdx Expression sözdizimi 2,0 sürümünü](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)kullanarak bileşik bir lisans belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-168">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="fef6a-169">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-169">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="fef6a-170">Lisans ifadeleri tarafından desteklenmeyen özel bir lisans kullanıyorsanız, `.txt` Lisans metniyle bir veya dosyasını paketleyebilir `.md` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-170">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="fef6a-171">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-171">For example:</span></span>

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

<span data-ttu-id="fef6a-172">MSBuild eşdeğeri için [Lisans ifadesi veya lisans dosyası paketleme](msbuild-targets.md#packing-a-license-expression-or-a-license-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-172">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="fef6a-173">NuGet 'in lisans ifadelerinin tam sözdizimi aşağıda, [Abnf](https://tools.ietf.org/html/rfc5234)' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-173">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="fef6a-174">Iurl</span><span class="sxs-lookup"><span data-stu-id="fef6a-174">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="fef6a-175">Iurl kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="fef6a-175">iconUrl is deprecated.</span></span> <span data-ttu-id="fef6a-176">Bunun yerine simgesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-176">Use icon instead.</span></span>

<span data-ttu-id="fef6a-177">UI görüntüsündeki paket için simge olarak kullanılacak saydamlık arka planına sahip 128x128 görüntüsünün URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="fef6a-177">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="fef6a-178">Bu öğenin, görüntüyü içeren bir Web sayfasının URL 'sini değil *doğrudan görüntü URL* 'sini içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fef6a-178">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="fef6a-179">Örneğin, GitHub 'dan bir görüntü kullanmak için <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>gibi ham dosya URL 'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-179">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="fef6a-180">Bir paketi nuget.org 'e yüklerken, `iconUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-180">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="fef6a-181">simg</span><span class="sxs-lookup"><span data-stu-id="fef6a-181">icon</span></span>

<span data-ttu-id="fef6a-182">***NuGet 5.3.0** ve üzeri sürümlerde desteklenir*</span><span class="sxs-lookup"><span data-stu-id="fef6a-182">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="fef6a-183">Paket içindeki bir görüntü dosyasının yoludur ve genellikle paket simgesi olarak nuget.org gibi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-183">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="fef6a-184">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-184">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="fef6a-185">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-185">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="fef6a-186">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-186">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="fef6a-187">Örneğin, nuget.exe kullanarak bir paket oluştururken nuspec ' e şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fef6a-187">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="fef6a-188">Paket simgesi nuspec örneği.</span><span class="sxs-lookup"><span data-stu-id="fef6a-188">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="fef6a-189">MSBuild eşdeğeri için, [bir simge görüntüsü dosyası paketleme](msbuild-targets.md#packing-an-icon-image-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-189">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="fef6a-190">`icon` `iconUrl` Desteği olmayan kaynaklarla geriye dönük uyumluluğu sürdürmek için ve ikisini de belirtebilirsiniz `icon` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-190">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="fef6a-191">Visual Studio, `icon` gelecek sürümlerde klasör tabanlı bir kaynaktan gelen paketleri destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-191">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="fef6a-192">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="fef6a-192">requireLicenseAcceptance</span></span>
<span data-ttu-id="fef6a-193">İstemcinin paketi yüklemeden önce, tüketicinin paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fef6a-193">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="fef6a-194">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="fef6a-194">developmentDependency</span></span>
<span data-ttu-id="fef6a-195">*(2.8 +)* Paketin yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten, paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fef6a-195">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="fef6a-196">PackageReference (NuGet 4.8 +) ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-196">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="fef6a-197">[PackageReference için bkz. Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="fef6a-197">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="fef6a-198">Özet</span><span class="sxs-lookup"><span data-stu-id="fef6a-198">summary</span></span>
> [!Important]
> <span data-ttu-id="fef6a-199">`summary` kullanım dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="fef6a-199">`summary` is being deprecated.</span></span> <span data-ttu-id="fef6a-200">Bunun yerine `description` kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-200">Use `description` instead.</span></span>

<span data-ttu-id="fef6a-201">UI görüntülemesi için paketin kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="fef6a-201">A short description of the package for UI display.</span></span> <span data-ttu-id="fef6a-202">Atlanırsa, kesilen bir sürümü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-202">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="fef6a-203">Bir paketi nuget.org 'e yüklerken, `summary` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-203">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="fef6a-204">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="fef6a-204">releaseNotes</span></span>
<span data-ttu-id="fef6a-205">*(1,5 +)* Paketin bu sürümünde yapılan değişikliklerin açıklaması, genellikle, paket açıklaması yerine Visual Studio Paket Yöneticisi 'nin **güncelleştirmeler** sekmesi gibi Kullanıcı arabiriminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-205">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="fef6a-206">Bir paketi nuget.org 'e yüklerken, `releaseNotes` alan 35.000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-206">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="fef6a-207">telif hakkı</span><span class="sxs-lookup"><span data-stu-id="fef6a-207">copyright</span></span>
<span data-ttu-id="fef6a-208">*(1,5 +)* Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="fef6a-208">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="fef6a-209">Bir paketi nuget.org 'e yüklerken, `copyright` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-209">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="fef6a-210">language</span><span class="sxs-lookup"><span data-stu-id="fef6a-210">language</span></span>
<span data-ttu-id="fef6a-211">Paket için yerel ayar KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="fef6a-211">The locale ID for the package.</span></span> <span data-ttu-id="fef6a-212">Bkz. [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="fef6a-212">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="fef6a-213">etiketler</span><span class="sxs-lookup"><span data-stu-id="fef6a-213">tags</span></span>
<span data-ttu-id="fef6a-214">Paketi tanımlayan ve arama ve filtreleme aracılığıyla paketlerin bulunabilirliğini sağlayan, boşlukla ayrılmış etiketlerin ve anahtar kelimelerin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="fef6a-214">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="fef6a-215">Bir paketi nuget.org 'e yüklerken, `tags` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-215">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="fef6a-216">hizmet verebilir</span><span class="sxs-lookup"><span data-stu-id="fef6a-216">serviceable</span></span> 
<span data-ttu-id="fef6a-217">*(3.3 +)* Yalnızca iç NuGet kullanımı için.</span><span class="sxs-lookup"><span data-stu-id="fef6a-217">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="fef6a-218">depo</span><span class="sxs-lookup"><span data-stu-id="fef6a-218">repository</span></span>
<span data-ttu-id="fef6a-219">Dört isteğe bağlı öznitelikten oluşan depo meta verileri: `type` ve `url` *(4.0 +)* ve `branch` ve `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="fef6a-219">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="fef6a-220">Bu öznitelikler, kendisini oluşturan depoya eşlemenize olanak tanır. Bu, `.nupkg` tek bir dal adı olarak daha ayrıntılı bir şekilde ele alınır ve/veya paketi oluşturan SHA-1 karmasını işleyin.</span><span class="sxs-lookup"><span data-stu-id="fef6a-220">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="fef6a-221">Bu, doğrudan bir sürüm denetim yazılımıyla çağrılabilen, genel olarak kullanılabilir bir URL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-221">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="fef6a-222">Bu, bilgisayar için amaçlanmış olduğu için bir HTML sayfası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-222">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="fef6a-223">Proje sayfasına bağlantı için, `projectUrl` bunun yerine alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-223">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="fef6a-224">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-224">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="fef6a-225">Bir paketi nuget.org 'e yüklerken, `type` öznitelik 100 karakterle sınırlıdır ve `url` öznitelik 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-225">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="fef6a-226">başlık</span><span class="sxs-lookup"><span data-stu-id="fef6a-226">title</span></span>
<span data-ttu-id="fef6a-227">Paketin bazı Kullanıcı arabiriminde kullanılabilen, okunabilir bir başlığı.</span><span class="sxs-lookup"><span data-stu-id="fef6a-227">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="fef6a-228">(nuget.org ve Visual Studio 'da Paket Yöneticisi başlık gösterme)</span><span class="sxs-lookup"><span data-stu-id="fef6a-228">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="fef6a-229">Bir paketi nuget.org 'e yüklerken, `title` alan 256 karakterle sınırlıdır, ancak herhangi bir görüntüleme amacıyla kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-229">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="fef6a-230">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-230">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="fef6a-231">packageTypes</span><span class="sxs-lookup"><span data-stu-id="fef6a-231">packageTypes</span></span>
<span data-ttu-id="fef6a-232">*(3,5 +)* `<packageType>` Geleneksel bir bağımlılık paketi dışında paketin türünü belirten sıfır veya daha fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fef6a-232">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="fef6a-233">Her packageType 'ın *ad* ve *Sürüm*öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-233">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="fef6a-234">Bkz. [paket türünü ayarlama](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="fef6a-234">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="fef6a-235">bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="fef6a-235">dependencies</span></span>
<span data-ttu-id="fef6a-236">Paketin bağımlılıklarını belirten sıfır veya daha fazla `<dependency>` öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fef6a-236">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="fef6a-237">Her bağımlılığın *kimliği*, *sürümü*, *içerme* (3. x +) ve *exclude* (3. x +) öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-237">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="fef6a-238">Aşağıdaki [bağımlılıklara](#dependencies-element) bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-238">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="fef6a-239">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="fef6a-239">frameworkAssemblies</span></span>
<span data-ttu-id="fef6a-240">*(1.2 +)* `<frameworkAssembly>` Bu paketin gerektirdiği .NET Framework bütünleştirilmiş kod başvurularını tanımlayan sıfır veya daha fazla öğe koleksiyonu, bu, başvuruların paketi kullanan projelere eklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fef6a-240">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="fef6a-241">Her frameworkAssembly *AssemblyName* ve *TargetFramework* öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-241">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="fef6a-242">Aşağıdaki [Framework derleme BAŞVURULARı GAC 'Yi belirtme](#specifying-framework-assembly-references-gac) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-242">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="fef6a-243">başvurular</span><span class="sxs-lookup"><span data-stu-id="fef6a-243">references</span></span>
<span data-ttu-id="fef6a-244">*(1,5 +)* `<reference>` Paket `lib` klasöründeki, proje başvuruları olarak eklenen derlemeleri adlandırarak sıfır veya daha fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fef6a-244">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="fef6a-245">Her başvurunun bir *Dosya* özniteliği vardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-245">Each reference has a *file* attribute.</span></span> <span data-ttu-id="fef6a-246">`<references>` Ayrıca `<group>` , öğeleri içeren bir *TargetFramework* özniteliği içeren bir öğe içerebilir `<reference>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-246">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="fef6a-247">Atlanırsa, içindeki tüm başvurular `lib` dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-247">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="fef6a-248">Aşağıda [Açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-248">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="fef6a-249">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fef6a-249">contentFiles</span></span>
<span data-ttu-id="fef6a-250">*(3.3 +)* `<files>` Tüketim projesinde içerilecek içerik dosyalarını tanımlayan öğelerin koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="fef6a-250">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="fef6a-251">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-251">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="fef6a-252">Aşağıdaki [pakete dahil edilecek dosyaları belirtme](#specifying-files-to-include-in-the-package) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-252">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="fef6a-253">files</span><span class="sxs-lookup"><span data-stu-id="fef6a-253">files</span></span> 
<span data-ttu-id="fef6a-254">`<package>`Düğüm, `<files>` `<metadata>` `<contentFiles>` `<metadata>` pakete dahil edilecek derleme ve içerik dosyalarını belirtmek için eşdüzey öğesi olarak bir düğüm ve altında bir alt öğe içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-254">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="fef6a-255">Ayrıntılar için bu konunun ilerleyen kısımlarında [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files) dahil etme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-255">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="fef6a-256">meta veri öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-256">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="fef6a-257">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="fef6a-257">minClientVersion</span></span>
<span data-ttu-id="fef6a-258">Bu paketi yükleyecan nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan NuGet istemcisinin en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-258">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="fef6a-259">Bu, paket, `.nuspec` NuGet istemcisinin belirli bir sürümünde eklenmiş olan dosyanın belirli özelliklerine bağlı olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-259">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="fef6a-260">Örneğin, özniteliğini kullanan bir paket `developmentDependency` için "2,8" belirtmelidir `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-260">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="fef6a-261">Benzer şekilde, öğesini kullanan bir paket `contentFiles` (sonraki bölüme bakın) `minClientVersion` "3,3" olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-261">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="fef6a-262">Ayrıca, 2,5 ' den önceki NuGet istemcileri bu bayrağı tanımadığı için, *her zaman* ne içermesi gerektiğine bakılmaksızın paketi yüklemeyi reddeder `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-262">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="fef6a-263">Değiştirme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-263">Replacement tokens</span></span>

<span data-ttu-id="fef6a-264">Bir paket oluştururken, [ `nuget pack` komut](../reference/cli-reference/cli-ref-pack.md) dosyanın düğümündeki $-Delimited belirteçlerini `.nuspec` `<metadata>` bir proje dosyasından veya `pack` komutun `-properties` anahtarından değiştirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-264">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="fef6a-265">Komut satırında belirteç değerlerini ile belirtirsiniz `nuget pack -properties <name>=<value>;<name>=<value>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-265">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="fef6a-266">Örneğin, ve içinde gibi bir belirteç kullanabilir `$owners$` `$desc$` `.nuspec` ve değerlerini paketleme zamanında aşağıdaki şekilde sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef6a-266">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="fef6a-267">Bir projeden değerleri kullanmak için, aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo, dosyanın `Properties` `AssemblyInfo.cs` veya gibi `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="fef6a-267">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="fef6a-268">Bu belirteçleri kullanmak için, `nuget pack` yalnızca yerine proje dosyası ile çalıştırın `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-268">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="fef6a-269">Örneğin, aşağıdaki komutu kullanırken, `$id$` `$version$` bir dosyadaki ve belirteçleri `.nuspec` Proje `AssemblyName` ve `AssemblyVersion` değerleriyle değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-269">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="fef6a-270">Genellikle, bir projeniz olduğunda, `.nuspec` `nuget spec MyProject.csproj` Bu standart belirteçlerden bazılarını otomatik olarak içeren ilk kullanımı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-270">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="fef6a-271">Ancak, bir proje gerekli öğeler için değerler eksikse `.nuspec` , `nuget pack` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fef6a-271">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="fef6a-272">Ayrıca, proje değerlerini değiştirirseniz, paketi oluşturmadan önce yeniden oluşturmayı unutmayın; Bu, paket komutunun anahtarıyla kolayca yapılabilir `build` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-272">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="fef6a-273">Özel durumu ile `$configuration$` , projedeki değerler, komut satırında aynı belirtece atanmış herhangi bir tercih halinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-273">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="fef6a-274">Belirteç</span><span class="sxs-lookup"><span data-stu-id="fef6a-274">Token</span></span> | <span data-ttu-id="fef6a-275">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="fef6a-275">Value source</span></span> | <span data-ttu-id="fef6a-276">Değer</span><span class="sxs-lookup"><span data-stu-id="fef6a-276">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="fef6a-277">**$id $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-277">**$id$**</span></span> | <span data-ttu-id="fef6a-278">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="fef6a-278">Project file</span></span> | <span data-ttu-id="fef6a-279">Proje dosyasından AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="fef6a-279">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="fef6a-280">**$version $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-280">**$version$**</span></span> | <span data-ttu-id="fef6a-281">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fef6a-281">AssemblyInfo</span></span> | <span data-ttu-id="fef6a-282">Varsa Assemblyformationalversion, yoksa AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="fef6a-282">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="fef6a-283">**$author $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-283">**$author$**</span></span> | <span data-ttu-id="fef6a-284">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fef6a-284">AssemblyInfo</span></span> | <span data-ttu-id="fef6a-285">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="fef6a-285">AssemblyCompany</span></span> |
| <span data-ttu-id="fef6a-286">**$title $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-286">**$title$**</span></span> | <span data-ttu-id="fef6a-287">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fef6a-287">AssemblyInfo</span></span> | <span data-ttu-id="fef6a-288">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="fef6a-288">AssemblyTitle</span></span> |
| <span data-ttu-id="fef6a-289">**$description $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-289">**$description$**</span></span> | <span data-ttu-id="fef6a-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fef6a-290">AssemblyInfo</span></span> | <span data-ttu-id="fef6a-291">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="fef6a-291">AssemblyDescription</span></span> |
| <span data-ttu-id="fef6a-292">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-292">**$copyright$**</span></span> | <span data-ttu-id="fef6a-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="fef6a-293">AssemblyInfo</span></span> | <span data-ttu-id="fef6a-294">Assemblytelif hakkı</span><span class="sxs-lookup"><span data-stu-id="fef6a-294">AssemblyCopyright</span></span> |
| <span data-ttu-id="fef6a-295">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="fef6a-295">**$configuration$**</span></span> | <span data-ttu-id="fef6a-296">Derleme DLL 'SI</span><span class="sxs-lookup"><span data-stu-id="fef6a-296">Assembly DLL</span></span> | <span data-ttu-id="fef6a-297">Derlemeyi oluşturmak için kullanılan yapılandırma, hata ayıklamayı varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="fef6a-297">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="fef6a-298">Yayın yapılandırması kullanarak bir paket oluşturmak için her zaman komut satırında ' ı kullanın `-properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-298">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="fef6a-299">Belirteçler, [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files)dahil ettiğinizde yolları çözümlemek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-299">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="fef6a-300">Belirteçler, MSBuild özellikleriyle aynı adlara sahiptir ve geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyaları seçmenizi mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-300">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="fef6a-301">Örneğin, dosyasında aşağıdaki belirteçleri kullanıyorsanız `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="fef6a-301">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="fef6a-302">Ve `AssemblyName` `LoggingLibrary` MSBuild 'de yapılandırma ile olan bir derleme oluşturduğunuzda `Release` , `.nuspec` paketteki dosyadaki sonuç çizgileri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-302">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="fef6a-303">Dependencies öğesi</span><span class="sxs-lookup"><span data-stu-id="fef6a-303">Dependencies element</span></span>

<span data-ttu-id="fef6a-304">`<dependencies>`İçindeki öğesi, `<metadata>` `<dependency>` üst düzey paketin bağımlı olduğu diğer paketleri tanımlayan herhangi bir sayıda öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-304">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="fef6a-305">Her biri için öznitelikleri `<dependency>` aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-305">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="fef6a-306">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="fef6a-306">Attribute</span></span> | <span data-ttu-id="fef6a-307">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fef6a-307">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="fef6a-308">Istenir "EntityFramework" ve "NUnit" gibi bağımlılığın paket KIMLIĞI, nuget.org paketinin adı bir paket sayfasında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-308">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="fef6a-309">Istenir Bağımlılık olarak kabul edilebilir sürüm aralığı.</span><span class="sxs-lookup"><span data-stu-id="fef6a-309">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="fef6a-310">Tam sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-310">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="fef6a-311">Kayan sürümler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="fef6a-311">Floating versions are not supported.</span></span> |
| <span data-ttu-id="fef6a-312">include</span><span class="sxs-lookup"><span data-stu-id="fef6a-312">include</span></span> | <span data-ttu-id="fef6a-313">Son pakete dahil edilecek bağımlılığı belirten, etiketleri ekle/çıkar (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="fef6a-313">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="fef6a-314">Varsayılan değer: `all`.</span><span class="sxs-lookup"><span data-stu-id="fef6a-314">The default value is `all`.</span></span> |
| <span data-ttu-id="fef6a-315">dışlama</span><span class="sxs-lookup"><span data-stu-id="fef6a-315">exclude</span></span> | <span data-ttu-id="fef6a-316">Son pakette hariç tutulacak bağımlılığı belirten, etiketleri dahil et/hariç tut (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="fef6a-316">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="fef6a-317">Varsayılan değer, `build,analyzers` üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-317">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="fef6a-318">Ancak `content/ ContentFiles` , üzerine yazılabilir olmayan son pakette da örtük olarak hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="fef6a-318">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="fef6a-319">İle belirtilen Etiketler `exclude` , ile belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir `include` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-319">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="fef6a-320">Örneğin, `include="runtime, compile" exclude="compile"` ile aynıdır `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-320">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="fef6a-321">Bir paketi nuget.org 'e yüklerken, her bağımlılığın `id` özniteliği 128 karakterle sınırlıdır ve `version` öznitelik 256 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-321">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="fef6a-322">Dahil etme/hariç tutma etiketi</span><span class="sxs-lookup"><span data-stu-id="fef6a-322">Include/Exclude tag</span></span> | <span data-ttu-id="fef6a-323">Hedefin etkilenen klasörleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-323">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="fef6a-324">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fef6a-324">contentFiles</span></span> | <span data-ttu-id="fef6a-325">İçerik</span><span class="sxs-lookup"><span data-stu-id="fef6a-325">Content</span></span> |
| <span data-ttu-id="fef6a-326">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="fef6a-326">runtime</span></span> | <span data-ttu-id="fef6a-327">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="fef6a-327">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="fef6a-328">derle</span><span class="sxs-lookup"><span data-stu-id="fef6a-328">compile</span></span> | <span data-ttu-id="fef6a-329">LIB</span><span class="sxs-lookup"><span data-stu-id="fef6a-329">lib</span></span> |
| <span data-ttu-id="fef6a-330">derleme</span><span class="sxs-lookup"><span data-stu-id="fef6a-330">build</span></span> | <span data-ttu-id="fef6a-331">Build (MSBuild props ve targets)</span><span class="sxs-lookup"><span data-stu-id="fef6a-331">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="fef6a-332">yerel</span><span class="sxs-lookup"><span data-stu-id="fef6a-332">native</span></span> | <span data-ttu-id="fef6a-333">yerel</span><span class="sxs-lookup"><span data-stu-id="fef6a-333">native</span></span> |
| <span data-ttu-id="fef6a-334">yok</span><span class="sxs-lookup"><span data-stu-id="fef6a-334">none</span></span> | <span data-ttu-id="fef6a-335">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="fef6a-335">No folders</span></span> |
| <span data-ttu-id="fef6a-336">tümü</span><span class="sxs-lookup"><span data-stu-id="fef6a-336">all</span></span> | <span data-ttu-id="fef6a-337">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="fef6a-337">All folders</span></span> |

<span data-ttu-id="fef6a-338">Örneğin, aşağıdaki satırlar `PackageA` Sürüm 1.1.0 veya üzeri ve `PackageB` Sürüm 1. x bağımlılıklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-338">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="fef6a-339">Aşağıdaki satırlar aynı paketlere yönelik bağımlılıkları gösterir, ancak ve klasörlerinin yanı sıra, ve `contentFiles` `build` `PackageA` `native` `compile` klasörlerinin `PackageB` da dahil edileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-339">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="fef6a-340">`.nuspec`Kullanarak bir projeden oluştururken `nuget spec` , bu projede var olan bağımlılıklar elde edilen dosyaya otomatik olarak eklenmez `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-340">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="fef6a-341">Bunun yerine `nuget pack myproject.csproj` , öğesini kullanın ve oluşturulan *. nupkg* dosyasının içinden *. nuspec* dosyasını alın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-341">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="fef6a-342">Bu *. nuspec* , bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-342">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="fef6a-343">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="fef6a-343">Dependency groups</span></span>

<span data-ttu-id="fef6a-344">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="fef6a-344">*Version 2.0+*</span></span>

<span data-ttu-id="fef6a-345">Tek bir düz listeye alternatif olarak, bağımlılıklar içindeki öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir `<group>` `<dependencies>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-345">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="fef6a-346">Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<dependency>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-346">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="fef6a-347">Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-347">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="fef6a-348">`<group>`Özniteliği olmayan öğe, `targetFramework` bağımlılıkların varsayılan veya geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-348">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="fef6a-349">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="fef6a-349">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="fef6a-350">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-350">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="fef6a-351">Klasöründe kullanılan [hedef çerçeve bilinen adı (tfd)](../reference/target-frameworks.md) biçimi, `lib/ref` ' de kullanılan tfd ile karşılaştırıldığında farklıdır `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-351">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="fef6a-352">İçinde belirtilen hedef çerçeveler `dependencies group` ve `lib/ref` dosya klasöründe tam eşleşmeler yoksa, `.nuspec` `pack` komut [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md)öğesini yükseltir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-352">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="fef6a-353">Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :</span><span class="sxs-lookup"><span data-stu-id="fef6a-353">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="fef6a-354">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="fef6a-354">Explicit assembly references</span></span>

<span data-ttu-id="fef6a-355">`<references>`Öğesi, `packages.config` paket kullanılırken hedef projenin başvurması gereken derlemeleri açıkça belirtmek için kullanan projeler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-355">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="fef6a-356">Açık başvurular genellikle yalnızca tasarım zamanı derlemeler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-356">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="fef6a-357">Daha fazla bilgi için bkz. [projeler tarafından başvurulan derlemeleri seçme](../create-packages/select-assemblies-referenced-by-projects.md) hakkında daha fazla bilgi için bu sayfaya bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-357">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="fef6a-358">Örneğin, aşağıdaki öğe, `<references>` NuGet 'e yalnızca başvuru eklemesi için, `xunit.dll` `xunit.extensions.dll` pakette ek derlemeler olsa bile:</span><span class="sxs-lookup"><span data-stu-id="fef6a-358">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="fef6a-359">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="fef6a-359">Reference groups</span></span>

<span data-ttu-id="fef6a-360">Tek bir düz listeye alternatif olarak, başvurular, içindeki öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir `<group>` `<references>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-360">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="fef6a-361">Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<reference>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-361">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="fef6a-362">Hedef çerçeve projenin çerçeve profiliyle uyumluysa, bu başvurular bir projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-362">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="fef6a-363">`<group>`Özniteliği olmayan öğe, `targetFramework` başvuru varsayılan veya geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-363">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="fef6a-364">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="fef6a-364">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="fef6a-365">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="fef6a-365">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="fef6a-366">Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :</span><span class="sxs-lookup"><span data-stu-id="fef6a-366">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="fef6a-367">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="fef6a-367">Framework assembly references</span></span>

<span data-ttu-id="fef6a-368">Framework derlemeleri, .NET Framework 'ün bir parçası olan ve belirli bir makine için genel derleme önbelleğinde (GAC) olması gereken olanlardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-368">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="fef6a-369">`<frameworkAssemblies>`Bir paket, öğesi içindeki bu derlemeleri tanımlayarak, gerekli başvuruların projenin bu tür başvurularına sahip olmadığı olayda bir projeye eklendiğinden emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-369">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="fef6a-370">Kuşkusuz bu tür derlemeler doğrudan bir pakete dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="fef6a-370">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="fef6a-371">`<frameworkAssemblies>`Öğesi `<frameworkAssembly>` , her biri aşağıdaki öznitelikleri belirten sıfır veya daha fazla öğe içeriyor:</span><span class="sxs-lookup"><span data-stu-id="fef6a-371">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="fef6a-372">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="fef6a-372">Attribute</span></span> | <span data-ttu-id="fef6a-373">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fef6a-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fef6a-374">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="fef6a-374">**assemblyName**</span></span> | <span data-ttu-id="fef6a-375">Istenir Tam nitelikli derleme adı.</span><span class="sxs-lookup"><span data-stu-id="fef6a-375">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="fef6a-376">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="fef6a-376">**targetFramework**</span></span> | <span data-ttu-id="fef6a-377">Seçim Bu başvurunun uygulandığı hedef çerçeveyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-377">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="fef6a-378">Atlanırsa, başvurunun tüm çerçeveler için geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-378">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="fef6a-379">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="fef6a-379">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="fef6a-380">Aşağıdaki örnekte `System.Net` , tüm hedef çerçeveler için bir başvuru ve `System.ServiceModel` yalnızca .NET Framework 4,0 için bir başvuru gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-380">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="fef6a-381">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="fef6a-381">Including assembly files</span></span>

<span data-ttu-id="fef6a-382">[Paket oluşturma](../create-packages/creating-a-package.md)bölümünde açıklanan kuralları izlerseniz, dosyadaki dosyaların listesini açıkça belirtmeniz gerekmez `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-382">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="fef6a-383">`nuget pack`Komut, gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="fef6a-383">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="fef6a-384">Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'Lerine derleme başvuruları *ekler, çünkü bu,* `.resources.dll` yerelleştirilmiş uydu derlemeleri oldukları varsayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-384">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="fef6a-385">Bu nedenle, `.resources.dll` başka bir şekilde temel paket kodu içeren dosyalar için kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="fef6a-385">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="fef6a-386">Bu otomatik davranışı atlamak ve bir pakete hangi dosyaların ekleneceğini açıkça denetlemek için, bir `<files>` öğeyi bir alt öğesi `<package>` (ve eşdüzey) olarak yerleştirin ve `<metadata>` her bir dosyayı ayrı bir `<file>` öğeyle tanımlayarak.</span><span class="sxs-lookup"><span data-stu-id="fef6a-386">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="fef6a-387">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-387">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="fef6a-388">NuGet 2. x ve öncesiyle ve kullanan projelerde, `packages.config` `<files>` bir paket yüklendiğinde değişmez içerik dosyalarını dahil etmek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-388">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="fef6a-389">NuGet 3.3 + ve projeleri PackageReference ile, `<contentFiles>` bunun yerine öğesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-389">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="fef6a-390">Ayrıntılar için aşağıdaki [içerik dosyalarını ekleme](#including-content-files) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-390">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="fef6a-391">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="fef6a-391">File element attributes</span></span>

<span data-ttu-id="fef6a-392">Her `<file>` öğe aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-392">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="fef6a-393">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="fef6a-393">Attribute</span></span> | <span data-ttu-id="fef6a-394">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fef6a-394">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fef6a-395">**src**</span><span class="sxs-lookup"><span data-stu-id="fef6a-395">**src**</span></span> | <span data-ttu-id="fef6a-396">Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu `exclude` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-396">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="fef6a-397">`.nuspec`Mutlak bir yol belirtilmediği takdirde yol dosyayla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-397">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="fef6a-398">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-398">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fef6a-399">**hedef**</span><span class="sxs-lookup"><span data-stu-id="fef6a-399">**target**</span></span> | <span data-ttu-id="fef6a-400">Kaynak dosyaların yerleştirildiği,,, veya ile başlaması gereken paket içindeki klasörün göreli yolu `lib` `content` `build` `tools` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-400">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="fef6a-401">Bkz. [kural tabanlı çalışma dizininden. nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="fef6a-401">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="fef6a-402">**dışlama**</span><span class="sxs-lookup"><span data-stu-id="fef6a-402">**exclude**</span></span> | <span data-ttu-id="fef6a-403">Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi `src` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="fef6a-404">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="fef6a-405">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fef6a-405">Examples</span></span>

<span data-ttu-id="fef6a-406">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="fef6a-406">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="fef6a-407">**Hedef çerçeveye özgü tek bütünleştirilmiş kod**</span><span class="sxs-lookup"><span data-stu-id="fef6a-407">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="fef6a-408">**Joker karakter kullanan DLL 'Ler kümesi**</span><span class="sxs-lookup"><span data-stu-id="fef6a-408">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="fef6a-409">**Farklı çerçeveler için dll 'Ler**</span><span class="sxs-lookup"><span data-stu-id="fef6a-409">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="fef6a-410">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="fef6a-410">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="fef6a-411">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="fef6a-411">Including content files</span></span>

<span data-ttu-id="fef6a-412">İçerik dosyaları, bir paketin bir projeye eklemesi gereken sabit dosyalardır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-412">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="fef6a-413">Sabit olması, tüketim projesi tarafından değiştirilmeleri amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-413">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="fef6a-414">Örnek içerik dosyaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fef6a-414">Example content files include:</span></span>

- <span data-ttu-id="fef6a-415">Kaynak olarak gömülü görüntüler</span><span class="sxs-lookup"><span data-stu-id="fef6a-415">Images that are embedded as resources</span></span>
- <span data-ttu-id="fef6a-416">Zaten derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="fef6a-416">Source files that are already compiled</span></span>
- <span data-ttu-id="fef6a-417">Projenin derleme çıktısına dahil olması gereken betikler</span><span class="sxs-lookup"><span data-stu-id="fef6a-417">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="fef6a-418">Projeye dahil olması gereken ancak projeye özgü değişikliklere gerek gerektirmeyen paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="fef6a-418">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="fef6a-419">İçerik dosyaları, `<files>` özniteliğinde klasörü belirtilerek öğesini kullanarak bir pakete dahil edilir `content` `target` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-419">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="fef6a-420">Ancak, bu tür dosyalar, bir paket bir projeye yüklendiğinde, bunun yerine öğesini kullanarak yok sayılır `<contentFiles>` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-420">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="fef6a-421">Tüketen projelerle maksimum uyumluluk için, her iki öğe içinde içerik dosyalarını ideal bir paket belirler.</span><span class="sxs-lookup"><span data-stu-id="fef6a-421">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="fef6a-422">İçerik dosyaları için Files öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="fef6a-422">Using the files element for content files</span></span>

<span data-ttu-id="fef6a-423">İçerik dosyaları için yalnızca derleme dosyaları için aynı biçimi kullanın, ancak `content` `target` Aşağıdaki örneklerde gösterildiği gibi özniteliğinde temel klasör olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="fef6a-423">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="fef6a-424">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="fef6a-424">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="fef6a-425">**Dizin yapısıyla içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="fef6a-425">**Content files with directory structure**</span></span>

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

<span data-ttu-id="fef6a-426">**Hedef çerçeveye özgü içerik dosyası**</span><span class="sxs-lookup"><span data-stu-id="fef6a-426">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="fef6a-427">**İçerik dosyası ada sahip bir klasöre kopyalanmış**</span><span class="sxs-lookup"><span data-stu-id="fef6a-427">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="fef6a-428">Bu durumda, ' deki uzantının içindeki `target` uzantıyla eşleşmediği `src` ve bu nedenle adın bu bölümünü `target` bir klasör olarak değerlendirmiş olduğunu görür:</span><span class="sxs-lookup"><span data-stu-id="fef6a-428">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="fef6a-429">**Uzantısız içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="fef6a-429">**Content files without extensions**</span></span>

<span data-ttu-id="fef6a-430">Uzantısı olmayan dosyaları dahil etmek için, `*` veya `**` joker karakterleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="fef6a-430">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="fef6a-431">**Derin yolu ve derin hedefi olan içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="fef6a-431">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="fef6a-432">Bu durumda, kaynak ve hedef için dosya uzantıları eşleştiğinden, NuGet hedefin bir klasör değil bir dosya adı olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="fef6a-432">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="fef6a-433">**Paketteki bir içerik dosyasını yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="fef6a-433">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="fef6a-434">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="fef6a-434">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="fef6a-435">İçerik dosyaları için contentFiles öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="fef6a-435">Using the contentFiles element for content files</span></span>

<span data-ttu-id="fef6a-436">*PackageReference ile NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="fef6a-436">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="fef6a-437">Varsayılan olarak, bir paket içeriği bir klasöre koyar `contentFiles` (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-437">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="fef6a-438">Bu durumda, ' a bir düğüm eklemek gerekli değildir `contentFiles` `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-438">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="fef6a-439">Hangi dosyaların ekleneceğini denetlemek için, öğesi, `<contentFiles>` `<files>` tam dosyaları içeren öğelerin bir koleksiyonu olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="fef6a-439">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="fef6a-440">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-440">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="fef6a-441">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="fef6a-441">Attribute</span></span> | <span data-ttu-id="fef6a-442">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fef6a-442">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fef6a-443">**içeriyor**</span><span class="sxs-lookup"><span data-stu-id="fef6a-443">**include**</span></span> | <span data-ttu-id="fef6a-444">Istenir Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu `exclude` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-444">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="fef6a-445">`contentFiles`Mutlak bir yol belirtilmediği takdirde yol klasöre göre değişir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-445">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="fef6a-446">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-446">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fef6a-447">**dışlama**</span><span class="sxs-lookup"><span data-stu-id="fef6a-447">**exclude**</span></span> | <span data-ttu-id="fef6a-448">Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi `src` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-448">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="fef6a-449">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-449">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="fef6a-450">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="fef6a-450">**buildAction**</span></span> | <span data-ttu-id="fef6a-451">,,, `Content` `None` `Embedded Resource` Vb. gibi MSBuild için içerik öğesine atanacak yapı eylemi `Compile` . Varsayılan değer `Compile` .</span><span class="sxs-lookup"><span data-stu-id="fef6a-451">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="fef6a-452">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="fef6a-452">**copyToOutput**</span></span> | <span data-ttu-id="fef6a-453">İçerik öğelerinin derleme (veya yayımlama) çıkış klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fef6a-453">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="fef6a-454">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="fef6a-454">The default is false.</span></span> |
| <span data-ttu-id="fef6a-455">**leştirebilir**</span><span class="sxs-lookup"><span data-stu-id="fef6a-455">**flatten**</span></span> | <span data-ttu-id="fef6a-456">İçerik öğelerinin derleme çıkışında tek bir klasöre mi kopyalanacağını (true) veya paketteki klasör yapısını korumayı (false) gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fef6a-456">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="fef6a-457">Bu bayrak yalnızca copyToOutput bayrağı true olarak ayarlandığında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-457">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="fef6a-458">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="fef6a-458">The default is false.</span></span> |

<span data-ttu-id="fef6a-459">Bir paket yüklenirken NuGet, alt öğelerini `<contentFiles>` yukarıdan aşağıya uygular.</span><span class="sxs-lookup"><span data-stu-id="fef6a-459">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="fef6a-460">Aynı dosyayla birden çok giriş eşleşiyorsa, tüm girişler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-460">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="fef6a-461">Aynı öznitelik için bir çakışma varsa en üstteki girdi alt girişleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="fef6a-461">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="fef6a-462">Paket klasörü yapısı</span><span class="sxs-lookup"><span data-stu-id="fef6a-462">Package folder structure</span></span>

<span data-ttu-id="fef6a-463">Paket projesi, aşağıdaki kalıbı kullanarak içerik yapısını almalıdır:</span><span class="sxs-lookup"><span data-stu-id="fef6a-463">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="fef6a-464">`codeLanguages` ,, `cs` , `vb` `fs` `any` veya belirli bir `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="fef6a-464">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="fef6a-465">`TxM` NuGet tarafından desteklenen geçerli bir hedef çerçeve adıdır (bkz. [hedef çerçeveler](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="fef6a-465">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="fef6a-466">Bu söz dizimi sonuna herhangi bir klasör yapısı eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-466">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="fef6a-467">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fef6a-467">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="fef6a-468">Boş klasörler `.` , belirli dil birleşimleri ve TxM için içerik sağlamayı devre dışı bırakmak için kullanılabilir. Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fef6a-468">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="fef6a-469">Örnek contentFiles bölümü</span><span class="sxs-lookup"><span data-stu-id="fef6a-469">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="fef6a-470">Framework başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="fef6a-470">Framework reference groups</span></span>

<span data-ttu-id="fef6a-471">*Sürüm 5.1 + wih PackageReference*</span><span class="sxs-lookup"><span data-stu-id="fef6a-471">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="fef6a-472">Framework başvuruları, WPF veya Windows Forms gibi paylaşılan çerçeveleri temsil eden bir .NET Core kavramıdır.</span><span class="sxs-lookup"><span data-stu-id="fef6a-472">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="fef6a-473">Paket, paylaşılan bir çerçeve belirterek, tüm çerçeve bağımlılıklarının başvuru projesine dahil edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fef6a-473">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="fef6a-474">Her `<group>` öğe için bir `targetFramework` öznitelik ve sıfır veya daha fazla `<frameworkReference>` öğe gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-474">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="fef6a-475">Aşağıdaki örnek, bir .NET Core WPF projesi için oluşturulan bir nuspec gösterir.</span><span class="sxs-lookup"><span data-stu-id="fef6a-475">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="fef6a-476">Çerçeve başvurularını içeren nusö 'lerin birlikte yazılması önerilmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fef6a-476">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="fef6a-477">Bunun yerine, bunları projeden otomatik olarak çıkarmayacak olan [hedefler](msbuild-targets.md) paketini kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="fef6a-477">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="fef6a-478">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="fef6a-478">Example nuspec files</span></span>

<span data-ttu-id="fef6a-479">**`.nuspec`Bağımlılıklar veya dosyalar belirtmeyen bir basit**</span><span class="sxs-lookup"><span data-stu-id="fef6a-479">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="fef6a-480">**`.nuspec`Bağımlılıkları olan A**</span><span class="sxs-lookup"><span data-stu-id="fef6a-480">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="fef6a-481">**`.nuspec`Dosyalarla birlikte**</span><span class="sxs-lookup"><span data-stu-id="fef6a-481">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="fef6a-482">**Bir `.nuspec` Framework Derlemeleriyle**</span><span class="sxs-lookup"><span data-stu-id="fef6a-482">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="fef6a-483">Bu örnekte, belirli proje hedefleri için aşağıdakiler yüklenir:</span><span class="sxs-lookup"><span data-stu-id="fef6a-483">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="fef6a-484">. NET4-> `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="fef6a-484">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="fef6a-485">. NET4 Istemci profili-> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="fef6a-485">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="fef6a-486">Silverlight 3-> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="fef6a-486">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="fef6a-487">WindowsPhone-> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="fef6a-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
