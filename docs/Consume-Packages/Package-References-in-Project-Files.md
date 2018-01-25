---
title: "NuGet PackageReference biçimi (proje dosyalarına paket referanslarını) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet PackageReference NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi proje dosyalarına ayrıntıları"
keywords: "NuGet Paket bağımlılıklarını, paket referanslarını proje dosyalarını, PackageReference, packages.config VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 24a977f9de535559dcb0392749298ea502c3c7ce
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a468b-104">Proje dosyalarına paket referanslarını (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a468b-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a468b-105">Paketini kullanarak başvurular `PackageReference` düğümü, ayrı bir gerek yerine NuGet bağımlılıkları doğrudan proje dosyalarını yönetmenize olanak `packages.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="a468b-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` file.</span></span> <span data-ttu-id="a468b-106">Bu yöntem, NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a468b-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="a468b-107">Şu anda paket referanslarını Visual Studio 2017 içinde yalnızca, .NET Core projeleri, .NET standart projeleri ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a468b-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="a468b-108">`PackageReference` Yaklaşım paket referanslarını hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına seçmek için MSBuild koşulları kullanmanıza olanak verir.</span><span class="sxs-lookup"><span data-stu-id="a468b-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a468b-109">Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a468b-109">It also allows for fine-grained control over dependencies and content flow.</span></span>

<span data-ttu-id="a468b-110">MSBuild proje dosyalarına paket referanslarını tümleştirilmesi hakkında daha fazla bilgi için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="a468b-110">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a468b-111">Bir PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="a468b-111">Adding a PackageReference</span></span>

<span data-ttu-id="a468b-112">Bir bağımlılık aşağıdaki sözdizimini kullanarak, proje dosyasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a468b-112">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a468b-113">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="a468b-113">Controlling dependency version</span></span>

