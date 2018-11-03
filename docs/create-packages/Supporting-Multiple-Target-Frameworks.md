---
title: NuGet paketleri için çoklu sürüm desteği
description: Tek bir NuGet paketi birden çok .NET Framework sürümlerini hedeflemek için çeşitli yöntemler açıklaması.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: c59839240935e2a6c590dea3adf623313f79f02f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981151"
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="e1ccc-103">Birden çok .NET framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="e1ccc-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="e1ccc-104">*NuGet 4.0 + kullanarak .NET Core projeleri için bkz: [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md) çapraz hedefleme hakkında ayrıntılı bilgi için.*</span><span class="sxs-lookup"><span data-stu-id="e1ccc-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="e1ccc-105">Birçok kitaplıkları belirli bir .NET Framework sürümünü hedefler.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="e1ccc-106">Örneğin, kitaplığınıza UWP için belirli bir sürümünü ve .NET Framework 4. 6'içinde özelliklerinden yararlanır başka bir sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="e1ccc-107">Bu, birden çok sürümünü aynı kitaplığı tek bir paket içinde açıklanan dayanan çalışma dizini yöntemi kullanılırken koyarak NuGet destekler uyum sağlayacak şekilde [paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="e1ccc-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="e1ccc-108">Framework sürümü klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="e1ccc-108">Framework version folder structure</span></span>

