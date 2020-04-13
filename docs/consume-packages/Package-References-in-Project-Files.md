---
title: NuGet PackageReference formatı (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0+ ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428872"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="92dfa-103">Proje dosyalarındaki paket referansları (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="92dfa-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="92dfa-104">Paket başvuruları, `PackageReference` düğümü kullanarak, NuGet bağımlılıklarını doğrudan proje dosyaları içinde `packages.config` yönetin (ayrı bir dosyanın aksine).</span><span class="sxs-lookup"><span data-stu-id="92dfa-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="92dfa-105">PackageReference'ı kullanmak, nuget'in diğer yönlerini etkilemez; örneğin, dosyalardaki `NuGet.config` ayarlar (paket kaynakları dahil) Ortak [NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="92dfa-106">PackageReference ile, hedef çerçeve veya diğer gruplandırmalar başına paket başvuruları seçmek için MSBuild koşullarını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="92dfa-107">Ayrıca bağımlılıklar ve içerik akışı üzerinde ince taneli kontrol sağlar.</span><span class="sxs-lookup"><span data-stu-id="92dfa-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="92dfa-108">(Daha fazla bilgi için [NuGet paketi ve MSBuild hedefleri olarak geri yükleyin](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="92dfa-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="92dfa-109">Proje türü desteği</span><span class="sxs-lookup"><span data-stu-id="92dfa-109">Project type support</span></span>

<span data-ttu-id="92dfa-110">Varsayılan olarak PackageReference, C++ UWP projeleri dışında Windows 10 Build 15063 (Creators Update) ve daha sonrasını hedefleyen .NET Core projeleri, .NET Standard projeleri ve UWP projeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="92dfa-111">.NET Framework projeleri PackageReference'ı `packages.config`destekler, ancak şu anda varsayılan .</span><span class="sxs-lookup"><span data-stu-id="92dfa-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="92dfa-112">PackageReference'ı kullanmak için, bağımlılıkları `packages.config` proje dosyanıza [geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve ardından packages.config'i kaldırın.</span><span class="sxs-lookup"><span data-stu-id="92dfa-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="92dfa-113">ASP.NET .NET Framework'u hedefleyen uygulamalar, PackageReference için [yalnızca sınırlı destek](https://github.com/NuGet/Home/issues/5877) içerir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="92dfa-114">C++ ve JavaScript proje türleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="92dfa-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="92dfa-115">PackageReference Ekleme</span><span class="sxs-lookup"><span data-stu-id="92dfa-115">Adding a PackageReference</span></span>

<span data-ttu-id="92dfa-116">Aşağıdaki sözdizimini kullanarak proje dosyanıza bağımlılık ekleyin:</span><span class="sxs-lookup"><span data-stu-id="92dfa-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="92dfa-117">Bağımlılık sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="92dfa-117">Controlling dependency version</span></span>

<span data-ttu-id="92dfa-118">Bir paketin sürümünü belirtmek için sözleşme kullanırken `packages.config`aynıdır:</span><span class="sxs-lookup"><span data-stu-id="92dfa-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="92dfa-119">Yukarıdaki örnekte, 3.6.0, [Paket sürümünde](../concepts/package-versioning.md#version-ranges)açıklandığı gibi, en düşük sürümü tercih eden >=3.6.0 olan herhangi bir sürüm anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="92dfa-120">PackageReferences olmayan bir proje için PackageReference kullanma</span><span class="sxs-lookup"><span data-stu-id="92dfa-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="92dfa-121">Gelişmiş: Bir projede yüklü paketleriniz yoksa (proje dosyasında Paket Başvurusu yok ve packages.config dosyası yok) ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, proje dosyanızda PackageReference için Project özelliği RestoreProjectStyle ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="92dfa-122">Bu, PackageReference stilinde olan projelere (mevcut csproj veya SDK tarzı projeler) başvurursanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="92dfa-123">Bu, bu projelerin atıfta bulunduğu paketlerin projeniz tarafından "geçişli" olarak başvurulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="92dfa-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="92dfa-124">PackageReference ve kaynaklar</span><span class="sxs-lookup"><span data-stu-id="92dfa-124">PackageReference and sources</span></span>

<span data-ttu-id="92dfa-125">PackageReference projelerinde, geçişli bağımlılık sürümleri geri yükleme zamanında çözülür.</span><span class="sxs-lookup"><span data-stu-id="92dfa-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="92dfa-126">Bu nedenle, PackageReference projelerinde tüm kaynakların tüm geri yüklemeler için kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="92dfa-127">Kayan Sürümler</span><span class="sxs-lookup"><span data-stu-id="92dfa-127">Floating Versions</span></span>

<span data-ttu-id="92dfa-128">[Kayan sürümler:](../concepts/dependency-resolution.md#floating-versions) `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="92dfa-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="92dfa-129">Bağımlılık varlıklarını denetleme</span><span class="sxs-lookup"><span data-stu-id="92dfa-129">Controlling dependency assets</span></span>

<span data-ttu-id="92dfa-130">Bir bağımlılığı tamamen geliştirme donanımı olarak kullanıyor olabilirsiniz ve bunu paketinizi tüketecek projelere maruz bırakmak istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="92dfa-131">Bu senaryoda, bu `PrivateAssets` davranışı denetlemek için meta verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="92dfa-132">Aşağıdaki meta veri etiketleri bağımlılık varlıklarını denetler:</span><span class="sxs-lookup"><span data-stu-id="92dfa-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="92dfa-133">Etiket</span><span class="sxs-lookup"><span data-stu-id="92dfa-133">Tag</span></span> | <span data-ttu-id="92dfa-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92dfa-134">Description</span></span> | <span data-ttu-id="92dfa-135">Varsayılan Değer</span><span class="sxs-lookup"><span data-stu-id="92dfa-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92dfa-136">Dahil Varlıklar</span><span class="sxs-lookup"><span data-stu-id="92dfa-136">IncludeAssets</span></span> | <span data-ttu-id="92dfa-137">Bu varlıklar tüketilecek</span><span class="sxs-lookup"><span data-stu-id="92dfa-137">These assets will be consumed</span></span> | <span data-ttu-id="92dfa-138">tümü</span><span class="sxs-lookup"><span data-stu-id="92dfa-138">all</span></span> |
| <span data-ttu-id="92dfa-139">Varlıkları Hariç Tutma</span><span class="sxs-lookup"><span data-stu-id="92dfa-139">ExcludeAssets</span></span> | <span data-ttu-id="92dfa-140">Bu varlıklar tüketilmeyecek</span><span class="sxs-lookup"><span data-stu-id="92dfa-140">These assets will not be consumed</span></span> | <span data-ttu-id="92dfa-141">yok</span><span class="sxs-lookup"><span data-stu-id="92dfa-141">none</span></span> |
| <span data-ttu-id="92dfa-142">Özel Varlıklar</span><span class="sxs-lookup"><span data-stu-id="92dfa-142">PrivateAssets</span></span> | <span data-ttu-id="92dfa-143">Bu varlıklar tüketilecek, ancak ana projeye akmayacak</span><span class="sxs-lookup"><span data-stu-id="92dfa-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="92dfa-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="92dfa-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="92dfa-145">Bu etiketler için izin verilen değerler aşağıdaki gibidir, birden çok `all` `none` değer bir yarı kolon ile ayrılmış dışında ve kendi kendine görünmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="92dfa-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="92dfa-146">Değer</span><span class="sxs-lookup"><span data-stu-id="92dfa-146">Value</span></span> | <span data-ttu-id="92dfa-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92dfa-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="92dfa-148">derle</span><span class="sxs-lookup"><span data-stu-id="92dfa-148">compile</span></span> | <span data-ttu-id="92dfa-149">Klasörün `lib` içeriği ve projenizin klasör içindeki derlemelere karşı derlenip derlenip derlemeyeceğini denetler</span><span class="sxs-lookup"><span data-stu-id="92dfa-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="92dfa-150">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="92dfa-150">runtime</span></span> | <span data-ttu-id="92dfa-151">Klasörün `lib` içeriği `runtimes` ve içeriği ve bu derlemelerin yapı çıktı dizini için kopyalanıp kopyalanmayacağını denetler</span><span class="sxs-lookup"><span data-stu-id="92dfa-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="92dfa-152">içerikDosyalar</span><span class="sxs-lookup"><span data-stu-id="92dfa-152">contentFiles</span></span> | <span data-ttu-id="92dfa-153">Klasörün `contentfiles` içeriği</span><span class="sxs-lookup"><span data-stu-id="92dfa-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="92dfa-154">derleme</span><span class="sxs-lookup"><span data-stu-id="92dfa-154">build</span></span> | <span data-ttu-id="92dfa-155">`.props`ve `.targets` klasörde `build`</span><span class="sxs-lookup"><span data-stu-id="92dfa-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="92dfa-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="92dfa-156">buildMultitargeting</span></span> | <span data-ttu-id="92dfa-157">*(4.0)* `.props` `.targets` ve `buildMultitargeting` klasörde, çapraz çerçeve hedefleme için</span><span class="sxs-lookup"><span data-stu-id="92dfa-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="92dfa-158">buildGeçişive</span><span class="sxs-lookup"><span data-stu-id="92dfa-158">buildTransitive</span></span> | <span data-ttu-id="92dfa-159">*(5.0+)* `.props` `.targets` ve `buildTransitive` klasörde, herhangi bir tüketen projeye geçişli olarak akan varlıklar için.</span><span class="sxs-lookup"><span data-stu-id="92dfa-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="92dfa-160">[Özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="92dfa-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="92dfa-161">Analizörleri</span><span class="sxs-lookup"><span data-stu-id="92dfa-161">analyzers</span></span> | <span data-ttu-id="92dfa-162">.NET analizörleri</span><span class="sxs-lookup"><span data-stu-id="92dfa-162">.NET analyzers</span></span> |
| <span data-ttu-id="92dfa-163">yerel</span><span class="sxs-lookup"><span data-stu-id="92dfa-163">native</span></span> | <span data-ttu-id="92dfa-164">Klasörün `native` içeriği</span><span class="sxs-lookup"><span data-stu-id="92dfa-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="92dfa-165">yok</span><span class="sxs-lookup"><span data-stu-id="92dfa-165">none</span></span> | <span data-ttu-id="92dfa-166">Yukarıdakilerin hiçbiri kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-166">None of the above are used.</span></span> |
| <span data-ttu-id="92dfa-167">tümü</span><span class="sxs-lookup"><span data-stu-id="92dfa-167">all</span></span> | <span data-ttu-id="92dfa-168">Yukarıdakilerin tümü (hariç) `none`</span><span class="sxs-lookup"><span data-stu-id="92dfa-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="92dfa-169">Aşağıdaki örnekte, paketteki içerik dosyaları dışındaki her şey proje tarafından tüketilir ve içerik dosyaları ve çözümleyiciler dışındaki her şey ana projeye akar.</span><span class="sxs-lookup"><span data-stu-id="92dfa-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="92dfa-170">`build` Dahil `PrivateAssets`olmadığından, hedeflerin ve sahne desteklerinin ana projeye *akacağını* unutmayın.</span><span class="sxs-lookup"><span data-stu-id="92dfa-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="92dfa-171">Örneğin, yukarıdaki başvurunun AppLogger adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="92dfa-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="92dfa-172">AppLogger hedefleri ve sahne tüketebilir `Contoso.Utility.UsefulStuff`, AppLogger tüketen projeler gibi.</span><span class="sxs-lookup"><span data-stu-id="92dfa-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="92dfa-173">Bir `developmentDependency` `.nuspec` `true` dosyada ayarlandığında, bu paket yalnızca geliştirme bağımlılığı olarak işaretler ve bu da paketin diğer paketlere bağımlılık olarak eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="92dfa-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="92dfa-174">PackageReference *(NuGet 4.8+)* ile bu bayrak, derleme zamanı varlıklarını derlemeden hariç tutacağı anlamına da gelir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="92dfa-175">Daha fazla bilgi [için PackageReference için DevelopmentDependency desteğine](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)bakın.</span><span class="sxs-lookup"><span data-stu-id="92dfa-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="92dfa-176">PackageReference koşulu ekleme</span><span class="sxs-lookup"><span data-stu-id="92dfa-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="92dfa-177">Bir paketin dahil edilip edilemeyeceğini, koşulların herhangi bir MSBuild değişkenini veya hedefler veya sahne dosyasında tanımlanan bir değişkeni kullanabildiği bir koşul kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="92dfa-178">Ancak, şu anda `TargetFramework` yalnızca değişken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="92dfa-179">Örneğin, hedeflediğinizi, `netstandard1.4` `net452` ancak yalnızca `net452`.</span><span class="sxs-lookup"><span data-stu-id="92dfa-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="92dfa-180">Bu durumda, paketinizi tüketen bir `netstandard1.4` projenin bu gereksiz bağımlılık eklemesini istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="92dfa-181">Bunu önlemek için aşağıdaki `PackageReference` gibi bir koşul belirtirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92dfa-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="92dfa-182">Bu proje kullanılarak oluşturulmuş bir paket Newtonsoft.Json'ın yalnızca bir `net452` hedef için bağımlılık olarak dahil edildiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="92dfa-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 ile PackageReference Koşulu uygulama nın sonucu](media/PackageReference-Condition.png)

<span data-ttu-id="92dfa-184">Koşullar aynı `ItemGroup` düzeyde de uygulanabilir ve tüm `PackageReference` çocuklar için geçerli olacaktır:</span><span class="sxs-lookup"><span data-stu-id="92dfa-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="92dfa-185">PathÖzelliği Ni Oluştur</span><span class="sxs-lookup"><span data-stu-id="92dfa-185">GeneratePathProperty</span></span>

<span data-ttu-id="92dfa-186">Bu özellik NuGet **5.0** ve üzeri ve Visual Studio 2019 **16.0** ve üzeri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="92dfa-187">Bazen bir MSBuild hedefinden bir paketteki dosyalara başvurmak istenir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="92dfa-188">Tabanlı `packages.config` projelerde, paketler proje dosyasına göre bir klasöre yüklenir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="92dfa-189">Ancak PackageReference'da paketler, makineden makineye değişebilen *küresel paketler* klasöründen [tüketilir.](../concepts/package-installation-process.md)</span><span class="sxs-lookup"><span data-stu-id="92dfa-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="92dfa-190">Bu boşluğu kapatmak için NuGet, paketin tüketileceği yeri gösteren bir özellik sundu.</span><span class="sxs-lookup"><span data-stu-id="92dfa-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="92dfa-191">Örnek:</span><span class="sxs-lookup"><span data-stu-id="92dfa-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="92dfa-192">Ayrıca NuGet, bir araç klasörü içeren paketler için otomatik olarak özellikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="92dfa-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="92dfa-193">MSBuild özellikleri ve paket kimlikleri aynı kısıtlamalara sahip değildir, bu nedenle paket kimliğinin sözcük `Pkg`tarafından önceden belirlenmiş bir MSBuild dostu adı ile değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="92dfa-194">Oluşturulan özelliğin tam adını doğrulamak için oluşturulan [nuget.g.prop](../reference/msbuild-targets.md#restore-outputs) dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="92dfa-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="92dfa-195">NuGet uyarıları ve hataları</span><span class="sxs-lookup"><span data-stu-id="92dfa-195">NuGet warnings and errors</span></span>

<span data-ttu-id="92dfa-196">*Bu özellik NuGet **4.3** ve üzeri ve Visual Studio 2017 **15.3** ve üzeri ile kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="92dfa-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="92dfa-197">Birçok paket ve geri yükleme senaryoları için, tüm NuGet `NU****`uyarıları ve hataları kodlanır ve .</span><span class="sxs-lookup"><span data-stu-id="92dfa-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="92dfa-198">Tüm NuGet uyarıları ve hataları [başvuru](../reference/errors-and-warnings.md) belgelerinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="92dfa-199">NuGet aşağıdaki uyarı özelliklerini gözlemler:</span><span class="sxs-lookup"><span data-stu-id="92dfa-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="92dfa-200">`TreatWarningsAsErrors`, tüm uyarıları hata olarak ele</span><span class="sxs-lookup"><span data-stu-id="92dfa-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="92dfa-201">`WarningsAsErrors`, belirli uyarıları hata olarak ele</span><span class="sxs-lookup"><span data-stu-id="92dfa-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="92dfa-202">`NoWarn`, proje genelinde veya paket genelinde belirli uyarıları gizleyin.</span><span class="sxs-lookup"><span data-stu-id="92dfa-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="92dfa-203">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="92dfa-203">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="92dfa-204">NuGet uyarılarını bastırma</span><span class="sxs-lookup"><span data-stu-id="92dfa-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="92dfa-205">Paketiniz sırasında tüm NuGet uyarılarını çözmeniz ve işlemleri geri yüklemeniz önerilirken, bazı durumlarda bunları bastırmanız garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="92dfa-206">Bir uyarı projesini geniş bir şekilde bastırmak için şunları yapmayı düşünün:</span><span class="sxs-lookup"><span data-stu-id="92dfa-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="92dfa-207">Bazen uyarılar yalnızca grafikteki belirli bir paketiçin geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="92dfa-208">PackageReference öğesine bir tane `NoWarn` ekleyerek bu uyarıyı daha seçici bir şekilde bastırmayı seçebiliriz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="92dfa-209">Visual Studio'da NuGet paket uyarılarını bastırma</span><span class="sxs-lookup"><span data-stu-id="92dfa-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="92dfa-210">Visual Studio'da, [IDE](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) aracılığıyla uyarıları da bastırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="92dfa-211">Kilitleme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="92dfa-211">Locking dependencies</span></span>

<span data-ttu-id="92dfa-212">*Bu özellik NuGet **4.9** ve üzeri ve Visual Studio 2017 **15.9** ve üzeri ile kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="92dfa-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="92dfa-213">NuGet geri yükleme girişi, proje dosyasından (üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıktı, geçişli bağımlılıklar da dahil olmak üzere tüm paket bağımlılıklarının tam olarak kapatılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="92dfa-214">NuGet, paket Başvuru listesi değişmediyse, paket bağımlılıklarının her zaman aynı tam kapatılmasını sağlamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="92dfa-215">Ancak, bunu yapamaz bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="92dfa-216">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="92dfa-216">For example:</span></span>

* <span data-ttu-id="92dfa-217">Gibi kayan sürümleri `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`kullandığınızda .</span><span class="sxs-lookup"><span data-stu-id="92dfa-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="92dfa-218">Buradaki amaç, paketlerin her geri yüklemesinde en son sürüme float etmek olsa da, kullanıcıların grafiğin belirli bir son sürüme kilitlenmesini ve varsa açık bir hareketle daha sonraki bir sürüme doğru yüzdürülmesi gereken senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="92dfa-219">PackageReference sürüm gereksinimlerini eşleştiren paketin daha yeni bir sürümü yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="92dfa-220">Örneğin</span><span class="sxs-lookup"><span data-stu-id="92dfa-220">E.g.</span></span> 

  * <span data-ttu-id="92dfa-221">1. Gün: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` NuGet depolarında bulunan sürümleri n için belirtirseniz 4.1.0, 4.2.0 ve 4.3.0 idi.</span><span class="sxs-lookup"><span data-stu-id="92dfa-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="92dfa-222">Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözülmüş olurdu</span><span class="sxs-lookup"><span data-stu-id="92dfa-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="92dfa-223">2. Gün: Sürüm 4.0.0 yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="92dfa-224">NuGet şimdi tam eşleşmeyi bulacak ve 4.0.0'a çözmeye başlayacak</span><span class="sxs-lookup"><span data-stu-id="92dfa-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="92dfa-225">Belirli bir paket sürümü depodan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="92dfa-226">nuget.org paket silmelere izin vermese de, tüm paket depolarında bu kısıtlamalar yoktur.</span><span class="sxs-lookup"><span data-stu-id="92dfa-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="92dfa-227">Bu, NuGet'in silinen sürüme çözüm leyemediği zaman en iyi eşleşmeyi bulmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="92dfa-228">Kilit dosyasını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="92dfa-228">Enabling lock file</span></span>

<span data-ttu-id="92dfa-229">Paket bağımlılıklarının tamamen kapatılmasını sürdürmek için, projeniz için MSBuild özelliğini `RestorePackagesWithLockFile` ayarlayarak kilit dosyası özelliğini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92dfa-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="92dfa-230">Bu özellik ayarlanırsa, NuGet geri yüklemesi, tüm paket bağımlılıklarını listeleyen proje kök dizininde bir kilit dosyası - `packages.lock.json` dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="92dfa-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="92dfa-231">Bir proje `packages.lock.json` kök dizininde dosya varsa, özellik ayarlanmasa `RestorePackagesWithLockFile` bile kilit dosyası her zaman geri yükleme ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="92dfa-232">Bu nedenle, bu özelliği kabul etmenin başka bir `packages.lock.json` yolu da projenin kök dizininde sahte boş bir dosya oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="92dfa-233">`restore`kilit dosyası ile davranış</span><span class="sxs-lookup"><span data-stu-id="92dfa-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="92dfa-234">Proje için bir kilit dosyası varsa, NuGet çalıştırmak `restore`için bu kilit dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="92dfa-235">NuGet, proje dosyasında (veya bağımlı projelerin dosyalarında) belirtildiği gibi paket bağımlılıklarında herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve herhangi bir değişiklik yoksa, kilit dosyasında belirtilen paketleri geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="92dfa-236">Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="92dfa-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="92dfa-237">NuGet, proje dosyasında(lar) belirtilen tanımlı bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="92dfa-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="92dfa-238">Anında paket bağımlılıklarını değiştirmek istemediğiniz CI/CD ve diğer senaryolar `lockedmode` için `true`şunları ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92dfa-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="92dfa-239">dotnet.exe için, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="92dfa-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="92dfa-240">msbuild.exe için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="92dfa-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="92dfa-241">Bu koşullu MSBuild özelliğini proje dosyanızda da ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92dfa-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="92dfa-242">Kilitli mod `true`varsa, kilit dosyası oluşturulduktan sonra proje için tanımlanan paket bağımlılıklarını güncellediyseniz, kilit dosyasında listelenen tam paketleri geri yükleyin veya başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="92dfa-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="92dfa-243">Kilit dosyanızı kaynak deponuzun bir parçası yapma</span><span class="sxs-lookup"><span data-stu-id="92dfa-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="92dfa-244">Bir uygulama, yürütülebilir bir uygulama oluşturuyorsanız ve söz konusu proje bağımlılık zincirinin başındaysa, NuGet'in geri yükleme sırasında bu uygulamadan yararlanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.</span><span class="sxs-lookup"><span data-stu-id="92dfa-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="92dfa-245">Ancak, projeniz göndermediğiniz bir kitaplık projesi veya diğer projelerin bağlı olduğu ortak bir kod projesiyse, kaynak kodunuzun bir parçası olarak kilit dosyasını iade **etmemelisiniz.**</span><span class="sxs-lookup"><span data-stu-id="92dfa-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="92dfa-246">Kilit dosyasını tutmanın bir sakıncası yoktur, ancak bu ortak kod projesine bağlı olan bir projenin geri yüklenir/oluşturulması sırasında kilit dosyasında listelenen ortak kod projesi için kilitli paket bağımlılıkları kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="92dfa-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="92dfa-247">Örn.</span><span class="sxs-lookup"><span data-stu-id="92dfa-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="92dfa-248">Bir `ProjectA` `PackageX` `2.0.0` sürüme bağımlıysa ve `ProjectB` `PackageX` aynı zamanda sürüme `1.0.0`bağlı olarak başvurular `ProjectB` da varsa, `PackageX` kilit `1.0.0`dosyası sürüme bir bağımlılık listeleyecek.</span><span class="sxs-lookup"><span data-stu-id="92dfa-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="92dfa-249">Ancak, `ProjectA` ne zaman inşa edilir, onun kilit `PackageX` **`2.0.0`** dosyası sürümü bir bağımlılık içerir `ProjectB`ve kilit dosyasında listelenen **değil.** `1.0.0`</span><span class="sxs-lookup"><span data-stu-id="92dfa-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="92dfa-250">Bu nedenle, ortak bir kod projesinin kilit dosyası, bağlı olan projeler için çözülen paketler üzerinde çok az söz hakkı vardır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="92dfa-251">Dosya genişletilebilirliğini kilitle</span><span class="sxs-lookup"><span data-stu-id="92dfa-251">Lock file extensibility</span></span>

<span data-ttu-id="92dfa-252">Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme çeşitli davranışları denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92dfa-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="92dfa-253">NuGet.exe seçeneği</span><span class="sxs-lookup"><span data-stu-id="92dfa-253">NuGet.exe option</span></span> | <span data-ttu-id="92dfa-254">dotnet seçeneği</span><span class="sxs-lookup"><span data-stu-id="92dfa-254">dotnet option</span></span> | <span data-ttu-id="92dfa-255">MSBuild eşdeğer seçeneği</span><span class="sxs-lookup"><span data-stu-id="92dfa-255">MSBuild equivalent option</span></span> | <span data-ttu-id="92dfa-256">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92dfa-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="92dfa-257">Geri YüklemePaketleriWithLockFile</span><span class="sxs-lookup"><span data-stu-id="92dfa-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="92dfa-258">Kilit dosyasının kullanımını seçer.</span><span class="sxs-lookup"><span data-stu-id="92dfa-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="92dfa-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="92dfa-259">RestoreLockedMode</span></span> | <span data-ttu-id="92dfa-260">Geri yükleme için kilitli modu sağlar.</span><span class="sxs-lookup"><span data-stu-id="92dfa-260">Enables locked mode for restore.</span></span> <span data-ttu-id="92dfa-261">Bu, yinelenebilir yapılar istediğiniz CI/CD senaryolarında yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="92dfa-262">Geri YüklemeGücü Değerlendirin</span><span class="sxs-lookup"><span data-stu-id="92dfa-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="92dfa-263">Bu seçenek, projede tanımlanan kayan sürümü olan paketler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="92dfa-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="92dfa-264">Varsayılan olarak, NuGet geri yüklemesi, bu seçenekle geri yükleme çalıştırmadığınız sürece paket sürümünü her geri yüklemede otomatik olarak güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="92dfa-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="92dfa-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="92dfa-265">NuGetLockFilePath</span></span> | <span data-ttu-id="92dfa-266">Proje için özel bir kilit dosyası konumunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="92dfa-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="92dfa-267">Varsayılan olarak, NuGet kök dizininde destekler. `packages.lock.json`</span><span class="sxs-lookup"><span data-stu-id="92dfa-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="92dfa-268">Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="92dfa-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
