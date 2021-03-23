---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: df7c793d115622f04a148cbbc3ebf396a3e4ab69
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859193"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="e2090-103">Proje dosyalarındaki paket başvuruları ( `PackageReference` )</span><span class="sxs-lookup"><span data-stu-id="e2090-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="e2090-104">Paket başvuruları, düğümü kullanarak `PackageReference` , NuGet bağımlılıklarını doğrudan proje dosyaları içinde (ayrı bir `packages.config` dosyanın aksine) yönetir.</span><span class="sxs-lookup"><span data-stu-id="e2090-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="e2090-105">Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalardaki (paket kaynakları dahil) ayarlar, [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e2090-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="e2090-106">PackageReference ile, MSBuild koşullarını hedef çerçeve başına paket başvurularını veya diğer gruplandırmaları seçmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2090-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="e2090-107">Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2090-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="e2090-108">(Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="e2090-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="e2090-109">Proje türü desteği</span><span class="sxs-lookup"><span data-stu-id="e2090-109">Project type support</span></span>

<span data-ttu-id="e2090-110">Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projeleri dışında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e2090-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="e2090-111">.NET Framework projeler, PackageReference destekler, ancak şu anda varsayılan olarak `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="e2090-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="e2090-112">PackageReference kullanmak için, [](../consume-packages/migrate-packages-config-to-package-reference.md) bağımlılıkları `packages.config` proje dosyanıza geçirin ve ardından packages.config kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e2090-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="e2090-113">Tam .NET Framework hedefleyen uygulamalar, PackageReference için yalnızca [sınırlı desteği](https://github.com/NuGet/Home/issues/5877) içerir.</span><span class="sxs-lookup"><span data-stu-id="e2090-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="e2090-114">C++ ve JavaScript proje türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e2090-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="e2090-115">PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="e2090-115">Adding a PackageReference</span></span>

<span data-ttu-id="e2090-116">Aşağıdaki sözdizimini kullanarak proje dosyanıza bir bağımlılık ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e2090-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="e2090-117">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="e2090-117">Controlling dependency version</span></span>

<span data-ttu-id="e2090-118">Bir paketin sürümünü belirtme kuralı, kullanırken olduğu gibi aynıdır `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="e2090-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e2090-119">Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip >= 3.6.0 olan herhangi bir sürüm anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e2090-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="e2090-120">Packagereferde olmayan bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="e2090-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="e2090-121">Gelişmiş: bir projede yüklü paketleriniz yoksa (proje dosyasında ve hiçbir packages.config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği olarak bir proje özelliği olarak, proje dosyanızda PackageReference olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2090-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="e2090-122">Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="e2090-123">Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e2090-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="e2090-124">PackageReference ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="e2090-124">PackageReference and sources</span></span>

<span data-ttu-id="e2090-125">PackageReference projelerinde, geçişli bağımlılık sürümleri geri yükleme sırasında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="e2090-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="e2090-126">Bu nedenle, PackageReference projelerinde tüm kaynakların tüm geri yüklemeler için kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2090-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="e2090-127">Kayan sürümler</span><span class="sxs-lookup"><span data-stu-id="e2090-127">Floating Versions</span></span>