<span data-ttu-id="a468b-114">Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a468b-114">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a468b-115">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir. > açıklandığı gibi en düşük sürüm tercihini ile 3.6.0 = [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a468b-115">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a468b-116">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="a468b-116">Floating Versions</span></span>

<span data-ttu-id="a468b-117">[Sürümleri kayan](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a468b-117">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a468b-118">Bağımlılık varlıklar denetleme</span><span class="sxs-lookup"><span data-stu-id="a468b-118">Controlling dependency assets</span></span>

<span data-ttu-id="a468b-119">Bir bağımlılık tamamen geliştirme bandı kullanıyor olabilir ve paketinizi tüketir projelerine kullanıma istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a468b-119">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a468b-120">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışı denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="a468b-120">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a468b-121">Aşağıdaki meta veri etiketlerini bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="a468b-121">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a468b-122">Etiket</span><span class="sxs-lookup"><span data-stu-id="a468b-122">Tag</span></span> | <span data-ttu-id="a468b-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a468b-123">Description</span></span> | <span data-ttu-id="a468b-124">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="a468b-124">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a468b-125">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a468b-125">IncludeAssets</span></span> | <span data-ttu-id="a468b-126">Bu varlıklar kullanılır</span><span class="sxs-lookup"><span data-stu-id="a468b-126">These assets will be consumed</span></span> | <span data-ttu-id="a468b-127">tüm</span><span class="sxs-lookup"><span data-stu-id="a468b-127">all</span></span> |
| <span data-ttu-id="a468b-128">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a468b-128">ExcludeAssets</span></span> | <span data-ttu-id="a468b-129">Bu varlıklar tüketilen değil</span><span class="sxs-lookup"><span data-stu-id="a468b-129">These assets will not be consumed</span></span> | <span data-ttu-id="a468b-130">yok</span><span class="sxs-lookup"><span data-stu-id="a468b-130">none</span></span> |
| <span data-ttu-id="a468b-131">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a468b-131">PrivateAssets</span></span> | <span data-ttu-id="a468b-132">Bu varlıklar kullanılır, ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="a468b-132">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a468b-133">Content dosyaları, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="a468b-133">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a468b-134">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değerlerle `all` ve `none` gerekir göründüğü tek başına:</span><span class="sxs-lookup"><span data-stu-id="a468b-134">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a468b-135">Değer</span><span class="sxs-lookup"><span data-stu-id="a468b-135">Value</span></span> | <span data-ttu-id="a468b-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a468b-136">Description</span></span> |
| --- | ---
| <span data-ttu-id="a468b-137">Derleme</span><span class="sxs-lookup"><span data-stu-id="a468b-137">compile</span></span> | <span data-ttu-id="a468b-138">İçeriği `lib` klasörü</span><span class="sxs-lookup"><span data-stu-id="a468b-138">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="a468b-139">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="a468b-139">runtime</span></span> | <span data-ttu-id="a468b-140">İçeriği `runtime` klasörü</span><span class="sxs-lookup"><span data-stu-id="a468b-140">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="a468b-141">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="a468b-141">contentFiles</span></span> | <span data-ttu-id="a468b-142">İçeriği `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="a468b-142">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a468b-143">derleme</span><span class="sxs-lookup"><span data-stu-id="a468b-143">build</span></span> | <span data-ttu-id="a468b-144">Özellik ve içinde hedefler `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="a468b-144">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a468b-145">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a468b-145">analyzers</span></span> | <span data-ttu-id="a468b-146">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a468b-146">.NET analyzers</span></span> |
| <span data-ttu-id="a468b-147">yerel</span><span class="sxs-lookup"><span data-stu-id="a468b-147">native</span></span> | <span data-ttu-id="a468b-148">İçeriği `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="a468b-148">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a468b-149">yok</span><span class="sxs-lookup"><span data-stu-id="a468b-149">none</span></span> | <span data-ttu-id="a468b-150">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a468b-150">None of the above are used.</span></span> |
| <span data-ttu-id="a468b-151">tüm</span><span class="sxs-lookup"><span data-stu-id="a468b-151">all</span></span> | <span data-ttu-id="a468b-152">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="a468b-152">All of the above (except `none`)</span></span> |

<span data-ttu-id="a468b-153">Aşağıdaki örnekte, paket içerik dosyalarını dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a468b-153">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a468b-154">Çünkü unutmayın `build` ile dahil edilmeyen `PrivateAssets`, hedefleri ve özellik *olacak* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a468b-154">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a468b-155">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi derlemeler bir projede kullanıldığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="a468b-155">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a468b-156">Hedefleri ve özellik gelen AppLogger tüketebileceği `Contoso.Utility.UsefulStuff`AppLogger tüketen projelerini gibi.</span><span class="sxs-lookup"><span data-stu-id="a468b-156">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a468b-157">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="a468b-157">Adding a PackageReference condition</span></span>

<span data-ttu-id="a468b-158">Koşullar herhangi bir MSBuild değişkeni kullanabilirsiniz veya bir değişkeni hedefler ya da özellik dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a468b-158">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a468b-159">Ancak, şu anda yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a468b-159">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a468b-160">Örneğin, hedefleme deyin `netstandard1.4` yanı `net452` ancak yalnızca için geçerli bir bağımlılığı olan `net452`.</span><span class="sxs-lookup"><span data-stu-id="a468b-160">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a468b-161">Bu durumda istemediğiniz bir `netstandard1.4` gereksiz bu bağımlılığı eklemek için paket tüketen projesi.</span><span class="sxs-lookup"><span data-stu-id="a468b-161">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a468b-162">Bunu önlemek için bir koşul üzerinde belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="a468b-162">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a468b-163">Bu proje kullanılarak oluşturulmuş bir paketin Newtonsoft.json yalnızca için bağımlılık olarak dahil olduğunu göstermek bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="a468b-163">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul VS2017 ile PackageReference üzerinde uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="a468b-165">Koşullar da uygulanabilir adresindeki `ItemGroup` düzey ve tüm alt öğelerine uygulanır `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="a468b-165">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
