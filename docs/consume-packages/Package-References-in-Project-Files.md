---
title: NuGet Packagereference'a biçimi (proje dosyalarında paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference hakkında ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 648b2679538e38b2451d7857beb5d070deeef7c5
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516210"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="f3fbf-103">Proje dosyalarında paket başvuruları (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="f3fbf-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="f3fbf-104">Paket başvuruları kullanılarak, `PackageReference` düğümü, NuGet bağımlılıklarını doğrudan proje dosyaları içinde yönetme (ayrı bir aksine `packages.config` dosya).</span><span class="sxs-lookup"><span data-stu-id="f3fbf-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="f3fbf-105">PackageReference, kullanarak çağrılır, NuGet diğer yönleri etkilemez; Örneğin, ayarlarında `NuGet.Config` (paket kaynaklarını dahil) dosyaları yine de açıklandığı gibi uygulanan [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f3fbf-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f3fbf-106">PackageReference ile paket başvuruları her hedef çerçeve, yapılandırma, platform veya diğer grupları seçmek için MSBuild koşulları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="f3fbf-107">Ayrıca bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="f3fbf-108">(Daha fazla ayrıntı için [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="f3fbf-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="f3fbf-109">Varsayılan olarak, .NET Core projeleri, .NET Standard projelerine ve Windows 10 derleme 15063 (Creators Update) hedefleyen UWP projeleri için ve sonraki sürümlerinde, C++ UWP projeleri hariç PackageReference kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="f3fbf-110">.NET framework projeleri PackageReference destekler, ancak şu anda varsayılan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="f3fbf-111">PackageReference kullanmak için bağımlılıklardan geçirme `packages.config` proje dosyanıza ardından packages.config kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="f3fbf-112">PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-112">Adding a PackageReference</span></span>

<span data-ttu-id="f3fbf-113">Bir bağımlılık aşağıdaki sözdizimini kullanarak proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="f3fbf-114">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-114">Controlling dependency version</span></span>

<span data-ttu-id="f3fbf-115">Bir paketin sürümü belirtmek için kural aynı kullanıldığında `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f3fbf-116">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir > üzerinde açıklandığı 3.6.0 tercih en düşük sürümü ile = [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="f3fbf-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="f3fbf-117">Hiçbir packagereferences'ı içeren bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="f3fbf-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="f3fbf-118">Gelişmiş: sahip paket yüklü bir projede (proje dosyasında hiçbir PackageReferences) ve hiçbir packages.config dosyası yok, ancak stili Packagereference'a geri yüklenmesini istediğiniz projesinin, proje özelliği RestoreProjectStyle Packagereference'a ayarlayabileceğiniz içinde Proje dosyanız.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="f3fbf-119">(Mevcut csproj veya SDK stili projeleri) stili Packagereference'a olan projeleri başvuruyorsa yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="f3fbf-120">Bu projelerdeki "geçişli" projeniz tarafından başvurulabilmesi için başvuran paketleri olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="f3fbf-121">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="f3fbf-121">Floating Versions</span></span>

<span data-ttu-id="f3fbf-122">[Kayan sürümleri](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="f3fbf-123">Bağımlılık varlıkları denetleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-123">Controlling dependency assets</span></span>

<span data-ttu-id="f3fbf-124">Bir bağımlılık yalnızca bir geliştirme bandı kullanabilecek ve, paketiniz tüketecektir projeler için kullanıma sunmak istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="f3fbf-125">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışını denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f3fbf-126">Şu meta veri etiketleri bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="f3fbf-127">Etiket</span><span class="sxs-lookup"><span data-stu-id="f3fbf-127">Tag</span></span> | <span data-ttu-id="f3fbf-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f3fbf-128">Description</span></span> | <span data-ttu-id="f3fbf-129">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="f3fbf-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3fbf-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="f3fbf-130">IncludeAssets</span></span> | <span data-ttu-id="f3fbf-131">Bu varlıklar tarafından kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f3fbf-131">These assets will be consumed</span></span> | <span data-ttu-id="f3fbf-132">tüm</span><span class="sxs-lookup"><span data-stu-id="f3fbf-132">all</span></span> |
| <span data-ttu-id="f3fbf-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="f3fbf-133">ExcludeAssets</span></span> | <span data-ttu-id="f3fbf-134">Bu varlıklar tüketilir değil</span><span class="sxs-lookup"><span data-stu-id="f3fbf-134">These assets will not be consumed</span></span> | <span data-ttu-id="f3fbf-135">yok</span><span class="sxs-lookup"><span data-stu-id="f3fbf-135">none</span></span> |
| <span data-ttu-id="f3fbf-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="f3fbf-136">PrivateAssets</span></span> | <span data-ttu-id="f3fbf-137">Bu varlıklar tarafından kullanılabilir ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="f3fbf-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="f3fbf-138">contentfiles, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="f3fbf-139">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değer ile `all` ve `none` gerekir göründüğü başlarına:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="f3fbf-140">Değer</span><span class="sxs-lookup"><span data-stu-id="f3fbf-140">Value</span></span> | <span data-ttu-id="f3fbf-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f3fbf-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="f3fbf-142">Derleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-142">compile</span></span> | <span data-ttu-id="f3fbf-143">İçeriğini `lib` klasörü ve denetimleri klasördeki derlemelere karşı olup projenizi derleyin</span><span class="sxs-lookup"><span data-stu-id="f3fbf-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="f3fbf-144">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="f3fbf-144">runtime</span></span> | <span data-ttu-id="f3fbf-145">İçeriğini `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için derleme olup kopyalanacak çıktı dizini</span><span class="sxs-lookup"><span data-stu-id="f3fbf-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="f3fbf-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f3fbf-146">contentFiles</span></span> | <span data-ttu-id="f3fbf-147">İçeriğini `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="f3fbf-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="f3fbf-148">derleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-148">build</span></span> | <span data-ttu-id="f3fbf-149">Özellikler ve hedeflediğini `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="f3fbf-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="f3fbf-150">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="f3fbf-150">analyzers</span></span> | <span data-ttu-id="f3fbf-151">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="f3fbf-151">.NET analyzers</span></span> |
| <span data-ttu-id="f3fbf-152">yerel</span><span class="sxs-lookup"><span data-stu-id="f3fbf-152">native</span></span> | <span data-ttu-id="f3fbf-153">İçeriğini `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="f3fbf-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="f3fbf-154">yok</span><span class="sxs-lookup"><span data-stu-id="f3fbf-154">none</span></span> | <span data-ttu-id="f3fbf-155">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-155">None of the above are used.</span></span> |
| <span data-ttu-id="f3fbf-156">tüm</span><span class="sxs-lookup"><span data-stu-id="f3fbf-156">all</span></span> | <span data-ttu-id="f3fbf-157">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="f3fbf-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="f3fbf-158">Aşağıdaki örnekte, içerik dosyalarını paketinden dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="f3fbf-159">Dikkat edin çünkü `build` ile bulunmaz `PrivateAssets`, hedeflerini ve özellik *olur* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="f3fbf-160">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi oluşturan bir projesinde kullanıldığını düşünün.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="f3fbf-161">AppLogger hedeflerini ve özellik gelen kullanabileceği `Contoso.Utility.UsefulStuff`, AppLogger kullanan projeler gibi.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="f3fbf-162">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="f3fbf-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="f3fbf-163">Koşullar herhangi bir MSBuild değişken kullanabilirsiniz veya bir değişkeni hedefler ya da Özellikler dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="f3fbf-164">Ancak, şu anda, yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="f3fbf-165">Örneğin, hedefleyen düşünelim `netstandard1.4` yanı `net452` ancak yalnızca için geçerli olan bir bağımlılığa sahip `net452`.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="f3fbf-166">Bu durumda istemediğiniz bir `netstandard1.4` paketiniz, gereksiz bağımlılık eklemek için kullanan bir proje.</span><span class="sxs-lookup"><span data-stu-id="f3fbf-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="f3fbf-167">Bunu önlemek için bir koşul belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="f3fbf-168">Bu proje kullanılarak oluşturulan bir paket Newtonsoft.Json yalnızca bağımlılık olarak dahil olduğunu gösterir bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul ile VS2017 PackageReference üzerinde sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="f3fbf-170">Koşul da uygulanabilir `ItemGroup` düzeyi ve tüm alt öğelere uygulanacak `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="f3fbf-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