<span data-ttu-id="e1ccc-109">Her zaman tek bir kitaplığı veya hedef sürümünü içeren bir paket birden çok çerçeveyi oluştururken, alt yapmanız `lib` farklı büyük/küçük harfe framework adları ile aşağıdaki kural kullanılarak:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="e1ccc-110">Desteklenen adlarının tam bir listesi için bkz. [hedef çerçeve başvurusu](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="e1ccc-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="e1ccc-111">Hiçbir zaman doğrudan kök yerleştirilmiştir ve bir çerçeve özel değil kitaplığı sürümünü olmalıdır `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="e1ccc-112">(Bu özellik yalnızca desteklenen `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="e1ccc-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="e1ccc-113">Bunun yapılması kitaplığı herhangi bir hedef çerçevesi ile uyumlu hale getirmek ve her yerden yüklenmesi için büyük olasılıkla beklenmeyen çalışma zamanı hatalarıyla kaynaklanan izin.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="e1ccc-114">Derleme kök klasöründe ekleme (gibi `lib\abc.dll`) veya alt klasörleri (gibi `lib\abc\abc.dll`) kullanım dışı bırakıldı ve PackagesReference biçimi kullanılırken göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="e1ccc-115">Örneğin, aşağıdaki klasör yapısına çerçeveye özgü dört derleme sürümlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="e1ccc-116">Bu dosyalar paket oluştururken kolayca dahil etmek için bir özyinelemeli kullanın `**` joker karakterin `<files>` bölümünü, `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="e1ccc-117">Mimariye özel klasörler</span><span class="sxs-lookup"><span data-stu-id="e1ccc-117">Architecture-specific folders</span></span>

<span data-ttu-id="e1ccc-118">Mimariye özel derlemeler, diğer bir deyişle, ARM, x 86 ve x64, hedef ayrı derlemeler varsa bunları adlı bir klasörde yerleştirmelisiniz `runtimes` alt klasörleri içinde `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="e1ccc-119">Örneğin, Windows 10 hedefleyen yerel ve yönetilen DLL'leri aşağıdaki klasör yapısına kapsayan ve `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="e1ccc-120">Böylece karşılık gelen sağlamak istiyorsanız derleme zamanı derlemesi de sonra bu derlemeler yalnızca çalışma zamanında kullanılabilir `AnyCPU` derlemede `/ref{tfm}` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-120">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="e1ccc-121">Lütfen unutmayın, NuGet her zaman seçer bu derleme veya çalışma zamanı varlıklar bir klasörden bunu uyumlu bazı varlıklarından varsa `/ref` ardından `/lib` derleme zamanı derlemeleri eklemek için yok sayılacak.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-121">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="e1ccc-122">Benzer şekilde, bazı uyumlu varlıklarından varsa `/runtime` aynı zamanda `/lib` için çalışma zamanı yok sayılacak.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-122">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="e1ccc-123">Bkz: [UWP paketleri oluşturma](../guides/create-uwp-packages.md) içinde bu dosyaları başvuran bir örnek için `.nuspec` bildirimi.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-123">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="e1ccc-124">Ayrıca bkz [bir Windows mağazası uygulama bileşeni NuGet ile paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="e1ccc-124">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="e1ccc-125">Eşleşen derleme sürümlerini ve hedef Framework'ü bir projedeki</span><span class="sxs-lookup"><span data-stu-id="e1ccc-125">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="e1ccc-126">NuGet birden çok bütünleştirilmiş kod sürümü olan bir paketi yüklendiğinde, derlemenin framework adı projenin hedef çerçevesi ile eşleştirmeyi dener.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-126">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="e1ccc-127">Bir eşleşme bulunmazsa, NuGet derleme varsa ya da projenin hedef çerçevesi eşit olan en yüksek sürüm için kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-127">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="e1ccc-128">Uyumlu hiçbir derleme tespit edilirse, NuGet uygun bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-128">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="e1ccc-129">Örneğin, bir paket içinde aşağıdaki klasör yapısına göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-129">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="e1ccc-130">Bu paket, .NET Framework 4.6 hedefleyen bir proje içinde yüklerken, NuGet derleme içinde yükler `net45` klasöründe, 4.6 küçük veya ona eşit olan en yüksek kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-130">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="e1ccc-131">Öte yandan, projenin hedeflediği .NET Framework 4.6.1, NuGet derleme içinde yükler `net461` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-131">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="e1ccc-132">Projenin hedeflediği .NET framework 4.0 ve daha önceki NuGet uyumlu bütünleştirilmiş bulma değil için uygun bir hata iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-132">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="e1ccc-133">Framework sürümüne göre gruplandırma derlemeleri</span><span class="sxs-lookup"><span data-stu-id="e1ccc-133">Grouping assemblies by framework version</span></span>

<span data-ttu-id="e1ccc-134">NuGet paketinde yalnızca tek kitaplığı klasör derlemeleri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-134">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="e1ccc-135">Örneğin, bir paketi aşağıdaki klasör yapısına olduğunu varsayın:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-135">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="e1ccc-136">.NET Framework 4.5 hedefleyen bir proje içinde paketi yüklendiğinde `MyAssembly.dll` (v2.0) yüklü tek bir derleme olduğundan.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-136">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="e1ccc-137">`MyAssembly.Core.dll` içinde listelenmediğinden (v1.0) yüklü değil `net45` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-137">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="e1ccc-138">NuGet, çünkü bu şekilde davranır `MyAssembly.Core.dll` sürümüne 2.0 birleştirilmiş `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-138">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="e1ccc-139">İsterseniz `MyAssembly.Core.dll` .NET Framework 4.5 için yüklenecek bir kopyasını yerleştirmek `net45` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-139">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="e1ccc-140">Derlemeleri framework profile göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="e1ccc-140">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="e1ccc-141">NuGet, tire ve profil adına klasörü sonuna ekleyerek belirli framework profili hedefleyen da destekler.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-141">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="e1ccc-142">Desteklenen profilleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-142">The supported profiles are as follows:</span></span>

- <span data-ttu-id="e1ccc-143">`client`: İstemci profili</span><span class="sxs-lookup"><span data-stu-id="e1ccc-143">`client`: Client Profile</span></span>
- <span data-ttu-id="e1ccc-144">`full`: Tam profili</span><span class="sxs-lookup"><span data-stu-id="e1ccc-144">`full`: Full Profile</span></span>
- <span data-ttu-id="e1ccc-145">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e1ccc-145">`wp`: Windows Phone</span></span>
- <span data-ttu-id="e1ccc-146">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="e1ccc-146">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="e1ccc-147">Kullanmak için hangi NuGet hedef belirleme</span><span class="sxs-lookup"><span data-stu-id="e1ccc-147">Determining which NuGet target to use</span></span>

<span data-ttu-id="e1ccc-148">Ne zaman taşınabilir sınıf kitaplığı hedefleyen paketleme kitaplıkları olabilir hangi NuGet hedef klasör adlarınızı kullanmanız gerektiğini belirlemek zor ve `.nuspec` , özellikle de yalnızca bir alt kümesini PCL hedefleyen dosyası.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-148">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="e1ccc-149">Aşağıdaki dış kaynaklar bu konuda yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-149">The following external resources will help you with this:</span></span>

- <span data-ttu-id="e1ccc-150">[.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="e1ccc-150">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="e1ccc-151">[Taşınabilir sınıf kitaplığı profilleri](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tablo PCL profilleri ile eşdeğer NuGet hedeflerine numaralandırma</span><span class="sxs-lookup"><span data-stu-id="e1ccc-151">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="e1ccc-152">[Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): PCL belirlemek için komut satırı aracını sisteminizde kullanılabilir profiller</span><span class="sxs-lookup"><span data-stu-id="e1ccc-152">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="e1ccc-153">İçerik dosyaları ve PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="e1ccc-153">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="e1ccc-154">Mutable içerik dosyaları ve komut dosyası yürütme bulunan `packages.config` yalnızca biçimini; sahip diğer biçimlere kullanım dışıdır ve yeni tüm paketler için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-154">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="e1ccc-155">İle `packages.config`, içeriği içinde aynı klasör kuralı kullanarak hedef Framework'ü göre dosyaları ve PowerShell betiklerini gruplandırılabilir `content` ve `tools` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-155">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="e1ccc-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e1ccc-156">For example:</span></span>

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

<span data-ttu-id="e1ccc-157">Çerçeve klasörü boş bırakılırsa, NuGet derleme başvuruları veya içerik dosyalarını eklemek değil veya bu çerçeve için PowerShell betikleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-157">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="e1ccc-158">Çünkü `init.ps1` yürütülür çözüm düzeyinde ve proje bağımlı olmayan, bunu doğrudan altında yerleştirilmelidir `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-158">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="e1ccc-159">Bir çerçeve klasörü altında yerleştirdiyseniz göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="e1ccc-159">It's ignored if placed under a framework folder.</span></span>
