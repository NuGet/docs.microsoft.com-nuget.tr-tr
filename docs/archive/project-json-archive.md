---
title: NuGet project.json arşiv içeriği
description: Çeşitli bitleri project.json içerik NuGet belgeleri diğer alanlarından kaldırıldı.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: aa5cd1a2f3e3a6707a9d68204306db85651b0a18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545206"
---
# <a name="projectjson-archive"></a><span data-ttu-id="30dd7-103">Project.JSON arşiv</span><span class="sxs-lookup"><span data-stu-id="30dd7-103">project.json archive</span></span>

<span data-ttu-id="30dd7-104">`project.json` Yönetim biçimi, NuGet ile tanıtılmıştır 3.x ve belirli proje türleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="30dd7-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="30dd7-105">Bu bağımlılıklar doğrudan proje dosyasında listelenen PackageReference biçimi sunulmasıyla birlikte kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="30dd7-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="30dd7-106">Ayrıca bkz:</span><span class="sxs-lookup"><span data-stu-id="30dd7-106">Also see:</span></span>

- [<span data-ttu-id="30dd7-107">Project.JSON şeması</span><span class="sxs-lookup"><span data-stu-id="30dd7-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="30dd7-108">Paket yazarlarının Project.JSON etkisi</span><span class="sxs-lookup"><span data-stu-id="30dd7-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="30dd7-109">project.json ve UWP</span><span class="sxs-lookup"><span data-stu-id="30dd7-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="30dd7-110">Project.JSON yönetim biçimi</span><span class="sxs-lookup"><span data-stu-id="30dd7-110">project.json management format</span></span>

<span data-ttu-id="30dd7-111">*İlk olarak [paket geri yükleme](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="30dd7-112">Yönetim biçim listesinde:</span><span class="sxs-lookup"><span data-stu-id="30dd7-112">In the list of management formats:</span></span>

- <span data-ttu-id="30dd7-113">[`project.json`](project-json.md): *(kullanım dışı)* genel bir paket grafikte ilişkili bir dosya ile proje bağımlılıklarınızı listesini tutar bir JSON dosyası `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="30dd7-114">Bu biçim ile değiştiriliyor PackageReference kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="30dd7-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="30dd7-115">Mono nuget geri yükleme</span><span class="sxs-lookup"><span data-stu-id="30dd7-115">nuget restore on Mono</span></span>

<span data-ttu-id="30dd7-116">*İlk olarak [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="30dd7-117">Çalışan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="30dd7-118">Geri yükleme ile kısıtlayan paket sürümleri</span><span class="sxs-lookup"><span data-stu-id="30dd7-118">Constraining package versions with restore</span></span>

<span data-ttu-id="30dd7-119">*İlk olarak [paket geri yükleme](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="30dd7-120">`project.json`: Doğrudan bağımlılık'ın sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="30dd7-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="30dd7-121">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="30dd7-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="30dd7-122">NuGet CLI komutları</span><span class="sxs-lookup"><span data-stu-id="30dd7-122">NuGet CLI commands</span></span>

- <span data-ttu-id="30dd7-123">`nuget install` ile çalışmıyor `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="30dd7-124">`nuget restore`: kullanarak projeleri ile `project.json`, oluşturur bir `project.lock.json` dosyası ve bir `<project>.nuget.props` gerekirse dosya.</span><span class="sxs-lookup"><span data-stu-id="30dd7-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="30dd7-125">(Her iki dosya kaynak denetiminden atlanabilir.) `<projectPath>` İşaret edebilir bağımsız değişkeni bir `project.json` dosya ve işaret olarak aynı davranışa sahip bir `packages.config` ya da proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="30dd7-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="30dd7-126">Paket klasörler için öncelik sırasına `%userprofile%\.nuget\packages` kullanırken ilk aranır `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="30dd7-127">`nuget update`: Mono üzerinde bu komutu kullanarak projeleriyle çalışmıyor `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="30dd7-128">PackageReference ile bağımlılık çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="30dd7-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="30dd7-129">*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="30dd7-130">Ayrıca PackageReference davranışını uygular `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="30dd7-131">NuGet geri yükleme, bağımlılık grafiği adlı bir dosyaya yazar `project.lock.json` yanı sıra `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="30dd7-132">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="30dd7-132">Managing dependency assets</span></span>

<span data-ttu-id="30dd7-133">*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="30dd7-134">Kullanırken `project.json` biçimi, üst düzey proje bağımlılıkları akışına hangi varlıklarından denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30dd7-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="30dd7-135">Ayrıntılar için bkz [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="30dd7-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="30dd7-136">Başvuruları hariç</span><span class="sxs-lookup"><span data-stu-id="30dd7-136">Excluding references</span></span>

<span data-ttu-id="30dd7-137">*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="30dd7-138">`project.json`: ekleme `"exclude" : "all"` PackageC için bağımlılık olarak:</span><span class="sxs-lookup"><span data-stu-id="30dd7-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="30dd7-139">Uyumsuz paket hatalarını çözme</span><span class="sxs-lookup"><span data-stu-id="30dd7-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="30dd7-140">*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="30dd7-141">Hataları çözümleme eklenen anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="30dd7-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="30dd7-142">**Tavsiye**: geçici bir çözüm, paket yazarı ile çalışırken, proje hedefleme `netcore`, `netstandard`, ve `netcoreapp` diğer çerçeveler, böylece bu hedefleme paketleri izin vererek, uyumlu olarak belirtmek kullanılacak diğer çerçeveler.</span><span class="sxs-lookup"><span data-stu-id="30dd7-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="30dd7-143">Bkz: [project.json içeri aktarır](project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="30dd7-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="30dd7-144">Bu beklenmeyen davranışlara neden olabilir bir güncelleştirme üzerinde paket yazarı ile çalışarak paket uyumsuzlukları çözmek en iyi şekilde yeniden.</span><span class="sxs-lookup"><span data-stu-id="30dd7-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="30dd7-145">Hedef Çerçeve</span><span class="sxs-lookup"><span data-stu-id="30dd7-145">Target frameworks</span></span>

<span data-ttu-id="30dd7-146">*İlk olarak [hedef çerçeveyi](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="30dd7-147">[Project.JSON](project-json.md): `frameworks` düğüm karşı projenin derlenebilir framework sürümlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="30dd7-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="30dd7-148">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="30dd7-148">Creating a package</span></span>

<span data-ttu-id="30dd7-149">*İlk olarak [paket oluşturma](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="30dd7-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="30dd7-150">Ayar paket türü</span><span class="sxs-lookup"><span data-stu-id="30dd7-150">Setting a package type</span></span>

<span data-ttu-id="30dd7-151">.NET Core ile 1.x DotnetCliTool paketi, Visual Studio paketinde yerleştirir `project.json` `tools` yerine düğüm `dependencies` düğümü.</span><span class="sxs-lookup"><span data-stu-id="30dd7-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="30dd7-152">Paket türlerinin ayarlanır `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="30dd7-153">`project.json`: Paket türü içinde göstermek bir `packOptions.packageType` json özelliği:</span><span class="sxs-lookup"><span data-stu-id="30dd7-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="30dd7-154">MSBuild hedeflerini ve özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="30dd7-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="30dd7-155">*İlk olarak [.NET standart NuGet paketleri ile Visual Studio 2015 oluşturma](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="30dd7-156">Kullanırken `project.json`, hedef projeye eklenmez ancak kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="30dd7-157">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="30dd7-157">Package versioning</span></span>

<span data-ttu-id="30dd7-158">*İlk olarak [Paket sürümü oluşturma](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="30dd7-159">Kullanırken `project.json` biçimi, NuGet ayrıca bir joker karakter gösterimi kullanılmasını destekler \*büyük, küçük, düzeltme eki ve sayının yayın öncesi son bölümü için.</span><span class="sxs-lookup"><span data-stu-id="30dd7-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="30dd7-160">NuGet.Config başvurusu</span><span class="sxs-lookup"><span data-stu-id="30dd7-160">NuGet.Config reference</span></span>

<span data-ttu-id="30dd7-161">*İlk olarak [NuGet.Config başvuru](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="30dd7-162">`globalPackagesFolder` yalnızca geçerli `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="30dd7-163">(Not eklendi: PackageReference için de geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="30dd7-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="30dd7-164">nuspec dosya başvurusu</span><span class="sxs-lookup"><span data-stu-id="30dd7-164">nuspec file reference</span></span>

<span data-ttu-id="30dd7-165">*İlk olarak [nuspec başvuru](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="30dd7-166">`<contentFiles>` Öğe yerine kullanılır `<files>` ile `project.json`.</span><span class="sxs-lookup"><span data-stu-id="30dd7-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="30dd7-167">Paket Yöneticisi seçenekleri denetimi</span><span class="sxs-lookup"><span data-stu-id="30dd7-167">Package manager options control</span></span>

<span data-ttu-id="30dd7-168">*İlk olarak [Paket Yöneticisi kullanıcı Arabirimi başvurusu](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="30dd7-169">Kullanarak projeleri `project.json` yönetim biçimi zobrazit pouze **Show Önizleme penceresini** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="30dd7-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="30dd7-170">Visual Studio şablonları</span><span class="sxs-lookup"><span data-stu-id="30dd7-170">Visual Studio Templates</span></span>

<span data-ttu-id="30dd7-171">*İlk olarak [Visual Studio şablonları NuGet paketlerinde](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="30dd7-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="30dd7-172">En iyi uygulamalar: şablonlar içermez bir `project.json` dosya ve ekleme veya tüm başvuruları veya NuGet paketleri yüklendiğinde eklenir içeriği.</span><span class="sxs-lookup"><span data-stu-id="30dd7-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>