---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428872"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="17bfb-103">Proje dosyalarında paket başvuruları (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="17bfb-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="17bfb-104">Paket başvuruları, `PackageReference` düğümünü kullanarak, NuGet bağımlılıklarını doğrudan proje dosyaları içinde (ayrı bir `packages.config` dosyasına karşılık) yönetir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="17bfb-105">Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalardaki (paket kaynakları dahil) ayarlar [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="17bfb-106">PackageReference ile, MSBuild koşullarını hedef çerçeve başına paket başvurularını veya diğer gruplandırmaları seçmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="17bfb-107">Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="17bfb-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="17bfb-108">(Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="17bfb-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="17bfb-109">Proje türü desteği</span><span class="sxs-lookup"><span data-stu-id="17bfb-109">Project type support</span></span>

<span data-ttu-id="17bfb-110">Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projelerinin dışında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="17bfb-111">.NET Framework projeler, PackageReference destekler, ancak şu anda varsayılan olarak `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="17bfb-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="17bfb-112">PackageReference kullanmak için `packages.config` bağımlılıkları proje dosyanıza [geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) , sonra Packages. config 'i kaldırın.</span><span class="sxs-lookup"><span data-stu-id="17bfb-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="17bfb-113">Tam .NET Framework hedefleyen uygulamalar, PackageReference için yalnızca [sınırlı desteği](https://github.com/NuGet/Home/issues/5877) içerir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="17bfb-114">C++ve JavaScript proje türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="17bfb-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="17bfb-115">PackageReference ekleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-115">Adding a PackageReference</span></span>

<span data-ttu-id="17bfb-116">Aşağıdaki sözdizimini kullanarak proje dosyanıza bir bağımlılık ekleyin:</span><span class="sxs-lookup"><span data-stu-id="17bfb-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="17bfb-117">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-117">Controlling dependency version</span></span>

<span data-ttu-id="17bfb-118">Bir paketin sürümünü belirtme kuralı, `packages.config`kullanırken olduğu gibi aynıdır:</span><span class="sxs-lookup"><span data-stu-id="17bfb-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17bfb-119">Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip > = 3.6.0 olan herhangi bir sürüm anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="17bfb-120">Packagereferde olmayan bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="17bfb-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="17bfb-121">Gelişmiş: bir projede yüklü paketleriniz yoksa (proje dosyasında ve paket. config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği RestoreProjectStyle ' ı PackageReference olarak ayarlayabilirsiniz. Proje dosyanız.</span><span class="sxs-lookup"><span data-stu-id="17bfb-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="17bfb-122">Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="17bfb-123">Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="17bfb-124">PackageReference ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="17bfb-124">PackageReference and sources</span></span>

<span data-ttu-id="17bfb-125">PackageReference projelerinde, geçişli bağımlılık sürümleri geri yükleme sırasında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="17bfb-126">Bu nedenle, PackageReference projelerinde tüm kaynakların tüm geri yüklemeler için kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="17bfb-127">Kayan sürümler</span><span class="sxs-lookup"><span data-stu-id="17bfb-127">Floating Versions</span></span>

<span data-ttu-id="17bfb-128">[Kayan sürümler](../concepts/dependency-resolution.md#floating-versions) `PackageReference`desteklenir:</span><span class="sxs-lookup"><span data-stu-id="17bfb-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="17bfb-129">Bağımlılık varlıklarını denetleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-129">Controlling dependency assets</span></span>

<span data-ttu-id="17bfb-130">Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="17bfb-131">Bu senaryoda, bu davranışı denetlemek için `PrivateAssets` meta verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17bfb-132">Aşağıdaki meta veri etiketleri denetim bağımlılığı varlıkları:</span><span class="sxs-lookup"><span data-stu-id="17bfb-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="17bfb-133">Etiket</span><span class="sxs-lookup"><span data-stu-id="17bfb-133">Tag</span></span> | <span data-ttu-id="17bfb-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="17bfb-134">Description</span></span> | <span data-ttu-id="17bfb-135">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="17bfb-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17bfb-136">Includevarlıklarını</span><span class="sxs-lookup"><span data-stu-id="17bfb-136">IncludeAssets</span></span> | <span data-ttu-id="17bfb-137">Bu varlıklar tüketilecektir</span><span class="sxs-lookup"><span data-stu-id="17bfb-137">These assets will be consumed</span></span> | <span data-ttu-id="17bfb-138">tümü</span><span class="sxs-lookup"><span data-stu-id="17bfb-138">all</span></span> |
| <span data-ttu-id="17bfb-139">Excludevarlıklarının</span><span class="sxs-lookup"><span data-stu-id="17bfb-139">ExcludeAssets</span></span> | <span data-ttu-id="17bfb-140">Bu varlıklar tüketilmeyecek</span><span class="sxs-lookup"><span data-stu-id="17bfb-140">These assets will not be consumed</span></span> | <span data-ttu-id="17bfb-141">yok</span><span class="sxs-lookup"><span data-stu-id="17bfb-141">none</span></span> |
| <span data-ttu-id="17bfb-142">Privatevarlıkların</span><span class="sxs-lookup"><span data-stu-id="17bfb-142">PrivateAssets</span></span> | <span data-ttu-id="17bfb-143">Bu varlıklar tüketilecektir, ancak üst projeye akamaz</span><span class="sxs-lookup"><span data-stu-id="17bfb-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="17bfb-144">ContentFiles; çözümleyiciler; derleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="17bfb-145">Bu etiketler için izin verilen değerler aşağıdaki gibidir: `all` ve `none` dışında noktalı virgülle ayrılmış birden çok değer ve kendileri tarafından görünmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="17bfb-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="17bfb-146">Değer</span><span class="sxs-lookup"><span data-stu-id="17bfb-146">Value</span></span> | <span data-ttu-id="17bfb-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="17bfb-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="17bfb-148">se</span><span class="sxs-lookup"><span data-stu-id="17bfb-148">compile</span></span> | <span data-ttu-id="17bfb-149">`lib` klasörünün içeriği ve projenizin, klasör içindeki derlemelere göre derleyemeyeceğini denetler</span><span class="sxs-lookup"><span data-stu-id="17bfb-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="17bfb-150">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="17bfb-150">runtime</span></span> | <span data-ttu-id="17bfb-151">`lib` ve `runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler</span><span class="sxs-lookup"><span data-stu-id="17bfb-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="17bfb-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="17bfb-152">contentFiles</span></span> | <span data-ttu-id="17bfb-153">`contentfiles` klasörünün içeriği</span><span class="sxs-lookup"><span data-stu-id="17bfb-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="17bfb-154">derleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-154">build</span></span> | <span data-ttu-id="17bfb-155">`build` klasöre `.props` ve `.targets`</span><span class="sxs-lookup"><span data-stu-id="17bfb-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="17bfb-156">Buildmultihedefleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-156">buildMultitargeting</span></span> | <span data-ttu-id="17bfb-157">*(4,0)* platformlar arası hedefleme için `buildMultitargeting` klasöründe `.props` ve `.targets`</span><span class="sxs-lookup"><span data-stu-id="17bfb-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="17bfb-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="17bfb-158">buildTransitive</span></span> | <span data-ttu-id="17bfb-159">*(5.0 +)* `.props` ve `buildTransitive` klasöründe `.targets`, herhangi bir tüketen projeye geçişli olarak akan varlıklar içindir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="17bfb-160">Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası.</span><span class="sxs-lookup"><span data-stu-id="17bfb-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="17bfb-161">Çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="17bfb-161">analyzers</span></span> | <span data-ttu-id="17bfb-162">.NET Çözümleyicileri</span><span class="sxs-lookup"><span data-stu-id="17bfb-162">.NET analyzers</span></span> |
| <span data-ttu-id="17bfb-163">yerel</span><span class="sxs-lookup"><span data-stu-id="17bfb-163">native</span></span> | <span data-ttu-id="17bfb-164">`native` klasörünün içeriği</span><span class="sxs-lookup"><span data-stu-id="17bfb-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="17bfb-165">yok</span><span class="sxs-lookup"><span data-stu-id="17bfb-165">none</span></span> | <span data-ttu-id="17bfb-166">Yukarıdakilerin hiçbiri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-166">None of the above are used.</span></span> |
| <span data-ttu-id="17bfb-167">tümü</span><span class="sxs-lookup"><span data-stu-id="17bfb-167">all</span></span> | <span data-ttu-id="17bfb-168">Yukarıdakilerin tümü (`none`hariç)</span><span class="sxs-lookup"><span data-stu-id="17bfb-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="17bfb-169">Aşağıdaki örnekte, paketteki içerik dosyaları hariç her şey proje tarafından, içerik dosyaları ve çözümleyiciler hariç her şey üst projeye akacaktır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="17bfb-170">`build` `PrivateAssets`dahil olmadığından, hedefler ve props üst projeye *akacak* .</span><span class="sxs-lookup"><span data-stu-id="17bfb-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="17bfb-171">Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="17bfb-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="17bfb-172">Appgünlükçü, Appgünlükçü kullanan projeler de içinde olmak üzere `Contoso.Utility.UsefulStuff`hedefleri ve props 'yi kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="17bfb-173">`developmentDependency` bir `.nuspec` dosyasında `true` olarak ayarlandığında, bu bir paketi yalnızca geliştirme bağımlılığı olarak işaretler. Bu, paketin diğer paketlere bağımlılık olarak eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="17bfb-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="17bfb-174">PackageReference *(NuGet 4.8 +)* ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="17bfb-175">Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="17bfb-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="17bfb-176">PackageReference koşulu ekleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="17bfb-177">Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="17bfb-178">Ancak şu anda yalnızca `TargetFramework` değişkeni desteklenir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="17bfb-179">Örneğin, `netstandard1.4` hedeflediğiniz ve `net452`, ancak yalnızca `net452`için geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="17bfb-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="17bfb-180">Bu durumda, bu gereksiz bağımlılığı eklemek için paketinizi kullanan `netstandard1.4` bir proje istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="17bfb-181">Bunu engellemek için `PackageReference` bir koşulu aşağıdaki gibi belirtirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17bfb-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17bfb-182">Bu proje kullanılarak oluşturulan bir paket, Newtonsoft. json ' ın yalnızca bir `net452` hedefi için bağımlılık olarak ekleneceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="17bfb-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="17bfb-184">Koşullar `ItemGroup` düzeyinde de uygulanabilir ve tüm alt öğelere `PackageReference` öğeler için geçerli olur:</span><span class="sxs-lookup"><span data-stu-id="17bfb-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="17bfb-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="17bfb-185">GeneratePathProperty</span></span>

<span data-ttu-id="17bfb-186">Bu özellik NuGet **5,0** veya sonraki sürümlerde ve Visual Studio 2019 **16,0** veya üzeri sürümlerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="17bfb-187">Bazen bir MSBuild hedefinden bir paketteki dosyalara başvurulmasına tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="17bfb-188">`packages.config` tabanlı projelerde, paketler proje dosyası ile ilişkili bir klasöre yüklenir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="17bfb-189">Ancak, PackageReference içinde paketler, makineden makineye değişebilen *küresel paketler* [klasöründen kullanılır.](../concepts/package-installation-process.md)</span><span class="sxs-lookup"><span data-stu-id="17bfb-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="17bfb-190">Bu boşluğu bağlamak için, NuGet paketin tükettiği konuma işaret eden bir özellik sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="17bfb-191">Örnek:</span><span class="sxs-lookup"><span data-stu-id="17bfb-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="17bfb-192">Ayrıca NuGet, bir Araçlar klasörü içeren paketler için otomatik olarak Özellikler oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="17bfb-193">MSBuild özellikleri ve paket kimlikleri aynı kısıtlamalara sahip değildir, bu nedenle paket kimliğinin bir MSBuild kolay adına değiştirilmesi gerekir, bu nedenle `Pkg`sözcüğü önekli.</span><span class="sxs-lookup"><span data-stu-id="17bfb-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="17bfb-194">Oluşturulan özelliğin tam adını doğrulamak için, oluşturulan [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="17bfb-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="17bfb-195">NuGet uyarıları ve hataları</span><span class="sxs-lookup"><span data-stu-id="17bfb-195">NuGet warnings and errors</span></span>

<span data-ttu-id="17bfb-196">*Bu özellik NuGet **4,3** veya sonraki sürümlerde ve Visual Studio 2017 **15,3** veya üzeri sürümlerde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="17bfb-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="17bfb-197">Birçok paket ve geri yükleme senaryosunda, tüm NuGet uyarıları ve hataları kodlanır ve `NU****`başlar.</span><span class="sxs-lookup"><span data-stu-id="17bfb-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="17bfb-198">Tüm NuGet uyarıları ve hataları [başvuru](../reference/errors-and-warnings.md) belgelerinde listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="17bfb-199">NuGet obonu aşağıdaki uyarı özelliklerine hizmet eder:</span><span class="sxs-lookup"><span data-stu-id="17bfb-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="17bfb-200">`TreatWarningsAsErrors`, tüm uyarıları hata olarak değerlendir</span><span class="sxs-lookup"><span data-stu-id="17bfb-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="17bfb-201">`WarningsAsErrors`, belirli uyarıları hata olarak değerlendir</span><span class="sxs-lookup"><span data-stu-id="17bfb-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="17bfb-202">`NoWarn`, proje genelinde veya paket genelinde belirli uyarıları gizleyin.</span><span class="sxs-lookup"><span data-stu-id="17bfb-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="17bfb-203">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="17bfb-203">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="17bfb-204">NuGet uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="17bfb-205">Paket ve geri yükleme işlemleri sırasında tüm NuGet uyarılarını çözmeniz önerilir, ancak bazı durumlarda bunların garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="17bfb-206">Bir uyarı projesini genelinde gizlemek için şunları yapmayı düşünün:</span><span class="sxs-lookup"><span data-stu-id="17bfb-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="17bfb-207">Bazen uyarılar yalnızca grafikteki belirli bir paket için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="17bfb-208">PackageReference öğesine bir `NoWarn` ekleyerek bu uyarının daha seçmeli olarak görüntülenmesini seçebiliriz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="17bfb-209">Visual Studio 'da NuGet paket uyarılarını gizleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="17bfb-210">Visual Studio 'da Ayrıca, uyarıları IDE aracılığıyla da [gizleyebilirsiniz](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) .</span><span class="sxs-lookup"><span data-stu-id="17bfb-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="17bfb-211">Bağımlılıkları kilitleme</span><span class="sxs-lookup"><span data-stu-id="17bfb-211">Locking dependencies</span></span>

<span data-ttu-id="17bfb-212">*Bu özellik NuGet **4,9** veya sonraki sürümlerde ve Visual Studio 2017 **15,9** veya üzeri sürümlerde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="17bfb-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="17bfb-213">NuGet geri yükleme girdisi, proje dosyasından (en üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıkış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının tam bir kapasitesinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="17bfb-214">NuGet, giriş PackageReference listesi değişmediğinde paket bağımlılıklarının her zaman aynı tam kapatılmasını üretmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="17bfb-215">Ancak, bunu yapamaması gereken bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="17bfb-216">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="17bfb-216">For example:</span></span>

* <span data-ttu-id="17bfb-217">`<PackageReference Include="My.Sample.Lib" Version="4.*"/>`gibi kayan sürümler kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="17bfb-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="17bfb-218">Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="17bfb-219">Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="17bfb-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="17bfb-220">Örneğin</span><span class="sxs-lookup"><span data-stu-id="17bfb-220">E.g.</span></span> 

  * <span data-ttu-id="17bfb-221">Gün 1: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` belirlediyseniz, NuGet depolarında bulunan sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="17bfb-222">Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir</span><span class="sxs-lookup"><span data-stu-id="17bfb-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="17bfb-223">2\. gün: sürüm 4.0.0 yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="17bfb-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="17bfb-224">NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak</span><span class="sxs-lookup"><span data-stu-id="17bfb-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="17bfb-225">Belirli bir paket sürümü depodan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="17bfb-226">Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="17bfb-227">Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="17bfb-228">Kilit dosyası etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="17bfb-228">Enabling lock file</span></span>

<span data-ttu-id="17bfb-229">Paket bağımlılıklarının tam kapatılmasını kalıcı hale getirmek için, projeniz için `RestorePackagesWithLockFile` MSBuild özelliğini ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17bfb-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="17bfb-230">Bu özellik ayarlandıysa, NuGet geri yükleme proje kök dizininde tüm paket bağımlılıklarını listeleyen bir kilit dosyası `packages.lock.json` dosyası oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="17bfb-231">Bir projenin kök dizininde `packages.lock.json` dosyası varsa, özellik `RestorePackagesWithLockFile` ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="17bfb-232">Bu nedenle, bu özelliği kabul etmenin başka bir yolu da projenin kök dizininde kukla bir boş `packages.lock.json` dosyası oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="17bfb-233">kilit dosyası ile `restore` davranışı</span><span class="sxs-lookup"><span data-stu-id="17bfb-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="17bfb-234">Proje için bir kilit dosyası varsa, NuGet `restore`çalıştırmak için bu kilit dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="17bfb-235">NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="17bfb-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="17bfb-236">Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="17bfb-237">NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="17bfb-238">CI/CD ve diğer senaryolar için, bir anında paket bağımlılıklarını değiştirmek istemediğiniz için, `lockedmode` `true`olarak ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17bfb-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="17bfb-239">DotNet. exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="17bfb-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="17bfb-240">MSBuild. exe için şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="17bfb-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="17bfb-241">Bu koşullu MSBuild özelliğini, proje dosyanızda de ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17bfb-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="17bfb-242">Kilitleme modu `true`ise, geri yükleme işlemi kilit dosyasında listelenen paketleri tam olarak geri yükler veya kilit dosyası oluşturulduktan sonra proje için tanımlanan paket bağımlılıklarını güncelleştirdiyseniz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="17bfb-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="17bfb-243">Kaynak deponuzun kilit dosyası parçasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="17bfb-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="17bfb-244">Bir uygulama oluşturuyorsanız, bir çalıştırılabilir dosya ve söz konusu proje, bağımlılık zincirinin başlangıcında yer alıyorsa, NuGet 'in geri yükleme sırasında kullanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.</span><span class="sxs-lookup"><span data-stu-id="17bfb-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="17bfb-245">Ancak, projeniz sevk ettiğiniz bir kitaplık projem veya diğer projelerin bağımlı olduğu ortak bir kod projesi ise, kilit dosyasını kaynak kodunuzun bir parçası olarak iade etmeniz **gerekir** .</span><span class="sxs-lookup"><span data-stu-id="17bfb-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="17bfb-246">Kilit dosyası tutulmayan bir sorun yoktur ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesine bağlı bir projenin geri yükleme/oluşturma işlemi sırasında kilit dosyasında listelendiği gibi kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="17bfb-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="17bfb-247">Örn.</span><span class="sxs-lookup"><span data-stu-id="17bfb-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="17bfb-248">`ProjectA` bir `PackageX` sürüm `2.0.0` bağımlılığı varsa ve aynı zamanda `PackageX` sürümüne bağımlı olan `ProjectB` de başvuruyorsa `1.0.0`için kilit dosyası `ProjectB` sürüm `PackageX` bir bağımlılık listeler.`1.0.0`</span><span class="sxs-lookup"><span data-stu-id="17bfb-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="17bfb-249">Ancak, `ProjectA` oluşturulduğunda kilit dosyası, `ProjectB`için kilit dosyasında listelendiği gibi `1.0.0` **değil** `PackageX` sürüm **`2.0.0`** bir bağımlılık içerecektir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="17bfb-250">Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="17bfb-251">Kilit dosyası genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="17bfb-251">Lock file extensibility</span></span>

<span data-ttu-id="17bfb-252">Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17bfb-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="17bfb-253">NuGet. exe seçeneği</span><span class="sxs-lookup"><span data-stu-id="17bfb-253">NuGet.exe option</span></span> | <span data-ttu-id="17bfb-254">DotNet seçeneği</span><span class="sxs-lookup"><span data-stu-id="17bfb-254">dotnet option</span></span> | <span data-ttu-id="17bfb-255">MSBuild eşdeğer seçeneği</span><span class="sxs-lookup"><span data-stu-id="17bfb-255">MSBuild equivalent option</span></span> | <span data-ttu-id="17bfb-256">Açıklama</span><span class="sxs-lookup"><span data-stu-id="17bfb-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="17bfb-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="17bfb-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="17bfb-258">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="17bfb-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="17bfb-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="17bfb-259">RestoreLockedMode</span></span> | <span data-ttu-id="17bfb-260">Geri yükleme için kilitli modu etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="17bfb-260">Enables locked mode for restore.</span></span> <span data-ttu-id="17bfb-261">Bu, yinelenebilir derlemeler istediğiniz CI/CD senaryolarında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="17bfb-262">Restoreforcedeğerlendir</span><span class="sxs-lookup"><span data-stu-id="17bfb-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="17bfb-263">Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="17bfb-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="17bfb-264">Varsayılan olarak, NuGet geri yükleme, bu seçenekle geri yükleme çalıştırılmadığınız takdirde, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="17bfb-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="17bfb-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="17bfb-265">NuGetLockFilePath</span></span> | <span data-ttu-id="17bfb-266">Bir proje için özel bir kilit dosyası konumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="17bfb-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="17bfb-267">NuGet, varsayılan olarak kök dizinde `packages.lock.json` destekler.</span><span class="sxs-lookup"><span data-stu-id="17bfb-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="17bfb-268">Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="17bfb-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
