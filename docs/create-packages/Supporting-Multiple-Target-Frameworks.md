---
title: NuGet Paketleri için çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden fazla .NET Framework sürümlerini hedefleyen çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429012"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="7aaa2-103">Birden çok .NET sürümü destekleyin</span><span class="sxs-lookup"><span data-stu-id="7aaa2-103">Support multiple .NET versions</span></span>

<span data-ttu-id="7aaa2-104">Birçok kitaplık .NET Framework'ün belirli bir sürümünü hedeflemektedir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="7aaa2-105">Örneğin, kitaplığınızın UWP'ye özgü bir sürümü ve .NET Framework 4.6'daki özelliklerden yararlanan başka bir sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="7aaa2-106">Bunu karşılamak için NuGet, aynı kitaplığın birden çok sürümüne tek bir pakete koymayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="7aaa2-107">Bu makalede, paket veya derlemelerin nasıl inşa edildiğine bakılmaksızın bir NuGet paketinin düzeni açıklanır (diğer bir süre önce düzen, birden fazla SDK tarzı olmayan *.csproj* dosyası ve özel bir *.nuspec* dosyası veya tek bir çok hedefli SDK stili *.csproj*kullanarak aynıdır).</span><span class="sxs-lookup"><span data-stu-id="7aaa2-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="7aaa2-108">Bir SDK tarzı proje için, NuGet [paketi hedefleri](../reference/msbuild-targets.md) paketin nasıl döşenmesi gerektiğini bilir ve derlemeleri doğru lib klasörlerine koyarak ve her hedef çerçevesi (TFM) için bağımlılık grupları oluşturmayı otomatikleştirir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="7aaa2-109">Ayrıntılı yönergeler için [proje dosyanızdaki birden çok .NET Framework sürümüne](multiple-target-frameworks-project-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="7aaa2-110">[Paket Oluşturma'da](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)açıklanan kural tabanlı çalışma dizini yöntemini kullanırken paketi bu makalede açıklandığı şekilde el ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="7aaa2-111">SDK tarzı bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı şekilde el ile birlikte vermeyi de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="7aaa2-112">Çerçeve sürüm klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="7aaa2-112">Framework version folder structure</span></span>

