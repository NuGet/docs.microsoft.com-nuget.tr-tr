---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 464bf52cabe64696270fc391b2c23de9c6ba24f7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488145"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="62791-103">Proje dosyalarında paket başvuruları (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="62791-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="62791-104">Paket başvuruları, `PackageReference` düğümü kullanarak, NuGet bağımlılıklarını doğrudan proje dosyaları içinde (ayrı `packages.config` bir dosyanın aksine) yönetir.</span><span class="sxs-lookup"><span data-stu-id="62791-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="62791-105">Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalardaki (paket kaynakları dahil) ayarlar, [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.</span><span class="sxs-lookup"><span data-stu-id="62791-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="62791-106">PackageReference ile, MSBuild koşullarını hedef çerçeve, yapılandırma, platform veya diğer gruplandırmalar için paket başvuruları seçmek üzere de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62791-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="62791-107">Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="62791-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="62791-108">(Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="62791-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="62791-109">Proje türü desteği</span><span class="sxs-lookup"><span data-stu-id="62791-109">Project type support</span></span>

<span data-ttu-id="62791-110">Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projelerinin dışında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62791-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="62791-111">.NET Framework projeler, PackageReference destekler, ancak şu anda `packages.config`varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="62791-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="62791-112">Packagereference kullanmak için, [](../consume-packages/migrate-packages-config-to-package-reference.md) bağımlılıkları `packages.config` proje dosyanıza geçirin, sonra Packages. config 'i kaldırın.</span><span class="sxs-lookup"><span data-stu-id="62791-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="62791-113">Tam .NET Framework hedefleyen uygulamalar, PackageReference için yalnızca [sınırlı desteği](https://github.com/NuGet/Home/issues/5877) içerir.</span><span class="sxs-lookup"><span data-stu-id="62791-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="62791-114">C++ve JavaScript proje türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="62791-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="62791-115">PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="62791-115">Adding a PackageReference</span></span>

<span data-ttu-id="62791-116">Aşağıdaki sözdizimini kullanarak proje dosyanıza bir bağımlılık ekleyin:</span><span class="sxs-lookup"><span data-stu-id="62791-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="62791-117">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="62791-117">Controlling dependency version</span></span>

<span data-ttu-id="62791-118">Bir paketin sürümünü belirtme kuralı, kullanırken `packages.config`olduğu gibi aynıdır:</span><span class="sxs-lookup"><span data-stu-id="62791-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62791-119">Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges-and-wildcards)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip > = 3.6.0 olan herhangi bir sürüm anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="62791-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="62791-120">Packagereferde olmayan bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="62791-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="62791-121">İleri Bir projede yüklü paketleriniz yoksa (proje dosyasında ve hiçbir paket. config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği RestoreProjectStyle öğesini projenizde PackageReference olarak ayarlayabilirsiniz dosyasýný.</span><span class="sxs-lookup"><span data-stu-id="62791-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="62791-122">Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="62791-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="62791-123">Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="62791-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="62791-124">Kayan sürümler</span><span class="sxs-lookup"><span data-stu-id="62791-124">Floating Versions</span></span>

<span data-ttu-id="62791-125">[Kayan sürümler](../concepts/dependency-resolution.md#floating-versions) ile `PackageReference`desteklenir:</span><span class="sxs-lookup"><span data-stu-id="62791-125">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="62791-126">Bağımlılık varlıklarını denetleme</span><span class="sxs-lookup"><span data-stu-id="62791-126">Controlling dependency assets</span></span>

<span data-ttu-id="62791-127">Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62791-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="62791-128">Bu senaryoda, bu davranışı denetlemek için `PrivateAssets` meta verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62791-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62791-129">Aşağıdaki meta veri etiketleri denetim bağımlılığı varlıkları:</span><span class="sxs-lookup"><span data-stu-id="62791-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="62791-130">Etiket</span><span class="sxs-lookup"><span data-stu-id="62791-130">Tag</span></span> | <span data-ttu-id="62791-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62791-131">Description</span></span> | <span data-ttu-id="62791-132">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="62791-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62791-133">Includevarlıklarını</span><span class="sxs-lookup"><span data-stu-id="62791-133">IncludeAssets</span></span> | <span data-ttu-id="62791-134">Bu varlıklar tüketilecektir</span><span class="sxs-lookup"><span data-stu-id="62791-134">These assets will be consumed</span></span> | <span data-ttu-id="62791-135">tüm</span><span class="sxs-lookup"><span data-stu-id="62791-135">all</span></span> |
| <span data-ttu-id="62791-136">Excludevarlıklarının</span><span class="sxs-lookup"><span data-stu-id="62791-136">ExcludeAssets</span></span> | <span data-ttu-id="62791-137">Bu varlıklar tüketilmeyecek</span><span class="sxs-lookup"><span data-stu-id="62791-137">These assets will not be consumed</span></span> | <span data-ttu-id="62791-138">yok</span><span class="sxs-lookup"><span data-stu-id="62791-138">none</span></span> |
| <span data-ttu-id="62791-139">Privatevarlıkların</span><span class="sxs-lookup"><span data-stu-id="62791-139">PrivateAssets</span></span> | <span data-ttu-id="62791-140">Bu varlıklar tüketilecektir, ancak üst projeye akamaz</span><span class="sxs-lookup"><span data-stu-id="62791-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="62791-141">ContentFiles; çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="62791-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="62791-142">Bu etiketler için izin verilen değerler aşağıdaki gibidir: ile `all` , ve arasında bir noktalı virgülle ayrılmış birden çok değer ve `none` kendileri tarafından görünmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="62791-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="62791-143">Değer</span><span class="sxs-lookup"><span data-stu-id="62791-143">Value</span></span> | <span data-ttu-id="62791-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62791-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="62791-145">se</span><span class="sxs-lookup"><span data-stu-id="62791-145">compile</span></span> | <span data-ttu-id="62791-146">`lib` Klasörün içeriği ve projenizin içindeki derlemelere göre derleyemeyeceğini denetler</span><span class="sxs-lookup"><span data-stu-id="62791-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="62791-147">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="62791-147">runtime</span></span> | <span data-ttu-id="62791-148">`lib` Ve`runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler</span><span class="sxs-lookup"><span data-stu-id="62791-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="62791-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="62791-149">contentFiles</span></span> | <span data-ttu-id="62791-150">`contentfiles` Klasörün içeriği</span><span class="sxs-lookup"><span data-stu-id="62791-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="62791-151">derleme</span><span class="sxs-lookup"><span data-stu-id="62791-151">build</span></span> | <span data-ttu-id="62791-152">`.props`ve `.targets` klasörü`build`</span><span class="sxs-lookup"><span data-stu-id="62791-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="62791-153">Buildmultihedefleme</span><span class="sxs-lookup"><span data-stu-id="62791-153">buildMultitargeting</span></span> | <span data-ttu-id="62791-154">`.props`ve `.targets`klasöründe,platformlar arasıhedeflemeiçin`buildMultitargeting`</span><span class="sxs-lookup"><span data-stu-id="62791-154">`.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="62791-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="62791-155">buildTransitive</span></span> | <span data-ttu-id="62791-156">*(5.0 +)* `.props` ve`.targets` klasörü, her bir tüketen projeye geçişli olarak akan varlıklar içindir. `buildTransitive`</span><span class="sxs-lookup"><span data-stu-id="62791-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="62791-157">Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası.</span><span class="sxs-lookup"><span data-stu-id="62791-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="62791-158">Çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="62791-158">analyzers</span></span> | <span data-ttu-id="62791-159">.NET Çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="62791-159">.NET analyzers</span></span> |
| <span data-ttu-id="62791-160">yerel</span><span class="sxs-lookup"><span data-stu-id="62791-160">native</span></span> | <span data-ttu-id="62791-161">`native` Klasörün içeriği</span><span class="sxs-lookup"><span data-stu-id="62791-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="62791-162">yok</span><span class="sxs-lookup"><span data-stu-id="62791-162">none</span></span> | <span data-ttu-id="62791-163">Yukarıdakilerin hiçbiri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="62791-163">None of the above are used.</span></span> |
| <span data-ttu-id="62791-164">tüm</span><span class="sxs-lookup"><span data-stu-id="62791-164">all</span></span> | <span data-ttu-id="62791-165">Yukarıdakilerin tümü (hariç `none`)</span><span class="sxs-lookup"><span data-stu-id="62791-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="62791-166">Aşağıdaki örnekte, paketteki içerik dosyaları hariç her şey proje tarafından, içerik dosyaları ve çözümleyiciler hariç her şey üst projeye akacaktır.</span><span class="sxs-lookup"><span data-stu-id="62791-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="62791-167">İle `build` birlikte`PrivateAssets`dahil edilmediğinden, hedefler ve props ana projeye akacağından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="62791-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="62791-168">Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="62791-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="62791-169">Appgünlükçü, appgünlükçü kullanan projeler gibi, `Contoso.Utility.UsefulStuff`öğesinden hedefleri ve props 'ı kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="62791-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="62791-170">`developmentDependency` , `true` Bir dosyada`.nuspec` olarak ayarlandığında, paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir paketi yalnızca geliştirme bağımlılığı olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="62791-170">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="62791-171">PackageReference *(NuGet 4.8 +)* ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="62791-171">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="62791-172">Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="62791-172">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="62791-173">PackageReference koşulu ekleme</span><span class="sxs-lookup"><span data-stu-id="62791-173">Adding a PackageReference condition</span></span>

<span data-ttu-id="62791-174">Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="62791-174">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="62791-175">Ancak şu anda yalnızca `TargetFramework` değişken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="62791-175">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="62791-176">Örneğin, hedeflentiğinizi `netstandard1.4` `net452` ve yalnızca için `net452`geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="62791-176">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="62791-177">Bu durumda, paketinize tüketen bir `netstandard1.4` projenin bu gereksiz bağımlılığı eklemesini istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="62791-177">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="62791-178">Bunu engellemek için aşağıdaki `PackageReference` şekilde bir koşul belirtirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62791-178">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="62791-179">Bu proje kullanılarak oluşturulan bir paket, Newtonsoft. json ' ın yalnızca bir `net452` hedef için bağımlılık olarak ekleneceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="62791-179">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="62791-181">Koşullar da `ItemGroup` düzeyde uygulanabilir ve tüm alt `PackageReference` öğeler için geçerli olacaktır:</span><span class="sxs-lookup"><span data-stu-id="62791-181">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="62791-182">Bağımlılıkları kilitleme</span><span class="sxs-lookup"><span data-stu-id="62791-182">Locking dependencies</span></span>
<span data-ttu-id="62791-183">*Bu özellik NuGet **4,9** veya sonraki sürümlerde ve Visual Studio 2017 **15,9** veya üzeri sürümlerde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="62791-183">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="62791-184">NuGet geri yükleme girdisi, proje dosyasından (en üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıkış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının tam bir kapasitesinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="62791-184">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="62791-185">NuGet, giriş PackageReference listesi değişmediğinde paket bağımlılıklarının her zaman aynı tam kapatılmasını üretmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="62791-185">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="62791-186">Ancak, bunu yapamaması gereken bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="62791-186">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="62791-187">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="62791-187">For example:</span></span>

* <span data-ttu-id="62791-188">Gibi `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`kayan sürümler kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="62791-188">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="62791-189">Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.</span><span class="sxs-lookup"><span data-stu-id="62791-189">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="62791-190">Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="62791-190">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="62791-191">Örneğin</span><span class="sxs-lookup"><span data-stu-id="62791-191">E.g.</span></span> 

  * <span data-ttu-id="62791-192">1\. gün: ancak NuGet `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` depolarında kullanılabilen sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="62791-192">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="62791-193">Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir</span><span class="sxs-lookup"><span data-stu-id="62791-193">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="62791-194">Gün 2: Sürüm 4.0.0 yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="62791-194">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="62791-195">NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak</span><span class="sxs-lookup"><span data-stu-id="62791-195">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="62791-196">Belirli bir paket sürümü depodan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="62791-196">A given package version is removed from the repository.</span></span> <span data-ttu-id="62791-197">Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="62791-197">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="62791-198">Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.</span><span class="sxs-lookup"><span data-stu-id="62791-198">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="62791-199">Kilit dosyası etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="62791-199">Enabling lock file</span></span>
<span data-ttu-id="62791-200">Paket bağımlılıklarının tam kapatılmasını kalıcı hale getirmek için, projeniz için MSBuild özelliğini `RestorePackagesWithLockFile` ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62791-200">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="62791-201">Bu özellik ayarlandıysa, NuGet geri yükleme proje kök dizininde tüm paket bağımlılıklarını listeleyen `packages.lock.json` bir kilit dosya dosyası oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="62791-201">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="62791-202">Bir projenin kök dizininde `packages.lock.json` dosyası varsa, özellik `RestorePackagesWithLockFile` ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62791-202">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="62791-203">Bu nedenle, bu özelliği kabul etmenin başka bir yolu da projenin kök dizininde kukla boş `packages.lock.json` bir dosya oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="62791-203">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="62791-204">`restore`kilit dosyası ile davranış</span><span class="sxs-lookup"><span data-stu-id="62791-204">`restore` behavior with lock file</span></span>
<span data-ttu-id="62791-205">Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak `restore`için kullanır.</span><span class="sxs-lookup"><span data-stu-id="62791-205">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="62791-206">NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="62791-206">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="62791-207">Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="62791-207">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="62791-208">NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="62791-208">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="62791-209">CI/CD ve diğer senaryolar için, anında paket bağımlılıklarını değiştirmek istemediğiniz için, ' yi ' `lockedmode` e `true`ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62791-209">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="62791-210">DotNet. exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="62791-210">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="62791-211">MSBuild. exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="62791-211">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="62791-212">Bu koşullu MSBuild özelliğini, proje dosyanızda de ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62791-212">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="62791-213">Kilitli mod ise `true`geri yükleme işlemi, kilit dosyası oluşturulduktan sonra, proje için tanımlanan paket bağımlılıklarını güncelleştirdikten sonra tam paketleri kilit dosyasında listelenen şekilde geri yükler ya da başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="62791-213">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="62791-214">Kaynak deponuzun kilit dosyası parçasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="62791-214">Make lock file part of your source repository</span></span>
<span data-ttu-id="62791-215">Bir uygulama oluşturuyorsanız, bir çalıştırılabilir dosya ve söz konusu proje, bağımlılık zincirinin başlangıcında yer alıyorsa, NuGet 'in geri yükleme sırasında kullanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.</span><span class="sxs-lookup"><span data-stu-id="62791-215">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="62791-216">Ancak, projeniz sevk ettiğiniz bir kitaplık projem veya diğer projelerin bağımlı olduğu ortak bir kod projesi ise, kilit dosyasını kaynak kodunuzun bir parçası olarak iade etmeniz **gerekir** .</span><span class="sxs-lookup"><span data-stu-id="62791-216">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="62791-217">Kilit dosyası tutulmayan bir sorun yoktur ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesine bağlı bir projenin geri yükleme/oluşturma işlemi sırasında kilit dosyasında listelendiği gibi kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="62791-217">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="62791-218">Örn.</span><span class="sxs-lookup"><span data-stu-id="62791-218">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="62791-219">Bir `ProjectA` `PackageX` sürüme bağımlılığının`ProjectB` yanı sıra `ProjectB` `PackageX` sürüme bağlı`1.0.0`olan başvurular varsa, için kilit dosyası şuna bir bağımlılık listeleyecek `PackageX` `2.0.0` Sürüm `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="62791-219">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="62791-220">Ancak, `ProjectA` yapılandırıldığında kilit dosyası, için kilit dosyasında listelenenlerin **değil** `1.0.0` , `PackageX` sürüm **`2.0.0`** için `ProjectB`bir bağımlılık içerecektir.</span><span class="sxs-lookup"><span data-stu-id="62791-220">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="62791-221">Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="62791-221">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="62791-222">Kilit dosyası genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="62791-222">Lock file extensibility</span></span>
<span data-ttu-id="62791-223">Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62791-223">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="62791-224">Seçenek</span><span class="sxs-lookup"><span data-stu-id="62791-224">Option</span></span> | <span data-ttu-id="62791-225">MSBuild eşdeğer seçeneği</span><span class="sxs-lookup"><span data-stu-id="62791-225">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="62791-226">Önyükleme bir proje için kilit dosyası kullanımı.</span><span class="sxs-lookup"><span data-stu-id="62791-226">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="62791-227">Alternatif olarak proje dosyasında `RestorePackagesWithLockFile` özelliği ayarlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="62791-227">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="62791-228">Geri yükleme için kilitli modu etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="62791-228">Enables locked mode for restore.</span></span> <span data-ttu-id="62791-229">Bu, yinelenebilir derlemeleri almak istediğiniz CI/CD senaryolarında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="62791-229">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="62791-230">Bu, `RestoreLockedMode` MSBuild özelliğinin ' i olarak ayarlanmasına de izin verebilir`true`</span><span class="sxs-lookup"><span data-stu-id="62791-230">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="62791-231">Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="62791-231">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="62791-232">Varsayılan olarak, geri yükle seçeneğini birlikte `--force-evaluate` çalıştırmadığınız takdirde NuGet geri yükleme, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="62791-232">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="62791-233">Bir proje için özel bir kilit dosyası konumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="62791-233">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="62791-234">Bu, MSBuild özelliği `NuGetLockFilePath`ayarlanarak da elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="62791-234">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="62791-235">Varsayılan olarak, NuGet kök `packages.lock.json` dizinde destekler.</span><span class="sxs-lookup"><span data-stu-id="62791-235">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="62791-236">Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="62791-236">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
