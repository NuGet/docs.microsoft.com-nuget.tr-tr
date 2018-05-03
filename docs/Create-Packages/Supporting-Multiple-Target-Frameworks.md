---
title: Çoklu sürüm desteği için NuGet paketleri
description: Tek bir NuGet paketi birden çok .NET Framework sürümü hedeflemek için çeşitli yöntemler açıklaması.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: d1a64c61954381b7ab3a7ecc8aa5a812cfa14e8b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="17e2a-103">Birden çok .NET framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="17e2a-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="17e2a-104">*NuGet 4.0 + kullanarak .NET Core projeleri için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md) arası hedefleme hakkında ayrıntılı bilgi için.*</span><span class="sxs-lookup"><span data-stu-id="17e2a-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="17e2a-105">Birçok kitaplıkları belirli bir .NET Framework sürümünü hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="17e2a-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="17e2a-106">Örneğin, kitaplığınızın UWP için belirli bir sürüm ve .NET Framework 4.6 özelliklerinden yararlanır başka bir sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="17e2a-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="17e2a-107">Bu, açıklanan kurala dayalı çalışma dizini yöntemi kullanırken, tek bir pakette aynı kitaplığı birden fazla sürümünü koyma NuGet destekler uyum sağlayacak şekilde [paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="17e2a-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="17e2a-108">Framework'te sürüm klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="17e2a-108">Framework version folder structure</span></span>

<span data-ttu-id="17e2a-109">Bir kitaplık veya hedef yalnızca bir sürümü içeren bir paket birden çok çerçeveyi oluştururken, her zaman klasörleriyle yaptığınız `lib` farklı büyük/küçük harfe framework adları ile aşağıdaki kural kullanılarak:</span><span class="sxs-lookup"><span data-stu-id="17e2a-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="17e2a-110">Desteklenen ad tam bir listesi için bkz: [hedef çerçeveyi başvuru](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="17e2a-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="17e2a-111">Hiçbir zaman bir çerçeve özgüdür ve doğrudan kök olarak yerleştirilen kitaplığı bir sürümüne sahip olmalıdır `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="17e2a-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="17e2a-112">(Bu özellik yalnızca destekleniyordu `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="17e2a-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="17e2a-113">Ve tüm hedef framework ile uyumlu hale olması izin verin Bunun yapılması her yerden, büyük olasılıkla beklenmeyen çalışma zamanı hataları kaynaklanan yüklü.</span><span class="sxs-lookup"><span data-stu-id="17e2a-113">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="17e2a-114">Kök klasöründe derlemeler ekleme (gibi `lib\abc.dll`) veya alt klasörlerinde (gibi `lib\abc\abc.dll`) kullanım dışı bırakıldı ve PackagesReference biçimi kullanılırken göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="17e2a-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="17e2a-115">Örneğin, aşağıdaki klasör yapısını bir derlemeyi çerçeveye özel dört sürümlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="17e2a-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="17e2a-116">Bu dosyalar paket oluştururken kolayca eklemek için bir özyinelemeli kullanın `**` joker karakter olarak `<files>` bölümü, `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="17e2a-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="17e2a-117">Mimariye özel klasörler</span><span class="sxs-lookup"><span data-stu-id="17e2a-117">Architecture-specific folders</span></span>

<span data-ttu-id="17e2a-118">Mimariye özel derlemeler, diğer bir deyişle, ARM, hedef x 86 ve x64, ayrı derlemeler varsa bunları adlı bir klasörde yerleştirmelisiniz `runtimes` adlı alt klasörlerdeki `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="17e2a-119">Örneğin, aşağıdaki klasör yapısını Windows 10 hedefleme yerel ve yönetilen DLL'leri kapsayan ve `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="17e2a-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="17e2a-120">Bkz: [UWP paketleri oluşturmak](../guides/create-uwp-packages.md) bu dosyalarda başvuran bir örnek için `.nuspec` bildirimi.</span><span class="sxs-lookup"><span data-stu-id="17e2a-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="17e2a-121">Derleme sürümlerini ve bir proje hedef çerçevesi eşleştirme</span><span class="sxs-lookup"><span data-stu-id="17e2a-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="17e2a-122">NuGet birden çok derleme sürümü olan bir paketi yüklendiğinde, projenin hedef çerçevesini derlemenin framework adla eşleşecek şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="17e2a-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="17e2a-123">Bir eşleşme bulunmazsa, NuGet projenin hedef çerçevesi eşit veya daha az kullanılabilir ise en yüksek sürüm için derleme kopyalar.</span><span class="sxs-lookup"><span data-stu-id="17e2a-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="17e2a-124">Uyumlu derleme bulunursa, NuGet uygun bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="17e2a-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="17e2a-125">Örneğin, bir paketi aşağıdaki klasör yapısındaki göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="17e2a-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="17e2a-126">.NET Framework 4.6 hedefleyen bir projede bu paket yükleme sırasında derlemede NuGet yükler `net45` klasörü, 4.6 küçük veya buna eşit olan en yüksek kullanılabilir olduğu için.</span><span class="sxs-lookup"><span data-stu-id="17e2a-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="17e2a-127">Diğer taraftan, projeniz .NET Framework 4.6.1 hedefliyorsa, derlemede NuGet yükler `net461` klasör.</span><span class="sxs-lookup"><span data-stu-id="17e2a-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="17e2a-128">Projeniz .NET framework 4.0 ve önceki hedefliyorsa, NuGet uyumlu derleme paylaşımın için uygun bir hata iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="17e2a-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="17e2a-129">Framework sürümüne göre gruplandırma derlemeler</span><span class="sxs-lookup"><span data-stu-id="17e2a-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="17e2a-130">NuGet yalnızca tek kitaplığı klasöründe paket derlemeleri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="17e2a-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="17e2a-131">Örneğin, bir paketi aşağıdaki klasör yapısını olduğunu varsayın:</span><span class="sxs-lookup"><span data-stu-id="17e2a-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="17e2a-132">.NET Framework 4. 5'i hedefleyen bir projede paketi yüklendiğinde `MyAssembly.dll` (v2.0) yalnızca derlemesinin yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="17e2a-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="17e2a-133">`MyAssembly.Core.dll` (v1.0) içinde listelenmediğinden yüklü değil `net45` klasör.</span><span class="sxs-lookup"><span data-stu-id="17e2a-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="17e2a-134">NuGet, çünkü bu şekilde davranır `MyAssembly.Core.dll` sürümüne 2.0 birleştirilmiş sahip `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="17e2a-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="17e2a-135">İsterseniz `MyAssembly.Core.dll` için .NET Framework 4.5 yüklü olması için bir kopyasını koyun `net45` klasör.</span><span class="sxs-lookup"><span data-stu-id="17e2a-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="17e2a-136">Derlemeleri framework profile göre gruplandırma</span><span class="sxs-lookup"><span data-stu-id="17e2a-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="17e2a-137">NuGet, bir tire ve profil adı klasörü sonuna ekleyerek belirli framework profili hedefleme de destekler.</span><span class="sxs-lookup"><span data-stu-id="17e2a-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="17e2a-138">Desteklenen profiller aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="17e2a-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="17e2a-139">`client`: İstemci profili</span><span class="sxs-lookup"><span data-stu-id="17e2a-139">`client`: Client Profile</span></span>
- <span data-ttu-id="17e2a-140">`full`: Tam profili</span><span class="sxs-lookup"><span data-stu-id="17e2a-140">`full`: Full Profile</span></span>
- <span data-ttu-id="17e2a-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="17e2a-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="17e2a-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="17e2a-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="17e2a-143">Kullanmak için hangi NuGet hedef belirleme</span><span class="sxs-lookup"><span data-stu-id="17e2a-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="17e2a-144">Ne zaman hedefleyen taşınabilir sınıf kitaplığı paketleme kitaplıkları olabilir, klasör adlarında kullandığınız hangi NuGet hedef belirlemek hassas ve `.nuspec` , özellikle yalnızca bir alt kümesini PCL hedefleme dosyası.</span><span class="sxs-lookup"><span data-stu-id="17e2a-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="17e2a-145">Aşağıdaki dış kaynaklara bu yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="17e2a-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="17e2a-146">[.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="17e2a-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="17e2a-147">[Taşınabilir sınıf kitaplığı profilleri](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tablo PCL profilleri ve eşdeğer NuGet hedeflerine numaralandırma</span><span class="sxs-lookup"><span data-stu-id="17e2a-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="17e2a-148">[Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com'u): PCL belirlemek için komut satırı aracı sisteminizde profilleri</span><span class="sxs-lookup"><span data-stu-id="17e2a-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="17e2a-149">İçerik dosyaları ve PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="17e2a-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="17e2a-150">Değişebilir içerik dosyaları ve komut dosyası yürütme ile kullanılabilir `packages.config` yalnızca biçimini; diğer biçimlere kullanım dışıdır ve herhangi bir yeni paket kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="17e2a-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="17e2a-151">İle `packages.config`, içeriği içinde aynı klasörü kuralını kullanarak hedef framework tarafından dosyaları ve PowerShell komut dosyaları gruplandırılabilir `content` ve `tools` klasörler.</span><span class="sxs-lookup"><span data-stu-id="17e2a-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="17e2a-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="17e2a-152">For example:</span></span>

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

<span data-ttu-id="17e2a-153">Bir çerçeve klasörünün boş bırakılırsa, NuGet değil derleme başvurusu veya içerik dosyası ekleyin veya bu çerçevesi için PowerShell komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="17e2a-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="17e2a-154">Çünkü `init.ps1` yürütülür düzeyi ve proje bağımlı çözüm için bunu doğrudan altında yerleştirilmelidir `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="17e2a-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="17e2a-155">Bir çerçeve klasörünün yerleştirilmiş durumunda yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="17e2a-155">It's ignored if placed under a framework folder.</span></span>
