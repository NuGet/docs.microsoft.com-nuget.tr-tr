---
title: NuGet paketleri için Çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385102"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="d6c31-103">Çoklu .NET sürümlerini destekler</span><span class="sxs-lookup"><span data-stu-id="d6c31-103">Support multiple .NET versions</span></span>

<span data-ttu-id="d6c31-104">Birçok kitaplık .NET Framework belirli bir sürümünü hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="d6c31-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="d6c31-105">Örneğin, kitaplıkınızın, UWP 'e özgü bir sürümüne ve .NET Framework 4,6 ' deki özelliklerden yararlanan başka bir sürüme sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6c31-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="d6c31-106">NuGet buna uyum sağlamak için, aynı kitaplığın birden çok sürümünü tek bir pakette yerleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="d6c31-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="d6c31-107">Bu makalede, paketin veya derlemelerin nasıl oluşturulduğuna bakılmaksızın bir NuGet paketinin düzeni açıklanmaktadır (yani, düzen birden çok SDK olmayan *. csproj* dosyası ve özel bir *. nuspec* dosyası ya da tek bir çok hedefli SDK stili *. csproj*) kullanmanın yanı sıra, düzen aynı olur.</span><span class="sxs-lookup"><span data-stu-id="d6c31-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="d6c31-108">Bir SDK stili proje için, NuGet [paketi](../reference/msbuild-targets.md) , paketin nasıl oluşturulması gerektiğini bilir ve derlemeleri doğru lib klasörlerine yerleştirmeyi ve her hedef çerçeve (tfd) için bağımlılık grupları oluşturmayı otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="d6c31-109">Ayrıntılı yönergeler için bkz. [proje dosyanızdaki çoklu .NET Framework sürümlerini destekleme](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="d6c31-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="d6c31-110">[Paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)bölümünde açıklanan kural tabanlı çalışma dizini yöntemi kullanılırken bu makalede açıklandığı gibi paketi el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="d6c31-111">SDK stili bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı gibi el ile düzenlemek de tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6c31-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="d6c31-112">Framework sürüm klasörü yapısı</span><span class="sxs-lookup"><span data-stu-id="d6c31-112">Framework version folder structure</span></span>

<span data-ttu-id="d6c31-113">Bir kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedef alan bir paket oluştururken, aşağıdaki kurala sahip farklı büyük/küçük harf duyarlı çerçeve adları kullanarak her zaman alt klasörleri `lib` altında yaparsınız:</span><span class="sxs-lookup"><span data-stu-id="d6c31-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="d6c31-114">Desteklenen adların tüm listesi için bkz. [hedef çerçeveler başvurusu](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="d6c31-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="d6c31-115">Bir çerçeveye özgü olmayan ve doğrudan kök `lib` klasöre yerleştirilebilecek bir kitaplığın sürümüne sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="d6c31-116">(Bu özellik yalnızca `packages.config`) ile desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="d6c31-117">Bunu yapmak, kitaplığı herhangi bir hedef çerçeve ile uyumlu hale getirir ve büyük olasılıkla beklenmedik çalışma zamanı hatalarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="d6c31-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="d6c31-118">Derlemeleri kök klasöre (örneğin, `lib\abc.dll`) veya alt klasörleri (örneğin, `lib\abc\abc.dll`) eklemek kullanım dışıdır ve PackagesReference biçimi kullanılırken yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="d6c31-119">Örneğin, aşağıdaki klasör yapısı çerçeveye özgü bir derlemenin dört sürümünü destekler:</span><span class="sxs-lookup"><span data-stu-id="d6c31-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="d6c31-120">Paketi oluştururken tüm bu dosyaları kolayca dahil etmek için, `.nuspec``<files>` bölümünde özyinelemeli bir `**` joker karakteri kullanın:</span><span class="sxs-lookup"><span data-stu-id="d6c31-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="d6c31-121">Mimariye özgü klasörler</span><span class="sxs-lookup"><span data-stu-id="d6c31-121">Architecture-specific folders</span></span>

