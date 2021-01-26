---
title: NuGet paketleri için Çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: e919b11670589900d9e588db33fd68b8df592ac2
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774563"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="c2e6e-103">Çoklu .NET sürümlerini destekler</span><span class="sxs-lookup"><span data-stu-id="c2e6e-103">Support multiple .NET versions</span></span>

<span data-ttu-id="c2e6e-104">Birçok kitaplık .NET Framework belirli bir sürümünü hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="c2e6e-105">Örneğin, kitaplıkınızın, UWP 'e özgü bir sürümüne ve .NET Framework 4,6 ' deki özelliklerden yararlanan başka bir sürüme sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="c2e6e-106">NuGet buna uyum sağlamak için, aynı kitaplığın birden çok sürümünü tek bir pakette yerleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="c2e6e-107">Bu makalede, paketin veya derlemelerin nasıl oluşturulduğuna bakılmaksızın bir NuGet paketinin düzeni açıklanmaktadır (yani, düzen birden çok SDK olmayan *. csproj* dosyası ve özel bir *. nuspec* dosyası ya da tek bir çok hedefli SDK stili *. csproj*) kullanmanın yanı sıra, düzen aynı olur.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="c2e6e-108">Bir SDK stili proje için, NuGet [paketi](../reference/msbuild-targets.md) , paketin nasıl oluşturulması gerektiğini bilir ve derlemeleri doğru lib klasörlerine yerleştirmeyi ve her hedef çerçeve (tfd) için bağımlılık grupları oluşturmayı otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="c2e6e-109">Ayrıntılı yönergeler için bkz. [proje dosyanızdaki çoklu .NET Framework sürümlerini destekleme](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="c2e6e-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="c2e6e-110">[Paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)bölümünde açıklanan kural tabanlı çalışma dizini yöntemi kullanılırken bu makalede açıklandığı gibi paketi el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="c2e6e-111">SDK stili bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı gibi el ile düzenlemek de tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="c2e6e-112">Framework sürüm klasörü yapısı</span><span class="sxs-lookup"><span data-stu-id="c2e6e-112">Framework version folder structure</span></span>

<span data-ttu-id="c2e6e-113">Bir kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedefleyen bir paket oluştururken, her zaman `lib` aşağıdaki kurala sahip farklı büyük/küçük harf duyarlı çerçeve adları kullanarak alt klasörler yaparsınız:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

```
lib\{framework name}[{version}]
```

<span data-ttu-id="c2e6e-114">Desteklenen adların tüm listesi için bkz. [hedef çerçeveler başvurusu](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="c2e6e-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="c2e6e-115">Bir çerçeveye özgü olmayan ve doğrudan kök klasöre yerleştirilebilecek bir kitaplığın sürümüne sahip olmanız gerekir `lib` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="c2e6e-116">(Bu özellik yalnızca ile desteklenir `packages.config` ).</span><span class="sxs-lookup"><span data-stu-id="c2e6e-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="c2e6e-117">Bunu yapmak, kitaplığı herhangi bir hedef çerçeve ile uyumlu hale getirir ve büyük olasılıkla beklenmedik çalışma zamanı hatalarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="c2e6e-118">Derlemeleri kök klasöre (gibi `lib\abc.dll` ) veya alt klasörlere (gibi) eklemek `lib\abc\abc.dll` kullanım dışı bırakılmıştır ve PackagesReference biçimi kullanılırken yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="c2e6e-119">Örneğin, aşağıdaki klasör yapısı çerçeveye özgü bir derlemenin dört sürümünü destekler:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

```
\lib
    \net46
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
    \uap
        \MyAssembly.dll
    \netcore
        \MyAssembly.dll
```

<span data-ttu-id="c2e6e-120">Paketi oluştururken tüm bu dosyaları kolayca dahil etmek için, ' `**` ın bölümünde özyinelemeli bir joker karakter kullanın `<files>` `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="c2e6e-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="c2e6e-121">Mimariye özgü klasörler</span><span class="sxs-lookup"><span data-stu-id="c2e6e-121">Architecture-specific folders</span></span>

<span data-ttu-id="c2e6e-122">Mimariye özgü derlemeleriniz, yani ARM, x86 ve x64 'u hedefleyen ayrı derlemeler varsa, bunları `runtimes` veya adlı alt klasörler içindeki adlı bir klasöre yerleştirmeniz gerekir `{platform}-{architecture}\lib\{framework}` `{platform}-{architecture}\native` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="c2e6e-123">Örneğin, aşağıdaki klasör yapısı, Windows 10 ve Framework 'ü hedefleyen hem yerel hem de yönetilen DLL 'Leri kapsayabilmelidir `uap10.0` :</span><span class="sxs-lookup"><span data-stu-id="c2e6e-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

```
\runtimes
    \win10-arm
        \native
        \lib\uap10.0
    \win10-x86
        \native
        \lib\uap10.0
    \win10-x64
        \native
        \lib\uap10.0
```

<span data-ttu-id="c2e6e-124">Bu derlemeler yalnızca çalışma zamanında kullanılabilir. bu nedenle, ilgili derleme zamanı derlemesini ve sonra da klasöründe derlemeye sahip olmak istiyorsanız `AnyCPU` `/ref/{tfm}` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="c2e6e-125">Lütfen NuGet bu derleme veya çalışma zamanı varlıklarını her zaman bir klasörden seçer, bundan sonra bazı uyumlu varlıklar varsa `/ref` `/lib` derleme zamanı derlemelerini eklemek için yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="c2e6e-126">Benzer şekilde, öğesinden bazı uyumlu varlıklar varsa, `/runtimes` `/lib` çalışma zamanı için de yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="c2e6e-127">Bildirimde bu dosyalara başvurma örneği için bkz. [UWP paketleri oluşturma](../guides/create-uwp-packages.md) `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="c2e6e-128">Ayrıca bkz. [NuGet Ile Windows Mağazası uygulama bileşeni paketleme](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="c2e6e-128">Also, see [Packing a Windows store app component with NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="c2e6e-129">Bir projede derleme sürümlerini ve hedef Framework 'ü eşleştirme</span><span class="sxs-lookup"><span data-stu-id="c2e6e-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="c2e6e-130">NuGet birden çok derleme sürümüne sahip bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="c2e6e-131">Bir eşleşme bulunmazsa, NuGet derlemeyi, varsa projenin hedef çerçevesine eşit veya daha küçük olan en yüksek sürüm için kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="c2e6e-132">Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="c2e6e-133">Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-133">For example, consider the following folder structure in a package:</span></span>

```
\lib
    \net45
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
```

<span data-ttu-id="c2e6e-134">Bu paketi, .NET Framework 4,6 ' i hedefleyen bir projeye yüklerken, `net45` en yüksek kullanılabilir sürüm 4,6 ' e eşit veya daha düşük olan en yüksek sürüm olan NuGet, derlemeyi klasöre yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="c2e6e-135">Proje .NET Framework 4.6.1 hedefliyorsa, diğer yandan NuGet, derlemeyi `net461` klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="c2e6e-136">Proje, .NET Framework 4,0 ve öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulmayan uygun bir hata iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="c2e6e-137">Derlemeleri Framework sürümüne göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="c2e6e-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="c2e6e-138">NuGet, derlemeleri yalnızca paketteki tek bir kitaplık klasöründen kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="c2e6e-139">Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-139">For example, suppose a package has the following folder structure:</span></span>

```
\lib
    \net40
        \MyAssembly.dll (v1.0)
        \MyAssembly.Core.dll (v1.0)
    \net45
        \MyAssembly.dll (v2.0)
```

<span data-ttu-id="c2e6e-140">Paket, .NET Framework 4,5 ' i hedefleyen bir projeye yüklendiğinde, `MyAssembly.dll` (v 2.0) yüklü tek derleme olur.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="c2e6e-141">`MyAssembly.Core.dll` (v 1.0) klasöründe listelenmediğinden yüklenmedi `net45` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="c2e6e-142">NuGet bu şekilde davranır çünkü `MyAssembly.Core.dll` sürüm 2,0 ' de birleştirilmiş olabilir `MyAssembly.dll` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="c2e6e-143">`MyAssembly.Core.dll`.NET Framework 4,5 için yüklemek istiyorsanız, klasöre bir kopya yerleştirin `net45` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="c2e6e-144">Derlemeleri çerçeve profiline göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="c2e6e-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="c2e6e-145">NuGet Ayrıca, klasörün sonuna bir tire ve profil adı ekleyerek belirli bir çerçeve profilinin hedeflenmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

<span data-ttu-id="c2e6e-146">LIB \{ Framework adı}-{profile}</span><span class="sxs-lookup"><span data-stu-id="c2e6e-146">lib\{framework name}-{profile}</span></span>

<span data-ttu-id="c2e6e-147">Desteklenen profiller şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-147">The supported profiles are as follows:</span></span>

- <span data-ttu-id="c2e6e-148">`client`: İstemci profili</span><span class="sxs-lookup"><span data-stu-id="c2e6e-148">`client`: Client Profile</span></span>
- <span data-ttu-id="c2e6e-149">`full`: Tam profil</span><span class="sxs-lookup"><span data-stu-id="c2e6e-149">`full`: Full Profile</span></span>
- <span data-ttu-id="c2e6e-150">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c2e6e-150">`wp`: Windows Phone</span></span>
- <span data-ttu-id="c2e6e-151">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="c2e6e-151">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="c2e6e-152">Bağımlılıkları bildirme (Gelişmiş)</span><span class="sxs-lookup"><span data-stu-id="c2e6e-152">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="c2e6e-153">Bir proje dosyası paketleme sırasında, NuGet otomatik olarak projeden bağımlılıkları oluşturmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-153">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="c2e6e-154">Bağımlılıkları bildirmek için bir *. nuspec* dosyası kullanma hakkında bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-154">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="c2e6e-155">*(Sürüm 2.0 +)* Öğesi içindeki öğeleri kullanarak hedef projenin hedef çerçevesine karşılık gelen *. nuspec* içinde paket bağımlılıklarını bildirebilirsiniz `<group>` `<dependencies>` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-155">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="c2e6e-156">Daha fazla bilgi için bkz. [Dependencies öğesi](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="c2e6e-156">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="c2e6e-157">Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<dependency>` öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-157">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="c2e6e-158">Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-158">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="c2e6e-159">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-159">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="c2e6e-160">*LIB/* ve *ref/* klasörlerdeki dosyalar için hedef çerçeve bilinen adı (tfd) başına bir grup kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-160">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="c2e6e-161">Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :</span><span class="sxs-lookup"><span data-stu-id="c2e6e-161">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="c2e6e-162">Hangi NuGet hedefinin kullanılacağını belirleme</span><span class="sxs-lookup"><span data-stu-id="c2e6e-162">Determining which NuGet target to use</span></span>

<span data-ttu-id="c2e6e-163">Taşınabilir sınıf kitaplığını hedefleyen paketleme kitaplıkları, `.nuspec` özellikle de yalnızca BIR PCL alt kümesini hedeflerken, klasör adlarında ve dosyanızda hangi NuGet hedefini kullanacağınızı tespit etmek için karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-163">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="c2e6e-164">Aşağıdaki dış kaynaklar bu konuda size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-164">The following external resources will help you with this:</span></span>

- <span data-ttu-id="c2e6e-165">[.Net 'Teki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="c2e6e-165">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="c2e6e-166">[Taşınabilir sınıf kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve bunların eşdeğer NuGet hedeflerini numaralandırma tablosu</span><span class="sxs-lookup"><span data-stu-id="c2e6e-166">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="c2e6e-167">[Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): SISTEMINIZDE bulunan PCL profillerinin belirlenmesi için komut satırı aracı</span><span class="sxs-lookup"><span data-stu-id="c2e6e-167">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="c2e6e-168">İçerik dosyaları ve PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="c2e6e-168">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="c2e6e-169">Kesilebilir içerik dosyaları ve betik yürütme yalnızca biçimlendirme ile kullanılabilir `packages.config` ; diğer tüm formatlarda kullanım dışı bırakılmıştır ve yeni paketler için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-169">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="c2e6e-170">İle `packages.config` , içerik dosyaları ve PowerShell betikleri, ve klasörlerinde aynı klasör kuralına göre hedef çerçeveye göre gruplanabilir `content` `tools` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-170">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="c2e6e-171">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c2e6e-171">For example:</span></span>

```
\content
    \net46
        \MyContent.txt
    \net461
        \MyContent461.txt
    \uap
        \MyUWPContent.html
    \netcore
\tools
    init.ps1
    \net46
        install.ps1
        uninstall.ps1
    \uap
        install.ps1
        uninstall.ps1
```

<span data-ttu-id="c2e6e-172">Bir çerçeve klasörü boş bırakılırsa NuGet, derleme başvuruları veya içerik dosyaları eklemez ya da bu çerçeve için PowerShell betikleri çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-172">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="c2e6e-173">, `init.ps1` Çözüm düzeyinde yürütüldüğü ve projeye bağımlı olmadığından, doğrudan klasörün altına yerleştirilmesi gerekir `tools` .</span><span class="sxs-lookup"><span data-stu-id="c2e6e-173">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="c2e6e-174">Çerçeve klasörü altına yerleştirildiğinde yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="c2e6e-174">It's ignored if placed under a framework folder.</span></span>