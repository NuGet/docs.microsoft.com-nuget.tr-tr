---
title: "NuGet project.json arşiv içerik | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Çeşitli BITS project.json içeriğin diğer NuGet belgelerine alanlarından kaldırıldı."
keywords: "NuGet project.json dosyası"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1cca7304ee3dbecaed3fbb337ad2d31f383f4c43
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="6d2e2-104">project.json archive</span><span class="sxs-lookup"><span data-stu-id="6d2e2-104">project.json archive</span></span>

<span data-ttu-id="6d2e2-105">`project.json` Başvuru biçimi NuGet ile sunulmuştur 3.x ve belirli proje türleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-105">The `project.json` reference format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="6d2e2-106">Bağımlılıklar doğrudan proje dosyasında listelenen PackageReference biçimi girişiyle kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="6d2e2-107">Ayrıca bkz.:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-107">Also see:</span></span>

- [<span data-ttu-id="6d2e2-108">project.json schema</span><span class="sxs-lookup"><span data-stu-id="6d2e2-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="6d2e2-109">Paketi yazarları Project.JSON etkisini</span><span class="sxs-lookup"><span data-stu-id="6d2e2-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="6d2e2-110">project.json ve UWP</span><span class="sxs-lookup"><span data-stu-id="6d2e2-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a><span data-ttu-id="6d2e2-111">project.json reference format</span><span class="sxs-lookup"><span data-stu-id="6d2e2-111">project.json reference format</span></span>

<span data-ttu-id="6d2e2-112">*İlk olarak, [paket geri yüklemesi](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="6d2e2-113">Başvuru biçimleri listesinde:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-113">In the list of reference formats:</span></span>

- <span data-ttu-id="6d2e2-114">[`project.json`](project-json.md): *(kullanım dışı)* proje bağımlılıkları ile ilişkili bir dosyası bir genel paket grafiğinde bir listesini tutar bir JSON dosyası `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="6d2e2-115">Bu biçim lehinde PackageReference kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="6d2e2-116">Mono nuget geri yükleme</span><span class="sxs-lookup"><span data-stu-id="6d2e2-116">nuget restore on Mono</span></span>

<span data-ttu-id="6d2e2-117">*İlk olarak, [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="6d2e2-118">İle birlikte çalışır `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="6d2e2-119">Geri yükleme ile kısıtlayan paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="6d2e2-119">Constraining package versions with restore</span></span>

<span data-ttu-id="6d2e2-120">*İlk olarak, [paket geri yüklemesi](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="6d2e2-121">`project.json`: Doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="6d2e2-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="6d2e2-123">NuGet CLI komutları</span><span class="sxs-lookup"><span data-stu-id="6d2e2-123">NuGet CLI commands</span></span>

- <span data-ttu-id="6d2e2-124">`nuget install`ile çalışmaz `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="6d2e2-125">`nuget restore`: kullanarak projeleri ile `project.json`, oluşturan bir `project.lock.json` dosyası ve bir `<project>.nuget.props` gerekirse, dosya.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="6d2e2-126">(Her iki dosyası kaynak denetiminden atlanabilir.) `<projectPath>` Bağımsız değişkeni noktası bir `project.json` işaret olarak aynı davranışı sahiptir ve dosya bir `packages.config` veya proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="6d2e2-127">Paket klasörler için öncelik sırasına `%userprofile%\.nuget\packages` kullanırken ilk aranır `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="6d2e2-128">`nuget update`: Mono üzerinde bu komutu kullanarak projeleri ile çalışmıyor `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="6d2e2-129">PackageReference bir bağımlılık çözümleme</span><span class="sxs-lookup"><span data-stu-id="6d2e2-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="6d2e2-130">*İlk olarak, [bağımlılık çözümlemesi](../Consume-Packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-130">*Originally in [Dependency resolution](../Consume-Packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="6d2e2-131">PackageReference davranışını için de geçerlidir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="6d2e2-132">NuGet restore bağımlılık grafiğinin adlı bir dosyaya yazar `project.lock.json` yanında `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="6d2e2-133">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="6d2e2-133">Managing dependency assets</span></span>

<span data-ttu-id="6d2e2-134">*İlk olarak, [bağımlılık çözümlemesi](../Consume-Packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-134">*Originally in [Dependency resolution](../Consume-Packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="6d2e2-135">Kullanırken `project.json` biçimi, en üst düzey proje bağımlılıkları akışına hangi varlıklarından kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="6d2e2-136">Ayrıntılar için bkz [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="6d2e2-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="6d2e2-137">Başvuruları hariç</span><span class="sxs-lookup"><span data-stu-id="6d2e2-137">Excluding references</span></span>

<span data-ttu-id="6d2e2-138">*İlk olarak, [bağımlılık çözümlemesi](../Consume-Packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-138">*Originally in [Dependency resolution](../Consume-Packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="6d2e2-139">`project.json`: eklemek `"exclude" : "all"` PackageC bağımlılığı içinde:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="6d2e2-140">Uyumsuz paket hatalarını çözme</span><span class="sxs-lookup"><span data-stu-id="6d2e2-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="6d2e2-141">*İlk olarak, [bağımlılık çözümlemesi](../Consume-Packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-141">*Originally in [Dependency resolution](../Consume-Packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="6d2e2-142">Hataları çözümleme eklenen anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="6d2e2-143">**Önerilmez**: geçici bir çözüm olarak için paket yazarına ile çalışırken projeleri hedefleyen `netcore`, `netstandard`, ve `netcoreapp` uyumlu, böylece bu hedefleme paketleri izin verme olarak diğer çerçeveler belirtmek kullanılacak diğer çerçeveler.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="6d2e2-144">Bkz: [project.json alır](project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../schema/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="6d2e2-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../schema/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="6d2e2-145">Bu beklenmeyen davranışları neden şekilde yeniden üzerinde bir güncelleştirme için paket yazarına ile çalışarak paket uyumsuzlukları gidermek en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="6d2e2-146">Hedef Çerçeve</span><span class="sxs-lookup"><span data-stu-id="6d2e2-146">Target frameworks</span></span>

<span data-ttu-id="6d2e2-147">*İlk olarak, [hedef çerçeveler](../schema/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-147">*Originally in [Target frameworks](../schema/target-frameworks.md).*</span></span>

- <span data-ttu-id="6d2e2-148">[Project.JSON](project-json.md): `frameworks` düğümü karşı proje derlenmiş framework sürümlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="6d2e2-149">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d2e2-149">Creating a package</span></span>

<span data-ttu-id="6d2e2-150">*İlk olarak, [paket oluşturma](../Create-Packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-150">*Originally in [Creating a package](../Create-Packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="6d2e2-151">Ayar paket türü</span><span class="sxs-lookup"><span data-stu-id="6d2e2-151">Setting a package type</span></span>

<span data-ttu-id="6d2e2-152">Pakette 1.x, paket yüklü DotnetCliTool, Visual Studio .NET Core ile yerleştirir `project.json` `tools` yerine düğümü `dependencies` düğümü.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="6d2e2-153">Paket türleri ayarlanır `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="6d2e2-154">`project.json`: İçinde paket türünü gösteren bir `packOptions.packageType` özelliği json:</span><span class="sxs-lookup"><span data-stu-id="6d2e2-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="6d2e2-155">MSBuild hedefleri ve özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="6d2e2-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="6d2e2-156">*İlk olarak, [Visual Studio 2015 ile birlikte .NET standart NuGet paketlerini oluşturmak](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="6d2e2-157">Kullanırken `project.json`, hedefleri projeye eklenmez ancak kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="6d2e2-158">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d2e2-158">Package versioning</span></span>

<span data-ttu-id="6d2e2-159">*İlk olarak, [paket sürüm](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="6d2e2-160">Kullanırken `project.json` biçimi, NuGet ayrıca bir joker karakter gösterimini kullanarak destekler \*, birincil, ikincil, düzeltme eki ve sayının yayın öncesi soneki bölümleri için.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="6d2e2-161">NuGet.Config başvurusu</span><span class="sxs-lookup"><span data-stu-id="6d2e2-161">NuGet.Config reference</span></span>

<span data-ttu-id="6d2e2-162">*İlk olarak, [NuGet.Config başvuru](../schema/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-162">*Originally in [NuGet.Config reference](../schema/nuget-config-file.md).*</span></span>

<span data-ttu-id="6d2e2-163">`globalPackagesFolder`yalnızca geçerli `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-163">`globalPackagesFolder` applies only to `project.json`.</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="6d2e2-164">nuspec dosyası başvurusu</span><span class="sxs-lookup"><span data-stu-id="6d2e2-164">nuspec file reference</span></span>

<span data-ttu-id="6d2e2-165">*İlk olarak, [nuspec başvuru](../schema/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-165">*Originally in [nuspec reference](../schema/nuspec.md).*</span></span>

<span data-ttu-id="6d2e2-166">`<contentFiles>` Öğe yerine kullanılır `<files>` ile `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="6d2e2-167">Paket Yöneticisi seçenekleri denetimi</span><span class="sxs-lookup"><span data-stu-id="6d2e2-167">Package manager options control</span></span>

<span data-ttu-id="6d2e2-168">*İlk olarak, [Paket Yöneticisi kullanıcı Arabirimi başvurusu](../tools/Package-Manager-UI.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-168">*Originally in [Package Manager UI reference](../tools/Package-Manager-UI.md).*</span></span>

<span data-ttu-id="6d2e2-169">Kullanarak projeleri `project.json` başvuru biçimi Göster yalnızca **Göster önizleme penceresi** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-169">Projects using `project.json` reference format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="6d2e2-170">Visual Studio şablonları</span><span class="sxs-lookup"><span data-stu-id="6d2e2-170">Visual Studio Templates</span></span>

<span data-ttu-id="6d2e2-171">*İlk olarak, [Visual Studio şablonları NuGet paketlerine](../Visual-Studio-Extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="6d2e2-171">*Originally in [NuGet Packages in Visual Studio templates](../Visual-Studio-Extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="6d2e2-172">En iyi uygulamalar: şablonları içermeyen bir `project.json` dosya ve içermeyen veya tüm başvuruları veya NuGet paketleri yüklendiğinde ekleneceği içerik.</span><span class="sxs-lookup"><span data-stu-id="6d2e2-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>