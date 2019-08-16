---
title: NuGet projesi. JSON Arşivi içeriği
description: Çeşitli proje. JSON içeriği NuGet belgelerinin diğer alanlarından kaldırılmıştır.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 87116669c1e685ffd0dbe4142c2f7e357c413497
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488253"
---
# <a name="projectjson-archive"></a><span data-ttu-id="b0ba3-103">Project. JSON Arşivi</span><span class="sxs-lookup"><span data-stu-id="b0ba3-103">project.json archive</span></span>

<span data-ttu-id="b0ba3-104">`project.json` Yönetim biçimi NuGet 3. x ile tanıtılmıştır ve belirli proje türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="b0ba3-105">Bağımlılıklar doğrudan bir proje dosyasında listelendiğinde, PackageReference biçiminin sunumundan kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="b0ba3-106">Ayrıca bkz.:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-106">Also see:</span></span>

- [<span data-ttu-id="b0ba3-107">Project. JSON şeması</span><span class="sxs-lookup"><span data-stu-id="b0ba3-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="b0ba3-108">paket yazarları üzerinde Project. JSON etkisi</span><span class="sxs-lookup"><span data-stu-id="b0ba3-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="b0ba3-109">project.json ve UWP</span><span class="sxs-lookup"><span data-stu-id="b0ba3-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="b0ba3-110">project.json yönetim biçimi</span><span class="sxs-lookup"><span data-stu-id="b0ba3-110">project.json management format</span></span>

<span data-ttu-id="b0ba3-111">*[Paket geri yükleme](../what-is-nuget.md)' de başlangıçta.*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="b0ba3-112">Yönetim biçimleri listesinde:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-112">In the list of management formats:</span></span>

- <span data-ttu-id="b0ba3-113">[`project.json`](project-json.md): *(kullanım dışı)* proje bağımlılıklarının bir listesini, `project.lock.json`ilişkili bir dosyadaki genel bir paket Graf ile koruyan bir JSON dosyası.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="b0ba3-114">Bu biçim, PackageReference 'ın yararına kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="b0ba3-115">Mono 'da NuGet geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b0ba3-115">nuget restore on Mono</span></span>

<span data-ttu-id="b0ba3-116">*Başlangıçta [NuGet istemci araçları 'Nı yükler](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="b0ba3-117">İle birlikte `project.json`kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="b0ba3-118">Paket sürümlerini restore ile kısıtlama</span><span class="sxs-lookup"><span data-stu-id="b0ba3-118">Constraining package versions with restore</span></span>

<span data-ttu-id="b0ba3-119">*[Paket geri yükleme](../consume-packages/package-restore.md#constrain-package-versions-with-restore)' de başlangıçta.*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="b0ba3-120">`project.json`: Bağımlılık sürüm numarasıyla doğrudan bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="b0ba3-121">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="b0ba3-122">NuGet CLı komutları</span><span class="sxs-lookup"><span data-stu-id="b0ba3-122">NuGet CLI commands</span></span>

- <span data-ttu-id="b0ba3-123">`nuget install`ile `project.json`çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="b0ba3-124">`nuget restore`: kullanan `project.json`projelerle, gerekirse bir `project.lock.json` dosya ve `<project>.nuget.props` dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="b0ba3-125">(Her iki dosya da kaynak denetiminden atlanabilir.) Bağımsız değişkeni bir `project.json` dosyayı işaret edebilir ve bir `packages.config` veya proje dosyasına işaret eden aynı davranışa sahiptir. `<projectPath>`</span><span class="sxs-lookup"><span data-stu-id="b0ba3-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="b0ba3-126">Paket klasörlerinin öncelik sırasına göre, `%userprofile%\.nuget\packages` kullanılırken `project.json`ilk olarak aranır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="b0ba3-127">`nuget update`: Mono 'da, bu komut kullanılarak `project.json`projelerle çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="b0ba3-128">PackageReference ile bağımlılık çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="b0ba3-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="b0ba3-129">*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-129">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="b0ba3-130">PackageReference davranışı için `project.json`de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="b0ba3-131">NuGet geri yükleme, bağımlılık grafiğini, adlı `project.lock.json` `project.json`bir dosyaya yazar.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="b0ba3-132">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b0ba3-132">Managing dependency assets</span></span>

<span data-ttu-id="b0ba3-133">*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-133">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="b0ba3-134">`project.json` Biçimini kullanırken, hangi varlıkların bağımlılıklardan en üst düzey projeye akabildiğini denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="b0ba3-135">Ayrıntılar için bkz. [Project. JSON](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="b0ba3-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="b0ba3-136">Başvuruları dışlama</span><span class="sxs-lookup"><span data-stu-id="b0ba3-136">Excluding references</span></span>

<span data-ttu-id="b0ba3-137">*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-137">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="b0ba3-138">`project.json`: PackageC `"exclude" : "all"` için bağımlılığa ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="b0ba3-139">Uyumsuz paket hatalarını çözme</span><span class="sxs-lookup"><span data-stu-id="b0ba3-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="b0ba3-140">*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-140">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="b0ba3-141">Hatanın çözümlenme yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="b0ba3-142">**Önerilmez**: paket yazarıyla `netcore` `netstandard`çalışırken geçici bir çözüm olarak,,, ve diğer çerçeveleri uyumlu olarak belirtebilir ve `netcoreapp` bu sayede, bu diğer çerçeveleri hedefleyen paketlere izin verebilir kullanılacak çerçeveler.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="b0ba3-143">Bkz. [Project. JSON içeri aktarmaları](project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="b0ba3-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="b0ba3-144">Bu, beklenmeyen davranışlara neden olabilir, bu nedenle bir güncelleştirmede paket yazarıyla çalışarak paket uyumsuzluklarını çözmeniz en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="b0ba3-145">Hedef çerçeveler</span><span class="sxs-lookup"><span data-stu-id="b0ba3-145">Target frameworks</span></span>

<span data-ttu-id="b0ba3-146">*Başlangıçta [hedef çerçeveler](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="b0ba3-147">[Project. JSON](project-json.md): `frameworks` Düğüm, projenin derlenebilecek çerçeve sürümlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="b0ba3-148">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0ba3-148">Creating a package</span></span>

<span data-ttu-id="b0ba3-149">*Başlangıçta [paket oluşturma](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="b0ba3-150">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="b0ba3-150">Setting a package type</span></span>

<span data-ttu-id="b0ba3-151">.NET Core 1. x ile bir dotnetclientool paketi yüklendiğinde, Visual Studio paketi `project.json` `tools` `dependencies` düğüm yerine düğümüne koyar.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="b0ba3-152">Paket türleri içinde `project.json`ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="b0ba3-153">`project.json`: Paket türünü JSON `packOptions.packageType` özelliği içinde belirtin:</span><span class="sxs-lookup"><span data-stu-id="b0ba3-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="b0ba3-154">MSBuild için hedef ve özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="b0ba3-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="b0ba3-155">*İlk olarak [Visual Studio 2015 ile .NET Standard NuGet paketleri oluşturun](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="b0ba3-156">Kullanırken `project.json`, hedefler projeye eklenmez, `project.lock.json`ancak aracılığıyla kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="b0ba3-157">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0ba3-157">Package versioning</span></span>

<span data-ttu-id="b0ba3-158">*[Paket sürümü oluşturma](../concepts/package-versioning.md)' da başlangıçta.*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-158">*Originally in [Package versioning](../concepts/package-versioning.md).*</span></span>

<span data-ttu-id="b0ba3-159">`project.json` Biçim kullanılırken, NuGet Ayrıca sayının büyük, küçük, yama ve yayın \*öncesi sonek bölümlerinin bir joker karakter gösterimini kullanmayı da destekler.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="b0ba3-160">NuGet. config başvurusu</span><span class="sxs-lookup"><span data-stu-id="b0ba3-160">NuGet.Config reference</span></span>

<span data-ttu-id="b0ba3-161">*İlk olarak [NuGet. config başvurusu](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="b0ba3-162">`globalPackagesFolder`yalnızca için `project.json`geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="b0ba3-163">(Eklenen Note: PackageReference için de geçerlidir.)</span><span class="sxs-lookup"><span data-stu-id="b0ba3-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="b0ba3-164">nuspec dosya başvurusu</span><span class="sxs-lookup"><span data-stu-id="b0ba3-164">nuspec file reference</span></span>

<span data-ttu-id="b0ba3-165">*[Nuspec başvurusunda](../reference/nuspec.md)başlangıçta.*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="b0ba3-166">`<contentFiles>` Öğesi`<files>` yerine`project.json`kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="b0ba3-167">Paket Yöneticisi seçenekler denetimi</span><span class="sxs-lookup"><span data-stu-id="b0ba3-167">Package manager options control</span></span>

<span data-ttu-id="b0ba3-168">*[Paket Yöneticisi Kullanıcı arabirimi başvurusunda](../consume-packages/install-use-packages-visual-studio.md)başlangıçta.*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-168">*Originally in [Package Manager UI reference](../consume-packages/install-use-packages-visual-studio.md).*</span></span>

<span data-ttu-id="b0ba3-169">Yönetim biçimi `project.json` kullanan projeler yalnızca **Önizlemeyi göster pencere** seçeneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="b0ba3-170">Visual Studio şablonları</span><span class="sxs-lookup"><span data-stu-id="b0ba3-170">Visual Studio Templates</span></span>

<span data-ttu-id="b0ba3-171">*İlk olarak [Visual Studio şablonlarındaki NuGet paketlerinde](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="b0ba3-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="b0ba3-172">En iyi Yöntemler: Şablonlar bir `project.json` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları ya da içeriği içermez.</span><span class="sxs-lookup"><span data-stu-id="b0ba3-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>