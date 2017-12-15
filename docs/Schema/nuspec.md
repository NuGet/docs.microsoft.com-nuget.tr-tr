---
title: "NuGet için'.nuspec dosyası başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d4a4db9b-5c2d-46aa-9107-d2b01733df7c
description: ".Nuspec dosyası bir paketi ve paket tüketicilere bilgi sağlamak için oluştururken kullanılan paket meta verileri içerir."
keywords: "nuspec başvurusu, NuGet paket meta verileri, NuGet paket bildirimi, nuspec şeması"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 91efd4b4cd2ec0bee4425ab66e0152e580e7975c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuspec-reference"></a><span data-ttu-id="ff377-104">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="ff377-104">.nuspec reference</span></span>

<span data-ttu-id="ff377-105">A `.nuspec` paket meta verileri içeren bir XML bildiriminden bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="ff377-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="ff377-106">Bu bildirim paketi oluşturmak ve bilgileri tüketicilere sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="ff377-107">Bildirim her zaman bir pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="ff377-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="ff377-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="ff377-108">In this topic:</span></span>

- [<span data-ttu-id="ff377-109">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="ff377-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="ff377-110">[Değiştirme belirteçleri](#replacement-tokens) (Visual Studio projesi ile kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="ff377-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="ff377-111">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="ff377-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="ff377-112">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="ff377-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="ff377-113">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="ff377-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="ff377-114">Derleme dosyaları dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="ff377-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="ff377-115">İçerik dosyaları dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="ff377-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="ff377-116">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ff377-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="ff377-117">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="ff377-117">General form and schema</span></span>

<span data-ttu-id="ff377-118">Geçerli `nuspec.xsd` şema dosyası bulunabilir [NuGet GitHub deposunu](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="ff377-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="ff377-119">Bu şemayı içinde bir `.nuspec` dosyası aşağıdaki genel biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ff377-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="ff377-120">Şema NET bir görsel gösterimi için şema dosyasını Visual Studio'da Tasarım modunda açın ve tıklayın **XML Şeması Explorer** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ff377-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="ff377-121">Alternatif olarak, kod olarak dosyasını açın, Düzenleyicisi'nde sağ tıklatın ve seçin **Göster XML Şeması Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ff377-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="ff377-122">Her iki şekilde (çoğunlukla genişletildiğinde) bir görünüm aşağıdaki gibi alın:</span><span class="sxs-lookup"><span data-stu-id="ff377-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio şema Gezgini ile nuspec.xsd Aç](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="ff377-124">Meta veri öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="ff377-124">Metadata attributes</span></span>

<span data-ttu-id="ff377-125">`<metadata>` Öğesi aşağıdaki tabloda açıklanan öznitelikleri destekler.</span><span class="sxs-lookup"><span data-stu-id="ff377-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="ff377-126">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ff377-126">Attribute</span></span> | <span data-ttu-id="ff377-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ff377-127">Required</span></span> | <span data-ttu-id="ff377-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="ff377-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="ff377-129">**minClientVersion**</span></span> | <span data-ttu-id="ff377-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff377-130">No</span></span> | <span data-ttu-id="ff377-131">*(2.5 +)*  Nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yükleyebilmek için NuGet istemci en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff377-131">*(2.5+)* Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="ff377-132">Bu paket belirli özelliklerine bağlıdır her kullanılır `.nuspec` belirli bir NuGet istemci sürümünün eklenen dosya.</span><span class="sxs-lookup"><span data-stu-id="ff377-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="ff377-133">Örneğin, bir paketini kullanarak `developmentDependency` özniteliği için "2.8" belirtmelidir `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="ff377-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="ff377-134">Benzer şekilde, bir paketini kullanarak `contentFiles` öğesi (sonraki bölüme bakın) ayarlamalıdır `minClientVersion` "3.3" için.</span><span class="sxs-lookup"><span data-stu-id="ff377-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="ff377-135">NuGet istemcileri 2.5 önce bu bayrak tanımıyor çünkü Ayrıca bunlar *her zaman* ne olursa olsun paketini yüklemek Reddet `minClientVersion` içerir.</span><span class="sxs-lookup"><span data-stu-id="ff377-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="ff377-136">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="ff377-136">Required metadata elements</span></span>

<span data-ttu-id="ff377-137">Aşağıdaki öğeler bir paket için en düşük gereksinimler olsa da, eklemeyi düşünmelisiniz [isteğe bağlı meta veri öğeleri](#optional-metadata-elements) genel deneyimini geliştirmek için geliştiricilere paketinizle birlikte sahip.</span><span class="sxs-lookup"><span data-stu-id="ff377-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="ff377-138">Bu öğeleri içinde görünmesi gereken bir `<metadata>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ff377-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="ff377-139">Öğe</span><span class="sxs-lookup"><span data-stu-id="ff377-139">Element</span></span> | <span data-ttu-id="ff377-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-141">**id**</span><span class="sxs-lookup"><span data-stu-id="ff377-141">**id**</span></span> | <span data-ttu-id="ff377-142">Nuget.org ya da ihtiyacınız arasında benzersiz olması büyük küçük harf duyarsız paket tanımlayıcısı galeri paketi bulunur.</span><span class="sxs-lookup"><span data-stu-id="ff377-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="ff377-143">Kimlikleri değil boşluk ya da bir URL için geçerli olmayan karakterler içeren ve genellikle .NET ad alanı kuralları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ff377-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="ff377-144">Bkz: [benzersiz paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="ff377-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="ff377-145">**Sürüm**</span><span class="sxs-lookup"><span data-stu-id="ff377-145">**version**</span></span> | <span data-ttu-id="ff377-146">Aşağıdaki şekilde paketin sürümü *major.minor.patch* düzeni.</span><span class="sxs-lookup"><span data-stu-id="ff377-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="ff377-147">Sürüm numaraları, yayın öncesi soneki içerebilir, açıklandığı gibi [paket sürüm](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="ff377-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="ff377-148">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="ff377-148">**description**</span></span> | <span data-ttu-id="ff377-149">Paket UI görüntü için uzun bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="ff377-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="ff377-150">**yazarları**</span><span class="sxs-lookup"><span data-stu-id="ff377-150">**authors**</span></span> | <span data-ttu-id="ff377-151">Nuget.org profil adları eşleşen paketleri yazarlar, virgülle ayrılmış listesi. Bunlar nuget.org NuGet galerisinde görüntülenir ve paketleri çapraz başvuru için aynı yazarlar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="ff377-152">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="ff377-152">Optional metadata elements</span></span>

<span data-ttu-id="ff377-153">Bu öğeleri içinde görünmesi gereken bir `<metadata>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ff377-153">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="ff377-154">Tek öğeleri</span><span class="sxs-lookup"><span data-stu-id="ff377-154">Single elements</span></span>

| <span data-ttu-id="ff377-155">Öğe</span><span class="sxs-lookup"><span data-stu-id="ff377-155">Element</span></span> | <span data-ttu-id="ff377-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-157">**Başlık**</span><span class="sxs-lookup"><span data-stu-id="ff377-157">**title**</span></span> | <span data-ttu-id="ff377-158">Nuget.org ve Visual Studio'da Paket Yöneticisi gibi UI görünümlerde genellikle kullanılan paket, bir insan kolay başlığı.</span><span class="sxs-lookup"><span data-stu-id="ff377-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="ff377-159">Belirtilmezse, paket kimliği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="ff377-160">**sahipleri**</span><span class="sxs-lookup"><span data-stu-id="ff377-160">**owners**</span></span> | <span data-ttu-id="ff377-161">Nuget.org üzerinde profil adları kullanarak paket oluşturucuları virgülle ayrılmış listesi. Bu genellikle aynı olarak listesidir `authors`ve paket için nuget.org karşıya yüklenirken göz ardı edilir. Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="ff377-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="ff377-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="ff377-162">**projectUrl**</span></span> | <span data-ttu-id="ff377-163">Paketin giriş sayfası, genellikle kullanıcı Arabiriminde gösterilen URL'sini nuget.org yanı sıra görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ff377-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="ff377-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="ff377-164">**licenseUrl**</span></span> | <span data-ttu-id="ff377-165">Genellikle nuget.org yanı sıra kullanıcı Arabirimi görüntüler gösterilen paketin lisans URL'sini.</span><span class="sxs-lookup"><span data-stu-id="ff377-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="ff377-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="ff377-166">**iconUrl**</span></span> | <span data-ttu-id="ff377-167">UI görüntü paketinde simgesi olarak kullanılacak bir URL 64 x 64 görüntünün saydamlık arka plana sahip.</span><span class="sxs-lookup"><span data-stu-id="ff377-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="ff377-168">Bu öğe içerdiğinden emin olun *resim URL'si doğrudan* ve görüntüyü içeren bir web sayfasının URL değil.</span><span class="sxs-lookup"><span data-stu-id="ff377-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="ff377-169">Örneğin, görüntüyü github'dan, URL gibi raw dosyasını kullanmayı `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span><span class="sxs-lookup"><span data-stu-id="ff377-169">For example, to use an image from GitHub, use the raw file URL like `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span></span> |
| <span data-ttu-id="ff377-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="ff377-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="ff377-171">İstemci paketi lisans paketi yüklemeden önce kabul etmek için tüketici sor olup olmadığını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ff377-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="ff377-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="ff377-172">**developmentDependency**</span></span> | <span data-ttu-id="ff377-173">*(2.8 +)*  Paket olup olmadığını belirten bir Boolean değeri bir geliştirme-yalnızca-paket diğer paketler bağımlılık olarak dahil önleyen bağımlılık olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="ff377-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="ff377-174">**Özet**</span><span class="sxs-lookup"><span data-stu-id="ff377-174">**summary**</span></span> | <span data-ttu-id="ff377-175">UI görüntülenmesi için paket kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="ff377-175">A short description of the package for UI display.</span></span> <span data-ttu-id="ff377-176">Atlanırsa, kesilmiş bir sürümünü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="ff377-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="ff377-177">**releaseNotes**</span></span> | <span data-ttu-id="ff377-178">*(1.5 +)*  Kullanıcı arabiriminde gibi sık kullanılan şekilde paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesi, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine.</span><span class="sxs-lookup"><span data-stu-id="ff377-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="ff377-179">**Telif Hakkı**</span><span class="sxs-lookup"><span data-stu-id="ff377-179">**copyright**</span></span> | <span data-ttu-id="ff377-180">*(1.5 +)*  Paket ayrıntılarını telif hakkı.</span><span class="sxs-lookup"><span data-stu-id="ff377-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="ff377-181">**Dil**</span><span class="sxs-lookup"><span data-stu-id="ff377-181">**language**</span></span> | <span data-ttu-id="ff377-182">Paketi için yerel ayar kimliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-182">The locale ID for the package.</span></span> <span data-ttu-id="ff377-183">Bkz: [yerelleştirilmiş paketleri oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ff377-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="ff377-184">**etiketleri**</span><span class="sxs-lookup"><span data-stu-id="ff377-184">**tags**</span></span> | <span data-ttu-id="ff377-185">Etiketleri ve paketler arama ve filtreleme aracılığıyla paket ve yardımcı bulunabilirliğini açıklayan anahtar sözcükleri boşlukla ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ff377-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="ff377-186">**Hizmet verilebilen**</span><span class="sxs-lookup"><span data-stu-id="ff377-186">**serviceable**</span></span> | <span data-ttu-id="ff377-187">*(3.3 +)*  İç NuGet için kullanım içindir.</span><span class="sxs-lookup"><span data-stu-id="ff377-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="ff377-188">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="ff377-188">Collection elements</span></span>

| <span data-ttu-id="ff377-189">Öğe</span><span class="sxs-lookup"><span data-stu-id="ff377-189">Element</span></span> | <span data-ttu-id="ff377-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="ff377-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="ff377-191">**packageTypes**</span></span> | <span data-ttu-id="ff377-192">*(3.3 +)*  Sıfır veya daha fazla koleksiyonu `<packageType>` geleneksel bağımlılık paketi varsa dışında paket türünü belirleyen öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-192">*(3.3+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="ff377-193">Her packageType öznitelikleri *adı* ve *sürüm*.</span><span class="sxs-lookup"><span data-stu-id="ff377-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="ff377-194">Bkz: [ayar paket türü](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="ff377-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="ff377-195">**Bağımlılıklar**</span><span class="sxs-lookup"><span data-stu-id="ff377-195">**dependencies**</span></span> | <span data-ttu-id="ff377-196">Sıfır veya daha fazla koleksiyonu `<dependency>` öğeleri paketi için bağımlılıklar belirtme.</span><span class="sxs-lookup"><span data-stu-id="ff377-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="ff377-197">Her bir bağımlılığın öznitelikleri *kimliği*, *sürüm*, *dahil* (3.x+) ve *hariç* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="ff377-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="ff377-198">Bkz: [bağımlılıkları](#dependencies) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ff377-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="ff377-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="ff377-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="ff377-200">*(1.2 +)*  Sıfır veya daha fazla koleksiyonu `<frameworkAssembly>` öğeleri, bu paket için gerekli .NET Framework derleme başvurularını tanımlayan da sağlar başvuruları paketi kullanan projeler için eklenir.</span><span class="sxs-lookup"><span data-stu-id="ff377-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="ff377-201">Her frameworkAssembly sahip *assemblyName* ve *targetFramework* öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="ff377-202">Bkz: [framework derlemeyi belirtmeyi başvuran GAC](#specifying-framework-assembly-references-gac) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ff377-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="ff377-203">**başvuruları**</span><span class="sxs-lookup"><span data-stu-id="ff377-203">**references**</span></span> | <span data-ttu-id="ff377-204">*(1.5 +)*  Sıfır veya daha fazla koleksiyonu `<reference>` paketin derlemelerde adlandırma öğeleri `lib` proje başvuruları eklenen klasör.</span><span class="sxs-lookup"><span data-stu-id="ff377-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="ff377-205">Her başvurusu olan bir *dosya* özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="ff377-206">`<references>`Ayrıca içerebilir bir `<group>` öğesi ile bir *targetFramework* sonra içeren öznitelik `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="ff377-207">Atlanırsa, tüm başvuruları `lib` dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="ff377-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="ff377-208">Bkz: [açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ff377-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="ff377-209">**Content dosyaları**</span><span class="sxs-lookup"><span data-stu-id="ff377-209">**contentFiles**</span></span> | <span data-ttu-id="ff377-210">*(3.3 +)*  Koleksiyonu `<files>` tüketim projeye dahil etmek için içerik dosyaları belirlemek öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="ff377-211">Bu dosyalar, proje sistem içinde bunların nasıl kullanılacağını açıklayan özniteliklerinin kümesiyle belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ff377-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="ff377-212">Bkz: [pakete eklenecek dosyaları belirtme](#specifying-files-to-include-in-the-package) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ff377-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="ff377-213">Dosyalar öğesi</span><span class="sxs-lookup"><span data-stu-id="ff377-213">Files element</span></span>

<span data-ttu-id="ff377-214">`<package>` Düğüm içerebilir bir `<files>` düğümü bir eşdüzeyi olarak `<metadata>`ve bir ya da `<contentFiles>` altındaki `<metadata>`, pakete eklenecek hangi derleme ve içerik dosyaları belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="ff377-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="ff377-215">Bkz: [derleme dosyaları dahil olmak üzere](#including-assembly-files) ve [içerik dosyaları dahil olmak üzere](#including-content-files) Ayrıntılar için bu konudaki sonraki.</span><span class="sxs-lookup"><span data-stu-id="ff377-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="ff377-216">Değiştirme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="ff377-216">Replacement tokens</span></span>

<span data-ttu-id="ff377-217">Bir paket oluştururken [ `nuget pack` komutu](../tools/cli-ref-pack.md) $ayrılmış belirteçlerinde değiştirir `.nuspec` dosyanın `<metadata>` herhangi birinden bir proje dosyası değerlerini düğümle veya `pack` komutunun `-properties`geçin.</span><span class="sxs-lookup"><span data-stu-id="ff377-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="ff377-218">Komut satırında belirttiğiniz belirteci değerlerle `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="ff377-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="ff377-219">Örneğin, bir belirteç gibi kullanabilir `$owners$` ve `$desc$` içinde `.nuspec` ve saat gibi sevk adresindeki değerlerini belirtin:</span><span class="sxs-lookup"><span data-stu-id="ff377-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="ff377-220">Bir projeye ait değerleri kullanmak için aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo başvuruyor dosyasında `Properties` gibi `AssemblyInfo.cs` veya `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="ff377-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="ff377-221">Bu belirteçler kullanmak için çalıştırın `nuget pack` proje dosyası yerine yalnızca `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ff377-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="ff377-222">Örneğin aşağıdaki komutu kullanarak, `$id$` ve `$version$` içinde belirteçler bir `.nuspec` dosyası, projenin değiştirilir `AssemblyName` ve `AssemblyVersion` değerler:</span><span class="sxs-lookup"><span data-stu-id="ff377-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="ff377-223">Genellikle, sahip olduğunuz bir proje oluşturduğunuzda `.nuspec` başlangıçta kullanarak `nuget spec MyProject.csproj` otomatik olarak içeren bazı standart bu belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="ff377-224">Ancak, bir proje için değerler eksikse gerekli `.nuspec` öğeleri, ardından `nuget pack` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ff377-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="ff377-225">Ayrıca, proje değerleri değiştirirseniz, paket oluşturmadan önce yeniden emin olun; Bu paketi komutunun ile kolayca yapılabilir `build` geçin.</span><span class="sxs-lookup"><span data-stu-id="ff377-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="ff377-226">Dışında `$configuration$`, projedeki değerleri herhangi bir komut satırında aynı belirtecine atanmış yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="ff377-227">Belirteç</span><span class="sxs-lookup"><span data-stu-id="ff377-227">Token</span></span> | <span data-ttu-id="ff377-228">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="ff377-228">Value source</span></span> | <span data-ttu-id="ff377-229">Değer</span><span class="sxs-lookup"><span data-stu-id="ff377-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="ff377-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="ff377-230">**$id$**</span></span> | <span data-ttu-id="ff377-231">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="ff377-231">Project file</span></span> | <span data-ttu-id="ff377-232">Proje dosyasından AssemblyName</span><span class="sxs-lookup"><span data-stu-id="ff377-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="ff377-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="ff377-233">**$version$**</span></span> | <span data-ttu-id="ff377-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ff377-234">AssemblyInfo</span></span> | <span data-ttu-id="ff377-235">Assemblyınformationalversion bütünleştirilmiş varsa, aksi takdirde AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="ff377-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="ff377-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="ff377-236">**$author$**</span></span> | <span data-ttu-id="ff377-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ff377-237">AssemblyInfo</span></span> | <span data-ttu-id="ff377-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="ff377-238">AssemblyCompany</span></span> |
| <span data-ttu-id="ff377-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="ff377-239">**$description$**</span></span> | <span data-ttu-id="ff377-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ff377-240">AssemblyInfo</span></span> | <span data-ttu-id="ff377-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="ff377-241">AssemblyDescription</span></span> |
| <span data-ttu-id="ff377-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="ff377-242">**$copyright$**</span></span> | <span data-ttu-id="ff377-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ff377-243">AssemblyInfo</span></span> | <span data-ttu-id="ff377-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="ff377-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="ff377-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="ff377-245">**$configuration$**</span></span> | <span data-ttu-id="ff377-246">Derleme DLL</span><span class="sxs-lookup"><span data-stu-id="ff377-246">Assembly DLL</span></span> | <span data-ttu-id="ff377-247">Hata ayıklama için varsayılan değer olarak, derleme için kullanılan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ff377-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="ff377-248">Bir yayın Yapılandırması'nı kullanarak bir paket oluşturmak için her zaman kullanmanız gerektiğini unutmayın `-properties Configuration=Release` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="ff377-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="ff377-249">Belirteçleri de dahil, yolları çözümlemek için kullanılabilir [derleme dosyalarını](#including-assembly-files) ve [içerik dosyaları](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="ff377-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="ff377-250">Belirteçleri yapı yapılandırmasına bağlı olarak eklenecek dosyaları seçin edinerek MSBuild özellikleri olarak aynı ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ff377-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="ff377-251">Örneğin, aşağıdaki belirteçlerinde kullanırsanız `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="ff377-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="ff377-252">Ve bir derleme, `AssemblyName` olan `LoggingLibrary` ile `Release` MSBuild, sonuçta elde edilen satırları yapılandırmasında `.nuspec` paket dosyasında aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ff377-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="ff377-253">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="ff377-253">Dependencies</span></span>

<span data-ttu-id="ff377-254">`<dependencies>` Öğesi içinde `<metadata>` herhangi bir sayıda içeren `<dependency>` en üst düzey paketinin bağımlı olduğu diğer paketleri belirleyin öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="ff377-255">Her özniteliklerini `<dependency>` aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ff377-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="ff377-256">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ff377-256">Attribute</span></span> | <span data-ttu-id="ff377-257">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-257">Description</span></span> |
| --- | --- | 
| `id` | <span data-ttu-id="ff377-258">(Gerekli) Bağımlılık paket kimliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-258">(Required) The package ID of the dependency.</span></span> |
| `version` | <span data-ttu-id="ff377-259">(Gerekli) Sürümleri bağımlılık olarak kabul edilebilir aralık.</span><span class="sxs-lookup"><span data-stu-id="ff377-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="ff377-260">Bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards) söz dizimi için.</span><span class="sxs-lookup"><span data-stu-id="ff377-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="ff377-261">include</span><span class="sxs-lookup"><span data-stu-id="ff377-261">include</span></span> | <span data-ttu-id="ff377-262">Virgülle ayrılmış listesini içeren/çıkarma (aşağıya bakın) son pakete dahil etmek bağımlılığın belirten etiketler.</span><span class="sxs-lookup"><span data-stu-id="ff377-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="ff377-263">Varsayılan değer `none` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="ff377-263">The default value is `none`.</span></span> |
| <span data-ttu-id="ff377-264">exclude</span><span class="sxs-lookup"><span data-stu-id="ff377-264">exclude</span></span> | <span data-ttu-id="ff377-265">Virgülle ayrılmış listesini içeren/çıkarma (aşağıya bakın) son paketinde dışlanacak bağımlılığın belirten etiketler.</span><span class="sxs-lookup"><span data-stu-id="ff377-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="ff377-266">Varsayılan değer `all`.</span><span class="sxs-lookup"><span data-stu-id="ff377-266">The  default value is `all`.</span></span> <span data-ttu-id="ff377-267">İle belirtilen etiketleri `exclude` ile belirtilen önceliklidir `include`.</span><span class="sxs-lookup"><span data-stu-id="ff377-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="ff377-268">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="ff377-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="ff377-269">Etiket dahil etme/hariç tutma</span><span class="sxs-lookup"><span data-stu-id="ff377-269">Include/Exclude tag</span></span> | <span data-ttu-id="ff377-270">Hedef etkilenen klasörler</span><span class="sxs-lookup"><span data-stu-id="ff377-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-271">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="ff377-271">contentFiles</span></span> | <span data-ttu-id="ff377-272">İçerik</span><span class="sxs-lookup"><span data-stu-id="ff377-272">Content</span></span>  |
| <span data-ttu-id="ff377-273">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="ff377-273">runtime</span></span> | <span data-ttu-id="ff377-274">Çalışma zamanı, kaynakları ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="ff377-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="ff377-275">Derleme</span><span class="sxs-lookup"><span data-stu-id="ff377-275">compile</span></span> | <span data-ttu-id="ff377-276">LIB</span><span class="sxs-lookup"><span data-stu-id="ff377-276">lib</span></span> |
| <span data-ttu-id="ff377-277">derleme</span><span class="sxs-lookup"><span data-stu-id="ff377-277">build</span></span> | <span data-ttu-id="ff377-278">derleme (MSBuild özellik ve hedefleri)</span><span class="sxs-lookup"><span data-stu-id="ff377-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="ff377-279">yerel</span><span class="sxs-lookup"><span data-stu-id="ff377-279">native</span></span> | <span data-ttu-id="ff377-280">yerel</span><span class="sxs-lookup"><span data-stu-id="ff377-280">native</span></span> |
| <span data-ttu-id="ff377-281">yok</span><span class="sxs-lookup"><span data-stu-id="ff377-281">none</span></span> | <span data-ttu-id="ff377-282">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="ff377-282">No folders</span></span> |
| <span data-ttu-id="ff377-283">tüm</span><span class="sxs-lookup"><span data-stu-id="ff377-283">all</span></span> | <span data-ttu-id="ff377-284">Tüm klasörleri</span><span class="sxs-lookup"><span data-stu-id="ff377-284">All folders</span></span> |

<span data-ttu-id="ff377-285">Örneğin, aşağıdaki satırları üzerinde bağımlılıkları göstermek `PackageA` sürüm 1.1.0 veya daha yüksek ve `PackageB` sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="ff377-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="ff377-286">Aşağıdaki satırları aynı paketleri bağımlılıkları gösterir, ancak dahil edileceğini belirtin `contentFiles` ve `build` klasörleri `PackageA` ve her şeyi ancak `native` ve `compile` klasörleri `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="ff377-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="ff377-287">Not: oluştururken bir `.nuspec` kullanarak proje `nuget spec`, bu proje bağımlılıkları otomatik olarak eklenir kaynaklanan `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff377-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="ff377-288">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="ff377-288">Dependency groups</span></span>

<span data-ttu-id="ff377-289">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="ff377-289">*Version 2.0+*</span></span>

<span data-ttu-id="ff377-290">Tek düz bir liste için alternatif olarak, proje hedef kullanmanın framework profili göre bağımlılıkları belirtilebilir `<group>` içinde öğelerin `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="ff377-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="ff377-291">Her Grup adlı bir özniteliği olan `targetFramework` ve sıfır veya daha fazla içeren `<dependency>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="ff377-292">Hedef Framework'ü projenin framework profiliyle uyumlu olduğunda bu bağımlılıkların birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ff377-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ff377-293">`<group>` Öğesi olmadan bir `targetFramework` özniteliği bağımlılıkları varsayılan ya da geri dönüş liste olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="ff377-294">Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="ff377-294">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ff377-295">Grup biçimi ile düz bir liste intermixed olamaz.</span><span class="sxs-lookup"><span data-stu-id="ff377-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ff377-296">Aşağıdaki örnek, farklı varyasyonları gösterir `<group>` öğe:</span><span class="sxs-lookup"><span data-stu-id="ff377-296">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="ff377-297">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="ff377-297">Explicit assembly references</span></span>

<span data-ttu-id="ff377-298">`<references>` Öğesi açıkça hedef projeyi paket kullanırken başvurması gereken derlemeleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff377-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="ff377-299">Bu öğe varsa, NuGet yalnızca listelenen derlemelerine başvurular ekleyin; Bu başvurular için herhangi bir paketin derlemelerde eklemez `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="ff377-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="ff377-300">Örneğin, aşağıdaki `<references>` öğesi bildirir yalnızca başvuruları eklemek için NuGet `xunit.dll` ve `xunit.extensions.dll` olsa bile ek derlemeler pakette:</span><span class="sxs-lookup"><span data-stu-id="ff377-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="ff377-301">Açık başvurular genellikle tasarım zamanı yalnızca derlemeler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="ff377-302">Kullanırken [kod sözleşmeleri](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/code-contracts), örneğin, sözleşme derlemeleri bunlar artırabilir ve böylece Visual Studio bulmalarını çalışma zamanı derlemeleri yanındaki olması gerekiyor, ancak sözleşme derlemeleri olmaması gereken proje tarafından başvurulan veya kopyalama projenin içine `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="ff377-302">When using [Code Contracts](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="ff377-303">Benzer şekilde, açık başvurular derlemeleri çalışma zamanı derlemeleri yanında bulunan, ancak proje başvuruları dahil gerekmez mu araçlarını gereken XUnit gibi birim test çerçevelerini için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff377-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="ff377-304">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="ff377-304">Reference groups</span></span>

<span data-ttu-id="ff377-305">*Sürüm 2.5 +*</span><span class="sxs-lookup"><span data-stu-id="ff377-305">*Version 2.5+*</span></span>

<span data-ttu-id="ff377-306">Tek düz bir liste için alternatif olarak, proje hedef kullanmanın framework profili göre başvuruları belirtilebilir `<group>` içinde öğelerin `<references>`.</span><span class="sxs-lookup"><span data-stu-id="ff377-306">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="ff377-307">Her Grup adlı bir özniteliği olan `targetFramework` ve sıfır veya daha fazla içeren `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="ff377-307">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="ff377-308">Hedef Framework'ü projenin framework profiliyle uyumlu olduğunda bu başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="ff377-308">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ff377-309">`<group>` Öğesi olmadan bir `targetFramework` özniteliği başvuruları varsayılan ya da geri dönüş liste olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-309">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="ff377-310">Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="ff377-310">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ff377-311">Grup biçimi ile düz bir liste intermixed olamaz.</span><span class="sxs-lookup"><span data-stu-id="ff377-311">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ff377-312">Aşağıdaki örnek, farklı varyasyonları gösterir `<group>` öğe:</span><span class="sxs-lookup"><span data-stu-id="ff377-312">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="ff377-313">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="ff377-313">Framework assembly references</span></span>

<span data-ttu-id="ff377-314">Çerçeve derlemesi .NET framework'ün parçasıdır ve genel derleme önbelleğinde (GAC) belirli bir makine zaten olmalıdır izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="ff377-314">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="ff377-315">Bu derleme içinde tanımlayan tarafından `<frameworkAssemblies>` öğesi, bir paket emin olun proje zaten bu başvuruları yok gerektiğinde, gerekli başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="ff377-315">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="ff377-316">Bu tür derlemeler doğal olarak, bir pakette doğrudan dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="ff377-316">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="ff377-317">`<frameworkAssemblies>` Sıfır veya daha fazla öğe içeriyor `<frameworkAssembly>` öğeleri, her biri aşağıdaki öznitelikler belirtir:</span><span class="sxs-lookup"><span data-stu-id="ff377-317">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="ff377-318">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ff377-318">Attribute</span></span> | <span data-ttu-id="ff377-319">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-319">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-320">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="ff377-320">**assemblyName**</span></span> | <span data-ttu-id="ff377-321">(Gerekli) Tam nitelikli derleme adı.</span><span class="sxs-lookup"><span data-stu-id="ff377-321">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="ff377-322">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="ff377-322">**targetFramework**</span></span> | <span data-ttu-id="ff377-323">(İsteğe bağlı) Bu başvuru uygulandığı hedef Framework'ü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff377-323">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="ff377-324">Atlanırsa, başvuru tüm çerçeveler için geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff377-324">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="ff377-325">Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="ff377-325">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="ff377-326">Aşağıdaki örnek, başvuru gösterir `System.Net` tüm çerçeveler ve başvuru hedef için `System.ServiceModel` yalnızca .NET Framework 4.0 için:</span><span class="sxs-lookup"><span data-stu-id="ff377-326">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="ff377-327">Derleme dosyaları dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="ff377-327">Including assembly files</span></span>

<span data-ttu-id="ff377-328">Açıklanan kuralları izlerseniz [paket oluşturma](../create-packages/creating-a-package.md), dosyaların listesini açıkça belirtmek zorunda değilsiniz `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="ff377-328">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="ff377-329">`nuget pack` Komutu, gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="ff377-329">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="ff377-330">Bir paket bir projeye yüklendiğinde, NuGet paket DLL'leri derleme başvuruları otomatik olarak ekler. *hariç* adlandırıldığı o `.resources.dll` yerleştirilmiş yardımcı derlemeler olarak kabul olduğundan.</span><span class="sxs-lookup"><span data-stu-id="ff377-330">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="ff377-331">Bu nedenle, kullanmaktan kaçının `.resources.dll` , aksi takdirde temel paket kodu içeren dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="ff377-331">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="ff377-332">Bu otomatik davranışı atlayıp açıkça hangi dosyaların bir pakete dahil edilen denetlemek için yerleştirin bir `<files>` öğesi bir alt öğesi olarak `<package>` (ve bir eşdüzeyi `<metadata>`), her dosya ayrı bir tanımlayan `<file>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ff377-332">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="ff377-333">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ff377-333">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="ff377-334">NuGet ile 2.x ve önceki sürümleri ve kullanarak projeleri `packages.config`, `<files>` öğesi bir paket yüklendiğinde değişmez içerik dosyalarını eklemek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-334">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="ff377-335">NuGet 3.3 + ve kullanarak projeleri ile `project.json` pr PackageReference, `<contentFiles>` öğe yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff377-335">With NuGet 3.3+ and projects using `project.json` pr PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="ff377-336">Bkz: [içerik dosyaları dahil olmak üzere](#including-content-files) aşağıda Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="ff377-336">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="ff377-337">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="ff377-337">File element attributes</span></span>

<span data-ttu-id="ff377-338">Her `<file>` öğesi aşağıdaki özniteliklere belirtir:</span><span class="sxs-lookup"><span data-stu-id="ff377-338">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="ff377-339">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ff377-339">Attribute</span></span> | <span data-ttu-id="ff377-340">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-340">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-341">**src**</span><span class="sxs-lookup"><span data-stu-id="ff377-341">**src**</span></span> | <span data-ttu-id="ff377-342">Dosya veya dosyalar tarafından belirtilen Dışlamalar tabi dahil etmek için konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-342">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ff377-343">Göreli yol olduğundan `.nuspec` mutlak bir yol belirtilmediği sürece dosya.</span><span class="sxs-lookup"><span data-stu-id="ff377-343">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ff377-344">Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ff377-344">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ff377-345">**Hedef**</span><span class="sxs-lookup"><span data-stu-id="ff377-345">**target**</span></span> | <span data-ttu-id="ff377-346">Göreli yolu ile başlamalı, kaynak dosyaları yerleştirilir, paket içindeki klasöre `lib`, `content`, `build`, veya `tools`.</span><span class="sxs-lookup"><span data-stu-id="ff377-346">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="ff377-347">Bkz: [kurala dayalı bir çalışma dizininden bir .nuspec oluşturma](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="ff377-347">See [Creating a .nuspec from a convention-based working directory](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="ff377-348">**hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="ff377-348">**exclude**</span></span> | <span data-ttu-id="ff377-349">Dosya veya dosya desenlerinin ayarlayacağım noktalı virgülle ayrılmış listesini `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="ff377-349">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ff377-350">Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ff377-350">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="ff377-351">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ff377-351">Examples</span></span>

<span data-ttu-id="ff377-352">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="ff377-352">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="ff377-353">**Bir hedef framework belirli tek derleme**</span><span class="sxs-lookup"><span data-stu-id="ff377-353">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="ff377-354">**Joker karakter kullanarak DLL'leri kümesi**</span><span class="sxs-lookup"><span data-stu-id="ff377-354">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="ff377-355">**Farklı çerçeveleri DLL'leri**</span><span class="sxs-lookup"><span data-stu-id="ff377-355">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="ff377-356">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="ff377-356">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="ff377-357">İçerik dosyaları dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="ff377-357">Including content files</span></span>

<span data-ttu-id="ff377-358">İçerik dosyaları bir proje eklemek için bir paket gereken değişmez dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="ff377-358">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="ff377-359">Değişmez olmasının, bunlar Süren projenin değiştirilecek amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ff377-359">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="ff377-360">Örnek içerik dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="ff377-360">Example content files include:</span></span>

- <span data-ttu-id="ff377-361">Kaynaklar olarak katıştırılmış görüntüler</span><span class="sxs-lookup"><span data-stu-id="ff377-361">Images that are embedded as resources</span></span>
- <span data-ttu-id="ff377-362">Önceden derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="ff377-362">Source files that are already compiled</span></span>
- <span data-ttu-id="ff377-363">Proje derleme çıktı ile dahil edilmesi gereken komut</span><span class="sxs-lookup"><span data-stu-id="ff377-363">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="ff377-364">Projeye dahil edilmesi gereken ancak projeye özgü değişiklikleri gerekmeyen bir paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="ff377-364">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="ff377-365">İçerik dosyalarını kullanarak bir paket dahil edilir `<files>` öğesini belirterek `content` klasöründe `target` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-365">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="ff377-366">Paket kullanarak bir projeye yüklendiğinde ancak, bu tür dosyaları göz ardı edilir `project.json` yerine kullanan sistem NuGet 3.3 + ya da NuGet 4 + PackageReference `<contentFiles>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ff377-366">However, such files are ignored when the package is installed in a project using the `project.json` system in NuGet 3.3+ or PackageReference in NuGet 4+, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="ff377-367">Projeleri kullanma ile en fazla uyumluluk için bir paket içerik dosyalarını ideal olarak her iki öğelerinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff377-367">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="ff377-368">Dosyalar öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="ff377-368">Using the files element for content files</span></span>

<span data-ttu-id="ff377-369">İçerik dosyaları için yalnızca derleme dosyaları için olduğu gibi aynı biçimi kullanır, ancak belirtin `content` temel klasör olarak `target` özniteliği aşağıdaki örneklerde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="ff377-369">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="ff377-370">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="ff377-370">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="ff377-371">**İçerik dosyaları dizin yapısı**</span><span class="sxs-lookup"><span data-stu-id="ff377-371">**Content files with directory structure**</span></span>

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

<span data-ttu-id="ff377-372">**İçerik dosyası için bir hedef çerçevesine özgü**</span><span class="sxs-lookup"><span data-stu-id="ff377-372">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="ff377-373">**İçerik dosyası adında nokta olan bir klasöre kopyalanır**</span><span class="sxs-lookup"><span data-stu-id="ff377-373">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="ff377-374">Bu durumda, NuGet, görür uzantı `target` uzantı eşleşmiyor `src` ve bu nedenle adı kısmı değerlendirir `target` bir klasör olarak:</span><span class="sxs-lookup"><span data-stu-id="ff377-374">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="ff377-375">**İçerik dosyaları uzantısız**</span><span class="sxs-lookup"><span data-stu-id="ff377-375">**Content files without extensions**</span></span>

<span data-ttu-id="ff377-376">Bir uzantısı olmayan dosyaları eklemek için kullanın `*` veya `**` joker karakterler:</span><span class="sxs-lookup"><span data-stu-id="ff377-376">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="ff377-377">**Derin yolu ve derin hedefi olan içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="ff377-377">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="ff377-378">Bu durumda, kaynak ve hedef dosya uzantılarını eşleştiğinden NuGet hedef dosya adını ve bir klasör olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="ff377-378">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="ff377-379">**Paketteki içerik dosyasını yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="ff377-379">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="ff377-380">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="ff377-380">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="ff377-381">Content dosyaları öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="ff377-381">Using the contentFiles element for content files</span></span>

<span data-ttu-id="ff377-382">*Sürümüyle 3.3 + project.json ve 4.0 + PackageReference ile*</span><span class="sxs-lookup"><span data-stu-id="ff377-382">*Version 3.3+ with project.json and 4.0+ with PackageReference*</span></span>

<span data-ttu-id="ff377-383">Varsayılan olarak, bir paket içeriği yerleştirir bir `contentFiles` klasörü (aşağıya bakın) ve `nuget pack` varsayılan özniteliklerini kullanarak bu klasördeki tüm dosyaları dahil.</span><span class="sxs-lookup"><span data-stu-id="ff377-383">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="ff377-384">Bu durumda dahil etmek gerekli değildir bir `contentFiles` düğümünde `.nuspec` hiç.</span><span class="sxs-lookup"><span data-stu-id="ff377-384">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="ff377-385">Hangi dosyaların dahil olduğunu denetlemek için `<contentFiles>` öğesi belirttiğinden bir koleksiyonu `<files>` tam dosyaları belirlemek öğeler içerir.</span><span class="sxs-lookup"><span data-stu-id="ff377-385">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="ff377-386">Bu dosyalar, proje sistem içinde bunların nasıl kullanılacağını açıklayan özniteliklerinin kümesiyle belirtilir:</span><span class="sxs-lookup"><span data-stu-id="ff377-386">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="ff377-387">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ff377-387">Attribute</span></span> | <span data-ttu-id="ff377-388">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff377-388">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff377-389">**içerir**</span><span class="sxs-lookup"><span data-stu-id="ff377-389">**include**</span></span> | <span data-ttu-id="ff377-390">(Gerekli) Dosya veya dosyalar tarafından belirtilen Dışlamalar tabi dahil etmek için konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ff377-390">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ff377-391">Göreli yol olduğundan `.nuspec` mutlak bir yol belirtilmediği sürece dosya.</span><span class="sxs-lookup"><span data-stu-id="ff377-391">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ff377-392">Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ff377-392">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ff377-393">**hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="ff377-393">**exclude**</span></span> | <span data-ttu-id="ff377-394">Dosya veya dosya desenlerinin ayarlayacağım noktalı virgülle ayrılmış listesini `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="ff377-394">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ff377-395">Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ff377-395">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ff377-396">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="ff377-396">**buildAction**</span></span> | <span data-ttu-id="ff377-397">MSBuild için içerik öğesine gibi atanacak yapı eylemi `Content`, `None`, `Embedded Resource`, `Compile`vb. Varsayılan, `Compile` değeridir.</span><span class="sxs-lookup"><span data-stu-id="ff377-397">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="ff377-398">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="ff377-398">**copyToOutput**</span></span> | <span data-ttu-id="ff377-399">İçerik öğeleri yapı çıktı klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ff377-399">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="ff377-400">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="ff377-400">The default is false.</span></span> |
| <span data-ttu-id="ff377-401">**düzleştirme**</span><span class="sxs-lookup"><span data-stu-id="ff377-401">**flatten**</span></span> | <span data-ttu-id="ff377-402">İçerik öğeleri yapı çıktı (true) tek bir klasöre kopyalayın veya klasör yapısı (false) paketindeki korumak için gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ff377-402">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="ff377-403">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="ff377-403">The default is false.</span></span> |

<span data-ttu-id="ff377-404">Bir paket yüklerken, alt öğelerini NuGet geçerlidir `<contentFiles>` yukarıdan aşağıya.</span><span class="sxs-lookup"><span data-stu-id="ff377-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="ff377-405">Aynı dosyanın eşleşen birden fazla giriş varsa tüm girişleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ff377-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="ff377-406">Aynı öznitelik için bir çakışma varsa en üstteki girişi alt girişleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ff377-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="ff377-407">Paket klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="ff377-407">Package folder structure</span></span>

<span data-ttu-id="ff377-408">Paket proje şu biçimi kullanarak içerik yapısı:</span><span class="sxs-lookup"><span data-stu-id="ff377-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="ff377-409">`codeLanguages`olabilir `cs`, `vb`, `fs`, `any`, veya küçük harf denk bir verilen`$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="ff377-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="ff377-410">`TxM`NuGet destekleyen tüm yasal hedef framework addır (bkz [hedef çerçeveler](../schema/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="ff377-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../schema/target-frameworks.md)).</span></span>
- <span data-ttu-id="ff377-411">Herhangi bir klasör yapısını bu söz dizimini sonuna eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="ff377-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="ff377-412">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ff377-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="ff377-413">Boş klasörler kullanabileceğiniz `.` dil ve TxM, belirli bir kombinasyonu için içerik örneğin sağlama dışında kabul etmek için:</span><span class="sxs-lookup"><span data-stu-id="ff377-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="ff377-414">Örnek Content dosyaları bölümüne</span><span class="sxs-lookup"><span data-stu-id="ff377-414">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="ff377-415">Örnek .nuspec dosyası</span><span class="sxs-lookup"><span data-stu-id="ff377-415">Example .nuspec files</span></span>

<span data-ttu-id="ff377-416">**Basit bir `.nuspec` , bağımlılıkları veya dosyaları belirtmiyor**</span><span class="sxs-lookup"><span data-stu-id="ff377-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="ff377-417">**A `.nuspec` bağımlılıkları**</span><span class="sxs-lookup"><span data-stu-id="ff377-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="ff377-418">**A `.nuspec` dosyalarla**</span><span class="sxs-lookup"><span data-stu-id="ff377-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="ff377-419">**A `.nuspec` framework derlemeler ile**</span><span class="sxs-lookup"><span data-stu-id="ff377-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="ff377-420">Bu örnekte, belirli bir proje hedefleri için aşağıdaki yüklenir:</span><span class="sxs-lookup"><span data-stu-id="ff377-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="ff377-421">. NET4 -> `System.Web`,`System.Net`</span><span class="sxs-lookup"><span data-stu-id="ff377-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="ff377-422">. NET4 İstemci profili ->`System.Net`</span><span class="sxs-lookup"><span data-stu-id="ff377-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="ff377-423">Silverlight 3 ->`System.Json`</span><span class="sxs-lookup"><span data-stu-id="ff377-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="ff377-424">Silverlight 4 ->`System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="ff377-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="ff377-425">WindowsPhone ->`Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="ff377-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
