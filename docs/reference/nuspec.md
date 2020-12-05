---
title: NuGet için. nuspec dosya başvurusu
description: . Nuspec dosyası, bir paket oluştururken ve paket tüketicilere bilgi sağlamak için kullanılan paket meta verilerini içerir.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6e5107ac05046ea46cc819ebe2a504ba6b030634
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738948"
---
# <a name="nuspec-reference"></a><span data-ttu-id="b7d8f-103">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="b7d8f-103">.nuspec reference</span></span>

<span data-ttu-id="b7d8f-104">`.nuspec`Dosya, paket meta verilerini içeren BIR XML bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="b7d8f-105">Bu bildirim her ikisi de paketini derlemek ve tüketicilere bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="b7d8f-106">Bildirim her zaman bir pakete dahildir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="b7d8f-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-107">In this topic:</span></span>

- [<span data-ttu-id="b7d8f-108">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="b7d8f-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="b7d8f-109">[Değiştirme belirteçleri](#replacement-tokens) (bir Visual Studio projesiyle kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="b7d8f-110">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="b7d8f-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="b7d8f-111">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="b7d8f-112">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="b7d8f-113">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="b7d8f-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="b7d8f-114">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="b7d8f-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="b7d8f-115">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="b7d8f-116">Proje türü uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="b7d8f-116">Project type compatibility</span></span>

- <span data-ttu-id="b7d8f-117">Kullanan `.nuspec` `nuget.exe pack` SDK olmayan projeler için ile kullanın `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="b7d8f-118">`.nuspec` [SDK stilindeki projelere](../resources/check-project-format.md) yönelik paketler oluşturmak için bir dosya gerekli değildir (genellikle .NET Core ve [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanan .NET Standard projeler).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="b7d8f-119">( `.nuspec` Paketi oluşturduğunuzda bir ' nin oluşturulduğunu unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="b7d8f-120">Veya kullanarak bir paket oluşturuyorsanız `dotnet.exe pack` `msbuild pack target` , bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri dahil](../reference/msbuild-targets.md#pack-target) etmenizi öneririz `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="b7d8f-121">Ancak, bunun yerine [ `.nuspec` `dotnet.exe` `msbuild pack target` veya kullanarak paketbir dosya kullanmayı ](../reference/msbuild-targets.md#packing-using-a-nuspec)seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="b7d8f-122">`packages.config`' Den [packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için, `.nuspec` paketi oluşturmak için bir dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="b7d8f-123">Bunun yerine, [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="b7d8f-124">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="b7d8f-124">General form and schema</span></span>

<span data-ttu-id="b7d8f-125">Geçerli `nuspec.xsd` şema dosyası [NuGet GitHub deposunda](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="b7d8f-126">Bu şema içinde, bir `.nuspec` dosya aşağıdaki genel biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="b7d8f-127">Şemanın net bir görsel temsili için, şema dosyasını Visual Studio 'da tasarım modunda açın ve **XML şema Gezgini** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="b7d8f-128">Alternatif olarak, dosyayı kod olarak açın, düzenleyicide sağ tıklayın ve **XML şeması Gezginini göster**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="b7d8f-129">Aşağıdakilerden biri gibi bir görünüm alacağınız şekilde (çoğunlukla genişletilir):</span><span class="sxs-lookup"><span data-stu-id="b7d8f-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Nuspec. xsd Open ile Visual Studio şema Gezgini](media/SchemaExplorer.png)

<span data-ttu-id="b7d8f-131">. Nuspec dosyasındaki tüm XML öğesi adları büyük/küçük harfe duyarlıdır, çünkü genel olarak XML için bu durumdur.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="b7d8f-132">Örneğin, meta veri öğesinin kullanılması `<description>` doğru ve `<Description>` doğru değildir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="b7d8f-133">Her öğe adı için uygun büyük küçük harf aşağıda belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="b7d8f-134">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-134">Required metadata elements</span></span>

<span data-ttu-id="b7d8f-135">Aşağıdaki öğeler bir paket için en düşük gereksinimlerdir, ancak geliştiricilerin paketinize sahip olduğu genel deneyimi geliştirmek için [isteğe bağlı meta veri öğelerini](#optional-metadata-elements) eklemeyi göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="b7d8f-136">Bu öğelerin bir öğesi içinde görünmesi gerekir `<metadata>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="b7d8f-137">kimlik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-137">id</span></span> 
<span data-ttu-id="b7d8f-138">Nuget.org genelinde benzersiz olması gereken büyük/küçük harf duyarsız paket tanımlayıcısı veya paketin bulunduğu Galeri.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="b7d8f-139">Kimlikler, URL için geçerli olmayan boşluk veya karakterler içeremez ve genellikle .NET ad alanı kurallarını izler.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="b7d8f-140">Bkz. rehberlik için [benzersiz bir paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="b7d8f-141">Bir paketi nuget.org 'e yüklerken, `id` alan 128 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="b7d8f-142">sürüm</span><span class="sxs-lookup"><span data-stu-id="b7d8f-142">version</span></span>
<span data-ttu-id="b7d8f-143">*Ana. Minor. Patch* deseninin ardından paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="b7d8f-144">Sürüm numaraları, [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions)bölümünde açıklandığı gibi bir ön sürüm son eki içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="b7d8f-145">Bir paketi nuget.org 'e yüklerken, `version` alan 64 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="b7d8f-146">açıklama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-146">description</span></span>
<span data-ttu-id="b7d8f-147">UI görüntüleme paketinin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-147">A description of the package for UI display.</span></span>

<span data-ttu-id="b7d8f-148">Bir paketi nuget.org 'e yüklerken, `description` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="b7d8f-149">düzenliyor</span><span class="sxs-lookup"><span data-stu-id="b7d8f-149">authors</span></span>
<span data-ttu-id="b7d8f-150">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="b7d8f-151">Bir paketi nuget.org 'e yüklerken, `authors` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="b7d8f-152">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="b7d8f-153">lere</span><span class="sxs-lookup"><span data-stu-id="b7d8f-153">owners</span></span>
> [!Important]
> <span data-ttu-id="b7d8f-154">sahipler kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-154">owners is deprecated.</span></span> <span data-ttu-id="b7d8f-155">Bunun yerine yazarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-155">Use authors instead.</span></span>

<span data-ttu-id="b7d8f-156">Nuget.org üzerindeki profil adlarını kullanan paket oluşturucularının virgülle ayrılmış listesi. Bu, genellikle ile aynı listeyle aynıdır `authors` ve paket NuGet.org 'e yüklenirken yok sayılır. Bkz. [NuGet.org üzerinde paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="b7d8f-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="b7d8f-157">projectUrl</span></span>
<span data-ttu-id="b7d8f-158">Genellikle kullanıcı arabiriminde gösterildiği gibi, paketin ana sayfası için bir URL de nuget.org görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="b7d8f-159">Bir paketi nuget.org 'e yüklerken, `projectUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="b7d8f-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="b7d8f-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="b7d8f-161">licenseUrl kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="b7d8f-162">Bunun yerine lisans kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-162">Use license instead.</span></span>

<span data-ttu-id="b7d8f-163">Genellikle Unuget.org gibi gösterilen paket lisansının URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="b7d8f-164">Bir paketi nuget.org 'e yüklerken, `licenseUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="b7d8f-165">lisans</span><span class="sxs-lookup"><span data-stu-id="b7d8f-165">license</span></span>

<span data-ttu-id="b7d8f-166">***NuGet 4.9.0** ve üzeri sürümlerde desteklenir*</span><span class="sxs-lookup"><span data-stu-id="b7d8f-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="b7d8f-167">Bir SPDX lisans ifadesi veya paket içindeki bir lisans dosyasının yolu, genellikle Usıs nuget.org gibidir. Paketi MıT veya BSD-2 yan tümcesi gibi ortak bir lisans altında lisansladıysanız, ilişkili [Spdx lisans tanımlayıcısını](https://spdx.org/licenses/)kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="b7d8f-168">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="b7d8f-169">NuGet.org yalnızca açık kaynak girişimi veya ücretsiz yazılım temeli tarafından onaylanan lisans ifadelerini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="b7d8f-170">Paketinizin birden çok ortak lisans kapsamında lisansı varsa, [Spdx Expression sözdizimi 2,0 sürümünü](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)kullanarak bileşik bir lisans belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="b7d8f-171">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="b7d8f-172">Lisans ifadeleri tarafından desteklenmeyen özel bir lisans kullanıyorsanız, `.txt` Lisans metniyle bir veya dosyasını paketleyebilir `.md` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="b7d8f-173">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-173">For example:</span></span>

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

<span data-ttu-id="b7d8f-174">MSBuild eşdeğeri için [Lisans ifadesi veya lisans dosyası paketleme](msbuild-targets.md#packing-a-license-expression-or-a-license-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="b7d8f-175">NuGet 'in lisans ifadelerinin tam sözdizimi aşağıda, [Abnf](https://tools.ietf.org/html/rfc5234)' de açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="b7d8f-176">Iurl</span><span class="sxs-lookup"><span data-stu-id="b7d8f-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="b7d8f-177">Iurl kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-177">iconUrl is deprecated.</span></span> <span data-ttu-id="b7d8f-178">Bunun yerine simgesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-178">Use icon instead.</span></span>

<span data-ttu-id="b7d8f-179">UI görüntüsündeki paket için simge olarak kullanılacak saydamlık arka planına sahip 128x128 görüntüsünün URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="b7d8f-180">Bu öğenin, görüntüyü içeren bir Web sayfasının URL 'sini değil *doğrudan görüntü URL* 'sini içerdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="b7d8f-181">Örneğin, GitHub 'dan bir görüntü kullanmak için <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>gibi ham dosya URL 'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="b7d8f-182">Bir paketi nuget.org 'e yüklerken, `iconUrl` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="b7d8f-183">simg</span><span class="sxs-lookup"><span data-stu-id="b7d8f-183">icon</span></span>

<span data-ttu-id="b7d8f-184">***NuGet 5.3.0** ve üzeri sürümlerde desteklenir*</span><span class="sxs-lookup"><span data-stu-id="b7d8f-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="b7d8f-185">Paket içindeki bir görüntü dosyasının yoludur ve genellikle paket simgesi olarak nuget.org gibi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="b7d8f-186">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="b7d8f-187">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="b7d8f-188">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="b7d8f-189">Örneğin, nuget.exe kullanarak bir paket oluştururken nuspec ' e şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="b7d8f-190">Paket simgesi nuspec örneği.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="b7d8f-191">MSBuild eşdeğeri için, [bir simge görüntüsü dosyası paketleme](msbuild-targets.md#packing-an-icon-image-file)konusuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="b7d8f-192">`icon` `iconUrl` Desteği olmayan kaynaklarla geriye dönük uyumluluğu sürdürmek için ve ikisini de belirtebilirsiniz `icon` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="b7d8f-193">Visual Studio, `icon` gelecek sürümlerde klasör tabanlı bir kaynaktan gelen paketleri destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="b7d8f-194">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="b7d8f-194">requireLicenseAcceptance</span></span>
<span data-ttu-id="b7d8f-195">İstemcinin paketi yüklemeden önce, tüketicinin paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-195">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="b7d8f-196">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="b7d8f-196">developmentDependency</span></span>
<span data-ttu-id="b7d8f-197">*(2.8 +)* Paketin yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten, paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-197">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="b7d8f-198">PackageReference (NuGet 4.8 +) ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-198">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="b7d8f-199">[PackageReference için bkz. Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-199">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="b7d8f-200">Özet</span><span class="sxs-lookup"><span data-stu-id="b7d8f-200">summary</span></span>
> [!Important]
> <span data-ttu-id="b7d8f-201">`summary` kullanım dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-201">`summary` is being deprecated.</span></span> <span data-ttu-id="b7d8f-202">Bunun yerine `description` kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-202">Use `description` instead.</span></span>

<span data-ttu-id="b7d8f-203">UI görüntülemesi için paketin kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-203">A short description of the package for UI display.</span></span> <span data-ttu-id="b7d8f-204">Atlanırsa, kesilen bir sürümü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-204">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="b7d8f-205">Bir paketi nuget.org 'e yüklerken, `summary` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-205">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="b7d8f-206">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-206">releaseNotes</span></span>
<span data-ttu-id="b7d8f-207">*(1,5 +)* Paketin bu sürümünde yapılan değişikliklerin açıklaması, genellikle, paket açıklaması yerine Visual Studio Paket Yöneticisi 'nin **güncelleştirmeler** sekmesi gibi Kullanıcı arabiriminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-207">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="b7d8f-208">Bir paketi nuget.org 'e yüklerken, `releaseNotes` alan 35.000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-208">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="b7d8f-209">telif hakkı</span><span class="sxs-lookup"><span data-stu-id="b7d8f-209">copyright</span></span>
<span data-ttu-id="b7d8f-210">*(1,5 +)* Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-210">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="b7d8f-211">Bir paketi nuget.org 'e yüklerken, `copyright` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-211">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="b7d8f-212">language</span><span class="sxs-lookup"><span data-stu-id="b7d8f-212">language</span></span>
<span data-ttu-id="b7d8f-213">Paket için yerel ayar KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-213">The locale ID for the package.</span></span> <span data-ttu-id="b7d8f-214">Bkz. [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-214">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="b7d8f-215">etiketler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-215">tags</span></span>
<span data-ttu-id="b7d8f-216">Paketi tanımlayan ve arama ve filtreleme aracılığıyla paketlerin bulunabilirliğini sağlayan, boşlukla ayrılmış etiketlerin ve anahtar kelimelerin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-216">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="b7d8f-217">Bir paketi nuget.org 'e yüklerken, `tags` alan 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-217">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="b7d8f-218">hizmet verebilir</span><span class="sxs-lookup"><span data-stu-id="b7d8f-218">serviceable</span></span> 
<span data-ttu-id="b7d8f-219">*(3.3 +)* Yalnızca iç NuGet kullanımı için.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-219">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="b7d8f-220">depo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-220">repository</span></span>
<span data-ttu-id="b7d8f-221">Dört isteğe bağlı öznitelikten oluşan depo meta verileri: `type` ve `url` *(4.0 +)* ve `branch` ve `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-221">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="b7d8f-222">Bu öznitelikler, kendisini oluşturan depoya eşlemenize olanak tanır. Bu, `.nupkg` tek bir dal adı olarak daha ayrıntılı bir şekilde ele alınır ve/veya paketi oluşturan SHA-1 karmasını işleyin.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-222">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="b7d8f-223">Bu, doğrudan bir sürüm denetim yazılımıyla çağrılabilen, genel olarak kullanılabilir bir URL olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-223">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="b7d8f-224">Bu, bilgisayar için amaçlanmış olduğu için bir HTML sayfası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-224">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="b7d8f-225">Proje sayfasına bağlantı için, `projectUrl` bunun yerine alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-225">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="b7d8f-226">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-226">For example:</span></span>
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

<span data-ttu-id="b7d8f-227">Bir paketi nuget.org 'e yüklerken, `type` öznitelik 100 karakterle sınırlıdır ve `url` öznitelik 4000 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-227">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="b7d8f-228">başlık</span><span class="sxs-lookup"><span data-stu-id="b7d8f-228">title</span></span>
<span data-ttu-id="b7d8f-229">Paketin bazı Kullanıcı arabiriminde kullanılabilen, okunabilir bir başlığı.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-229">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="b7d8f-230">(nuget.org ve Visual Studio 'da Paket Yöneticisi başlık gösterme)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-230">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="b7d8f-231">Bir paketi nuget.org 'e yüklerken, `title` alan 256 karakterle sınırlıdır, ancak herhangi bir görüntüleme amacıyla kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-231">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="b7d8f-232">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-232">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="b7d8f-233">packageTypes</span><span class="sxs-lookup"><span data-stu-id="b7d8f-233">packageTypes</span></span>
<span data-ttu-id="b7d8f-234">*(3,5 +)* `<packageType>` Geleneksel bir bağımlılık paketi dışında paketin türünü belirten sıfır veya daha fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-234">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="b7d8f-235">Her packageType 'ın *ad* ve *Sürüm* öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-235">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="b7d8f-236">Bkz. [paket türünü ayarlama](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-236">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="b7d8f-237">bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="b7d8f-237">dependencies</span></span>
<span data-ttu-id="b7d8f-238">Paketin bağımlılıklarını belirten sıfır veya daha fazla `<dependency>` öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-238">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="b7d8f-239">Her bağımlılığın *kimliği*, *sürümü*, *içerme* (3. x +) ve *exclude* (3. x +) öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-239">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="b7d8f-240">Aşağıdaki [bağımlılıklara](#dependencies-element) bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-240">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="b7d8f-241">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="b7d8f-241">frameworkAssemblies</span></span>
<span data-ttu-id="b7d8f-242">*(1.2 +)* `<frameworkAssembly>` Bu paketin gerektirdiği .NET Framework bütünleştirilmiş kod başvurularını tanımlayan sıfır veya daha fazla öğe koleksiyonu, bu, başvuruların paketi kullanan projelere eklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-242">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="b7d8f-243">Her frameworkAssembly *AssemblyName* ve *TargetFramework* öznitelikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-243">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="b7d8f-244">Aşağıdaki [Framework derleme BAŞVURULARı GAC 'Yi belirtme](#specifying-framework-assembly-references-gac) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-244">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="b7d8f-245">başvurular</span><span class="sxs-lookup"><span data-stu-id="b7d8f-245">references</span></span>
<span data-ttu-id="b7d8f-246">*(1,5 +)* `<reference>` Paket `lib` klasöründeki, proje başvuruları olarak eklenen derlemeleri adlandırarak sıfır veya daha fazla öğe koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-246">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="b7d8f-247">Her başvurunun bir *Dosya* özniteliği vardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-247">Each reference has a *file* attribute.</span></span> <span data-ttu-id="b7d8f-248">`<references>` Ayrıca `<group>` , öğeleri içeren bir *TargetFramework* özniteliği içeren bir öğe içerebilir `<reference>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-248">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="b7d8f-249">Atlanırsa, içindeki tüm başvurular `lib` dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-249">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="b7d8f-250">Aşağıda [Açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-250">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="b7d8f-251">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b7d8f-251">contentFiles</span></span>
<span data-ttu-id="b7d8f-252">*(3.3 +)* `<files>` Tüketim projesinde içerilecek içerik dosyalarını tanımlayan öğelerin koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-252">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="b7d8f-253">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-253">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="b7d8f-254">Aşağıdaki [pakete dahil edilecek dosyaları belirtme](#specifying-files-to-include-in-the-package) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-254">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="b7d8f-255">files</span><span class="sxs-lookup"><span data-stu-id="b7d8f-255">files</span></span> 
<span data-ttu-id="b7d8f-256">`<package>`Düğüm, `<files>` `<metadata>` `<contentFiles>` `<metadata>` pakete dahil edilecek derleme ve içerik dosyalarını belirtmek için eşdüzey öğesi olarak bir düğüm ve altında bir alt öğe içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-256">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="b7d8f-257">Ayrıntılar için bu konunun ilerleyen kısımlarında [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files) dahil etme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-257">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="b7d8f-258">meta veri öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-258">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="b7d8f-259">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="b7d8f-259">minClientVersion</span></span>
<span data-ttu-id="b7d8f-260">Bu paketi yükleyecan nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan NuGet istemcisinin en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-260">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="b7d8f-261">Bu, paket, `.nuspec` NuGet istemcisinin belirli bir sürümünde eklenmiş olan dosyanın belirli özelliklerine bağlı olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-261">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="b7d8f-262">Örneğin, özniteliğini kullanan bir paket `developmentDependency` için "2,8" belirtmelidir `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-262">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="b7d8f-263">Benzer şekilde, öğesini kullanan bir paket `contentFiles` (sonraki bölüme bakın) `minClientVersion` "3,3" olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-263">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="b7d8f-264">Ayrıca, 2,5 ' den önceki NuGet istemcileri bu bayrağı tanımadığı için, *her zaman* ne içermesi gerektiğine bakılmaksızın paketi yüklemeyi reddeder `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-264">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="b7d8f-265">Değiştirme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-265">Replacement tokens</span></span>

<span data-ttu-id="b7d8f-266">Bir paket oluştururken, [ `nuget pack` komut](../reference/cli-reference/cli-ref-pack.md) dosyanın düğümündeki $-Delimited belirteçlerini `.nuspec` `<metadata>` bir proje dosyasından veya `pack` komutun `-properties` anahtarından değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-266">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="b7d8f-267">Komut satırında belirteç değerlerini ile belirtirsiniz `nuget pack -properties <name>=<value>;<name>=<value>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-267">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="b7d8f-268">Örneğin, ve içinde gibi bir belirteç kullanabilir `$owners$` `$desc$` `.nuspec` ve değerlerini paketleme zamanında aşağıdaki şekilde sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-268">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="b7d8f-269">Bir projeden değerleri kullanmak için, aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo, dosyanın `Properties` `AssemblyInfo.cs` veya gibi `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-269">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="b7d8f-270">Bu belirteçleri kullanmak için, `nuget pack` yalnızca yerine proje dosyası ile çalıştırın `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-270">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="b7d8f-271">Örneğin, aşağıdaki komutu kullanırken, `$id$` `$version$` bir dosyadaki ve belirteçleri `.nuspec` Proje `AssemblyName` ve `AssemblyVersion` değerleriyle değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-271">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="b7d8f-272">Genellikle, bir projeniz olduğunda, `.nuspec` `nuget spec MyProject.csproj` Bu standart belirteçlerden bazılarını otomatik olarak içeren ilk kullanımı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-272">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="b7d8f-273">Ancak, bir proje gerekli öğeler için değerler eksikse `.nuspec` , `nuget pack` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-273">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="b7d8f-274">Ayrıca, proje değerlerini değiştirirseniz, paketi oluşturmadan önce yeniden oluşturmayı unutmayın; Bu, paket komutunun anahtarıyla kolayca yapılabilir `build` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-274">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="b7d8f-275">Özel durumu ile `$configuration$` , projedeki değerler, komut satırında aynı belirtece atanmış herhangi bir tercih halinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-275">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="b7d8f-276">Belirteç</span><span class="sxs-lookup"><span data-stu-id="b7d8f-276">Token</span></span> | <span data-ttu-id="b7d8f-277">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="b7d8f-277">Value source</span></span> | <span data-ttu-id="b7d8f-278">Değer</span><span class="sxs-lookup"><span data-stu-id="b7d8f-278">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="b7d8f-279">**$id $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-279">**$id$**</span></span> | <span data-ttu-id="b7d8f-280">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="b7d8f-280">Project file</span></span> | <span data-ttu-id="b7d8f-281">Proje dosyasından AssemblyName (title)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-281">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="b7d8f-282">**$version $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-282">**$version$**</span></span> | <span data-ttu-id="b7d8f-283">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-283">AssemblyInfo</span></span> | <span data-ttu-id="b7d8f-284">Varsa Assemblyformationalversion, yoksa AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="b7d8f-284">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="b7d8f-285">**$author $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-285">**$author$**</span></span> | <span data-ttu-id="b7d8f-286">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-286">AssemblyInfo</span></span> | <span data-ttu-id="b7d8f-287">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="b7d8f-287">AssemblyCompany</span></span> |
| <span data-ttu-id="b7d8f-288">**$title $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-288">**$title$**</span></span> | <span data-ttu-id="b7d8f-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-289">AssemblyInfo</span></span> | <span data-ttu-id="b7d8f-290">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="b7d8f-290">AssemblyTitle</span></span> |
| <span data-ttu-id="b7d8f-291">**$description $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-291">**$description$**</span></span> | <span data-ttu-id="b7d8f-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-292">AssemblyInfo</span></span> | <span data-ttu-id="b7d8f-293">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="b7d8f-293">AssemblyDescription</span></span> |
| <span data-ttu-id="b7d8f-294">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-294">**$copyright$**</span></span> | <span data-ttu-id="b7d8f-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b7d8f-295">AssemblyInfo</span></span> | <span data-ttu-id="b7d8f-296">Assemblytelif hakkı</span><span class="sxs-lookup"><span data-stu-id="b7d8f-296">AssemblyCopyright</span></span> |
| <span data-ttu-id="b7d8f-297">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-297">**$configuration$**</span></span> | <span data-ttu-id="b7d8f-298">Derleme DLL 'SI</span><span class="sxs-lookup"><span data-stu-id="b7d8f-298">Assembly DLL</span></span> | <span data-ttu-id="b7d8f-299">Derlemeyi oluşturmak için kullanılan yapılandırma, hata ayıklamayı varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-299">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="b7d8f-300">Yayın yapılandırması kullanarak bir paket oluşturmak için her zaman komut satırında ' ı kullanın `-properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-300">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="b7d8f-301">Belirteçler, [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files)dahil ettiğinizde yolları çözümlemek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-301">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="b7d8f-302">Belirteçler, MSBuild özellikleriyle aynı adlara sahiptir ve geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyaları seçmenizi mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-302">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="b7d8f-303">Örneğin, dosyasında aşağıdaki belirteçleri kullanıyorsanız `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="b7d8f-303">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="b7d8f-304">Ve `AssemblyName` `LoggingLibrary` MSBuild 'de yapılandırma ile olan bir derleme oluşturduğunuzda `Release` , `.nuspec` paketteki dosyadaki sonuç çizgileri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-304">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="b7d8f-305">Dependencies öğesi</span><span class="sxs-lookup"><span data-stu-id="b7d8f-305">Dependencies element</span></span>

<span data-ttu-id="b7d8f-306">`<dependencies>`İçindeki öğesi, `<metadata>` `<dependency>` üst düzey paketin bağımlı olduğu diğer paketleri tanımlayan herhangi bir sayıda öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-306">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="b7d8f-307">Her biri için öznitelikleri `<dependency>` aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-307">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="b7d8f-308">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-308">Attribute</span></span> | <span data-ttu-id="b7d8f-309">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-309">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="b7d8f-310">Istenir "EntityFramework" ve "NUnit" gibi bağımlılığın paket KIMLIĞI, nuget.org paketinin adı bir paket sayfasında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-310">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="b7d8f-311">Istenir Bağımlılık olarak kabul edilebilir sürüm aralığı.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-311">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="b7d8f-312">Tam sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-312">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="b7d8f-313">Kayan sürümler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-313">Floating versions are not supported.</span></span> |
| <span data-ttu-id="b7d8f-314">include</span><span class="sxs-lookup"><span data-stu-id="b7d8f-314">include</span></span> | <span data-ttu-id="b7d8f-315">Son pakete dahil edilecek bağımlılığı belirten, etiketleri ekle/çıkar (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-315">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="b7d8f-316">`all` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-316">The default value is `all`.</span></span> |
| <span data-ttu-id="b7d8f-317">dışlama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-317">exclude</span></span> | <span data-ttu-id="b7d8f-318">Son pakette hariç tutulacak bağımlılığı belirten, etiketleri dahil et/hariç tut (aşağıya bakın) listesi.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-318">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="b7d8f-319">Varsayılan değer, `build,analyzers` üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-319">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="b7d8f-320">Ancak `content/ ContentFiles` , üzerine yazılabilir olmayan son pakette da örtük olarak hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-320">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="b7d8f-321">İle belirtilen Etiketler `exclude` , ile belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir `include` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-321">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="b7d8f-322">Örneğin, `include="runtime, compile" exclude="compile"` ile aynıdır `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-322">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="b7d8f-323">Bir paketi nuget.org 'e yüklerken, her bağımlılığın `id` özniteliği 128 karakterle sınırlıdır ve `version` öznitelik 256 karakterle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-323">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="b7d8f-324">Dahil etme/hariç tutma etiketi</span><span class="sxs-lookup"><span data-stu-id="b7d8f-324">Include/Exclude tag</span></span> | <span data-ttu-id="b7d8f-325">Hedefin etkilenen klasörleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-325">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="b7d8f-326">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b7d8f-326">contentFiles</span></span> | <span data-ttu-id="b7d8f-327">İçerik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-327">Content</span></span> |
| <span data-ttu-id="b7d8f-328">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="b7d8f-328">runtime</span></span> | <span data-ttu-id="b7d8f-329">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="b7d8f-329">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="b7d8f-330">derle</span><span class="sxs-lookup"><span data-stu-id="b7d8f-330">compile</span></span> | <span data-ttu-id="b7d8f-331">LIB</span><span class="sxs-lookup"><span data-stu-id="b7d8f-331">lib</span></span> |
| <span data-ttu-id="b7d8f-332">derleme</span><span class="sxs-lookup"><span data-stu-id="b7d8f-332">build</span></span> | <span data-ttu-id="b7d8f-333">Build (MSBuild props ve targets)</span><span class="sxs-lookup"><span data-stu-id="b7d8f-333">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="b7d8f-334">yerel</span><span class="sxs-lookup"><span data-stu-id="b7d8f-334">native</span></span> | <span data-ttu-id="b7d8f-335">yerel</span><span class="sxs-lookup"><span data-stu-id="b7d8f-335">native</span></span> |
| <span data-ttu-id="b7d8f-336">yok</span><span class="sxs-lookup"><span data-stu-id="b7d8f-336">none</span></span> | <span data-ttu-id="b7d8f-337">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="b7d8f-337">No folders</span></span> |
| <span data-ttu-id="b7d8f-338">tümü</span><span class="sxs-lookup"><span data-stu-id="b7d8f-338">all</span></span> | <span data-ttu-id="b7d8f-339">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-339">All folders</span></span> |

<span data-ttu-id="b7d8f-340">Örneğin, aşağıdaki satırlar `PackageA` Sürüm 1.1.0 veya üzeri ve `PackageB` Sürüm 1. x bağımlılıklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-340">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="b7d8f-341">Aşağıdaki satırlar aynı paketlere yönelik bağımlılıkları gösterir, ancak ve klasörlerinin yanı sıra, ve `contentFiles` `build` `PackageA` `native` `compile` klasörlerinin `PackageB` da dahil edileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-341">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="b7d8f-342">`.nuspec`Kullanarak bir projeden oluştururken `nuget spec` , bu projede var olan bağımlılıklar elde edilen dosyaya otomatik olarak eklenmez `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-342">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="b7d8f-343">Bunun yerine `nuget pack myproject.csproj` , öğesini kullanın ve oluşturulan *. nupkg* dosyasının içinden *. nuspec* dosyasını alın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-343">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="b7d8f-344">Bu *. nuspec* , bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-344">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="b7d8f-345">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-345">Dependency groups</span></span>

<span data-ttu-id="b7d8f-346">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="b7d8f-346">*Version 2.0+*</span></span>

<span data-ttu-id="b7d8f-347">Tek bir düz listeye alternatif olarak, bağımlılıklar içindeki öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir `<group>` `<dependencies>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-347">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="b7d8f-348">Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<dependency>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-348">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="b7d8f-349">Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-349">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="b7d8f-350">`<group>`Özniteliği olmayan öğe, `targetFramework` bağımlılıkların varsayılan veya geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-350">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="b7d8f-351">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-351">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="b7d8f-352">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-352">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="b7d8f-353">Klasöründe kullanılan [hedef çerçeve bilinen adı (tfd)](../reference/target-frameworks.md) biçimi, `lib/ref` ' de kullanılan tfd ile karşılaştırıldığında farklıdır `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-353">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="b7d8f-354">İçinde belirtilen hedef çerçeveler `dependencies group` ve `lib/ref` dosya klasöründe tam eşleşmeler yoksa, `.nuspec` `pack` komut [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md)öğesini yükseltir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-354">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="b7d8f-355">Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :</span><span class="sxs-lookup"><span data-stu-id="b7d8f-355">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="b7d8f-356">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-356">Explicit assembly references</span></span>

<span data-ttu-id="b7d8f-357">`<references>`Öğesi, `packages.config` paket kullanılırken hedef projenin başvurması gereken derlemeleri açıkça belirtmek için kullanan projeler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-357">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="b7d8f-358">Açık başvurular genellikle yalnızca tasarım zamanı derlemeler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-358">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="b7d8f-359">Daha fazla bilgi için bkz. [projeler tarafından başvurulan derlemeleri seçme](../create-packages/select-assemblies-referenced-by-projects.md) hakkında daha fazla bilgi için bu sayfaya bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-359">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="b7d8f-360">Örneğin, aşağıdaki öğe, `<references>` NuGet 'e yalnızca başvuru eklemesi için, `xunit.dll` `xunit.extensions.dll` pakette ek derlemeler olsa bile:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-360">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="b7d8f-361">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-361">Reference groups</span></span>

<span data-ttu-id="b7d8f-362">Tek bir düz listeye alternatif olarak, başvurular, içindeki öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir `<group>` `<references>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-362">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="b7d8f-363">Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<reference>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-363">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="b7d8f-364">Hedef çerçeve projenin çerçeve profiliyle uyumluysa, bu başvurular bir projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-364">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="b7d8f-365">`<group>`Özniteliği olmayan öğe, `targetFramework` başvuru varsayılan veya geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-365">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="b7d8f-366">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-366">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="b7d8f-367">Grup biçimi düz bir liste ile birlikte karıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-367">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="b7d8f-368">Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :</span><span class="sxs-lookup"><span data-stu-id="b7d8f-368">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="b7d8f-369">Framework derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-369">Framework assembly references</span></span>

<span data-ttu-id="b7d8f-370">Framework derlemeleri, .NET Framework 'ün bir parçası olan ve belirli bir makine için genel derleme önbelleğinde (GAC) olması gereken olanlardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-370">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="b7d8f-371">`<frameworkAssemblies>`Bir paket, öğesi içindeki bu derlemeleri tanımlayarak, gerekli başvuruların projenin bu tür başvurularına sahip olmadığı olayda bir projeye eklendiğinden emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-371">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="b7d8f-372">Kuşkusuz bu tür derlemeler doğrudan bir pakete dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-372">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="b7d8f-373">`<frameworkAssemblies>`Öğesi `<frameworkAssembly>` , her biri aşağıdaki öznitelikleri belirten sıfır veya daha fazla öğe içeriyor:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-373">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="b7d8f-374">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-374">Attribute</span></span> | <span data-ttu-id="b7d8f-375">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b7d8f-376">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-376">**assemblyName**</span></span> | <span data-ttu-id="b7d8f-377">Istenir Tam nitelikli derleme adı.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-377">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="b7d8f-378">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-378">**targetFramework**</span></span> | <span data-ttu-id="b7d8f-379">Seçim Bu başvurunun uygulandığı hedef çerçeveyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-379">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="b7d8f-380">Atlanırsa, başvurunun tüm çerçeveler için geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-380">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="b7d8f-381">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-381">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="b7d8f-382">Aşağıdaki örnekte `System.Net` , tüm hedef çerçeveler için bir başvuru ve `System.ServiceModel` yalnızca .NET Framework 4,0 için bir başvuru gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-382">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="b7d8f-383">Derleme dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="b7d8f-383">Including assembly files</span></span>

<span data-ttu-id="b7d8f-384">[Paket oluşturma](../create-packages/creating-a-package.md)bölümünde açıklanan kuralları izlerseniz, dosyadaki dosyaların listesini açıkça belirtmeniz gerekmez `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-384">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="b7d8f-385">`nuget pack`Komut, gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-385">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="b7d8f-386">Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'Lerine derleme başvuruları *ekler, çünkü bu,* `.resources.dll` yerelleştirilmiş uydu derlemeleri oldukları varsayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-386">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="b7d8f-387">Bu nedenle, `.resources.dll` başka bir şekilde temel paket kodu içeren dosyalar için kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-387">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="b7d8f-388">Bu otomatik davranışı atlamak ve bir pakete hangi dosyaların ekleneceğini açıkça denetlemek için, bir `<files>` öğeyi bir alt öğesi `<package>` (ve eşdüzey) olarak yerleştirin ve `<metadata>` her bir dosyayı ayrı bir `<file>` öğeyle tanımlayarak.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-388">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="b7d8f-389">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-389">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="b7d8f-390">NuGet 2. x ve öncesiyle ve kullanan projelerde, `packages.config` `<files>` bir paket yüklendiğinde değişmez içerik dosyalarını dahil etmek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-390">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="b7d8f-391">NuGet 3.3 + ve projeleri PackageReference ile, `<contentFiles>` bunun yerine öğesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-391">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="b7d8f-392">Ayrıntılar için aşağıdaki [içerik dosyalarını ekleme](#including-content-files) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-392">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="b7d8f-393">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="b7d8f-393">File element attributes</span></span>

<span data-ttu-id="b7d8f-394">Her `<file>` öğe aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-394">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="b7d8f-395">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-395">Attribute</span></span> | <span data-ttu-id="b7d8f-396">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b7d8f-397">**src**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-397">**src**</span></span> | <span data-ttu-id="b7d8f-398">Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu `exclude` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-398">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="b7d8f-399">`.nuspec`Mutlak bir yol belirtilmediği takdirde yol dosyayla ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="b7d8f-400">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b7d8f-401">**hedef**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-401">**target**</span></span> | <span data-ttu-id="b7d8f-402">Kaynak dosyaların yerleştirildiği,,, veya ile başlaması gereken paket içindeki klasörün göreli yolu `lib` `content` `build` `tools` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-402">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="b7d8f-403">Bkz. [kural tabanlı çalışma dizininden. nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-403">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="b7d8f-404">**amaz**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-404">**exclude**</span></span> | <span data-ttu-id="b7d8f-405">Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi `src` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-405">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="b7d8f-406">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="b7d8f-407">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-407">Examples</span></span>

<span data-ttu-id="b7d8f-408">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-408">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="b7d8f-409">**Hedef çerçeveye özgü tek bütünleştirilmiş kod**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-409">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="b7d8f-410">**Joker karakter kullanan DLL 'Ler kümesi**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-410">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="b7d8f-411">**Farklı çerçeveler için dll 'Ler**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-411">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="b7d8f-412">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-412">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="b7d8f-413">İçerik dosyalarını dahil etme</span><span class="sxs-lookup"><span data-stu-id="b7d8f-413">Including content files</span></span>

<span data-ttu-id="b7d8f-414">İçerik dosyaları, bir paketin bir projeye eklemesi gereken sabit dosyalardır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-414">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="b7d8f-415">Sabit olması, tüketim projesi tarafından değiştirilmeleri amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-415">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="b7d8f-416">Örnek içerik dosyaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-416">Example content files include:</span></span>

- <span data-ttu-id="b7d8f-417">Kaynak olarak gömülü görüntüler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-417">Images that are embedded as resources</span></span>
- <span data-ttu-id="b7d8f-418">Zaten derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-418">Source files that are already compiled</span></span>
- <span data-ttu-id="b7d8f-419">Projenin derleme çıktısına dahil olması gereken betikler</span><span class="sxs-lookup"><span data-stu-id="b7d8f-419">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="b7d8f-420">Projeye dahil olması gereken ancak projeye özgü değişikliklere gerek gerektirmeyen paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-420">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="b7d8f-421">İçerik dosyaları, `<files>` özniteliğinde klasörü belirtilerek öğesini kullanarak bir pakete dahil edilir `content` `target` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-421">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="b7d8f-422">Ancak, bu tür dosyalar, bir paket bir projeye yüklendiğinde, bunun yerine öğesini kullanarak yok sayılır `<contentFiles>` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-422">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="b7d8f-423">Tüketen projelerle maksimum uyumluluk için, her iki öğe içinde içerik dosyalarını ideal bir paket belirler.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-423">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="b7d8f-424">İçerik dosyaları için Files öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="b7d8f-424">Using the files element for content files</span></span>

<span data-ttu-id="b7d8f-425">İçerik dosyaları için yalnızca derleme dosyaları için aynı biçimi kullanın, ancak `content` `target` Aşağıdaki örneklerde gösterildiği gibi özniteliğinde temel klasör olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-425">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="b7d8f-426">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-426">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="b7d8f-427">**Dizin yapısıyla içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-427">**Content files with directory structure**</span></span>

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

<span data-ttu-id="b7d8f-428">**Hedef çerçeveye özgü içerik dosyası**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-428">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="b7d8f-429">**İçerik dosyası ada sahip bir klasöre kopyalanmış**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-429">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="b7d8f-430">Bu durumda, ' deki uzantının içindeki `target` uzantıyla eşleşmediği `src` ve bu nedenle adın bu bölümünü `target` bir klasör olarak değerlendirmiş olduğunu görür:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-430">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="b7d8f-431">**Uzantısız içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-431">**Content files without extensions**</span></span>

<span data-ttu-id="b7d8f-432">Uzantısı olmayan dosyaları dahil etmek için, `*` veya `**` joker karakterleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-432">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="b7d8f-433">**Derin yolu ve derin hedefi olan içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-433">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="b7d8f-434">Bu durumda, kaynak ve hedef için dosya uzantıları eşleştiğinden, NuGet hedefin bir klasör değil bir dosya adı olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-434">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="b7d8f-435">**Paketteki bir içerik dosyasını yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-435">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="b7d8f-436">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-436">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="b7d8f-437">İçerik dosyaları için contentFiles öğesini kullanma</span><span class="sxs-lookup"><span data-stu-id="b7d8f-437">Using the contentFiles element for content files</span></span>

<span data-ttu-id="b7d8f-438">*PackageReference ile NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="b7d8f-438">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="b7d8f-439">Varsayılan olarak, bir paket içeriği bir klasöre koyar `contentFiles` (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-439">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="b7d8f-440">Bu durumda, ' a bir düğüm eklemek gerekli değildir `contentFiles` `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-440">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="b7d8f-441">Hangi dosyaların ekleneceğini denetlemek için, öğesi, `<contentFiles>` `<files>` tam dosyaları içeren öğelerin bir koleksiyonu olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-441">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="b7d8f-442">Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-442">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="b7d8f-443">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="b7d8f-443">Attribute</span></span> | <span data-ttu-id="b7d8f-444">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7d8f-444">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b7d8f-445">**içeriyor**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-445">**include**</span></span> | <span data-ttu-id="b7d8f-446">Istenir Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu `exclude` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-446">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="b7d8f-447">`contentFiles`Mutlak bir yol belirtilmediği takdirde yol klasöre göre değişir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-447">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="b7d8f-448">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-448">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b7d8f-449">**amaz**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-449">**exclude**</span></span> | <span data-ttu-id="b7d8f-450">Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi `src` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-450">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="b7d8f-451">Joker karaktere `*` izin verilir ve çift joker karakter `**` özyinelemeli bir klasör aramasını ifade etmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-451">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b7d8f-452">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-452">**buildAction**</span></span> | <span data-ttu-id="b7d8f-453">,,, `Content` `None` `Embedded Resource` Vb. gibi MSBuild için içerik öğesine atanacak yapı eylemi `Compile` . Varsayılan değer `Compile` .</span><span class="sxs-lookup"><span data-stu-id="b7d8f-453">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="b7d8f-454">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-454">**copyToOutput**</span></span> | <span data-ttu-id="b7d8f-455">İçerik öğelerinin derleme (veya yayımlama) çıkış klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-455">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="b7d8f-456">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-456">The default is false.</span></span> |
| <span data-ttu-id="b7d8f-457">**leştirebilir**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-457">**flatten**</span></span> | <span data-ttu-id="b7d8f-458">İçerik öğelerinin derleme çıkışında tek bir klasöre mi kopyalanacağını (true) veya paketteki klasör yapısını korumayı (false) gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-458">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="b7d8f-459">Bu bayrak yalnızca copyToOutput bayrağı true olarak ayarlandığında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-459">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="b7d8f-460">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-460">The default is false.</span></span> |

<span data-ttu-id="b7d8f-461">Bir paket yüklenirken NuGet, alt öğelerini `<contentFiles>` yukarıdan aşağıya uygular.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-461">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="b7d8f-462">Aynı dosyayla birden çok giriş eşleşiyorsa, tüm girişler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-462">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="b7d8f-463">Aynı öznitelik için bir çakışma varsa en üstteki girdi alt girişleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-463">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="b7d8f-464">Paket klasörü yapısı</span><span class="sxs-lookup"><span data-stu-id="b7d8f-464">Package folder structure</span></span>

<span data-ttu-id="b7d8f-465">Paket projesi, aşağıdaki kalıbı kullanarak içerik yapısını almalıdır:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-465">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="b7d8f-466">`codeLanguages` ,, `cs` , `vb` `fs` `any` veya belirli bir `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="b7d8f-466">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="b7d8f-467">`TxM` NuGet tarafından desteklenen geçerli bir hedef çerçeve adıdır (bkz. [hedef çerçeveler](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="b7d8f-467">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="b7d8f-468">Bu söz dizimi sonuna herhangi bir klasör yapısı eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-468">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="b7d8f-469">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-469">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="b7d8f-470">Boş klasörler `.` , belirli dil birleşimleri ve TxM için içerik sağlamayı devre dışı bırakmak için kullanılabilir. Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-470">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="b7d8f-471">Örnek contentFiles bölümü</span><span class="sxs-lookup"><span data-stu-id="b7d8f-471">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="b7d8f-472">Framework başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-472">Framework reference groups</span></span>

<span data-ttu-id="b7d8f-473">*Sürüm 5.1 + wih PackageReference*</span><span class="sxs-lookup"><span data-stu-id="b7d8f-473">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="b7d8f-474">Framework başvuruları, WPF veya Windows Forms gibi paylaşılan çerçeveleri temsil eden bir .NET Core kavramıdır.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-474">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="b7d8f-475">Paket, paylaşılan bir çerçeve belirterek, tüm çerçeve bağımlılıklarının başvuru projesine dahil edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-475">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="b7d8f-476">Her `<group>` öğe için bir `targetFramework` öznitelik ve sıfır veya daha fazla `<frameworkReference>` öğe gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-476">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="b7d8f-477">Aşağıdaki örnek, bir .NET Core WPF projesi için oluşturulan bir nuspec gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-477">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="b7d8f-478">Çerçeve başvurularını içeren nusö 'lerin birlikte yazılması önerilmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-478">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="b7d8f-479">Bunun yerine, bunları projeden otomatik olarak çıkarmayacak olan [hedefler](msbuild-targets.md) paketini kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="b7d8f-479">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="b7d8f-480">Örnek nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="b7d8f-480">Example nuspec files</span></span>

<span data-ttu-id="b7d8f-481">**`.nuspec`Bağımlılıklar veya dosyalar belirtmeyen bir basit**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-481">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="b7d8f-482">**`.nuspec`Bağımlılıkları olan A**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-482">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="b7d8f-483">**`.nuspec`Dosyalarla birlikte**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-483">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="b7d8f-484">**Bir `.nuspec` Framework Derlemeleriyle**</span><span class="sxs-lookup"><span data-stu-id="b7d8f-484">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="b7d8f-485">Bu örnekte, belirli proje hedefleri için aşağıdakiler yüklenir:</span><span class="sxs-lookup"><span data-stu-id="b7d8f-485">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="b7d8f-486">. NET4-> `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="b7d8f-486">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="b7d8f-487">. NET4 Istemci profili-> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="b7d8f-487">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="b7d8f-488">Silverlight 3-> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="b7d8f-488">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="b7d8f-489">WindowsPhone-> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="b7d8f-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
