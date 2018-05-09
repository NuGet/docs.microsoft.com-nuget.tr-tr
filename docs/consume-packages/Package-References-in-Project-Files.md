---
title: NuGet PackageReference biçimi (proje dosyalarına paket referanslarını)
description: NuGet PackageReference NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi proje dosyalarına ayrıntıları
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a4755-103">Proje dosyalarına paket referanslarını (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a4755-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a4755-104">Paketini kullanarak başvurular `PackageReference` düğümü, NuGet bağımlılıkları doğrudan proje dosyalarını Yönet (ayrı bir aksine `packages.config` dosyası).</span><span class="sxs-lookup"><span data-stu-id="a4755-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="a4755-105">Denir, PackageReference, kullanarak NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a4755-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a4755-106">PackageReference ile hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına paket referanslarını seçmek için MSBuild koşulları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4755-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a4755-107">Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4755-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="a4755-108">(Daha fazla ayrıntı için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="a4755-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="a4755-109">Varsayılan olarak, PackageReference .NET Core projeleri, .NET standart projeler ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için ve daha sonra C++ UWP projeleri hariç olmak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a4755-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="a4755-110">.NET framework tam projeleri PackageReference destekler, ancak şu anda varsayılan olarak `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a4755-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="a4755-111">PackageReference kullanmak için bağımlılıklardan geçirmek `packages.config` proje dosyanıza ardından packages.config kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a4755-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a4755-112">Bir PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="a4755-112">Adding a PackageReference</span></span>

<span data-ttu-id="a4755-113">Bir bağımlılık aşağıdaki sözdizimini kullanarak, proje dosyasında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a4755-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a4755-114">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="a4755-114">Controlling dependency version</span></span>

<span data-ttu-id="a4755-115">Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a4755-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a4755-116">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir. > açıklandığı gibi en düşük sürüm tercihini ile 3.6.0 = [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a4755-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a4755-117">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="a4755-117">Floating Versions</span></span>

<span data-ttu-id="a4755-118">[Sürümleri kayan](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a4755-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a4755-119">Bağımlılık varlıklar denetleme</span><span class="sxs-lookup"><span data-stu-id="a4755-119">Controlling dependency assets</span></span>

<span data-ttu-id="a4755-120">Bir bağımlılık tamamen geliştirme bandı kullanıyor olabilir ve paketinizi tüketir projelerine kullanıma istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4755-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a4755-121">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışı denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="a4755-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a4755-122">Aşağıdaki meta veri etiketlerini bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="a4755-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a4755-123">Etiket</span><span class="sxs-lookup"><span data-stu-id="a4755-123">Tag</span></span> | <span data-ttu-id="a4755-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4755-124">Description</span></span> | <span data-ttu-id="a4755-125">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="a4755-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4755-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a4755-126">IncludeAssets</span></span> | <span data-ttu-id="a4755-127">Bu varlıklar kullanılır</span><span class="sxs-lookup"><span data-stu-id="a4755-127">These assets will be consumed</span></span> | <span data-ttu-id="a4755-128">tüm</span><span class="sxs-lookup"><span data-stu-id="a4755-128">all</span></span> |
| <span data-ttu-id="a4755-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a4755-129">ExcludeAssets</span></span> | <span data-ttu-id="a4755-130">Bu varlıklar tüketilen değil</span><span class="sxs-lookup"><span data-stu-id="a4755-130">These assets will not be consumed</span></span> | <span data-ttu-id="a4755-131">yok</span><span class="sxs-lookup"><span data-stu-id="a4755-131">none</span></span> |
| <span data-ttu-id="a4755-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a4755-132">PrivateAssets</span></span> | <span data-ttu-id="a4755-133">Bu varlıklar kullanılır, ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="a4755-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a4755-134">Content dosyaları, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="a4755-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a4755-135">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değerlerle `all` ve `none` gerekir göründüğü tek başına:</span><span class="sxs-lookup"><span data-stu-id="a4755-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a4755-136">Değer</span><span class="sxs-lookup"><span data-stu-id="a4755-136">Value</span></span> | <span data-ttu-id="a4755-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4755-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="a4755-138">Derleme</span><span class="sxs-lookup"><span data-stu-id="a4755-138">compile</span></span> | <span data-ttu-id="a4755-139">İçeriği `lib` klasörü ve denetimleri klasördeki derlemeleri karşı olup projenizi derleme</span><span class="sxs-lookup"><span data-stu-id="a4755-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="a4755-140">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="a4755-140">runtime</span></span> | <span data-ttu-id="a4755-141">İçeriği `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için yapı olup kopyalanacak çıktı dizini</span><span class="sxs-lookup"><span data-stu-id="a4755-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="a4755-142">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="a4755-142">contentFiles</span></span> | <span data-ttu-id="a4755-143">İçeriği `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="a4755-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a4755-144">derleme</span><span class="sxs-lookup"><span data-stu-id="a4755-144">build</span></span> | <span data-ttu-id="a4755-145">Özellik ve içinde hedefler `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="a4755-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a4755-146">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a4755-146">analyzers</span></span> | <span data-ttu-id="a4755-147">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="a4755-147">.NET analyzers</span></span> |
| <span data-ttu-id="a4755-148">yerel</span><span class="sxs-lookup"><span data-stu-id="a4755-148">native</span></span> | <span data-ttu-id="a4755-149">İçeriği `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="a4755-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a4755-150">yok</span><span class="sxs-lookup"><span data-stu-id="a4755-150">none</span></span> | <span data-ttu-id="a4755-151">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a4755-151">None of the above are used.</span></span> |
| <span data-ttu-id="a4755-152">tüm</span><span class="sxs-lookup"><span data-stu-id="a4755-152">all</span></span> | <span data-ttu-id="a4755-153">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="a4755-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="a4755-154">Aşağıdaki örnekte, paket içerik dosyalarını dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a4755-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a4755-155">Çünkü unutmayın `build` ile dahil edilmeyen `PrivateAssets`, hedefleri ve özellik *olacak* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="a4755-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a4755-156">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi derlemeler bir projede kullanıldığını değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="a4755-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a4755-157">Hedefleri ve özellik gelen AppLogger tüketebileceği `Contoso.Utility.UsefulStuff`AppLogger tüketen projelerini gibi.</span><span class="sxs-lookup"><span data-stu-id="a4755-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a4755-158">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="a4755-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="a4755-159">Koşullar herhangi bir MSBuild değişkeni kullanabilirsiniz veya bir değişkeni hedefler ya da özellik dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4755-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a4755-160">Ancak, şu anda yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a4755-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a4755-161">Örneğin, hedefleme deyin `netstandard1.4` yanı `net452` ancak yalnızca için geçerli bir bağımlılığı olan `net452`.</span><span class="sxs-lookup"><span data-stu-id="a4755-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a4755-162">Bu durumda istemediğiniz bir `netstandard1.4` gereksiz bu bağımlılığı eklemek için paket tüketen projesi.</span><span class="sxs-lookup"><span data-stu-id="a4755-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a4755-163">Bunu önlemek için bir koşul üzerinde belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="a4755-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a4755-164">Bu proje kullanılarak oluşturulmuş bir paketin Newtonsoft.json yalnızca için bağımlılık olarak dahil olduğunu göstermek bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="a4755-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul VS2017 ile PackageReference üzerinde uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="a4755-166">Koşullar da uygulanabilir adresindeki `ItemGroup` düzey ve tüm alt öğelerine uygulanır `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="a4755-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