<span data-ttu-id="e2090-128">[Kayan sürümler](../concepts/dependency-resolution.md#floating-versions) ile desteklenir `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="e2090-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="e2090-129">Bağımlılık varlıklarını denetleme</span><span class="sxs-lookup"><span data-stu-id="e2090-129">Controlling dependency assets</span></span>

<span data-ttu-id="e2090-130">Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2090-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="e2090-131">Bu senaryoda, `PrivateAssets` Bu davranışı denetlemek için meta verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2090-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e2090-132">Aşağıdaki meta veri etiketleri denetim bağımlılığı varlıkları:</span><span class="sxs-lookup"><span data-stu-id="e2090-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="e2090-133">Etiket</span><span class="sxs-lookup"><span data-stu-id="e2090-133">Tag</span></span> | <span data-ttu-id="e2090-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e2090-134">Description</span></span> | <span data-ttu-id="e2090-135">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="e2090-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2090-136">Includevarlıklarını</span><span class="sxs-lookup"><span data-stu-id="e2090-136">IncludeAssets</span></span> | <span data-ttu-id="e2090-137">Bu varlıklar tüketilecektir</span><span class="sxs-lookup"><span data-stu-id="e2090-137">These assets will be consumed</span></span> | <span data-ttu-id="e2090-138">tümü</span><span class="sxs-lookup"><span data-stu-id="e2090-138">all</span></span> |
| <span data-ttu-id="e2090-139">Excludevarlıklarının</span><span class="sxs-lookup"><span data-stu-id="e2090-139">ExcludeAssets</span></span> | <span data-ttu-id="e2090-140">Bu varlıklar tüketilmeyecek</span><span class="sxs-lookup"><span data-stu-id="e2090-140">These assets will not be consumed</span></span> | <span data-ttu-id="e2090-141">yok</span><span class="sxs-lookup"><span data-stu-id="e2090-141">none</span></span> |
| <span data-ttu-id="e2090-142">Privatevarlıkların</span><span class="sxs-lookup"><span data-stu-id="e2090-142">PrivateAssets</span></span> | <span data-ttu-id="e2090-143">Bu varlıklar tüketilecektir, ancak üst projeye akamaz</span><span class="sxs-lookup"><span data-stu-id="e2090-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="e2090-144">ContentFiles; çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="e2090-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="e2090-145">Bu etiketler için izin verilen değerler aşağıdaki gibidir: ile, ve arasında bir noktalı virgülle ayrılmış birden çok değer `all` ve `none` kendileri tarafından görünmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2090-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="e2090-146">Değer</span><span class="sxs-lookup"><span data-stu-id="e2090-146">Value</span></span> | <span data-ttu-id="e2090-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e2090-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="e2090-148">derle</span><span class="sxs-lookup"><span data-stu-id="e2090-148">compile</span></span> | <span data-ttu-id="e2090-149">`lib`Klasörün içeriği ve projenizin içindeki derlemelere göre derleyemeyeceğini denetler</span><span class="sxs-lookup"><span data-stu-id="e2090-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="e2090-150">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="e2090-150">runtime</span></span> | <span data-ttu-id="e2090-151">`lib`Ve `runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler</span><span class="sxs-lookup"><span data-stu-id="e2090-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="e2090-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e2090-152">contentFiles</span></span> | <span data-ttu-id="e2090-153">`contentfiles`Klasörün içeriği</span><span class="sxs-lookup"><span data-stu-id="e2090-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="e2090-154">derleme</span><span class="sxs-lookup"><span data-stu-id="e2090-154">build</span></span> | <span data-ttu-id="e2090-155">`.props` ve `.targets` `build` klasörü</span><span class="sxs-lookup"><span data-stu-id="e2090-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="e2090-156">Buildmultihedefleme</span><span class="sxs-lookup"><span data-stu-id="e2090-156">buildMultitargeting</span></span> | <span data-ttu-id="e2090-157">*(4,0)* `.props` ve `.targets` `buildMultitargeting` klasöründe, platformlar arası hedefleme için</span><span class="sxs-lookup"><span data-stu-id="e2090-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="e2090-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="e2090-158">buildTransitive</span></span> | <span data-ttu-id="e2090-159">*(5.0 +)* `.props` ve `.targets` `buildTransitive` klasörü, her bir tüketen projeye geçişli olarak akan varlıklar içindir.</span><span class="sxs-lookup"><span data-stu-id="e2090-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="e2090-160">Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası.</span><span class="sxs-lookup"><span data-stu-id="e2090-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="e2090-161">Çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="e2090-161">analyzers</span></span> | <span data-ttu-id="e2090-162">.NET çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="e2090-162">.NET analyzers</span></span> |
| <span data-ttu-id="e2090-163">yerel</span><span class="sxs-lookup"><span data-stu-id="e2090-163">native</span></span> | <span data-ttu-id="e2090-164">`native`Klasörün içeriği</span><span class="sxs-lookup"><span data-stu-id="e2090-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="e2090-165">yok</span><span class="sxs-lookup"><span data-stu-id="e2090-165">none</span></span> | <span data-ttu-id="e2090-166">Yukarıdakilerin hiçbiri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="e2090-166">None of the above are used.</span></span> |
| <span data-ttu-id="e2090-167">tümü</span><span class="sxs-lookup"><span data-stu-id="e2090-167">all</span></span> | <span data-ttu-id="e2090-168">Yukarıdakilerin tümü (hariç `none` )</span><span class="sxs-lookup"><span data-stu-id="e2090-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="e2090-169">Aşağıdaki örnekte, paketteki içerik dosyaları hariç her şey proje tarafından, içerik dosyaları ve çözümleyiciler hariç her şey üst projeye akacaktır.</span><span class="sxs-lookup"><span data-stu-id="e2090-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="e2090-170">`build`İle birlikte dahil edilmediğinden `PrivateAssets` , hedefler ve props ana projeye akacağından  emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e2090-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="e2090-171">Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e2090-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="e2090-172">Appgünlükçü, `Contoso.Utility.UsefulStuff` Appgünlükçü kullanan projeler gibi, öğesinden hedefleri ve props 'ı kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="e2090-173">`developmentDependency` `true` , Bir dosyada olarak ayarlandığında `.nuspec` , paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir paketi yalnızca geliştirme bağımlılığı olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="e2090-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="e2090-174">PackageReference *(NuGet 4.8 +)* ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e2090-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="e2090-175">Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="e2090-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="e2090-176">PackageReference koşulu ekleme</span><span class="sxs-lookup"><span data-stu-id="e2090-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="e2090-177">Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="e2090-178">Ancak şu anda yalnızca `TargetFramework` değişken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e2090-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="e2090-179">Örneğin, hedeflentiğinizi ve `netstandard1.4` `net452` yalnızca için geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım `net452` .</span><span class="sxs-lookup"><span data-stu-id="e2090-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="e2090-180">Bu durumda, `netstandard1.4` paketinize tüketen bir projenin bu gereksiz bağımlılığı eklemesini istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2090-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="e2090-181">Bunu engellemek için aşağıdaki şekilde bir koşul belirtirsiniz `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="e2090-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e2090-182">Bu proje kullanılarak oluşturulan bir paket, üzerinde Newtonsoft.Js, yalnızca bir hedefin bağımlılığı olarak ekleneceğini gösterir `net452` :</span><span class="sxs-lookup"><span data-stu-id="e2090-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="e2090-184">Koşullar da `ItemGroup` düzeyde uygulanabilir ve tüm alt öğeler için geçerli olacaktır `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="e2090-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="e2090-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="e2090-185">GeneratePathProperty</span></span>

<span data-ttu-id="e2090-186">Bu özellik NuGet **5,0** veya sonraki sürümlerde ve Visual Studio 2019 **16,0** veya üzeri sürümlerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="e2090-187">Bazen bir MSBuild hedefinden bir paketteki dosyalara başvurulmasına tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="e2090-188">`packages.config`Tabanlı projelerde, paketler proje dosyası ile ilişkili bir klasöre yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e2090-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="e2090-189">Ancak, PackageReference içinde paketler, makineden makineye değişebilen *küresel paketler* [klasöründen kullanılır.](../concepts/package-installation-process.md)</span><span class="sxs-lookup"><span data-stu-id="e2090-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="e2090-190">Bu boşluğu bağlamak için, NuGet paketin tükettiği konuma işaret eden bir özellik sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="e2090-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="e2090-191">Örnek:</span><span class="sxs-lookup"><span data-stu-id="e2090-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="e2090-192">Ayrıca NuGet, bir Araçlar klasörü içeren paketler için otomatik olarak Özellikler oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="e2090-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="e2090-193">MSBuild özellikleri ve paket kimlikleri aynı kısıtlamalara sahip değildir, bu nedenle paket kimliğinin, sözcüğün ön eki olan MSBuild kolay adına değiştirilmesi gerekir `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="e2090-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="e2090-194">Oluşturulan özelliğin tam adını doğrulamak için, oluşturulan [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="e2090-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="e2090-195">PackageReference diğer adları</span><span class="sxs-lookup"><span data-stu-id="e2090-195">PackageReference Aliases</span></span>

<span data-ttu-id="e2090-196">Nadir bazı örneklerde farklı paketler aynı ad alanındaki sınıfları içerecektir.</span><span class="sxs-lookup"><span data-stu-id="e2090-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="e2090-197">NuGet 5,7 ' den başlayarak, ProjectReference ile eşdeğer olan Visual Studio 2019 güncelleştirme 7 &, PackageReference desteklenir [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="e2090-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="e2090-198">Varsayılan olarak, diğer ad sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="e2090-198">By default no aliases are provided.</span></span> <span data-ttu-id="e2090-199">Bir diğer ad belirtildiğinde, ek açıklamalı paketten gelen *Tüm* derlemeler bir diğer adla başvurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e2090-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="e2090-200">[Nuget\samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample) ' da örnek kullanıma bakabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2090-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="e2090-201">Proje dosyasında, diğer adları aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="e2090-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="e2090-202">kodda, bunu aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="e2090-202">and in the code use it as follows:</span></span>

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="e2090-203">NuGet uyarıları ve hataları</span><span class="sxs-lookup"><span data-stu-id="e2090-203">NuGet warnings and errors</span></span>

<span data-ttu-id="e2090-204">*Bu özellik NuGet **4,3** veya sonraki sürümlerde ve Visual Studio 2017 **15,3** veya üzeri sürümlerde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="e2090-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="e2090-205">Birçok paket ve geri yükleme senaryosunda, tüm NuGet uyarıları ve hataları kodlanır ve ile başlar `NU****` .</span><span class="sxs-lookup"><span data-stu-id="e2090-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="e2090-206">Tüm NuGet uyarıları ve hataları [başvuru](../reference/errors-and-warnings.md) belgelerinde listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e2090-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="e2090-207">NuGet obonu aşağıdaki uyarı özelliklerine hizmet eder:</span><span class="sxs-lookup"><span data-stu-id="e2090-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="e2090-208">`TreatWarningsAsErrors`, tüm uyarıları hata olarak değerlendir</span><span class="sxs-lookup"><span data-stu-id="e2090-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="e2090-209">`WarningsAsErrors`, belirli uyarıları hata olarak değerlendir</span><span class="sxs-lookup"><span data-stu-id="e2090-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="e2090-210">`NoWarn`, proje genelinde veya paket genelinde belirli uyarıları gizleyin.</span><span class="sxs-lookup"><span data-stu-id="e2090-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="e2090-211">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="e2090-211">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="e2090-212">NuGet uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="e2090-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="e2090-213">Paket ve geri yükleme işlemleri sırasında tüm NuGet uyarılarını çözmeniz önerilir, ancak bazı durumlarda bunların garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="e2090-214">Bir uyarı projesini genelinde gizlemek için şunları yapmayı düşünün:</span><span class="sxs-lookup"><span data-stu-id="e2090-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="e2090-215">Bazen uyarılar yalnızca grafikteki belirli bir paket için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e2090-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="e2090-216">PackageReference öğesine bir ekleyerek bu uyarının daha seçmeli şekilde görüntülenmesini seçebiliriz `NoWarn` .</span><span class="sxs-lookup"><span data-stu-id="e2090-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="e2090-217">Visual Studio 'da NuGet paket uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="e2090-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="e2090-218">Visual Studio 'da Ayrıca, uyarıları IDE aracılığıyla da [gizleyebilirsiniz](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) .</span><span class="sxs-lookup"><span data-stu-id="e2090-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="e2090-219">Bağımlılıkları kilitleme</span><span class="sxs-lookup"><span data-stu-id="e2090-219">Locking dependencies</span></span>

<span data-ttu-id="e2090-220">*Bu özellik NuGet **4,9** veya sonraki sürümlerde ve Visual Studio 2017 **15,9** veya üzeri sürümlerde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="e2090-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="e2090-221">NuGet geri yükleme girdisi, proje dosyasından (en üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıkış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının tam bir kapasitesinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="e2090-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="e2090-222">NuGet, giriş PackageReference listesi değişmediğinde paket bağımlılıklarının her zaman aynı tam kapatılmasını üretmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="e2090-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="e2090-223">Ancak, bunu yapamaması gereken bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="e2090-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="e2090-224">Örnek:</span><span class="sxs-lookup"><span data-stu-id="e2090-224">For example:</span></span>

* <span data-ttu-id="e2090-225">Gibi kayan sürümler kullandığınızda `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` .</span><span class="sxs-lookup"><span data-stu-id="e2090-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="e2090-226">Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.</span><span class="sxs-lookup"><span data-stu-id="e2090-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="e2090-227">Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="e2090-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="e2090-228">Örneğin</span><span class="sxs-lookup"><span data-stu-id="e2090-228">E.g.</span></span> 

  * <span data-ttu-id="e2090-229">1. gün: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ancak NuGet depolarında kullanılabilen sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e2090-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="e2090-230">Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir</span><span class="sxs-lookup"><span data-stu-id="e2090-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="e2090-231">2. gün: sürüm 4.0.0 yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="e2090-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="e2090-232">NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak</span><span class="sxs-lookup"><span data-stu-id="e2090-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="e2090-233">Belirli bir paket sürümü depodan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="e2090-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="e2090-234">Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="e2090-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="e2090-235">Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.</span><span class="sxs-lookup"><span data-stu-id="e2090-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="e2090-236">Kilit dosyası etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="e2090-236">Enabling lock file</span></span>

<span data-ttu-id="e2090-237">Paket bağımlılıklarının tam kapatılmasını kalıcı hale getirmek için, projeniz için MSBuild özelliğini ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz `RestorePackagesWithLockFile` :</span><span class="sxs-lookup"><span data-stu-id="e2090-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="e2090-238">Bu özellik ayarlandıysa, NuGet geri yükleme `packages.lock.json` Proje kök dizininde tüm paket bağımlılıklarını listeleyen bir kilit dosya dosyası oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="e2090-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="e2090-239">Bir projenin `packages.lock.json` kök dizininde dosyası varsa, özellik ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır `RestorePackagesWithLockFile` .</span><span class="sxs-lookup"><span data-stu-id="e2090-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="e2090-240">Bu nedenle, bu özelliği kabul etmenin başka bir yolu `packages.lock.json` da projenin kök dizininde kukla boş bir dosya oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="e2090-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="e2090-241">`restore` kilit dosyası ile davranış</span><span class="sxs-lookup"><span data-stu-id="e2090-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="e2090-242">Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak için kullanır `restore` .</span><span class="sxs-lookup"><span data-stu-id="e2090-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="e2090-243">NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="e2090-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="e2090-244">Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="e2090-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="e2090-245">NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e2090-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="e2090-246">CI/CD ve diğer senaryolar için, anında paket bağımlılıklarını değiştirmek istemediğiniz için, ' yi ' e ayarlayarak bunu yapabilirsiniz `lockedmode` `true` :</span><span class="sxs-lookup"><span data-stu-id="e2090-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="e2090-247">dotnet.exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2090-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="e2090-248">msbuild.exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2090-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="e2090-249">Bu koşullu MSBuild özelliğini, proje dosyanızda de ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e2090-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="e2090-250">Kilitli mod ise geri yükleme işlemi, kilit `true` dosyası oluşturulduktan sonra, proje için tanımlanan paket bağımlılıklarını güncelleştirdikten sonra tam paketleri kilit dosyasında listelenen şekilde geri yükler ya da başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e2090-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="e2090-251">Kaynak deponuzun kilit dosyası parçasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="e2090-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="e2090-252">Bir uygulama oluşturuyorsanız, bir çalıştırılabilir dosya ve söz konusu proje, bağımlılık zincirinin başlangıcında yer alıyorsa, NuGet 'in geri yükleme sırasında kullanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.</span><span class="sxs-lookup"><span data-stu-id="e2090-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="e2090-253">Ancak, projeniz sevk ettiğiniz bir kitaplık projem veya diğer projelerin bağımlı olduğu ortak bir kod projesi ise, kilit dosyasını kaynak kodunuzun bir parçası olarak iade etmeniz **gerekir** .</span><span class="sxs-lookup"><span data-stu-id="e2090-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="e2090-254">Kilit dosyası tutulmayan bir sorun yoktur ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesine bağlı bir projenin geri yükleme/oluşturma işlemi sırasında kilit dosyasında listelendiği gibi kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="e2090-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="e2090-255">Örn.</span><span class="sxs-lookup"><span data-stu-id="e2090-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="e2090-256">Bir `ProjectA` sürüme bağımlılığının yanı `PackageX` `2.0.0` sıra `ProjectB` sürüme bağlı olan başvurular varsa `PackageX` `1.0.0` , için kilit dosyası `ProjectB` sürüme bir bağımlılık listeleyecek `PackageX` `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="e2090-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="e2090-257">Ancak, yapılandırıldığında `ProjectA` kilit dosyası, `PackageX` **`2.0.0`**  `1.0.0` için kilit dosyasında listelenenlerin değil, sürüm için bir bağımlılık içerecektir `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="e2090-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="e2090-258">Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e2090-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="e2090-259">Kilit dosyası genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="e2090-259">Lock file extensibility</span></span>

<span data-ttu-id="e2090-260">Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e2090-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="e2090-261">NuGet.exe seçeneği</span><span class="sxs-lookup"><span data-stu-id="e2090-261">NuGet.exe option</span></span> | <span data-ttu-id="e2090-262">DotNet seçeneği</span><span class="sxs-lookup"><span data-stu-id="e2090-262">dotnet option</span></span> | <span data-ttu-id="e2090-263">MSBuild eşdeğer seçeneği</span><span class="sxs-lookup"><span data-stu-id="e2090-263">MSBuild equivalent option</span></span> | <span data-ttu-id="e2090-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e2090-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="e2090-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="e2090-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="e2090-266">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="e2090-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="e2090-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="e2090-267">RestoreLockedMode</span></span> | <span data-ttu-id="e2090-268">Geri yükleme için kilitli modu etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e2090-268">Enables locked mode for restore.</span></span> <span data-ttu-id="e2090-269">Bu, yinelenebilir derlemeler istediğiniz CI/CD senaryolarında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e2090-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="e2090-270">Restoreforcedeğerlendir</span><span class="sxs-lookup"><span data-stu-id="e2090-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="e2090-271">Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="e2090-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="e2090-272">Varsayılan olarak, NuGet geri yükleme, bu seçenekle geri yükleme çalıştırılmadığınız takdirde, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="e2090-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="e2090-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="e2090-273">NuGetLockFilePath</span></span> | <span data-ttu-id="e2090-274">Bir proje için özel bir kilit dosyası konumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e2090-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="e2090-275">Varsayılan olarak, NuGet `packages.lock.json` kök dizinde destekler.</span><span class="sxs-lookup"><span data-stu-id="e2090-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="e2090-276">Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="e2090-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="e2090-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="e2090-277">AssetTargetFallback</span></span>

<span data-ttu-id="e2090-278">Özelliği, projenizin `AssetTargetFallback` başvurduğu projeler için ek uyumlu çerçeve sürümlerini belirtmenizi sağlar ve projenizin kullandığı NuGet paketleri.</span><span class="sxs-lookup"><span data-stu-id="e2090-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="e2090-279">Kullanarak bir paket bağımlılığı belirtirseniz `PackageReference` , ancak bu paket, projelerinizin hedef çerçevesiyle uyumlu olan varlıkları içermiyorsa, `AssetTargetFallback` özelliği yürütmeye gelir.</span><span class="sxs-lookup"><span data-stu-id="e2090-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="e2090-280">Başvurulan paketin uyumluluğu, içinde belirtilen her bir hedef çerçeve kullanılarak yeniden denetlenir `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="e2090-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="e2090-281">Bir `project` veya `package` öğesine ile başvurulduğunda `AssetTargetFallback` , [NU1701](../reference/errors-and-warnings/NU1701.md) uyarısı başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e2090-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="e2090-282">Uyumluluğun nasıl etkilendiğine ilişkin örnekler için aşağıdaki tabloya bakın `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="e2090-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="e2090-283">Proje çerçevesi</span><span class="sxs-lookup"><span data-stu-id="e2090-283">Project framework</span></span> | <span data-ttu-id="e2090-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="e2090-284">AssetTargetFallback</span></span> | <span data-ttu-id="e2090-285">Paket çerçeveleri</span><span class="sxs-lookup"><span data-stu-id="e2090-285">Package frameworks</span></span> | <span data-ttu-id="e2090-286">Sonuç</span><span class="sxs-lookup"><span data-stu-id="e2090-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="e2090-287"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e2090-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="e2090-288">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="e2090-288">.NET Standard 2.0</span></span> | <span data-ttu-id="e2090-289">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="e2090-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="e2090-290">.NET Core uygulaması 3,1</span><span class="sxs-lookup"><span data-stu-id="e2090-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="e2090-291">.NET Standard 2,0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e2090-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="e2090-292">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="e2090-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="e2090-293">.NET Core uygulaması 3,1</span><span class="sxs-lookup"><span data-stu-id="e2090-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="e2090-294"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e2090-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="e2090-295">Uyumsuz, ile başarısız oldu [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="e2090-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="e2090-296">.NET Core uygulaması 3,1</span><span class="sxs-lookup"><span data-stu-id="e2090-296">.NET Core App 3.1</span></span> | <span data-ttu-id="e2090-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="e2090-297">net472;net471</span></span> | <span data-ttu-id="e2090-298"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e2090-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="e2090-299">.NET Framework 4.7.2 [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="e2090-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="e2090-300">Ayırıcı olarak kullanılarak birden çok çerçeve belirtilebilir `;` .</span><span class="sxs-lookup"><span data-stu-id="e2090-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="e2090-301">Bir geri dönüş çerçevesi eklemek için aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e2090-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="e2090-302">`$(AssetTargetFallback)`Varolan değerlere eklemek yerine üzerine yazmak isterseniz, ' ı kapatabilirsiniz `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="e2090-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="e2090-303">[.NET SDK tabanlı bir proje](/dotnet/core/sdk)kullanıyorsanız, uygun `$(AssetTargetFallback)` değerler yapılandırılır ve bunları el ile ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e2090-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="e2090-304">`$(PackageTargetFallback)` , bu zorluğu ele almaya çalıştı, ancak temel olarak *bozulmuş ve kullanılmamalıdır* .</span><span class="sxs-lookup"><span data-stu-id="e2090-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="e2090-305">' Dan ' a geçiş yapmak için `$(PackageTargetFallback)` `$(AssetTargetFallback)` özellik adını değiştirmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="e2090-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
