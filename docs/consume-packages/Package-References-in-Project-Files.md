---
title: NuGet Packagereference'a biçimi (proje dosyalarında paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference hakkında ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 16a14a72f8bb2e5d5a56f6c3c277f0988869273d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426690"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="9aebe-103">Proje dosyalarında paket başvuruları (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="9aebe-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="9aebe-104">Paket başvuruları kullanılarak, `PackageReference` düğümü, NuGet bağımlılıklarını doğrudan proje dosyaları içinde yönetme (ayrı bir aksine `packages.config` dosya).</span><span class="sxs-lookup"><span data-stu-id="9aebe-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="9aebe-105">PackageReference, kullanarak çağrılır, NuGet diğer yönleri etkilemez; Örneğin, ayarlarında `NuGet.config` (paket kaynaklarını dahil) dosyaları yine de açıklandığı gibi uygulanan [ortak NuGet yapılandırmaları](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="9aebe-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="9aebe-106">PackageReference ile paket başvuruları her hedef çerçeve, yapılandırma, platform veya diğer grupları seçmek için MSBuild koşulları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aebe-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="9aebe-107">Ayrıca bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aebe-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="9aebe-108">(Daha fazla ayrıntı için [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="9aebe-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="9aebe-109">Proje türü desteği</span><span class="sxs-lookup"><span data-stu-id="9aebe-109">Project type support</span></span>

<span data-ttu-id="9aebe-110">Varsayılan olarak, .NET Core projeleri, .NET Standard projelerine ve Windows 10 derleme 15063 (Creators Update) hedefleyen UWP projeleri için ve sonraki sürümlerinde, C++ UWP projeleri hariç PackageReference kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="9aebe-111">.NET framework projeleri PackageReference destekler, ancak şu anda varsayılan `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="9aebe-112">PackageReference, kullanılacak [geçirme](../reference/migrate-packages-config-to-package-reference.md) bağımlılıklardan `packages.config` proje dosyanıza ardından packages.config kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9aebe-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="9aebe-113">.NET Framework'ün tamamını hedefleyen ASP.NET uygulamaları dahil yalnızca [sınırlı destek](https://github.com/NuGet/Home/issues/5877) PackageReference için.</span><span class="sxs-lookup"><span data-stu-id="9aebe-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="9aebe-114">C++ve JavaScript proje türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9aebe-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="9aebe-115">PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-115">Adding a PackageReference</span></span>

<span data-ttu-id="9aebe-116">Bir bağımlılık aşağıdaki sözdizimini kullanarak proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9aebe-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="9aebe-117">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-117">Controlling dependency version</span></span>

<span data-ttu-id="9aebe-118">Bir paketin sürümü belirtmek için kural aynı kullanıldığında `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="9aebe-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="9aebe-119">Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir > üzerinde açıklandığı 3.6.0 tercih en düşük sürümü ile = [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="9aebe-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="9aebe-120">Hiçbir packagereferences'ı içeren bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="9aebe-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="9aebe-121">Gelişmiş: Artık paketler, bir projede (proje dosyasında hiçbir PackageReferences) ve hiçbir packages.config dosyası yüklü olan, ancak projesi stili Packagereference'a geri yüklenmesini istiyorsanız, projenizde bir proje özelliğini RestoreProjectStyle Packagereference'a ayarlayabilirsiniz dosya.</span><span class="sxs-lookup"><span data-stu-id="9aebe-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="9aebe-122">(Mevcut csproj veya SDK stili projeleri) stili Packagereference'a olan projeleri başvuruyorsa yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9aebe-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="9aebe-123">Bu projelerdeki "geçişli" projeniz tarafından başvurulabilmesi için başvuran paketleri olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9aebe-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="9aebe-124">Kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="9aebe-124">Floating Versions</span></span>