<span data-ttu-id="d6c31-122">Mimariye özgü derlemeleriniz, yani ARM, x86 ve x64 'u hedefleyen ayrı derlemeler varsa, bunları `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native`adlı alt klasörler içinde `runtimes` adlı bir klasöre yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="d6c31-123">Örneğin, aşağıdaki klasör yapısı, Windows 10 ' u ve `uap10.0` çerçevesini hedefleyen hem yerel hem de yönetilen DLL 'Leri kapsayabilmelidir:</span><span class="sxs-lookup"><span data-stu-id="d6c31-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="d6c31-124">Bu derlemeler yalnızca çalışma zamanında kullanılabilir. bu nedenle, ilgili derleme zamanı derlemesini sağlamak ve `/ref/{tfm}` klasöründe `AnyCPU` bütünleştirilmiş kodu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="d6c31-125">Lütfen NuGet her zaman bu derleme veya çalışma zamanı varlıklarını tek bir klasörden seçer. `/ref` bundan sonra bazı uyumlu varlıklar varsa, derleme zamanı derlemelerini eklemek için `/lib` yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="d6c31-126">Benzer şekilde, `/runtimes` ile ilgili bazı uyumlu varlıklar varsa, ayrıca çalışma zamanı için `/lib` yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="d6c31-127">`.nuspec` bildiriminde bu dosyalara başvurma örneği için bkz. [UWP paketleri oluşturma](../guides/create-uwp-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="d6c31-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="d6c31-128">Ayrıca bkz. [NuGet Ile Windows Mağazası uygulama bileşeni paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="d6c31-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="d6c31-129">Bir projede derleme sürümlerini ve hedef Framework 'ü eşleştirme</span><span class="sxs-lookup"><span data-stu-id="d6c31-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="d6c31-130">NuGet birden çok derleme sürümüne sahip bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="d6c31-131">Bir eşleşme bulunmazsa, NuGet derlemeyi, varsa projenin hedef çerçevesine eşit veya daha küçük olan en yüksek sürüm için kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d6c31-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="d6c31-132">Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6c31-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="d6c31-133">Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d6c31-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="d6c31-134">Bu paketi, .NET Framework 4,6 ' i hedefleyen bir projede yüklerken, en yüksek kullanılabilir sürüm 4,6 ' den küçük veya buna eşit olduğu için NuGet, derlemeyi `net45` klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="d6c31-135">Proje, diğer taraftan .NET Framework 4.6.1 hedefliyorsa, NuGet derlemeyi `net461` klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="d6c31-136">Proje, .NET Framework 4,0 ve öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulmayan uygun bir hata iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d6c31-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="d6c31-137">Derlemeleri Framework sürümüne göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="d6c31-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="d6c31-138">NuGet, derlemeleri yalnızca paketteki tek bir kitaplık klasöründen kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d6c31-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="d6c31-139">Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d6c31-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="d6c31-140">Paket, .NET Framework 4,5 ' i hedefleyen bir projeye yüklendiğinde, `MyAssembly.dll` (v 2.0) yüklü tek derleme olur.</span><span class="sxs-lookup"><span data-stu-id="d6c31-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="d6c31-141">`MyAssembly.Core.dll` (v 1.0), `net45` klasöründe listelenmediğinden yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="d6c31-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="d6c31-142">`MyAssembly.Core.dll`, `MyAssembly.dll`sürüm 2,0 ' de birleştirilmiş olabileceğinden NuGet bu şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="d6c31-143">`MyAssembly.Core.dll` .NET Framework 4,5 için yüklenmesini istiyorsanız `net45` klasöre bir kopya yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6c31-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="d6c31-144">Derlemeleri çerçeve profiline göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="d6c31-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="d6c31-145">NuGet Ayrıca, klasörün sonuna bir tire ve profil adı ekleyerek belirli bir çerçeve profilinin hedeflenmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="d6c31-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="d6c31-146">Desteklenen profiller şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d6c31-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="d6c31-147">`client`: Istemci profili</span><span class="sxs-lookup"><span data-stu-id="d6c31-147">`client`: Client Profile</span></span>
- <span data-ttu-id="d6c31-148">`full`: tam profil</span><span class="sxs-lookup"><span data-stu-id="d6c31-148">`full`: Full Profile</span></span>
- <span data-ttu-id="d6c31-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d6c31-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="d6c31-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="d6c31-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="d6c31-151">Bağımlılıkları bildirme (Gelişmiş)</span><span class="sxs-lookup"><span data-stu-id="d6c31-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="d6c31-152">Bir proje dosyası paketleme sırasında, NuGet otomatik olarak projeden bağımlılıkları oluşturmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="d6c31-153">Bağımlılıkları bildirmek için bir *. nuspec* dosyası kullanma hakkında bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="d6c31-154">*(Sürüm 2.0 +)* `<dependencies>` öğesi içinde `<group>` öğeleri kullanarak, hedef projenin hedef çerçevesine karşılık gelen *. nuspec* içinde paket bağımlılıklarını bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6c31-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="d6c31-155">Daha fazla bilgi için bkz. [Dependencies öğesi](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="d6c31-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="d6c31-156">Her grup `targetFramework` adlı bir özniteliğe sahiptir ve sıfır veya daha fazla `<dependency>` öğesi içerir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d6c31-157">Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="d6c31-158">Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="d6c31-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="d6c31-159">*LIB/* ve *ref/* klasörlerdeki dosyalar için hedef çerçeve bilinen adı (tfd) başına bir grup kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d6c31-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="d6c31-160">Aşağıdaki örnek `<group>` öğesinin farklı çeşitlemelerini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="d6c31-160">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="d6c31-161">Hangi NuGet hedefinin kullanılacağını belirleme</span><span class="sxs-lookup"><span data-stu-id="d6c31-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="d6c31-162">Taşınabilir sınıf kitaplığını hedefleyen paketleme kitaplıkları, özellikle yalnızca bir PCL alt kümesini hedeflerken, klasör adlarında ve `.nuspec` dosyasında hangi NuGet hedefini kullanacağınızı tespit etmek için karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="d6c31-163">Aşağıdaki dış kaynaklar bu konuda size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="d6c31-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="d6c31-164">[.Net 'Teki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="d6c31-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="d6c31-165">[Taşınabilir sınıf kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve bunların eşdeğer NuGet hedeflerini numaralandırma tablosu</span><span class="sxs-lookup"><span data-stu-id="d6c31-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="d6c31-166">[Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): SISTEMINIZDE bulunan PCL profillerinin belirlenmesi için komut satırı aracı</span><span class="sxs-lookup"><span data-stu-id="d6c31-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="d6c31-167">İçerik dosyaları ve PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="d6c31-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="d6c31-168">Kesilebilir içerik dosyaları ve betik yürütme yalnızca `packages.config` biçimiyle kullanılabilir; Bunlar diğer tüm biçimleriyle kullanımdan kaldırılmıştır ve yeni paketler için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="d6c31-169">`packages.config`, içerik dosyaları ve PowerShell betikleri, `content` ve `tools` klasörlerindeki aynı klasör kuralına göre hedef çerçeveye göre gruplanabilir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="d6c31-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d6c31-170">For example:</span></span>

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

<span data-ttu-id="d6c31-171">Bir çerçeve klasörü boş bırakılırsa NuGet, derleme başvuruları veya içerik dosyaları eklemez ya da bu çerçeve için PowerShell betikleri çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="d6c31-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="d6c31-172">`init.ps1` çözüm düzeyinde yürütüldüğü ve projeye bağımlı olmadığından, doğrudan `tools` klasörünün altına yerleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6c31-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="d6c31-173">Çerçeve klasörü altına yerleştirildiğinde yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d6c31-173">It's ignored if placed under a framework folder.</span></span>