<span data-ttu-id="7aaa2-113">Kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedef alan bir `lib` paket oluştururken, her zaman aşağıdaki kuralı içeren farklı büyük/küçük harf duyarlı çerçeve adlarını kullanarak alt klasörler oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="7aaa2-114">Desteklenen adların tam listesi için [Hedef Çerçeveler başvurusuna](../reference/target-frameworks.md#supported-frameworks)bakın.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="7aaa2-115">Kitaplığın bir çerçeveye özgü olmayan ve doğrudan kök `lib` klasörüne yerleştirilen bir sürümü olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="7aaa2-116">(Bu özellik yalnızca ile `packages.config`desteklenmiştir).</span><span class="sxs-lookup"><span data-stu-id="7aaa2-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="7aaa2-117">Bunu yapmak, kitaplığı herhangi bir hedef çerçeveyle uyumlu hale getirecek ve herhangi bir yere yüklenmesini sağlayarak beklenmeyen çalışma zamanı hatalarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="7aaa2-118">Kök klasöre (örneğin) `lib\abc.dll`veya alt klasörlere (örneğin) `lib\abc\abc.dll`derleme ler eklemek amortismana kaldırıldı ve PackagesReference biçimini kullanırken yoksayılıyor.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="7aaa2-119">Örneğin, aşağıdaki klasör yapısı çerçeveye özgü bir derlemenin dört sürümü destekler:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="7aaa2-120">Paketi kurarken tüm bu dosyaları kolayca eklemek için aşağıdaki `**` bölüme `<files>` özyinelemeli `.nuspec`bir joker karakter kullanın:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="7aaa2-121">Mimariye özel klasörler</span><span class="sxs-lookup"><span data-stu-id="7aaa2-121">Architecture-specific folders</span></span>

<span data-ttu-id="7aaa2-122">Mimariye özgü derlemeler, yani ARM, x86 ve x64'ü hedefleyen ayrı derlemeler varsa, `runtimes` bunları alt klasörler `{platform}-{architecture}\lib\{framework}` `{platform}-{architecture}\native`içinde adı verilen bir klasöre yerleştirmeniz gerekir veya .</span><span class="sxs-lookup"><span data-stu-id="7aaa2-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="7aaa2-123">Örneğin, aşağıdaki klasör yapısı, Windows 10'u ve çerçeveyi `uap10.0` hedefleyen hem yerel hem de yönetilen DL'leri barındırır:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="7aaa2-124">Bu derlemeler yalnızca çalışma zamanında kullanılabilir, bu nedenle ilgili derleme zaman derlemesini `AnyCPU` sağlamak `/ref/{tfm}` istiyorsanız klasörde derleme niz de vardır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="7aaa2-125">Lütfen unutmayın, NuGet her zaman bu derleme veya çalışma zamanı varlıklarını tek `/ref` bir `/lib` klasörden seçer, bu nedenle o zamana kadar uyumlu varlıklar varsa derleme zamanı derlemeleri eklemek için göz ardı edilecektir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="7aaa2-126">Benzer şekilde, o zaman bazı `/runtimes` uyumlu `/lib` varlıklar varsa da çalışma süresi için yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="7aaa2-127">Bu dosyaları bildirimde başvurmak için [UWP Paketleri](../guides/create-uwp-packages.md) `.nuspec` Oluştur'a bakın.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="7aaa2-128">Ayrıca, Bkz. [NuGet ile Windows mağazası uygulama bileşeni paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="7aaa2-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="7aaa2-129">Bir projedeki montaj sürümlerini ve hedef çerçeveyi eşleştirme</span><span class="sxs-lookup"><span data-stu-id="7aaa2-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="7aaa2-130">NuGet birden çok derleme sürümü olan bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="7aaa2-131">Bir eşleşme bulunamazsa, NuGet varsa, projenin hedef çerçevesinden daha az veya projenin hedef çerçevesine eşit olan en yüksek sürüm için derlemeyi kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="7aaa2-132">Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="7aaa2-133">Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="7aaa2-134">Bu paketi .NET Framework 4.6'yı hedefleyen bir projeye yüklerken, `net45` NuGet derlemeyi klasöre yükler, çünkü bu 4,6'dan daha az veya eşit olan kullanılabilir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="7aaa2-135">Proje .NET Framework 4.6.1'i hedefliyorsa, diğer taraftan, NuGet derlemeyi `net461` klasöre yükler.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="7aaa2-136">Proje .NET framework 4.0 ve daha öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulamadığı için uygun bir hata iletisi atar.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="7aaa2-137">Derlemeleri çerçeve sürümüne göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="7aaa2-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="7aaa2-138">NuGet, paketteki tek bir kitaplık klasöründen derlemeleri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="7aaa2-139">Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="7aaa2-140">Paket .NET Framework 4.5'i hedefleyen bir projeye `MyAssembly.dll` yüklendiğinde, (v2.0) yüklenen tek derlemedir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="7aaa2-141">`MyAssembly.Core.dll``net45` (v1.0) klasörde listelenmediği için yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="7aaa2-142">NuGet bu şekilde işlemktedir, çünkü `MyAssembly.Core.dll` sürüm 2.0'da `MyAssembly.dll`birleştirilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="7aaa2-143">.NET `MyAssembly.Core.dll` Framework 4.5 için yüklü olmak istiyorsanız, bir `net45` kopyasını klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="7aaa2-144">Derlemeleri çerçeve profiline göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="7aaa2-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="7aaa2-145">NuGet ayrıca, bir tire ve profil adını klasörün sonuna ekleyerek belirli bir çerçeve profilini hedeflemeyi de destekler.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="7aaa2-146">Desteklenen profiller aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="7aaa2-147">`client`: Müşteri Profili</span><span class="sxs-lookup"><span data-stu-id="7aaa2-147">`client`: Client Profile</span></span>
- <span data-ttu-id="7aaa2-148">`full`: Tam Profil</span><span class="sxs-lookup"><span data-stu-id="7aaa2-148">`full`: Full Profile</span></span>
- <span data-ttu-id="7aaa2-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7aaa2-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="7aaa2-150">`cf`: Kompakt Çerçeve</span><span class="sxs-lookup"><span data-stu-id="7aaa2-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="7aaa2-151">Bağımlılıkları bildirme (Gelişmiş)</span><span class="sxs-lookup"><span data-stu-id="7aaa2-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="7aaa2-152">Bir proje dosyasını paketlerken, NuGet projedeki bağımlılıkları otomatik olarak oluşturmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="7aaa2-153">Bağımlılıkları bildirmek için *.nuspec* dosyası kullanma yla ilgili bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="7aaa2-154">*(Sürüm 2.0+)* Öğe içindeki `<group>` `<dependencies>` öğeleri kullanarak hedef projenin hedef çerçevesine karşılık gelen *.nuspec'teki* paket bağımlılıklarını bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="7aaa2-155">Daha fazla bilgi için [bağımlılıklar öğesine](../reference/nuspec.md#dependencies-element)bakın.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="7aaa2-156">Her grubun adında `targetFramework` bir özniteliği vardır `<dependency>` ve sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="7aaa2-157">Hedef çerçeve projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="7aaa2-158">Tam çerçeve tanımlayıcıları için [Hedef çerçevelerine](../reference/target-frameworks.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="7aaa2-159">*Lib/* ve *ref/* klasörlerdeki dosyalar için Hedef Çerçeve Moniker (TFM) başına bir grup kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="7aaa2-160">Aşağıdaki örnek, öğenin `<group>` farklı varyasyonlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-160">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="7aaa2-161">Hangi NuGet hedefini kullanacağını belirleme</span><span class="sxs-lookup"><span data-stu-id="7aaa2-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="7aaa2-162">Taşınabilir Sınıf Kitaplığı'nı hedefleyen kitaplıkları paketlemekitaplarını klasör adlarınızda ve `.nuspec` dosyanızda kullanmanız gereken NuGet hedefini belirlemek zor olabilir, özellikle de PCL'nin yalnızca bir alt kümesini hedefliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="7aaa2-163">Aşağıdaki dış kaynaklar bu size yardımcı olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="7aaa2-164">[.NET 'deki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="7aaa2-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="7aaa2-165">[Taşınabilir Sınıf Kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve eşdeğernu NuGet hedeflerini tablo yakan</span><span class="sxs-lookup"><span data-stu-id="7aaa2-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="7aaa2-166">[Taşınabilir Sınıf Kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): sisteminizde bulunan PCL profillerini belirlemek için komut satırı aracı</span><span class="sxs-lookup"><span data-stu-id="7aaa2-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="7aaa2-167">İçerik dosyaları ve PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="7aaa2-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="7aaa2-168">Mutable içerik dosyaları ve komut `packages.config` dosyası yürütme yalnızca biçimi ile kullanılabilir; diğer tüm biçimlerle birlikte amortismana alınır ve yeni paketler için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="7aaa2-169">Ile, `packages.config`içerik dosyaları ve PowerShell komut dosyaları hedef çerçeve ve `content` `tools` klasörler içinde aynı klasör kuralı kullanılarak gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="7aaa2-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7aaa2-170">For example:</span></span>

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

<span data-ttu-id="7aaa2-171">Bir çerçeve klasörü boş bırakılırsa, NuGet derleme başvuruları veya içerik dosyaları eklemez veya bu çerçeve için PowerShell komut dosyalarını çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="7aaa2-172">Çözüm `init.ps1` düzeyinde yürütüldüğünden ve `tools` projeye bağlı değil, doğrudan klasörün altına yerleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="7aaa2-173">Bir çerçeve klasörü altına yerleştirilirse yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="7aaa2-173">It's ignored if placed under a framework folder.</span></span>
