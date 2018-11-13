---
title: NuGet için .nuspec dosyası başvurusu
description: Paket meta verileri bir paketi ve paket tüketicilere bilgi sağlamak için oluştururken kullanılan .nuspec dosyası içerir.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 48f56ec5f042f6e78e38a202f0879c6949e7ee11
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580405"
---
# <a name="nuspec-reference"></a><span data-ttu-id="e614f-103">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="e614f-103">.nuspec reference</span></span>

<span data-ttu-id="e614f-104">A `.nuspec` paket meta verileri içeren bir XML bildirimi dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="e614f-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="e614f-105">Bu bildirim, paket oluşturun ve tüketicilere bilgi sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="e614f-106">Bildirim her zaman bir paketine dahildir.</span><span class="sxs-lookup"><span data-stu-id="e614f-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="e614f-107">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="e614f-107">In this topic:</span></span>

- [<span data-ttu-id="e614f-108">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="e614f-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="e614f-109">[Belirteçleri değiştirme](#replacement-tokens) (Visual Studio projesi ile kullanıldığında)</span><span class="sxs-lookup"><span data-stu-id="e614f-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="e614f-110">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="e614f-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="e614f-111">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="e614f-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="e614f-112">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="e614f-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="e614f-113">Derleme dosyaları da dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="e614f-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="e614f-114">İçerik dosyaları dahil</span><span class="sxs-lookup"><span data-stu-id="e614f-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="e614f-115">Örneğin nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="e614f-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="e614f-116">Genel form ve şema</span><span class="sxs-lookup"><span data-stu-id="e614f-116">General form and schema</span></span>

<span data-ttu-id="e614f-117">Geçerli `nuspec.xsd` şema dosyası bulunabilir [NuGet GitHub deposu](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="e614f-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="e614f-118">Bu şema içinde bir `.nuspec` dosyası aşağıdaki genel form vardır:</span><span class="sxs-lookup"><span data-stu-id="e614f-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="e614f-119">Şema NET bir görsel bir temsili şema dosyasını Visual Studio'da Tasarım modunda açın ve tıklayarak **XML Şeması Gezgini** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e614f-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="e614f-120">Alternatif olarak, kod olarak dosyasını açın, Düzenleyicisi'nde sağ tıklatın ve seçin **XML Şeması Gezgini Göster**.</span><span class="sxs-lookup"><span data-stu-id="e614f-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="e614f-121">Her iki şekilde (çoğunlukla genişletildiğinde) aşağıdaki gibi bir görünümü açılır:</span><span class="sxs-lookup"><span data-stu-id="e614f-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio şema Gezgini ile nuspec.xsd Aç](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="e614f-123">Gerekli meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="e614f-123">Required metadata elements</span></span>

<span data-ttu-id="e614f-124">Aşağıdaki öğeleri bir paket için en düşük gereksinimler olsa da, eklemeyi düşünmelidir [isteğe bağlı meta veri öğeleri](#optional-metadata-elements) genel deneyimini iyileştirmek için paketinizle birlikte geliştiricileri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e614f-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="e614f-125">Bu öğeleri içinde görünmelidir bir `<metadata>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e614f-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="e614f-126">kimlik</span><span class="sxs-lookup"><span data-stu-id="e614f-126">id</span></span> 
<span data-ttu-id="e614f-127">Nuget.org veya ne olursa olsun arasında benzersiz olması gereken büyük küçük harf duyarsız paket tanımlayıcısı galeri paketi bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="e614f-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="e614f-128">Kimlikleri değil boşluk ya da bir URL için geçerli olmayan karakterler içeren ve genellikle .NET ad alanı kuralları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e614f-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="e614f-129">Bkz: [benzersiz paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="e614f-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="e614f-130">sürüm</span><span class="sxs-lookup"><span data-stu-id="e614f-130">version</span></span>
<span data-ttu-id="e614f-131">Aşağıdaki Paket sürümü *ana.İkincil.yama* deseni.</span><span class="sxs-lookup"><span data-stu-id="e614f-131">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="e614f-132">Sürüm numaraları, yayın öncesi son içerebilir, açıklandığı [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="e614f-132">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="e614f-133">açıklama</span><span class="sxs-lookup"><span data-stu-id="e614f-133">description</span></span>
<span data-ttu-id="e614f-134">Kullanıcı Arabirimi ekranı için paketinin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="e614f-134">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="e614f-135">Yazarları</span><span class="sxs-lookup"><span data-stu-id="e614f-135">authors</span></span>
<span data-ttu-id="e614f-136">Nuget.org profil adları eşleşen paketleri yazar, virgülle ayrılmış listesi. Bunlar nuget.org NuGet galerisinde görüntülenir ve paketleri çapraz başvuru için aynı yazarları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-136">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="e614f-137">İsteğe bağlı meta veri öğeleri</span><span class="sxs-lookup"><span data-stu-id="e614f-137">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="e614f-138">Başlık</span><span class="sxs-lookup"><span data-stu-id="e614f-138">title</span></span>
<span data-ttu-id="e614f-139">Nuget.org ve Visual Studio'da Paket Yöneticisi UI görünümlerde genellikle kullanılan paket bir insan dostu başlığı.</span><span class="sxs-lookup"><span data-stu-id="e614f-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="e614f-140">Belirtilmezse, paket kimliği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-140">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="e614f-141">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="e614f-141">owners</span></span>
<span data-ttu-id="e614f-142">Nuget.org adresinden profil adları kullanarak paket creators virgülle ayrılmış listesi. Bu genellikle aynı liste olarak olur `authors`ve nuget.org için paket karşıya yüklenirken göz ardı edilir. Bkz: [yönetme paket sahipleri nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="e614f-142">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="e614f-143">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="e614f-143">projectUrl</span></span>
<span data-ttu-id="e614f-144">Genellikle kullanıcı Arabiriminde gösterilir paketin giriş sayfası için bir URL yanı sıra nuget.org görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e614f-144">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="e614f-145">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="e614f-145">licenseUrl</span></span>
<span data-ttu-id="e614f-146">Genellikle kullanıcı Arabirimi görüntüler yanı sıra nuget.org adresinde gösterilir, paketi lisansının URL'si.</span><span class="sxs-lookup"><span data-stu-id="e614f-146">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="e614f-147">IconUrl</span><span class="sxs-lookup"><span data-stu-id="e614f-147">iconUrl</span></span>
<span data-ttu-id="e614f-148">Kullanıcı Arabirimi ekranı pakette için simge olarak kullanılacak bir URL saydam arka plana sahip 64 x 64 görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="e614f-148">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="e614f-149">Bu öğe içerdiğinden emin olun *resim URL'si doğrudan* ve görüntü içeren bir web sayfasının URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="e614f-149">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="e614f-150">Örneğin, github'dan bir görüntüyü kullanmak için URL gibi ham dosyasını kullanın. <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="e614f-150">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="e614f-151">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="e614f-151">requireLicenseAcceptance</span></span>
<span data-ttu-id="e614f-152">İstemci paketi yüklemeden önce paket lisansını kabul etmek için tüketici sor olup olmadığını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e614f-152">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="e614f-153">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="e614f-153">developmentDependency</span></span>
<span data-ttu-id="e614f-154">*(2.8+)* Paket olup olmadığını belirten bir Boole değeri, bir geliştirme-yalnızca-paket bağımlılık diğer paketleri olarak eklenmesini engelleyen bağımlılık olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="e614f-154">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="e614f-155">PackageReference (NuGet 4.8 +) bu bayrağı Ayrıca, derleme zamanı varlıklar derlemeden dışladığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e614f-155">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="e614f-156">Bkz: [PackageReference DevelopmentDependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="e614f-156">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="e614f-157">özet</span><span class="sxs-lookup"><span data-stu-id="e614f-157">summary</span></span>
<span data-ttu-id="e614f-158">Kullanıcı Arabirimi ekranı için paket kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="e614f-158">A short description of the package for UI display.</span></span> <span data-ttu-id="e614f-159">Atlanırsa, kesilmiş bir sürümünü `description` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-159">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="e614f-160">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="e614f-160">releaseNotes</span></span>
<span data-ttu-id="e614f-161">*(1.5+)* Kullanıcı arabiriminde gibi sık kullanılan paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesini, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine.</span><span class="sxs-lookup"><span data-stu-id="e614f-161">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="e614f-162">telif hakkı</span><span class="sxs-lookup"><span data-stu-id="e614f-162">copyright</span></span>
<span data-ttu-id="e614f-163">*(1.5+)* Ayrıntıları paketi için telif hakkı.</span><span class="sxs-lookup"><span data-stu-id="e614f-163">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="e614f-164">dil</span><span class="sxs-lookup"><span data-stu-id="e614f-164">language</span></span>
<span data-ttu-id="e614f-165">Paket için yerel ayar kimliği.</span><span class="sxs-lookup"><span data-stu-id="e614f-165">The locale ID for the package.</span></span> <span data-ttu-id="e614f-166">Bkz: [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e614f-166">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="e614f-167">etiketler</span><span class="sxs-lookup"><span data-stu-id="e614f-167">tags</span></span>
<span data-ttu-id="e614f-168">Etiketleri ve arama ve filtreleme yoluyla paketleri paket ve ürettiği bulunabilirliğini tanımlayan anahtar sözcükleri boşlukla ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="e614f-168">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="e614f-169">tutulabilmesi</span><span class="sxs-lookup"><span data-stu-id="e614f-169">serviceable</span></span> 
<span data-ttu-id="e614f-170">*(3.3+)* Yalnızca iç NuGet için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e614f-170">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="e614f-171">depo</span><span class="sxs-lookup"><span data-stu-id="e614f-171">repository</span></span>
<span data-ttu-id="e614f-172">Depo meta verileri, dört isteğe bağlı özniteliklerden oluşan: *türü* ve *url* *(4.0 +)*, ve *dal* ve  *işleme* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="e614f-172">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="e614f-173">Bu öznitelikler, alma olasılığı ile oluşturulan depo .nupkg eşlemek izin tek tek bir dalı veya da paket yerleşik işleme olarak ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="e614f-173">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="e614f-174">Bu, doğrudan bir sürüm denetim yazılımı tarafından çağrılabilen genel kullanıma açık bir url olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e614f-174">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="e614f-175">Bu bilgisayar için tasarlanmıştır olarak html sayfasından olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e614f-175">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="e614f-176">Proje sayfasına bağlamak için kullanın `projectUrl` , bunun yerine alan.</span><span class="sxs-lookup"><span data-stu-id="e614f-176">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="e614f-177">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="e614f-177">minClientVersion</span></span>
<span data-ttu-id="e614f-178">Nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yüklemek NuGet istemci en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="e614f-178">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="e614f-179">Bu paket belirli özelliklere bağımlı olduğunda kullanılır `.nuspec` belirli bir NuGet istemcisi sürümünde eklenen dosya.</span><span class="sxs-lookup"><span data-stu-id="e614f-179">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="e614f-180">Örneğin, bir paketini kullanarak `developmentDependency` özniteliği için "2.8" belirtmelidir `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="e614f-180">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="e614f-181">Benzer şekilde, bir paketini kullanarak `contentFiles` öğesi (sonraki bölüme bakın) ayarlamalıdır `minClientVersion` "3.3" için.</span><span class="sxs-lookup"><span data-stu-id="e614f-181">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="e614f-182">Bu bayrak, 2.5 önce NuGet istemcileri algılanmadığı için de unutmayın bunlar *her zaman* ne olursa olsun paketi yüklemek Reddet `minClientVersion` içerir.</span><span class="sxs-lookup"><span data-stu-id="e614f-182">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="e614f-183">Koleksiyon öğeleri</span><span class="sxs-lookup"><span data-stu-id="e614f-183">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="e614f-184">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="e614f-184">packageTypes</span></span>
<span data-ttu-id="e614f-185">*(3.5 +)*  Sıfır veya daha fazla koleksiyonu `<packageType>` dışında geleneksel bağımlılık paket, paketin türünü belirleyen öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-185">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="e614f-186">Her bir packageType öznitelikleri *adı* ve *sürüm*.</span><span class="sxs-lookup"><span data-stu-id="e614f-186">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="e614f-187">Bkz: [ayar paket türü](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="e614f-187">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="e614f-188">bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="e614f-188">dependencies</span></span>
<span data-ttu-id="e614f-189">Sıfır veya daha fazla koleksiyonu `<dependency>` paket için bağımlılıkları belirtme öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-189">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="e614f-190">Her bir bağımlılığı özniteliklerini *kimliği*, *sürüm*, *dahil* (3.x+) ve *hariç* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="e614f-190">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="e614f-191">Bkz: [bağımlılıkları](#dependencies-element) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="e614f-191">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="e614f-192">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="e614f-192">frameworkAssemblies</span></span>
<span data-ttu-id="e614f-193">*(1.2 +)*  Sıfır veya daha fazla koleksiyonu `<frameworkAssembly>` öğeleri, bu paket gerekli .NET Framework derleme başvurularını tanımlamak da sağlar başvurular paketi kullanan projeler için eklenir.</span><span class="sxs-lookup"><span data-stu-id="e614f-193">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="e614f-194">Her frameworkAssembly sahip *assemblyName* ve *targetFramework* öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-194">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="e614f-195">Bkz: [framework derlemesi belirterek başvuran GAC](#specifying-framework-assembly-references-gac) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="e614f-195">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="e614f-196">başvurular</span><span class="sxs-lookup"><span data-stu-id="e614f-196">references</span></span>
<span data-ttu-id="e614f-197">*(1.5 +)*  Sıfır veya daha fazla koleksiyonu `<reference>` paketin derlemelerde adlandırma öğeleri `lib` proje başvuru olarak eklediğiniz klasörü.</span><span class="sxs-lookup"><span data-stu-id="e614f-197">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="e614f-198">Her başvuru bir *dosya* özniteliği.</span><span class="sxs-lookup"><span data-stu-id="e614f-198">Each reference has a *file* attribute.</span></span> <span data-ttu-id="e614f-199">`<references>` de içerebilir bir `<group>` öğesi ile bir *targetFramework* ardından içeren öznitelik `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-199">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="e614f-200">Atlanırsa, tüm başvuruları `lib` dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e614f-200">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="e614f-201">Bkz: [açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="e614f-201">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="e614f-202">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e614f-202">contentFiles</span></span>
<span data-ttu-id="e614f-203">*(3.3 +)*  Koleksiyonunu `<files>` alıcı projeye eklenecek içerik dosyaları tanımlayan öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-203">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="e614f-204">Bu dosyaları nasıl bunlar içinde proje sisteminin kullanılması gerektiğini açıklayan öznitelikler kümesi ile belirtilir.</span><span class="sxs-lookup"><span data-stu-id="e614f-204">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="e614f-205">Bkz: [dosyalar paket içerisine dâhil etmek belirtme](#specifying-files-to-include-in-the-package) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="e614f-205">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="e614f-206">dosyaları</span><span class="sxs-lookup"><span data-stu-id="e614f-206">files</span></span> 
<span data-ttu-id="e614f-207">`<package>` Düğüm içerebilir bir `<files>` düğümü bir eşdüzeyi olarak `<metadata>`ve `<contentFiles>` altında alt `<metadata>`paket içerisine dâhil etmek hangi derleme ve içerik dosyaları belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="e614f-207">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="e614f-208">Bkz: [derleme dosyaları da dahil olmak üzere](#including-assembly-files) ve [içerik dosyaları dahil olmak üzere](#including-content-files) Ayrıntılar için bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="e614f-208">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="e614f-209">Belirteçleri değiştirme</span><span class="sxs-lookup"><span data-stu-id="e614f-209">Replacement tokens</span></span>

<span data-ttu-id="e614f-210">Bir paket oluştururken [ `nuget pack` komut](../tools/cli-ref-pack.md) $ayrılmış belirteçler değiştirir `.nuspec` dosyanın `<metadata>` düğümü'nden ya da proje dosyası gelen değerlerle veya `pack` komutunun `-properties`geçin.</span><span class="sxs-lookup"><span data-stu-id="e614f-210">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="e614f-211">Komut satırında belirttiğiniz belirteci değerlerle `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="e614f-211">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="e614f-212">Örneğin, bir belirteç gibi kullanabileceğiniz `$owners$` ve `$desc$` içinde `.nuspec` ve saat gibi paketleme sırasında değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="e614f-212">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="e614f-213">Bir projeden değerleri kullanmak için aşağıdaki tabloda açıklanan belirteçleri belirtin (dosyasında başvurduğu AssemblyInfo `Properties` gibi `AssemblyInfo.cs` veya `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="e614f-213">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="e614f-214">Bu belirteçleri kullanmak için çalıştırın `nuget pack` proje dosyası yerine yalnızca `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e614f-214">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="e614f-215">Örneğin aşağıdaki komutu kullanarak, `$id$` ve `$version$` içinde belirteçleri bir `.nuspec` dosyası proje değiştirilmiş `AssemblyName` ve `AssemblyVersion` değerleri:</span><span class="sxs-lookup"><span data-stu-id="e614f-215">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="e614f-216">Genellikle, sahip olduğunuz bir proje oluşturduğunuzda `.nuspec` başlangıçta kullanarak `nuget spec MyProject.csproj` otomatik olarak içeren bazı standart bu belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-216">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="e614f-217">Ancak, bir proje için değerler yoksa gerekli `.nuspec` öğeleri, ardından `nuget pack` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e614f-217">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="e614f-218">Ayrıca, Proje değeri değiştirirseniz, paket oluşturmadan önce yeniden emin olun; Bu paketi komut ile kolayca yapılabilir `build` geçin.</span><span class="sxs-lookup"><span data-stu-id="e614f-218">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="e614f-219">Dışında `$configuration$`, projedeki değerleri herhangi bir komut satırında aynı belirtece atanan yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-219">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="e614f-220">Belirteç</span><span class="sxs-lookup"><span data-stu-id="e614f-220">Token</span></span> | <span data-ttu-id="e614f-221">Değer kaynağı</span><span class="sxs-lookup"><span data-stu-id="e614f-221">Value source</span></span> | <span data-ttu-id="e614f-222">Değer</span><span class="sxs-lookup"><span data-stu-id="e614f-222">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="e614f-223">**$id$**</span><span class="sxs-lookup"><span data-stu-id="e614f-223">**$id$**</span></span> | <span data-ttu-id="e614f-224">Proje dosyası</span><span class="sxs-lookup"><span data-stu-id="e614f-224">Project file</span></span> | <span data-ttu-id="e614f-225">Proje dosyasında AssemblyName (başlık)</span><span class="sxs-lookup"><span data-stu-id="e614f-225">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="e614f-226">**$version$**</span><span class="sxs-lookup"><span data-stu-id="e614f-226">**$version$**</span></span> | <span data-ttu-id="e614f-227">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e614f-227">AssemblyInfo</span></span> | <span data-ttu-id="e614f-228">AssemblyInformationalVersion varsa, aksi takdirde AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="e614f-228">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="e614f-229">**$authors$**</span><span class="sxs-lookup"><span data-stu-id="e614f-229">**$authors$**</span></span> | <span data-ttu-id="e614f-230">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e614f-230">AssemblyInfo</span></span> | <span data-ttu-id="e614f-231">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="e614f-231">AssemblyCompany</span></span> |
| <span data-ttu-id="e614f-232">**$title$**</span><span class="sxs-lookup"><span data-stu-id="e614f-232">**$title$**</span></span> | <span data-ttu-id="e614f-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e614f-233">AssemblyInfo</span></span> | <span data-ttu-id="e614f-234">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="e614f-234">AssemblyTitle</span></span> |
| <span data-ttu-id="e614f-235">**$description$**</span><span class="sxs-lookup"><span data-stu-id="e614f-235">**$description$**</span></span> | <span data-ttu-id="e614f-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e614f-236">AssemblyInfo</span></span> | <span data-ttu-id="e614f-237">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="e614f-237">AssemblyDescription</span></span> |
| <span data-ttu-id="e614f-238">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="e614f-238">**$copyright$**</span></span> | <span data-ttu-id="e614f-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="e614f-239">AssemblyInfo</span></span> | <span data-ttu-id="e614f-240">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="e614f-240">AssemblyCopyright</span></span> |
| <span data-ttu-id="e614f-241">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="e614f-241">**$configuration$**</span></span> | <span data-ttu-id="e614f-242">Derleme DLL</span><span class="sxs-lookup"><span data-stu-id="e614f-242">Assembly DLL</span></span> | <span data-ttu-id="e614f-243">Hata ayıklama için varsayılan olarak ayarlanıyor derlemesi oluşturmak için kullanılan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e614f-243">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="e614f-244">Yayın Yapılandırması'nı kullanarak bir paket oluşturmak için her zaman kullanmanız gerektiğini unutmayın `-properties Configuration=Release` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="e614f-244">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="e614f-245">Belirteçleri de kullanılabilir, eklediğinizde yolları çözümlemek için [derleme dosyaları](#including-assembly-files) ve [içerik dosyaları](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="e614f-245">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="e614f-246">Belirteçler, geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyalar seçmek edinerek MSBuild özellikleri olarak aynı ada sahip.</span><span class="sxs-lookup"><span data-stu-id="e614f-246">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="e614f-247">Örneğin, aşağıdaki belirteçler kullanırsanız `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="e614f-247">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="e614f-248">Ve bir derleme, `AssemblyName` olduğu `LoggingLibrary` ile `Release` MSBuild, sonuçta elde edilen satırları yapılandırmasında `.nuspec` paket dosyasında aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e614f-248">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="e614f-249">Bağımlılıklar öğesi</span><span class="sxs-lookup"><span data-stu-id="e614f-249">Dependencies element</span></span>

<span data-ttu-id="e614f-250">`<dependencies>` Öğesiyle `<metadata>` içeren herhangi bir sayıda `<dependency>` en üst düzey paket olduğu diğer paketleri tanımlayan öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-250">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="e614f-251">Her öznitelik `<dependency>` aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e614f-251">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="e614f-252">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="e614f-252">Attribute</span></span> | <span data-ttu-id="e614f-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e614f-253">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="e614f-254">(Gerekli) Bir paketi sayfasında "EntityFramework" ve paket nuget.org adı "NUnit" gibi bir bağımlılık, uygulamanın paket Kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e614f-254">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="e614f-255">(Gerekli) Sürümleri bağımlılık olarak kabul edilebilir aralık.</span><span class="sxs-lookup"><span data-stu-id="e614f-255">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="e614f-256">Bkz: [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards) için söz dizimi.</span><span class="sxs-lookup"><span data-stu-id="e614f-256">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="e614f-257">include</span><span class="sxs-lookup"><span data-stu-id="e614f-257">include</span></span> | <span data-ttu-id="e614f-258">İçerme/dışlama virgülle ayrılmış listesi (aşağıya bakın) son pakette eklenecek bağımlılığın gösteren etiketler.</span><span class="sxs-lookup"><span data-stu-id="e614f-258">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="e614f-259">Varsayılan değer `all` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e614f-259">The default value is `all`.</span></span> |
| <span data-ttu-id="e614f-260">exclude</span><span class="sxs-lookup"><span data-stu-id="e614f-260">exclude</span></span> | <span data-ttu-id="e614f-261">İçerme/dışlama virgülle ayrılmış listesi (aşağıya bakın) son pakette dışlanacak bağımlılığın gösteren etiketler.</span><span class="sxs-lookup"><span data-stu-id="e614f-261">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="e614f-262">Varsayılan değer `build,analyzers` olabilen aşırı yazılmış.</span><span class="sxs-lookup"><span data-stu-id="e614f-262">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="e614f-263">Ancak `content/ ContentFiles` aşırı yazılı olamaz son pakette de örtülü olarak tutulur.</span><span class="sxs-lookup"><span data-stu-id="e614f-263">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="e614f-264">İle belirtilen etiketlere `exclude` ile belirtilenler üzerinde önceliklidir `include`.</span><span class="sxs-lookup"><span data-stu-id="e614f-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="e614f-265">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="e614f-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="e614f-266">Etiket Ekle/Dışla</span><span class="sxs-lookup"><span data-stu-id="e614f-266">Include/Exclude tag</span></span> | <span data-ttu-id="e614f-267">Etkilenen hedef klasör</span><span class="sxs-lookup"><span data-stu-id="e614f-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="e614f-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e614f-268">contentFiles</span></span> | <span data-ttu-id="e614f-269">İçerik</span><span class="sxs-lookup"><span data-stu-id="e614f-269">Content</span></span> |
| <span data-ttu-id="e614f-270">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="e614f-270">runtime</span></span> | <span data-ttu-id="e614f-271">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="e614f-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="e614f-272">Derleme</span><span class="sxs-lookup"><span data-stu-id="e614f-272">compile</span></span> | <span data-ttu-id="e614f-273">lib</span><span class="sxs-lookup"><span data-stu-id="e614f-273">lib</span></span> |
| <span data-ttu-id="e614f-274">derleme</span><span class="sxs-lookup"><span data-stu-id="e614f-274">build</span></span> | <span data-ttu-id="e614f-275">derleme (MSBuild özellikler ve hedefler)</span><span class="sxs-lookup"><span data-stu-id="e614f-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="e614f-276">yerel</span><span class="sxs-lookup"><span data-stu-id="e614f-276">native</span></span> | <span data-ttu-id="e614f-277">yerel</span><span class="sxs-lookup"><span data-stu-id="e614f-277">native</span></span> |
| <span data-ttu-id="e614f-278">yok</span><span class="sxs-lookup"><span data-stu-id="e614f-278">none</span></span> | <span data-ttu-id="e614f-279">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="e614f-279">No folders</span></span> |
| <span data-ttu-id="e614f-280">tüm</span><span class="sxs-lookup"><span data-stu-id="e614f-280">all</span></span> | <span data-ttu-id="e614f-281">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="e614f-281">All folders</span></span> |

<span data-ttu-id="e614f-282">Örneğin, aşağıdaki satırları üzerinde bağımlılıkları göstermek `PackageA` 1.1.0 sürümü veya sonraki bir sürümünü ve `PackageB` sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="e614f-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="e614f-283">Aşağıdaki satırları aynı paket bağımlılıkları gösterir, ancak dahil edileceğini belirtin `contentFiles` ve `build` klasörleri `PackageA` ve her şeyi ancak `native` ve `compile` klasörleri `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="e614f-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="e614f-284">Not: oluştururken bir `.nuspec` kullanarak proje `nuget spec`, o projede bağımlılıkları otomatik olarak dahil edilecek ortaya çıkan `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="e614f-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="e614f-285">Bağımlılık grupları</span><span class="sxs-lookup"><span data-stu-id="e614f-285">Dependency groups</span></span>

<span data-ttu-id="e614f-286">*Sürüm 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="e614f-286">*Version 2.0+*</span></span>

<span data-ttu-id="e614f-287">Tek bir düz liste alternatif, project kullanarak hedef framework profile göre bağımlılıklar belirtilebilir `<group>` öğeleri içinde `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="e614f-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="e614f-288">Her Grup adlı öznitelikle `targetFramework` ve sıfır veya daha fazlasını içeren `<dependency>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="e614f-289">Hedef Çerçeve proje framework profiliyle uyumlu olduğunda bu bağımlılıkların birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e614f-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="e614f-290">`<group>` Öğe olmadan bir `targetFramework` özniteliği bağımlılıkları varsayılan ya da geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="e614f-291">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="e614f-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="e614f-292">Grubu biçimi karıştırılmış, düz bir liste ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e614f-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="e614f-293">Aşağıdaki örnek, farklı çeşitleri gösterir `<group>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="e614f-293">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="e614f-294">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="e614f-294">Explicit assembly references</span></span>

<span data-ttu-id="e614f-295">`<references>` Öğesi paket kullanırken hedef projeye başvurması gereken derlemelerin açıkça belirtir.</span><span class="sxs-lookup"><span data-stu-id="e614f-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="e614f-296">Bu öğe varsa, NuGet yalnızca listelenen derlemelere başvurular ekleyin; Bu başvurular paketin içinde başka bir derleme için eklemez `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="e614f-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="e614f-297">Örneğin, aşağıdaki `<references>` öğe bildirir yalnızca başvuruları eklemek için NuGet `xunit.dll` ve `xunit.extensions.dll` olsa bile ek derlemeler paketi:</span><span class="sxs-lookup"><span data-stu-id="e614f-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="e614f-298">Açık başvuruları genellikle yalnızca tasarım zamanı derlemeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="e614f-299">Kullanırken [kod sözleşmeleri](/dotnet/framework/debug-trace-profile/code-contracts), örneğin, sözleşme derlemeleri bunlar artırabilir ve böylece Visual Studio bulabilmesi çalışma zamanı derlemeleri yanında olması gerekir, ancak sözleşme derlemeleri olmaması gerekir. proje tarafından başvurulan veya kopyalama projenin içine `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="e614f-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="e614f-300">Benzer şekilde, açık başvuruları araçlarında derlemeler çalışma zamanı derlemeleri yanında bulunan, ancak bunları projeye başvuru olarak dahil gerek yok gereken XUnit gibi birim test çerçeveleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e614f-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="e614f-301">Başvuru grupları</span><span class="sxs-lookup"><span data-stu-id="e614f-301">Reference groups</span></span>

<span data-ttu-id="e614f-302">Tek bir düz liste alternatif, project kullanarak hedef framework profile göre başvuruları belirtilebilir `<group>` öğeleri içinde `<references>`.</span><span class="sxs-lookup"><span data-stu-id="e614f-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="e614f-303">Her Grup adlı öznitelikle `targetFramework` ve sıfır veya daha fazlasını içeren `<reference>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e614f-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="e614f-304">Hedef Çerçeve proje framework profiliyle uyumlu olduğunda bu başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="e614f-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="e614f-305">`<group>` Öğe olmadan bir `targetFramework` özniteliği başvuruları varsayılan ya da geri dönüş listesi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="e614f-306">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="e614f-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="e614f-307">Grubu biçimi karıştırılmış, düz bir liste ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e614f-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="e614f-308">Aşağıdaki örnek, farklı çeşitleri gösterir `<group>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="e614f-308">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="e614f-309">Framework'te derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="e614f-309">Framework assembly references</span></span>

<span data-ttu-id="e614f-310">Framework derlemeleri, .NET framework'ün bir parçasıdır ve herhangi bir makine için genel derleme önbelleğinde (GAC) olması izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="e614f-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="e614f-311">Bu bütünleştirilmiş kodlarında belirleme `<frameworkAssemblies>` öğesi, bir paket sağlayabilirsiniz projesinde bu tür başvurularını zaten yok olay, gerekli başvuruları projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="e614f-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="e614f-312">Bu tür derlemeler, bir paket içinde doğrudan dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="e614f-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="e614f-313">`<frameworkAssemblies>` Sıfır veya daha fazla öğe içeriyor `<frameworkAssembly>` öğeleri, her biri aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="e614f-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="e614f-314">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="e614f-314">Attribute</span></span> | <span data-ttu-id="e614f-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e614f-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e614f-316">**AssemblyName**</span><span class="sxs-lookup"><span data-stu-id="e614f-316">**assemblyName**</span></span> | <span data-ttu-id="e614f-317">(Gerekli) Tam derleme adı.</span><span class="sxs-lookup"><span data-stu-id="e614f-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="e614f-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="e614f-318">**targetFramework**</span></span> | <span data-ttu-id="e614f-319">(İsteğe bağlı) Bu başvuru uygulandığı hedef Framework'ü belirtir.</span><span class="sxs-lookup"><span data-stu-id="e614f-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="e614f-320">Atlanırsa, başvuru için tüm çerçeveleri geçerli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e614f-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="e614f-321">Bkz: [hedef çerçeveyi](../reference/target-frameworks.md) tam framework tanımlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="e614f-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="e614f-322">Aşağıdaki örnek, bir başvuru gösterir `System.Net` için tüm çerçeveleri ve başvuru hedef `System.ServiceModel` yalnızca .NET Framework 4.0 için:</span><span class="sxs-lookup"><span data-stu-id="e614f-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="e614f-323">Derleme dosyaları da dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="e614f-323">Including assembly files</span></span>

<span data-ttu-id="e614f-324">Açıklanan kurallarını takip ederseniz [paket oluşturma](../create-packages/creating-a-package.md), dosyaların bir listesini açıkça belirtmeniz gerekmez `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="e614f-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="e614f-325">`nuget pack` Komutu, gerekli dosyaları otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="e614f-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="e614f-326">Bir projeye bir paketi yüklendiğinde, NuGet paket DLL'leri derleme başvurularını otomatik olarak ekler. *hariç* adlandırılmış olanlar `.resources.dll` çünkü yerelleştirilmiş yardımcı derlemeler olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e614f-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="e614f-327">Bu nedenle, kullanmaktan kaçının `.resources.dll` Aksi takdirde, gerekli paket kodu içeren dosyalar için.</span><span class="sxs-lookup"><span data-stu-id="e614f-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="e614f-328">Bu otomatik davranış atlayabilir ve hangi dosyaların bir paketine dahil edilen açıkça denetlemek için yerleştirin bir `<files>` öğesi alt öğesi olarak `<package>` (ve bir eşdüzeyi `<metadata>`), her dosyayı ayrı bir tanımlamak `<file>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e614f-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="e614f-329">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e614f-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="e614f-330">İle NuGet 2.x ve önceki sürümleri ve kullanarak projeleri `packages.config`, `<files>` öğesi bir paketi yüklendiğinde sabit içerik dosyalarını eklemek için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="e614f-331">NuGet 3.3 + ve projeleri PackageReference, `<contentFiles>` öğe yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e614f-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="e614f-332">Bkz: [içerik dosyaları dahil olmak üzere](#including-content-files) altındaki ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="e614f-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="e614f-333">Dosya öğesi öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="e614f-333">File element attributes</span></span>

<span data-ttu-id="e614f-334">Her `<file>` öğesi aşağıdaki öznitelikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="e614f-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="e614f-335">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="e614f-335">Attribute</span></span> | <span data-ttu-id="e614f-336">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e614f-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e614f-337">**src**</span><span class="sxs-lookup"><span data-stu-id="e614f-337">**src**</span></span> | <span data-ttu-id="e614f-338">Tarafından belirtilen dışlamaları tabi dahil edilecek dosyalar ve dosya konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="e614f-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="e614f-339">Yolun göreli olduğu `.nuspec` mutlak bir yol belirtilmezse dosya.</span><span class="sxs-lookup"><span data-stu-id="e614f-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="e614f-340">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e614f-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e614f-341">**Hedef**</span><span class="sxs-lookup"><span data-stu-id="e614f-341">**target**</span></span> | <span data-ttu-id="e614f-342">Klasörün başlamalıdır. burada kaynak dosyaları yerleştirilir, paket içindeki göreli yolu `lib`, `content`, `build`, veya `tools`.</span><span class="sxs-lookup"><span data-stu-id="e614f-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="e614f-343">Bkz: [kural tabanlı bir çalışma dizininden bir .nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="e614f-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="e614f-344">**Hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="e614f-344">**exclude**</span></span> | <span data-ttu-id="e614f-345">Dışlanacak dosya desenlerinin veya dosyaların noktalı virgülle ayrılmış listesi `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="e614f-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="e614f-346">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e614f-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="e614f-347">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e614f-347">Examples</span></span>

<span data-ttu-id="e614f-348">**Tek derleme**</span><span class="sxs-lookup"><span data-stu-id="e614f-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="e614f-349">**Belirli bir hedef çerçeve için tek bir derleme**</span><span class="sxs-lookup"><span data-stu-id="e614f-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="e614f-350">**Joker karakter kullanarak DLL'leri kümesi**</span><span class="sxs-lookup"><span data-stu-id="e614f-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="e614f-351">**Farklı çerçeveler için DLL'leri**</span><span class="sxs-lookup"><span data-stu-id="e614f-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="e614f-352">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="e614f-352">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="e614f-353">İçerik dosyaları dahil</span><span class="sxs-lookup"><span data-stu-id="e614f-353">Including content files</span></span>

<span data-ttu-id="e614f-354">İçerik dosyaları bir proje eklemek için bir paket gereken sabit dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="e614f-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="e614f-355">Sabit olduğundan, bunlar kullanan proje tarafından değiştirilmesi kullanılmaya yönelik değildir.</span><span class="sxs-lookup"><span data-stu-id="e614f-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="e614f-356">Örnek içerik dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="e614f-356">Example content files include:</span></span>

- <span data-ttu-id="e614f-357">Kaynak olarak gömülü görüntü</span><span class="sxs-lookup"><span data-stu-id="e614f-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="e614f-358">Önceden derlenmiş kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="e614f-358">Source files that are already compiled</span></span>
- <span data-ttu-id="e614f-359">Proje derleme çıktısı ile dahil edilmesi gereken komut</span><span class="sxs-lookup"><span data-stu-id="e614f-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="e614f-360">Projeye özgü herhangi bir değişiklik gerekmez ancak projeye dahil edilmesi gereken bir paket için yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="e614f-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="e614f-361">İçerik paketini kullanarak dosyaları eklenir `<files>` öğesini belirterek `content` klasöründe `target` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="e614f-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="e614f-362">Bunun yerine kullanan PackageReference kullanarak bir proje paketi yüklendiğinde, ancak bu tür dosyaları göz ardı edilir `<contentFiles>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e614f-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="e614f-363">Projeleri tüketen ile en fazla uyumluluk için bir paket içerik dosyalarını ideal olarak her iki öğeleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="e614f-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="e614f-364">Dosya öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="e614f-364">Using the files element for content files</span></span>

<span data-ttu-id="e614f-365">İçerik dosyaları için yalnızca derleme dosyalarında olduğu gibi aynı biçimi kullanır, ancak belirtin `content` temel klasör olarak `target` özniteliği aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e614f-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="e614f-366">**Temel içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e614f-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="e614f-367">**Dizin yapısı ile içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e614f-367">**Content files with directory structure**</span></span>

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

<span data-ttu-id="e614f-368">**İçerik dosyası için bir hedef çerçeve belirli**</span><span class="sxs-lookup"><span data-stu-id="e614f-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="e614f-369">**İçerik dosya adı nokta olan bir klasöre kopyalandı**</span><span class="sxs-lookup"><span data-stu-id="e614f-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="e614f-370">Bu durumda, NuGet görür uzantı `target` uzantı eşleşmiyor `src` ve bu nedenle bu bölümü adı değerlendirir `target` klasörü olarak:</span><span class="sxs-lookup"><span data-stu-id="e614f-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="e614f-371">**Uzantısız içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e614f-371">**Content files without extensions**</span></span>

<span data-ttu-id="e614f-372">Uzantısız dosyaları eklenip eklenmeyeceğini kullanın `*` veya `**` joker karakterleri:</span><span class="sxs-lookup"><span data-stu-id="e614f-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="e614f-373">**Ayrıntılı yolu ve ayrıntılı hedef içerik dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e614f-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="e614f-374">Bu durumda, kaynak ve hedef dosya uzantılarını aynı gerektiğinden, NuGet hedef dosya adını ve bir klasör olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="e614f-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="e614f-375">**Paketteki içerik bir dosyayı yeniden adlandırma**</span><span class="sxs-lookup"><span data-stu-id="e614f-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="e614f-376">**Dosyaları dışlama**</span><span class="sxs-lookup"><span data-stu-id="e614f-376">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="e614f-377">ContentFiles öğesi için içerik dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="e614f-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="e614f-378">*NuGet 4.0 + PackageReference ile*</span><span class="sxs-lookup"><span data-stu-id="e614f-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="e614f-379">Varsayılan olarak, bir paket içeriği yerleştirir bir `contentFiles` klasörü (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları dahil.</span><span class="sxs-lookup"><span data-stu-id="e614f-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="e614f-380">Bu durumda eklenmesi gerekli değil bir `contentFiles` düğümünde `.nuspec` hiç.</span><span class="sxs-lookup"><span data-stu-id="e614f-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="e614f-381">Hangi dosyaların dahil olduğunu denetlemek için `<contentFiles>` öğeyi belirten bir koleksiyonu `<files>` tam dosyaları tanımlayan öğeleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e614f-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="e614f-382">Bu dosyaları nasıl bunlar içinde proje sisteminin kullanılması gerektiğini açıklayan öznitelikler kümesi ile belirtilir:</span><span class="sxs-lookup"><span data-stu-id="e614f-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="e614f-383">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="e614f-383">Attribute</span></span> | <span data-ttu-id="e614f-384">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e614f-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e614f-385">**include**</span><span class="sxs-lookup"><span data-stu-id="e614f-385">**include**</span></span> | <span data-ttu-id="e614f-386">(Gerekli) Tarafından belirtilen dışlamaları tabi dahil edilecek dosyalar ve dosya konumunu `exclude` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="e614f-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="e614f-387">Yolun göreli olduğu `.nuspec` mutlak bir yol belirtilmezse dosya.</span><span class="sxs-lookup"><span data-stu-id="e614f-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="e614f-388">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e614f-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e614f-389">**Hariç tutma**</span><span class="sxs-lookup"><span data-stu-id="e614f-389">**exclude**</span></span> | <span data-ttu-id="e614f-390">Dışlanacak dosya desenlerinin veya dosyaların noktalı virgülle ayrılmış listesi `src` konumu.</span><span class="sxs-lookup"><span data-stu-id="e614f-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="e614f-391">Joker karakter `*` izin verilir ve çift joker `**` özyinelemeli klasör arama anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e614f-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="e614f-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="e614f-392">**buildAction**</span></span> | <span data-ttu-id="e614f-393">Derleme eylemi gibi MSBuild için içerik öğesinin atanacağı `Content`, `None`, `Embedded Resource`, `Compile`vb. Varsayılan, `Compile` değeridir.</span><span class="sxs-lookup"><span data-stu-id="e614f-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="e614f-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="e614f-394">**copyToOutput**</span></span> | <span data-ttu-id="e614f-395">Çıkış klasörü yapı içerik öğeleri kopyalama (veya yayımlamak) belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e614f-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="e614f-396">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="e614f-396">The default is false.</span></span> |
| <span data-ttu-id="e614f-397">**flatten**</span><span class="sxs-lookup"><span data-stu-id="e614f-397">**flatten**</span></span> | <span data-ttu-id="e614f-398">İçerik öğeleri derleme çıktı (true) tek bir klasöre kopyalamak ya da klasör yapısını (false) paketindeki korumak için etkinleştirilip etkinleştirilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e614f-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="e614f-399">Bu bayrağı yalnızca copyToOutput bayrak ayarlandığında çalışır true.</span><span class="sxs-lookup"><span data-stu-id="e614f-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="e614f-400">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="e614f-400">The default is false.</span></span> |

<span data-ttu-id="e614f-401">Bir paketi yüklerken NuGet alt öğelerinin geçerlidir `<contentFiles>` yukarıdan.</span><span class="sxs-lookup"><span data-stu-id="e614f-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="e614f-402">Daha sonra aynı dosyanın birden çok girişi eşleşen tüm girişleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e614f-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="e614f-403">Aynı öznitelik için bir çakışma varsa, en üstteki girişe daha aşağıdaki girişler geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="e614f-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="e614f-404">Paket klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="e614f-404">Package folder structure</span></span>

<span data-ttu-id="e614f-405">Şu biçimi kullanarak içerik paketi Proje yapısı:</span><span class="sxs-lookup"><span data-stu-id="e614f-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="e614f-406">`codeLanguages` olabilir `cs`, `vb`, `fs`, `any`, ya da küçük harfli eşdeğeri bir verilen `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="e614f-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="e614f-407">`TxM` NuGet destekleyen herhangi bir geçerli hedef çerçeve adı olan (bkz [hedef çerçeveyi](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="e614f-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="e614f-408">Bu söz dizimi sonuna kadar herhangi bir klasör yapısının eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e614f-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="e614f-409">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e614f-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="e614f-410">Boş klasörler kullanabileceğiniz `.` örneğin dil ve TxM, belirli bir kombinasyonu için içerik sağlama dışında katılmak için:</span><span class="sxs-lookup"><span data-stu-id="e614f-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="e614f-411">Örnek contentFiles bölümünde</span><span class="sxs-lookup"><span data-stu-id="e614f-411">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="e614f-412">Örneğin nuspec dosyaları</span><span class="sxs-lookup"><span data-stu-id="e614f-412">Example nuspec files</span></span>

<span data-ttu-id="e614f-413">**Basit bir `.nuspec` , bağımlılıklar veya dosyaları belirtmiyor**</span><span class="sxs-lookup"><span data-stu-id="e614f-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="e614f-414">**A `.nuspec` bağımlılıklar**</span><span class="sxs-lookup"><span data-stu-id="e614f-414">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="e614f-415">**A `.nuspec` dosyaları**</span><span class="sxs-lookup"><span data-stu-id="e614f-415">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="e614f-416">**A `.nuspec` framework derlemeleri ile**</span><span class="sxs-lookup"><span data-stu-id="e614f-416">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="e614f-417">Bu örnekte, belirli proje hedefleri aşağıdaki yüklenir:</span><span class="sxs-lookup"><span data-stu-id="e614f-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="e614f-418">. NET4 -&GT; `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="e614f-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="e614f-419">. NET4 İstemci profili -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="e614f-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="e614f-420">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="e614f-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="e614f-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="e614f-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="e614f-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="e614f-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
