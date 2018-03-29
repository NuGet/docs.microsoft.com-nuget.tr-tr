---
title: NuGet PackageReference biçimi (proje dosyalarına paket referanslarını) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet PackageReference NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi proje dosyalarına ayrıntıları
keywords: NuGet Paket bağımlılıklarını, paket referanslarını proje dosyalarını, PackageReference, packages.config VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a50e5-104">Proje dosyalarına paket referanslarını (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a50e5-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a50e5-105">Paketini kullanarak başvurular `PackageReference` düğümü, NuGet bağımlılıkları doğrudan proje dosyalarını Yönet (ayrı bir aksine `packages.config` dosyası).</span><span class="sxs-lookup"><span data-stu-id="a50e5-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="a50e5-106">Denir, PackageReference, kullanarak NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a50e5-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a50e5-107">PackageReference ile hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına paket referanslarını seçmek için MSBuild koşulları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50e5-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a50e5-108">Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a50e5-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="a50e5-109">(Daha fazla ayrıntı için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="a50e5-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="a50e5-110">Varsayılan olarak, PackageReference .NET Core projeleri, .NET standart projeler ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için ve daha sonra C++ UWP projeleri hariç olmak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a50e5-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="a50e5-111">.NET framework tam projeleri PackageReference destekler, ancak şu anda varsayılan olarak `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a50e5-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="a50e5-112">PackageReference kullanmak için bağımlılıklardan geçirmek `packages.config` proje dosyanıza ardından packages.config kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a50e5-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a50e5-113">Bir PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-113">Adding a PackageReference</span></span>

<span data-ttu-id="a50e5-114">Bir bağımlılık aşağıdaki sözdizimini kullanarak, proje dosyasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a50e5-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a50e5-115">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-115">Controlling dependency version</span></span>

<span data-ttu-id="a50e5-116">Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a50e5-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a50e5-117">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir. > açıklandığı gibi en düşük sürüm tercihini ile 3.6.0 = [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a50e5-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a50e5-118">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="a50e5-118">Floating Versions</span></span>

<span data-ttu-id="a50e5-119">[Sürümleri kayan](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a50e5-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a50e5-120">Bağımlılık varlıklar denetleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-120">Controlling dependency assets</span></span>

<span data-ttu-id="a50e5-121">Bir bağımlılık tamamen geliştirme bandı kullanıyor olabilir ve paketinizi tüketir projelerine kullanıma istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50e5-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a50e5-122">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışı denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="a50e5-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a50e5-123">Aşağıdaki meta veri etiketlerini bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="a50e5-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a50e5-124">Etiket</span><span class="sxs-lookup"><span data-stu-id="a50e5-124">Tag</span></span> | <span data-ttu-id="a50e5-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a50e5-125">Description</span></span> | <span data-ttu-id="a50e5-126">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="a50e5-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a50e5-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a50e5-127">IncludeAssets</span></span> | <span data-ttu-id="a50e5-128">Bu varlıklar kullanılır</span><span class="sxs-lookup"><span data-stu-id="a50e5-128">These assets will be consumed</span></span> | <span data-ttu-id="a50e5-129">tüm</span><span class="sxs-lookup"><span data-stu-id="a50e5-129">all</span></span> |
| <span data-ttu-id="a50e5-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a50e5-130">ExcludeAssets</span></span> | <span data-ttu-id="a50e5-131">Bu varlıklar tüketilen değil</span><span class="sxs-lookup"><span data-stu-id="a50e5-131">These assets will not be consumed</span></span> | <span data-ttu-id="a50e5-132">yok</span><span class="sxs-lookup"><span data-stu-id="a50e5-132">none</span></span> |
| <span data-ttu-id="a50e5-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a50e5-133">PrivateAssets</span></span> | <span data-ttu-id="a50e5-134">Bu varlıklar kullanılır, ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="a50e5-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a50e5-135">Content dosyaları, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a50e5-136">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değerlerle `all` ve `none` gerekir göründüğü tek başına:</span><span class="sxs-lookup"><span data-stu-id="a50e5-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a50e5-137">Değer</span><span class="sxs-lookup"><span data-stu-id="a50e5-137">Value</span></span> | <span data-ttu-id="a50e5-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a50e5-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="a50e5-139">Derleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-139">compile</span></span> | <span data-ttu-id="a50e5-140">İçeriği `lib` klasörü</span><span class="sxs-lookup"><span data-stu-id="a50e5-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="a50e5-141">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="a50e5-141">runtime</span></span> | <span data-ttu-id="a50e5-142">İçeriği `runtimes` klasörü</span><span class="sxs-lookup"><span data-stu-id="a50e5-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="a50e5-143">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="a50e5-143">contentFiles</span></span> | <span data-ttu-id="a50e5-144">İçeriği `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="a50e5-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a50e5-145">derleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-145">build</span></span> | <span data-ttu-id="a50e5-146">Özellik ve içinde hedefler `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="a50e5-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a50e5-147">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a50e5-147">analyzers</span></span> | <span data-ttu-id="a50e5-148">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a50e5-148">.NET analyzers</span></span> |
| <span data-ttu-id="a50e5-149">yerel</span><span class="sxs-lookup"><span data-stu-id="a50e5-149">native</span></span> | <span data-ttu-id="a50e5-150">İçeriği `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="a50e5-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a50e5-151">yok</span><span class="sxs-lookup"><span data-stu-id="a50e5-151">none</span></span> | <span data-ttu-id="a50e5-152">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a50e5-152">None of the above are used.</span></span> |
| <span data-ttu-id="a50e5-153">tüm</span><span class="sxs-lookup"><span data-stu-id="a50e5-153">all</span></span> | <span data-ttu-id="a50e5-154">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="a50e5-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="a50e5-155">Aşağıdaki örnekte, paket içerik dosyalarını dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a50e5-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a50e5-156">Çünkü unutmayın `build` ile dahil edilmeyen `PrivateAssets`, hedefleri ve özellik *olacak* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a50e5-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a50e5-157">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi derlemeler bir projede kullanıldığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="a50e5-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a50e5-158">Hedefleri ve özellik gelen AppLogger tüketebileceği `Contoso.Utility.UsefulStuff`AppLogger tüketen projelerini gibi.</span><span class="sxs-lookup"><span data-stu-id="a50e5-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a50e5-159">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="a50e5-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="a50e5-160">Koşullar herhangi bir MSBuild değişkeni kullanabilirsiniz veya bir değişkeni hedefler ya da özellik dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a50e5-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a50e5-161">Ancak, şu anda yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a50e5-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a50e5-162">Örneğin, hedefleme deyin `netstandard1.4` yanı `net452` ancak yalnızca için geçerli bir bağımlılığı olan `net452`.</span><span class="sxs-lookup"><span data-stu-id="a50e5-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a50e5-163">Bu durumda istemediğiniz bir `netstandard1.4` gereksiz bu bağımlılığı eklemek için paket tüketen projesi.</span><span class="sxs-lookup"><span data-stu-id="a50e5-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a50e5-164">Bunu önlemek için bir koşul üzerinde belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="a50e5-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a50e5-165">Bu proje kullanılarak oluşturulmuş bir paketin Newtonsoft.json yalnızca için bağımlılık olarak dahil olduğunu göstermek bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="a50e5-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul VS2017 ile PackageReference üzerinde uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="a50e5-167">Koşullar da uygulanabilir adresindeki `ItemGroup` düzey ve tüm alt öğelerine uygulanır `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="a50e5-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
