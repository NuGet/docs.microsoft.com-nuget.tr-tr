---
title: "Visual Studio proje dosyalarına NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet PackageReference NuGet 4.0 + ve VS2017 tarafından desteklenen gibi proje dosyalarına ayrıntıları"
keywords: "NuGet Paket bağımlılıklarını, paket referanslarını proje dosyalarını, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="7f882-104">Proje dosyalarına paket referanslarını (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="7f882-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="7f882-105">Paketini kullanarak başvurular `PackageReference` düğümü, ayrı bir gerek yerine NuGet bağımlılıkları doğrudan proje dosyalarını yönetmenize olanak `packages.config` veya `project.json` dosyası.</span><span class="sxs-lookup"><span data-stu-id="7f882-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="7f882-106">Bu yöntem, NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7f882-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="7f882-107">Şu anda paket referanslarını Visual Studio 2017 içinde yalnızca, .NET Core projeleri, .NET standart projeleri ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7f882-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="7f882-108">`PackageReference` Yaklaşım paket referanslarını hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına seçmek için MSBuild koşulları kullanmanıza olanak verir.</span><span class="sxs-lookup"><span data-stu-id="7f882-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="7f882-109">Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f882-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="7f882-110">Davranış açısından ve [bağımlılık çözümlemesi](Dependency-Resolution.md), kullanarak aynı olan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7f882-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="7f882-111">MSBuild proje dosyalarına paket referanslarını tümleştirilmesi hakkında daha fazla bilgi için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="7f882-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="7f882-112">Bir PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="7f882-112">Adding a PackageReference</span></span>

<span data-ttu-id="7f882-113">Bir bağımlılık aşağıdaki sözdizimini kullanarak, proje dosyasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7f882-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="7f882-114">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="7f882-114">Controlling dependency version</span></span>

<span data-ttu-id="7f882-115">Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config` veya `project.json`:</span><span class="sxs-lookup"><span data-stu-id="7f882-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7f882-116">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir. > açıklandığı gibi en düşük sürüm tercihini ile 3.6.0 = [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="7f882-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="7f882-117">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="7f882-117">Floating Versions</span></span>

<span data-ttu-id="7f882-118">[Sürümleri kayan](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="7f882-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="7f882-119">Bağımlılık varlıklar denetleme</span><span class="sxs-lookup"><span data-stu-id="7f882-119">Controlling dependency assets</span></span>

<span data-ttu-id="7f882-120">Bir bağımlılık tamamen geliştirme bandı kullanıyor olabilir ve paketinizi tüketir projelerine kullanıma istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f882-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="7f882-121">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışı denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="7f882-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7f882-122">Aşağıdaki meta veri etiketlerini bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="7f882-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="7f882-123">Etiket</span><span class="sxs-lookup"><span data-stu-id="7f882-123">Tag</span></span> | <span data-ttu-id="7f882-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7f882-124">Description</span></span> | <span data-ttu-id="7f882-125">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="7f882-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f882-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="7f882-126">IncludeAssets</span></span> | <span data-ttu-id="7f882-127">Bu varlıklar kullanılır</span><span class="sxs-lookup"><span data-stu-id="7f882-127">These assets will be consumed</span></span> | <span data-ttu-id="7f882-128">tüm</span><span class="sxs-lookup"><span data-stu-id="7f882-128">all</span></span> |
| <span data-ttu-id="7f882-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="7f882-129">ExcludeAssets</span></span> | <span data-ttu-id="7f882-130">Bu varlıklar tüketilen değil</span><span class="sxs-lookup"><span data-stu-id="7f882-130">These assets will not be consumed</span></span> | <span data-ttu-id="7f882-131">yok</span><span class="sxs-lookup"><span data-stu-id="7f882-131">none</span></span> | 
| <span data-ttu-id="7f882-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="7f882-132">PrivateAssets</span></span> | <span data-ttu-id="7f882-133">Bu varlıklar kullanılır, ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="7f882-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="7f882-134">Content dosyaları, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="7f882-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="7f882-135">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değerlerle `all` ve `none` gerekir göründüğü tek başına:</span><span class="sxs-lookup"><span data-stu-id="7f882-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="7f882-136">Değer</span><span class="sxs-lookup"><span data-stu-id="7f882-136">Value</span></span> | <span data-ttu-id="7f882-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7f882-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="7f882-138">Derleme</span><span class="sxs-lookup"><span data-stu-id="7f882-138">compile</span></span> | <span data-ttu-id="7f882-139">İçeriği `lib` klasörü</span><span class="sxs-lookup"><span data-stu-id="7f882-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="7f882-140">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="7f882-140">runtime</span></span> | <span data-ttu-id="7f882-141">İçeriği `runtime` klasörü</span><span class="sxs-lookup"><span data-stu-id="7f882-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="7f882-142">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="7f882-142">contentFiles</span></span> | <span data-ttu-id="7f882-143">İçeriği `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="7f882-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="7f882-144">derleme</span><span class="sxs-lookup"><span data-stu-id="7f882-144">build</span></span> | <span data-ttu-id="7f882-145">Özellik ve içinde hedefler `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="7f882-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="7f882-146">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="7f882-146">analyzers</span></span> | <span data-ttu-id="7f882-147">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="7f882-147">.NET analyzers</span></span> |
| <span data-ttu-id="7f882-148">yerel</span><span class="sxs-lookup"><span data-stu-id="7f882-148">native</span></span> | <span data-ttu-id="7f882-149">İçeriği `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="7f882-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="7f882-150">yok</span><span class="sxs-lookup"><span data-stu-id="7f882-150">none</span></span> | <span data-ttu-id="7f882-151">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f882-151">None of the above are used.</span></span> |
| <span data-ttu-id="7f882-152">tüm</span><span class="sxs-lookup"><span data-stu-id="7f882-152">all</span></span> | <span data-ttu-id="7f882-153">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="7f882-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="7f882-154">Aşağıdaki örnekte, paket içerik dosyalarını dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="7f882-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7f882-155">Çünkü unutmayın `build` ile dahil edilmeyen `PrivateAssets`, hedefleri ve özellik *olacak* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="7f882-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="7f882-156">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi derlemeler bir projede kullanıldığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="7f882-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="7f882-157">Hedefleri ve özellik gelen AppLogger tüketebileceği `Contoso.Utility.UsefulStuff`AppLogger tüketen projelerini gibi.</span><span class="sxs-lookup"><span data-stu-id="7f882-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="7f882-158">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="7f882-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="7f882-159">Koşullar herhangi bir MSBuild değişkeni kullanabilirsiniz veya bir değişkeni hedefler ya da özellik dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f882-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="7f882-160">Ancak, şu anda yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7f882-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="7f882-161">Örneğin, hedefleme deyin `netstandard1.4` yanı `net452` ancak yalnızca için geçerli bir bağımlılığı olan `net452`.</span><span class="sxs-lookup"><span data-stu-id="7f882-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="7f882-162">Bu durumda istemediğiniz bir `netstandard1.4` gereksiz bu bağımlılığı eklemek için paket tüketen projesi.</span><span class="sxs-lookup"><span data-stu-id="7f882-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="7f882-163">Bunu önlemek için bir koşul üzerinde belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="7f882-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7f882-164">Bu proje kullanılarak oluşturulmuş bir paketin Newtonsoft.json yalnızca için bağımlılık olarak dahil olduğunu göstermek bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="7f882-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul VS2017 ile PackageReference üzerinde uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="7f882-166">Koşullar da uygulanabilir adresindeki `ItemGroup` düzey ve tüm alt öğelerine uygulanır `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="7f882-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