<span data-ttu-id="9aebe-125">[Kayan sürümleri](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="9aebe-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="9aebe-126">Bağımlılık varlıkları denetleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-126">Controlling dependency assets</span></span>

<span data-ttu-id="9aebe-127">Bir bağımlılık yalnızca bir geliştirme bandı kullanabilecek ve, paketiniz tüketecektir projeler için kullanıma sunmak istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aebe-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="9aebe-128">Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışını denetlemek için meta verileri.</span><span class="sxs-lookup"><span data-stu-id="9aebe-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="9aebe-129">Şu meta veri etiketleri bağımlılık varlıklar kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="9aebe-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="9aebe-130">Etiket</span><span class="sxs-lookup"><span data-stu-id="9aebe-130">Tag</span></span> | <span data-ttu-id="9aebe-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9aebe-131">Description</span></span> | <span data-ttu-id="9aebe-132">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="9aebe-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9aebe-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="9aebe-133">IncludeAssets</span></span> | <span data-ttu-id="9aebe-134">Bu varlıklar tarafından kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="9aebe-134">These assets will be consumed</span></span> | <span data-ttu-id="9aebe-135">tüm</span><span class="sxs-lookup"><span data-stu-id="9aebe-135">all</span></span> |
| <span data-ttu-id="9aebe-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="9aebe-136">ExcludeAssets</span></span> | <span data-ttu-id="9aebe-137">Bu varlıklar tüketilir değil</span><span class="sxs-lookup"><span data-stu-id="9aebe-137">These assets will not be consumed</span></span> | <span data-ttu-id="9aebe-138">yok</span><span class="sxs-lookup"><span data-stu-id="9aebe-138">none</span></span> |
| <span data-ttu-id="9aebe-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="9aebe-139">PrivateAssets</span></span> | <span data-ttu-id="9aebe-140">Bu varlıklar tarafından kullanılabilir ancak üst projeye akış olmaz</span><span class="sxs-lookup"><span data-stu-id="9aebe-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="9aebe-141">contentfiles, çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="9aebe-142">Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değer ile `all` ve `none` gerekir göründüğü başlarına:</span><span class="sxs-lookup"><span data-stu-id="9aebe-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="9aebe-143">Değer</span><span class="sxs-lookup"><span data-stu-id="9aebe-143">Value</span></span> | <span data-ttu-id="9aebe-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9aebe-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="9aebe-145">Derleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-145">compile</span></span> | <span data-ttu-id="9aebe-146">İçeriğini `lib` klasörü ve denetimleri klasördeki derlemelere karşı olup projenizi derleyin</span><span class="sxs-lookup"><span data-stu-id="9aebe-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="9aebe-147">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="9aebe-147">runtime</span></span> | <span data-ttu-id="9aebe-148">İçeriğini `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için derleme olup kopyalanacak çıktı dizini</span><span class="sxs-lookup"><span data-stu-id="9aebe-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="9aebe-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="9aebe-149">contentFiles</span></span> | <span data-ttu-id="9aebe-150">İçeriğini `contentfiles` klasörü</span><span class="sxs-lookup"><span data-stu-id="9aebe-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="9aebe-151">derleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-151">build</span></span> | <span data-ttu-id="9aebe-152">Özellikler ve hedeflediğini `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="9aebe-152">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="9aebe-153">Çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="9aebe-153">analyzers</span></span> | <span data-ttu-id="9aebe-154">.NET çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="9aebe-154">.NET analyzers</span></span> |
| <span data-ttu-id="9aebe-155">yerel</span><span class="sxs-lookup"><span data-stu-id="9aebe-155">native</span></span> | <span data-ttu-id="9aebe-156">İçeriğini `native` klasörü</span><span class="sxs-lookup"><span data-stu-id="9aebe-156">Contents of the `native` folder</span></span> |
| <span data-ttu-id="9aebe-157">yok</span><span class="sxs-lookup"><span data-stu-id="9aebe-157">none</span></span> | <span data-ttu-id="9aebe-158">Yukarıdakilerin hiçbiri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-158">None of the above are used.</span></span> |
| <span data-ttu-id="9aebe-159">tüm</span><span class="sxs-lookup"><span data-stu-id="9aebe-159">all</span></span> | <span data-ttu-id="9aebe-160">Yukarıdakilerin tümü (dışında `none`)</span><span class="sxs-lookup"><span data-stu-id="9aebe-160">All of the above (except `none`)</span></span> |

<span data-ttu-id="9aebe-161">Aşağıdaki örnekte, içerik dosyalarını paketinden dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="9aebe-161">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="9aebe-162">Dikkat edin çünkü `build` ile bulunmaz `PrivateAssets`, hedeflerini ve özellik *olur* üst projeye akış.</span><span class="sxs-lookup"><span data-stu-id="9aebe-162">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="9aebe-163">Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi oluşturan bir projesinde kullanıldığını düşünün.</span><span class="sxs-lookup"><span data-stu-id="9aebe-163">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="9aebe-164">AppLogger hedeflerini ve özellik gelen kullanabileceği `Contoso.Utility.UsefulStuff`, AppLogger kullanan projeler gibi.</span><span class="sxs-lookup"><span data-stu-id="9aebe-164">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="9aebe-165">PackageReference koşul ekleme</span><span class="sxs-lookup"><span data-stu-id="9aebe-165">Adding a PackageReference condition</span></span>

<span data-ttu-id="9aebe-166">Koşullar herhangi bir MSBuild değişken kullanabilirsiniz veya bir değişkeni hedefler ya da Özellikler dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9aebe-166">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="9aebe-167">Ancak, şu anda, yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9aebe-167">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="9aebe-168">Örneğin, hedefleyen düşünelim `netstandard1.4` yanı `net452` ancak yalnızca için geçerli olan bir bağımlılığa sahip `net452`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-168">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="9aebe-169">Bu durumda istemediğiniz bir `netstandard1.4` paketiniz, gereksiz bağımlılık eklemek için kullanan bir proje.</span><span class="sxs-lookup"><span data-stu-id="9aebe-169">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="9aebe-170">Bunu önlemek için bir koşul belirttiğiniz `PackageReference` gibi:</span><span class="sxs-lookup"><span data-stu-id="9aebe-170">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="9aebe-171">Bu proje kullanılarak oluşturulan bir paket Newtonsoft.Json yalnızca bağımlılık olarak dahil olduğunu gösterir bir `net452` hedef:</span><span class="sxs-lookup"><span data-stu-id="9aebe-171">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Bir koşul ile VS2017 PackageReference üzerinde sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="9aebe-173">Koşul da uygulanabilir `ItemGroup` düzeyi ve tüm alt öğelere uygulanacak `PackageReference` öğeleri:</span><span class="sxs-lookup"><span data-stu-id="9aebe-173">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="9aebe-174">Kilitleme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="9aebe-174">Locking dependencies</span></span>
<span data-ttu-id="9aebe-175">*Bu özellik, NuGet ile kullanılabilir **4.9** veya yukarıda ve Visual Studio 2017 ile **15.9** veya üzeri.*</span><span class="sxs-lookup"><span data-stu-id="9aebe-175">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="9aebe-176">Giriş olarak NuGet geri yükleme, paket başvurularının proje dosyası (üst düzey veya doğrudan bağımlılıkları) kümesidir ve tam bir kapanış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının çıkış alınır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-176">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="9aebe-177">NuGet Packagereference'a listesi girişi değiştirilmediyse her zaman paket bağımlılıklarının aynı tam kapatma üretmek çalışır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-177">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="9aebe-178">Ancak, bunu yapmanız mümkün olduğu bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-178">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="9aebe-179">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9aebe-179">For example:</span></span>

* <span data-ttu-id="9aebe-180">Kayan kullandığınızda sürümleri ister `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-180">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="9aebe-181">Burada amaç, her geri yükleme paketlerinin en son sürüme kaydırmak için olsa da burada kullanıcıların grafiğin belirli en son sürümü ve sonraki bir sürüme kayan nokta varsa, açık bir hareket üzerine kilitlenmesine gerektiren senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-181">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="9aebe-182">Paket eşleşen PackageReference sürüm gereksinimleri daha yeni bir sürümü yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="9aebe-182">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="9aebe-183">Örneğin</span><span class="sxs-lookup"><span data-stu-id="9aebe-183">E.g.</span></span> 

  * <span data-ttu-id="9aebe-184">1\. günü: belirttiyseniz `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ancak NuGet depolarda sürüm 4.1.0, 4.2.0 ve 4.3.0 olmuştur.</span><span class="sxs-lookup"><span data-stu-id="9aebe-184">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="9aebe-185">Bu durumda, NuGet (en yakın en düşük sürüm) 4.1.0 çözümlendi</span><span class="sxs-lookup"><span data-stu-id="9aebe-185">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="9aebe-186">2\. gün: Sürüm 4.0.0 yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="9aebe-186">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="9aebe-187">NuGet şimdi tam eşleşme bulmak ve 4.0.0 için çözülmeye başlanacağı</span><span class="sxs-lookup"><span data-stu-id="9aebe-187">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="9aebe-188">Belirtilen Paket sürümü depodan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-188">A given package version is removed from the repository.</span></span> <span data-ttu-id="9aebe-189">Tüm paket depolarınızın nuget.org paket silme izin vermez ancak bu bir kısıtlama söz konusu.</span><span class="sxs-lookup"><span data-stu-id="9aebe-189">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="9aebe-190">En iyi eşleşen silinen sürümüne çözümleyemediğinde bulma NuGet sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-190">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="9aebe-191">Etkinleştirme kilidi dosyası</span><span class="sxs-lookup"><span data-stu-id="9aebe-191">Enabling lock file</span></span>
<span data-ttu-id="9aebe-192">Tam kapatma, kabul etme kilidi dosya özelliğini MSBuild özelliğini ayarlayarak paket bağımlılıklarının kalıcı hale getirmek için `RestorePackagesWithLockFile` projeniz için:</span><span class="sxs-lookup"><span data-stu-id="9aebe-192">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="9aebe-193">Bu özelliği ayarlarsanız, NuGet geri yükleme bir kilit dosyası - oluşturur `packages.lock.json` dosya proje kök dizininde tüm paket bağımlılıkları listeler.</span><span class="sxs-lookup"><span data-stu-id="9aebe-193">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="9aebe-194">Bir proje olduğunda `packages.lock.json` kök dizinde, kilit dosyanın dosyasındadır her zaman özelliği geri yükleme bile ile kullanılan `RestorePackagesWithLockFile` ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="9aebe-194">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="9aebe-195">İşlevsiz bir boş oluşturmak için kabul etmek için bu özellik için başka bir yolu, bu nedenle `packages.lock.json` proje kök dizinine dosyasında.</span><span class="sxs-lookup"><span data-stu-id="9aebe-195">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="9aebe-196">`restore` Kilit dosyasıyla davranışı</span><span class="sxs-lookup"><span data-stu-id="9aebe-196">`restore` behavior with lock file</span></span>
<span data-ttu-id="9aebe-197">Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak için kullanır. `restore`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-197">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="9aebe-198">NuGet Paket bağımlılıklarını proje dosyası (veya bağımlı proje dosyalarının) belirtildiği gibi herhangi bir değişiklik yoktu ve herhangi bir değişiklik varsa, yalnızca kilit dosyasında belirtilen paketleri geri yükler görmek için hızlı bir denetimi yapar.</span><span class="sxs-lookup"><span data-stu-id="9aebe-198">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="9aebe-199">Hiçbir Paket bağımlılıklarını değerlendirmeleri yoktur.</span><span class="sxs-lookup"><span data-stu-id="9aebe-199">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="9aebe-200">Proje dosyasında belirtildiği gibi bir değişiklik NuGet içinde tanımlanan bağımlılıklar algılar, paket grafiği yeniden değerlendirir ve kilit dosyası proje için yeni paket kapanış yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="9aebe-200">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="9aebe-201">CI/CD ve değil istediğiniz paket bağımlılıklarını hareket halindeyken değiştirmek için diğer senaryolar için ayarlayarak bunu yapabilirsiniz `lockedmode` için `true`:</span><span class="sxs-lookup"><span data-stu-id="9aebe-201">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="9aebe-202">DotNet.exe için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9aebe-202">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="9aebe-203">MSBuild.exe için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9aebe-203">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="9aebe-204">Ayrıca, proje dosyanızda koşullu bu MSBuild özelliği ayarlayabilir:</span><span class="sxs-lookup"><span data-stu-id="9aebe-204">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="9aebe-205">Kilitli modda ise `true`, geri yükleme ya da kilit dosyasında listelenen tam paketler geri veya proje için tanımlanmış Paket bağımlılıklarını kilit dosyası oluşturulduktan sonra güncelleştirdiyseniz başarısız.</span><span class="sxs-lookup"><span data-stu-id="9aebe-205">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="9aebe-206">Kilit dosya kaynak deponuza parçası olun</span><span class="sxs-lookup"><span data-stu-id="9aebe-206">Make lock file part of your source repository</span></span>
<span data-ttu-id="9aebe-207">NuGet yapabilmeleri için yürütülebilir bir uygulama oluşturuyorsanız ve söz konusu bağımlılık zincirinden başlangıcında projedir kilit dosyanın kaynak kod deposuna iade edin geri yükleme sırasında bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9aebe-207">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="9aebe-208">Projenizi gönderilen bir kitaplık projesi veya hangi diğer ortak bir kod projesi varsa ancak projeleri bağlı bağlıdır **barındırmamalıdır** kaynak kodunuzu bir parçası olarak kilit dosyasında denetleyin.</span><span class="sxs-lookup"><span data-stu-id="9aebe-208">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="9aebe-209">Kilit dosyası tutma içinde hiçbir zarar yoktur, ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesi üzerinde bağımlı bir proje geri yükleme/derleme sırasında kilit dosyasında listelenen kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9aebe-209">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="9aebe-210">Örn.</span><span class="sxs-lookup"><span data-stu-id="9aebe-210">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="9aebe-211">Varsa `ProjectA` bir bağımlılığa sahip bir `PackageX` sürüm `2.0.0` ve ayrıca başvuran `ProjectB` , bağımlı `PackageX` sürüm `1.0.0`, ardından kilit dosyası için `ProjectB` üzerinde bir bağımlılık listeler `PackageX` Sürüm `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-211">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="9aebe-212">Ancak, `ProjectA` yapılandırıldığında, kendi kilit dosya çubuğunda bir bağımlılık içerecek `PackageX` sürüm **`2.0.0`** ve **değil** `1.0.0` kilitdosyasındalistelenen`ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-212">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="9aebe-213">Bu nedenle, ortak bir kod projesi kilit dosyanın bağımlı projeler için çözülmüş paketleri üzerinde çok az say sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9aebe-213">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="9aebe-214">Kilit dosya genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="9aebe-214">Lock file extensibility</span></span>
<span data-ttu-id="9aebe-215">Aşağıda açıklandığı gibi çeşitli geri yükleme davranışlarını kilit dosyasıyla denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9aebe-215">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="9aebe-216">Seçenek</span><span class="sxs-lookup"><span data-stu-id="9aebe-216">Option</span></span> | <span data-ttu-id="9aebe-217">MSBuild eşdeğer seçeneği</span><span class="sxs-lookup"><span data-stu-id="9aebe-217">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="9aebe-218">Bir proje için kilit dosyasının bootstraps kullanın.</span><span class="sxs-lookup"><span data-stu-id="9aebe-218">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="9aebe-219">Alternatif olarak ayarlayabilirsiniz `RestorePackagesWithLockFile` proje dosyasındaki özelliği</span><span class="sxs-lookup"><span data-stu-id="9aebe-219">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="9aebe-220">Geri yükleme modunu etkinleştirir kilitli.</span><span class="sxs-lookup"><span data-stu-id="9aebe-220">Enables locked mode for restore.</span></span> <span data-ttu-id="9aebe-221">Bu, yinelenebilir derlemeleri almak istediğiniz CI/CD senaryolarda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-221">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="9aebe-222">Bu ayarlayarak olabilir `RestoreLockedMode` MSBuild özelliği `true`</span><span class="sxs-lookup"><span data-stu-id="9aebe-222">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="9aebe-223">Bu seçenek projede tanımlanan kayan sürümüyle paketlerle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9aebe-223">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="9aebe-224">Geri yükleme işlemi çalıştırmadığınız sürece varsayılan olarak NuGet geri yükleme Paket sürümü her geri yükleme sırasında otomatik olarak güncelleştirmez `--force-evaluate` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="9aebe-224">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="9aebe-225">Bir proje için özel kilit dosya konumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9aebe-225">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="9aebe-226">Bu ayrıca MSBuild özelliği ayarlanarak sağlanabilir `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="9aebe-226">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="9aebe-227">Varsayılan olarak, NuGet destekler `packages.lock.json` kök dizininde.</span><span class="sxs-lookup"><span data-stu-id="9aebe-227">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="9aebe-228">Aynı dizinde birden çok proje varsa, NuGet proje belirli kilit dosyası destekler. `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="9aebe-228">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
