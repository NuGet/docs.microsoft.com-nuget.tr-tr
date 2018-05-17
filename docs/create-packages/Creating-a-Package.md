---
title: Bir NuGet paketi oluşturma
description: Tasarlama ve dosyaları ve sürüm oluşturma gibi temel karar noktaları da dahil olmak üzere bir NuGet paketi oluşturma işlemi için ayrıntılı bir kılavuz.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: df1673875441ea3274ba0826c4cef168b74583d1
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="9a5bc-103">NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a5bc-103">Creating NuGet packages</span></span>

<span data-ttu-id="9a5bc-104">Konular paketinizi yaptığı veya ne kod içerir, kullandığınız `nuget.exe` işlevselliğini paylaşılan ve kullanılan bir bileşen herhangi bir sayıda diğer geliştiriciler tarafından halinde paketlemek için.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="9a5bc-105">Yüklemek için `nuget.exe`, bkz: [NuGet CLI yükleme](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="9a5bc-106">Visual Studio otomatik olarak içermemesi Not `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="9a5bc-107">Teknik olarak konuşarak bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olan `.nupkg` uzantısı ve içerikleri belirli kuralları eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="9a5bc-108">Bu konu, bu kuralları karşılayan paket oluşturma ayrıntılı işlemi açıklanır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="9a5bc-109">Odaklanmış bir anlatım için başvurmak [hızlı başlangıç: oluşturma ve bir paket yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="9a5bc-110">Paketleme derlenmiş kod (derlemeler), simgeler ve/veya paket olarak teslim etmek istediğiniz diğer dosyaları şununla başlar (bkz [genel bakış ve iş akışı](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="9a5bc-111">Bu işlem, derleme veya derlenmiş derlemeler ve paketleri eşitlenmiş tutmak için bir proje dosyası'ndan çizebilirsiniz rağmen pakete Git dosyalar Aksi takdirde oluşturma bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="9a5bc-112">Bu konu, Visual Studio 2017 ve NuGet 4.0 + kullanarak .NET Core projeleri dışında proje türleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="9a5bc-113">.NET Core projelerdeki NuGet bilgileri proje dosyasında doğrudan kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="9a5bc-114">Ayrıntılar için bkz [oluşturma .NET standart paketlerle Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) ve [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="9a5bc-115">Paketlemek için hangi derlemelerin karar verme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="9a5bc-116">En genel amaçlı paketler diğer geliştiricilerin kendi projelerinde kullanabileceğiniz bir veya daha fazla derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="9a5bc-117">Genel olarak, her derleme bağımsız olarak yararlıdır koşuluyla NuGet paketi, her bir derleme sağlamak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="9a5bc-118">Örneğin, bir `Utilities.dll` , bağımlı `Parser.dll`, ve `Parser.dll` , kendi yararlıdır sonra her biri için bir paket oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="9a5bc-119">Böylece geliştiriciler verir `Parser.dll` bağımsız `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="9a5bc-120">Ardından, kitaplık bağımsız olarak yararlı olmayan birden çok derlemelerinin oluşuyorsa, bir pakete birleştirmek sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="9a5bc-121">Önceki örnekte, kullanarak `Parser.dll` yalnızca kullanılan kodu içeren `Utilities.dll`, tutmak uygundur sonra `Parser.dll` aynı pakette.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="9a5bc-122">Benzer şekilde, varsa `Utilities.dll` bağlıdır `Utilities.resources.dll`, burada yeniden ikinci her ikisinde de aynı paket put, kendi, kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="9a5bc-123">Kaynak aslında, özel bir durum yok.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="9a5bc-124">Bir paket bir projeye yüklendiğinde, NuGet paket DLL'leri derleme başvuruları otomatik olarak ekler. *hariç* adlandırıldığı o `.resources.dll` yerleştirilmiş yardımcı derlemeler (bkz: olarakkabulçünkü[ Yerelleştirilmiş paketleri oluşturma](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="9a5bc-125">Bu nedenle, kullanmaktan kaçının `.resources.dll` , aksi takdirde temel paket kodu içeren dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="9a5bc-126">Kitaplığınızı yönergeleri COM birlikte çalışma derlemeleri, ek izleme içeriyorsa [COM birlikte çalışma derlemeleri paketlerle yazma](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="9a5bc-127">Rol ve .nuspec dosyası yapısı</span><span class="sxs-lookup"><span data-stu-id="9a5bc-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="9a5bc-128">İstediğiniz paketlemek için hangi dosyaların öğrendikten sonra sonraki adım bir paket bildirimi oluşturma bir `.nuspec` XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="9a5bc-129">Bildirim:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-129">The manifest:</span></span>

1. <span data-ttu-id="9a5bc-130">Paketin içeriği açıklar ve kendisi paketine dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="9a5bc-131">Her iki paket oluşturmayı sürücüleri ve paket bir projeye yüklemeye nasıl NuGet bildirir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="9a5bc-132">Örneğin, ana paketi yüklendiğinde NuGet bu bağımlılıkları da yükleyebilirsiniz, bildirim diğer Paket bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="9a5bc-133">Aşağıda açıklandığı gibi gerekli ve isteğe bağlı özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="9a5bc-134">Burada, geçmeyen diğer özellikleri de dahil olmak üzere, tam Ayrıntılar için bkz: [.nuspec başvuru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="9a5bc-135">Gerekli özellikleri:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-135">Required properties:</span></span>

- <span data-ttu-id="9a5bc-136">Paket tanımlayıcısı paketini barındıran galeri arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="9a5bc-137">Belirli bir sürüm numarasını biçiminde *Major.Minor.Patch [-soneki]* nerede *-soneki* tanımlayan [yayın öncesi sürümleri](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9a5bc-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="9a5bc-138">Gerektiği gibi (gibi nuget.org) ana bilgisayardaki paket başlığı görüntülenir</span><span class="sxs-lookup"><span data-stu-id="9a5bc-138">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="9a5bc-139">Yazar ve sahibi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-139">Author and owner information.</span></span>
- <span data-ttu-id="9a5bc-140">Paket, uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-140">A long description of the package.</span></span>

<span data-ttu-id="9a5bc-141">Ortak isteğe bağlı özellikleri:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-141">Common optional properties:</span></span>

- <span data-ttu-id="9a5bc-142">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9a5bc-142">Release notes</span></span>
- <span data-ttu-id="9a5bc-143">Telif hakkı bilgileri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-143">Copyright information</span></span>
- <span data-ttu-id="9a5bc-144">Kısa bir açıklaması [Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="9a5bc-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="9a5bc-145">Yerel ayar kimliği</span><span class="sxs-lookup"><span data-stu-id="9a5bc-145">A locale ID</span></span>
- <span data-ttu-id="9a5bc-146">Giriş sayfası ve lisans URL'leri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-146">Home page and license URLs</span></span>
- <span data-ttu-id="9a5bc-147">Bir simge URL'si</span><span class="sxs-lookup"><span data-stu-id="9a5bc-147">An icon URL</span></span>
- <span data-ttu-id="9a5bc-148">Bağımlılıklar ve başvurular listesi</span><span class="sxs-lookup"><span data-stu-id="9a5bc-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="9a5bc-149">Galeri aramalarda yardımcı etiketleri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="9a5bc-150">Tipik bir (ancak kurgusal) aşağıdadır `.nuspec` özelliklerini açıklayan yorumlarla dosyası:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="9a5bc-151">Bağımlılıklar bildirme ve sürüm numaralarını belirtme hakkında daha fazla bilgi için bkz: [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="9a5bc-152">Ayrıca yüzey varlıklarına bağımlılıkları doğrudan paketindeki gelen kullanarak mümkündür `include` ve `exclude` üzerinde öznitelikleri `dependency` öğesi.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="9a5bc-153">Bkz: [.nuspec başvuru - bağımlılıkları](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="9a5bc-154">Bildirim oluşturulan paketinde yer aldığından herhangi bir sayıda ek örnekler mevcut paketleri inceleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="9a5bc-155">İyi bir kaynaktır *paketleri genel* klasör konumunu aşağıdaki komutu tarafından döndürülen bilgisayarınızda:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="9a5bc-156">Tüm gidin *package\version* klasörü, kopya `.nupkg` dosyasını bir `.zip` dosya sonra açmak `.zip` dosya ve inceleyin `.nuspec` içindeki.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="9a5bc-157">Oluştururken bir `.nuspec` bir Visual Studio projesinden paketi yapılandırıldığında projeden bilgilerle değiştirilir belirteçleri bildirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="9a5bc-158">Bkz: [.nuspec bir Visual Studio projesi oluşturma](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="9a5bc-159">.Nuspec dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a5bc-159">Creating the .nuspec file</span></span>

<span data-ttu-id="9a5bc-160">Tam bildirim genellikle oluşturma başlar ile temel bir `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan dosyası:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="9a5bc-161">Bir kurala dayalı çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="9a5bc-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="9a5bc-162">DLL derleme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="9a5bc-163">Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="9a5bc-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="9a5bc-164">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="9a5bc-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="9a5bc-165">Böylece son paketinde istediğiniz tam içeriğini açıklayan, sonra dosyayı el ile düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="9a5bc-166">Oluşturulan `.nuspec` dosyalarını paket ile oluşturmadan önce değiştirilmelidir yer tutucuları içeren `nuget pack` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="9a5bc-167">Komutu, başarısız `.nuspec` herhangi yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="9a5bc-168">Bir kurala dayalı çalışma dizininden</span><span class="sxs-lookup"><span data-stu-id="9a5bc-168">From a convention-based working directory</span></span>

<span data-ttu-id="9a5bc-169">Bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğundan `.nupkg` uzantısı, kendi genellikle en kolay dosya sisteminde istediğiniz klasör yapısını oluşturun ardından oluşturma `.nuspec` yapıyı doğrudan dosyasından.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="9a5bc-170">`nuget pack` Komut sonra otomatik olarak ekler tüm dosyaları bu klasör yapısındaki (ile başlayan tüm klasörleri hariç `.`, aynı yapısında özel dosyaları tutmak izin vererek).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="9a5bc-171">Bu yaklaşımın avantajı, hangi dosyaların paketin içinde (Bu konunun ilerleyen bölümlerinde açıklandığı gibi) dahil etmek istediğiniz bildiriminde belirtmeniz gerekmez ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="9a5bc-172">Pakete gider tam klasör yapısı oluşturmak, oluşturma işlemi yalnızca olabilir ve bir projenin parçası Aksi durumda olmayabilir diğer dosyaları kolayca ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="9a5bc-173">Hedef projeye eklenen içerik ve kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="9a5bc-174">PowerShell komut dosyaları (NuGet içinde desteklenmeyen 2.x yükleme betikleri de dahil edebilirsiniz NuGet kullanılan paketler 3.x ve üzeri).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="9a5bc-175">Projede mevcut yapılandırma ve kaynak kodu dosyaları için dönüştürmeleri.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="9a5bc-176">Klasör kuralları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="9a5bc-177">Klasör</span><span class="sxs-lookup"><span data-stu-id="9a5bc-177">Folder</span></span> | <span data-ttu-id="9a5bc-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a5bc-178">Description</span></span> | <span data-ttu-id="9a5bc-179">Paketi Yükle üzerine gerçekleştirilecek eylemi</span><span class="sxs-lookup"><span data-stu-id="9a5bc-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a5bc-180">(kök)</span><span class="sxs-lookup"><span data-stu-id="9a5bc-180">(root)</span></span> | <span data-ttu-id="9a5bc-181">Readme.txt konumu</span><span class="sxs-lookup"><span data-stu-id="9a5bc-181">Location for readme.txt</span></span> | <span data-ttu-id="9a5bc-182">Paketi yüklendiğinde, visual Studio Paketi kök dizininde readme.txt dosyasına görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="9a5bc-183">LIB / {tfm}</span><span class="sxs-lookup"><span data-stu-id="9a5bc-183">lib/{tfm}</span></span> | <span data-ttu-id="9a5bc-184">Derleme (`.dll`), belgeleri (`.xml`) ve simge (`.pdb`) dosyaları belirtilen hedef Framework bilinen ad (TFM) için</span><span class="sxs-lookup"><span data-stu-id="9a5bc-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="9a5bc-185">Derlemeleri başvuru olarak eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-185">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="9a5bc-186">Bkz: [birden çok hedef çerçeveyi destekleyen](supporting-multiple-target-frameworks.md) framework hedef özgü alt klasörleri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="9a5bc-187">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="9a5bc-187">runtimes</span></span> | <span data-ttu-id="9a5bc-188">Mimariye özel derleme (`.dll`), simge (`.pdb`) ve yerel kaynak (`.pri`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="9a5bc-188">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="9a5bc-189">Derlemeleri başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-189">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="9a5bc-190">Bkz: [birden çok hedef çerçeveyi destekleyen](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-190">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="9a5bc-191">içerik</span><span class="sxs-lookup"><span data-stu-id="9a5bc-191">content</span></span> | <span data-ttu-id="9a5bc-192">İsteğe bağlı dosyalar</span><span class="sxs-lookup"><span data-stu-id="9a5bc-192">Arbitrary files</span></span> | <span data-ttu-id="9a5bc-193">İçeriği proje kök dizinine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-193">Contents are copied to the project root.</span></span> <span data-ttu-id="9a5bc-194">Düşünün **içerik** sonuçta paket tüketir hedef uygulama kökü olarak klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-194">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="9a5bc-195">Paketi uygulamanın bir görüntüsünü Ekle olmasını */görüntüleri* klasörü, paketin içinde yerleştirin *içeriği/görüntüleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-195">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="9a5bc-196">derleme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-196">build</span></span> | <span data-ttu-id="9a5bc-197">MSBuild `.targets` ve `.props` dosyaları</span><span class="sxs-lookup"><span data-stu-id="9a5bc-197">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="9a5bc-198">Otomatik olarak proje dosyasına eklenen veya `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-198">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="9a5bc-199">araçlar</span><span class="sxs-lookup"><span data-stu-id="9a5bc-199">tools</span></span> | <span data-ttu-id="9a5bc-200">PowerShell komut dosyaları ve programları Paket Yöneticisi Konsolu'ndan erişilebilir</span><span class="sxs-lookup"><span data-stu-id="9a5bc-200">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="9a5bc-201">`tools` Klasörü eklenen `PATH` yalnızca Paket Yöneticisi konsolu için ortam değişkeni (özellikle *değil* için `PATH` projesi oluştururken MSBuild için belirlenen).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-201">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="9a5bc-202">Klasör yapısı herhangi bir sayıda hedef çerçeve için derlemeleri herhangi bir sayıda içerdiğinden bu yöntem, birden çok çerçeveyi destekleyen paket oluştururken gereklidir</span><span class="sxs-lookup"><span data-stu-id="9a5bc-202">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="9a5bc-203">İstenen klasör yapısı yerinde olduktan sonra oluşturmak için bu klasörde herhangi bir durumda, aşağıdaki komutu çalıştırın `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-203">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="9a5bc-204">Yeniden oluşturulan `.nuspec` dosyaları klasörü yapısı içinde hiçbir açık başvurular içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-204">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="9a5bc-205">Paketi oluştururken NuGet tüm dosyaları otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-205">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="9a5bc-206">Hala bildiriminin diğer bölümlerinde yer tutucu değerlerini ancak düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-206">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="9a5bc-207">Bir derlemeyi DLL</span><span class="sxs-lookup"><span data-stu-id="9a5bc-207">From an assembly DLL</span></span>

<span data-ttu-id="9a5bc-208">Bir derlemeye ait bir paket oluşturma en basit durumda, oluşturduğunuz bir `.nuspec` aşağıdaki komutu kullanarak derleme meta dosyası:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-208">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="9a5bc-209">Bu formu kullanarak derlemesinden belirli değerleri içeren birkaç yer tutucuları bildiriminde yerini alır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-209">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="9a5bc-210">Örneğin, `<id>` özelliği, derleme adı için ayarlanır ve `<version>` derleme sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-210">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="9a5bc-211">Diğer özellikler bildiriminde ancak yoksa eşleşen değerleri bütünleştirilmiş ve hala böylece yer tutucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-211">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="9a5bc-212">Bir Visual Studio Proje</span><span class="sxs-lookup"><span data-stu-id="9a5bc-212">From a Visual Studio project</span></span>

<span data-ttu-id="9a5bc-213">Oluşturma bir `.nuspec` gelen bir `.csproj` veya `.vbproj` bu projeye yüklü diğer paketleri otomatik olarak bağımlılıklar olarak başvurulduğundan dosya uygun.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-213">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="9a5bc-214">Yalnızca proje dosyası ile aynı klasörde aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-214">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="9a5bc-215">Elde edilen `<project-name>.nuspec` dosyasını içeren *belirteçleri* , yerini paketleme zaman önceden yüklenmiş olan diğer Paketlerine yönelik başvuruları dahil olmak üzere projeden değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-215">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="9a5bc-216">Bir belirteç virgülle ayrılan `$` proje özelliği her iki tarafında simgeler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-216">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="9a5bc-217">Örneğin, `<id>` bu şekilde genellikle oluşturulan bildiriminde değer şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-217">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="9a5bc-218">Bu belirteç ile değiştirilir `AssemblyName` zaman sevk adresindeki Proje dosyasından değeri.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-218">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="9a5bc-219">Proje değerlerin tam eşlemesi için `.nuspec` belirteçleri bkz [değiştirme belirteçleri başvuru](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-219">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="9a5bc-220">Belirteçleri hafifletmek, sürüm numarası gibi önemli değerleri güncelleştirmek gerek `.nuspec` proje güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-220">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="9a5bc-221">(Her zaman belirteçleri değişmez değerler ile isterseniz değiştirebileceğiniz).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-221">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="9a5bc-222">Kullanılabilir olduğundan emin birkaç ek paketleme seçenekleri bir Visual Studio projesinden çalışırken açıklandığı gibi Not [.nupkg dosyasını oluşturmak için nuget paketi çalıştıran](#running-nuget-pack-to-generate-the-nupkg-file) daha sonra.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-222">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="9a5bc-223">Çözüm düzeyi paketleri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-223">Solution-level packages</span></span>

<span data-ttu-id="9a5bc-224">*NuGet yalnızca 2.x. NuGet 3.0 + kullanılamaz.*</span><span class="sxs-lookup"><span data-stu-id="9a5bc-224">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="9a5bc-225">NuGet 2.x desteklenen araçları veya ek komutlar için Paket Yöneticisi konsolu yükleyen bir çözüm düzeyi paket kavramı (içeriğini `tools` klasör), başvurular, içerik, eklemeyin veya hiçbir projede özelleştirmeleri yapı ancak çözümü.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-225">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="9a5bc-226">Kendi doğrudan hiçbir dosyaları gibi paketlerin içeren `lib`, `content`, veya `build` klasörlerin ve bağımlılıklarını hiçbiri sahip kendi ilgili dosyalarında `lib`, `content`, veya `build` klasörler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-226">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="9a5bc-227">NuGet parçaları çözüm düzeyi paketlerinde yüklü bir `packages.config` dosyasını `.nuget` projenin yerine klasör `packages.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-227">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="9a5bc-228">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="9a5bc-228">New file with default values</span></span>

<span data-ttu-id="9a5bc-229">Aşağıdaki komut bir varsayılan bildirimi yer tutucularını, uygun dosya yapısıyla başlayın sağlayan oluşturur:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-229">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="9a5bc-230">Atlarsanız \<paket adı\>, sonuçta elde edilen dosya `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-230">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="9a5bc-231">Bir ad gibi sağlarsanız, `Contoso.Utility.UsefulStuff`, dosya `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-231">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="9a5bc-232">Elde edilen `.nuspec` değerleri ister için yer tutucuları içeren `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-232">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="9a5bc-233">En son oluşturmak amacıyla kullanmadan önce dosyayı düzenlemek mutlaka `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-233">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="9a5bc-234">Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9a5bc-234">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="9a5bc-235">Paket tanımlayıcısı (`<id>` öğesi) ve uygulamanın sürüm numarasını (`<version>` öğesi) benzersiz şekilde pakette yer alan tam kodu belirttikleri iki en önemli bildiriminde değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-235">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="9a5bc-236">**Paket tanımlayıcısı için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="9a5bc-236">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="9a5bc-237">**Benzersizlik**: tanımlayıcısı nuget.org veya ne olursa olsun galeri paketi barındıran arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-237">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="9a5bc-238">Üzerinde bir tanımlayıcı karar vermeden önce ad zaten kullanımda olup olmadığını denetlemek için uygulanabilir galeri arayın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-238">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="9a5bc-239">Çakışmaları önlemek için iyi bir desen şirket adınızı tanımlayıcı ilk parçası olarak gibi kullanmaktır `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-239">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="9a5bc-240">**Namespace benzeri adları**: .NET, kısa çizgi yerine noktalı gösterim kullanılarak ad alanları için benzer bir yol izler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-240">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="9a5bc-241">Örneğin, `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-241">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="9a5bc-242">Paket tanımlayıcısı kod içinde kullanılan ad alanları eşleştiğinde tüketicileri de yararlı.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-242">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="9a5bc-243">**Örnek paketler**: başka bir paket kullanmak için iliştirmek nasıl gösteren örnek kod paketi oluşturmak, `.Sample` giriş olarak tanımlayıcısına soneki olarak `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-243">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="9a5bc-244">(Örnek paketi Elbette başka bir paketi bir bağımlılık gerekir.) Bir örnek paket oluştururken, daha önce açıklanan kurala dayalı çalışma dizini yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-244">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="9a5bc-245">İçinde `content` klasör adında bir klasör örnek kodda düzenleme `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-245">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="9a5bc-246">**Paket sürümü için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="9a5bc-246">**Best practices for the package version:**</span></span>

- <span data-ttu-id="9a5bc-247">Genel olarak, bu kesinlikle gerekli olmasa da kitaplığı eşleşecek şekilde paketin sürümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-247">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="9a5bc-248">Bir paketi tek bir derleme sınırladığınızda atmaktan daha önce açıklandığı gibi budur [hangi derlemelerin pakete karar](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-248">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="9a5bc-249">Genel olarak, bağımlılıkları, derleme sürümlerini çözülürken kendisini NuGet paketi sürümleri ile ilgilenir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-249">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="9a5bc-250">Standart sürüm düzeni kullanırken açıklandığı şekilde NuGet sürüm kuralları dikkate aldığınızdan emin olun [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-250">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="9a5bc-251">Kısa blog gönderileri aşağıdaki bir dizi ayrıca sürüm anlaşılması yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-251">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="9a5bc-252">1. Kısım: Alma DLL cehennemi üzerinde</span><span class="sxs-lookup"><span data-stu-id="9a5bc-252">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="9a5bc-253">2. Kısım: Çekirdek algoritması</span><span class="sxs-lookup"><span data-stu-id="9a5bc-253">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="9a5bc-254">3. Kısım: bağlama yeniden yönlendirmeleri aracılığıyla Birleştirici</span><span class="sxs-lookup"><span data-stu-id="9a5bc-254">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="9a5bc-255">Ayar paket türü</span><span class="sxs-lookup"><span data-stu-id="9a5bc-255">Setting a package type</span></span>

<span data-ttu-id="9a5bc-256">NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-256">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="9a5bc-257">NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere bir türü ile işaretli olmayan paketler için varsayılan değer `Dependency` türü.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-257">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="9a5bc-258">`Dependency` türü paketleri kitaplıkları ve uygulamalar için derleme veya çalışma zamanı varlıklar ekleyin ve (uyumlu olduğu varsayılarak) herhangi bir proje türü yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-258">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="9a5bc-259">`DotnetCliTool` türü paketlerdir uzantıları [.NET CLI](/dotnet/articles/core/tools/index) ve komut satırından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-259">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="9a5bc-260">Gibi paketlerin, yalnızca .NET çekirdeği projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-260">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="9a5bc-261">Bu proje başına uzantıları hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-261">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="9a5bc-262">Özel tür paketleri paket kimlikleri ile aynı biçimi kurallara uyan bir rastgele türü tanımlayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-262">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="9a5bc-263">Herhangi türdeki dışında `Dependency` ve `DotnetCliTool`, ancak, Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-263">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="9a5bc-264">Paket türleri ayarlanır `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-264">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="9a5bc-265">Geriye dönük için en iyi uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine bu türü tür varsayılarak NuGet üzerinde yararlanmayı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-265">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="9a5bc-266">`.nuspec`: İçinde paket türünü gösteren bir `packageTypes\packageType` düğümü altında `<metadata>` öğe:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-266">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="9a5bc-267">Bir Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-267">Adding a readme and other files</span></span>

<span data-ttu-id="9a5bc-268">Doğrudan pakete eklenecek dosyaları belirtmek için kullanın `<files>` düğümünde `.nuspec` dosyası, hangi *izleyen* `<metadata>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-268">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="9a5bc-269">Çalışma dizini kurala dayalı yaklaşım kullanırken, readme.txt paket kök ve diğer içerik yerleştirebilirsiniz `content` klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-269">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="9a5bc-270">Hayır `<file>` öğeleridir bildiriminde gerekli.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-270">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="9a5bc-271">Adlı bir dosya eklediğinizde `readme.txt` paket kök, Visual Studio bu dosyanın içeriğini düz metin olarak hemen paketi doğrudan yüklendikten sonra görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-271">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="9a5bc-272">(Benioku dosyaları bağımlılıklar olarak yüklenen paketler için görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-272">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="9a5bc-273">Örneğin, işte nasıl HtmlAgilityPack paketi için Benioku görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-273">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için Benioku dosyasını görüntüleme](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="9a5bc-275">Boş bir eklerseniz `<files>` düğümünde `.nuspec` dosyası NuGet içermez herhangi bir içerik paketinde ne olduğunu dışında `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-275">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="9a5bc-276">MSBuild özellik ve hedefleri bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-276">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="9a5bc-277">Bazı durumlarda, özel araç veya işlem sırasında derleme çalıştırma gibi paketinizi tüketen projelerine özel derleme hedefler ya da özellikleri eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-277">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="9a5bc-278">Dosya biçiminde girerek bunu `<package_id>.targets` veya `<package_id>.props` (gibi `Contoso.Utility.UsefulStuff.targets`) içinde `\build` projenin klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-278">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="9a5bc-279">Kök dosyalarında `\build` tüm çerçeveler hedef için klasör uygun değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-279">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="9a5bc-280">Çerçeveye özel dosyaları sağlamak için önce aşağıdaki gibi uygun alt içinde bulunanlar koyun:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-280">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="9a5bc-281">Ardından `.nuspec` dosya, bu dosyaları başvurmak mutlaka `<files>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-281">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="9a5bc-282">MSBuild özellik ve hedefleri bir pakete dahil edildi [NuGet 2.5 ile sunulan](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), bu nedenle eklemeniz önerilir `minClientVersion="2.5"` özniteliğini `metadata` için gereken en düşük NuGet İstemcisi sürüm belirtmek için öğesi Paket kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-282">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="9a5bc-283">NuGet paketi ile yüklendiğinde `\build` dosyaları MSBuild ekler `<Import>` işaret proje dosyasındaki öğeleri `.targets` ve `.props` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-283">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="9a5bc-284">(`.props` proje dosyası; en üstte eklenir `.targets` altındaki eklenir.) Ayrı bir koşullu MSBuild `<Import>` öğesi, her hedef çerçeve için eklenir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-284">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="9a5bc-285">MSBuild `.props` ve `.targets` arası framework hedefleme yerleştirilebilir dosyalarının `\buildCrossTargeting` klasör.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-285">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="9a5bc-286">Karşılık gelen NuGet paketi yüklemesi sırasında ekler `<Import>` hedef Framework'ü ayarlanmamış koşuluyla, proje dosyası öğelerine (MSBuild özelliği `$(TargetFramework)` boş olması gerekir).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-286">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="9a5bc-287">NuGet ile 3.x hedefleri projeye eklenmez ancak bunun yerine kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-287">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="9a5bc-288">COM birlikte çalışma derlemeleri paketlerle yazma</span><span class="sxs-lookup"><span data-stu-id="9a5bc-288">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="9a5bc-289">COM birlikte çalışma derlemeleri içeren paketleri uygun bir içermelidir [hedefler dosyası](#including-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` meta veri PackageReference biçimini kullanarak projelerine eklenir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-289">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="9a5bc-290">Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, hedefler dosyası bu meta verileri açıkça ekler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-290">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="9a5bc-291">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adı ve katıştırılmış, değiştirerek olan derleme oluşan bir bileşim kullanmanız `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-291">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="9a5bc-292">(Ayrıca bkz. [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek için.)</span><span class="sxs-lookup"><span data-stu-id="9a5bc-292">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="9a5bc-293">Kullanırken dikkat edin `packages.config` yönetim biçimi'nın paketlerinden derlemeler başvuruları ekleme neden olan NuGet ve Visual Studio COM birlikte çalışma derlemeleri için denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasında true.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-293">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="9a5bc-294">Bu durumda hedefleri kılınmadı ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-294">In this case the targets are overriden.</span></span>

<span data-ttu-id="9a5bc-295">Ayrıca, varsayılan olarak [yapı varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-295">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="9a5bc-296">Projeyi project başvurusundan geçişli bağımlılık olarak çekildiğinde burada iş farklı bir şekilde açıklandığı gibi yazılan paketler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-296">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="9a5bc-297">Paket tüketici yapı içermeyecek şekilde PrivateAssets varsayılan değerini değiştirerek akmasına izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-297">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="9a5bc-298">.Nupkg dosyasını oluşturmak için nuget paketi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9a5bc-298">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="9a5bc-299">Bir derlemeyi ya da kurala dayalı çalışma dizini kullanarak, bir paket çalıştırarak oluşturduğunuzda `nuget pack` ile `.nuspec` dosya, değiştirme `<manifest-name>` , belirli dosya adı:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-299">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="9a5bc-300">Visual Studio projesi kullanırken çalıştırmak `nuget pack` , proje dosyası ile otomatik olarak yükleyen projenin `.nuspec` dosya ve proje dosyasında değerleri kullanarak içinde herhangi bir belirtece değiştirir:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-300">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="9a5bc-301">Proje dosyası kullanarak doğrudan proje simge değerlerini kaynağı olduğundan belirteci yapabilmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-301">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="9a5bc-302">Belirteç değiştirme olmayacak kullanırsanız `nuget pack` ile bir `.nuspec` dosyası.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-302">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="9a5bc-303">Tüm durumlarda `nuget pack` gibi bir noktayla başlayan klasörleri dışlar `.git` veya `.hg`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-303">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="9a5bc-304">NuGet gösteren herhangi bir hata olup olmadığını `.nuspec` bildiriminde yer tutucu değerlerini değiştirmek işlerle gibi düzeltilmesi gereken dosya.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-304">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="9a5bc-305">Bir kez `nuget pack` başarılı, sahip olduğunuz bir `.nupkg` açıklandığı gibi uygun bir Galeriye yayımlayabilirsiniz dosya [yayımlama bir paketi](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-305">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="9a5bc-306">İçinde açmak için oluşturma tamamlandıktan sonra bir paket incelemek için kullanışlı bir yol [paket Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-306">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="9a5bc-307">Bu paket içeriğini ve onun bildirimi grafik bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-307">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="9a5bc-308">Elde edilen adlandırabilirsiniz `.nupkg` dosyasını bir `.zip` dosya ve içeriğini doğrudan inceleyin.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-308">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="9a5bc-309">Ek Seçenekler</span><span class="sxs-lookup"><span data-stu-id="9a5bc-309">Additional options</span></span>

<span data-ttu-id="9a5bc-310">Çeşitli komut satırı anahtarları ile kullanabileceğiniz `nuget pack` dosyaları hariç tutmak, bildiriminde sürüm numarası geçersiz kılmak ve diğer özellikler arasında çıkış klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-310">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="9a5bc-311">Tam bir listesi için bkz [pack komut başvurusu](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-311">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="9a5bc-312">Aşağıdaki seçenekler, birkaç Visual Studio projeleri ile ortak şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-312">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="9a5bc-313">**Projeleri başvurulan**: Proje diğer projeler başvuruyorsa, başvurulan projeleri paketinin bir parçası olarak ya da bağımlılık, kullanarak ekleyebileceğiniz `-IncludeReferencedProjects` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-313">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="9a5bc-314">Bu ekleme işlemi yinelemelidir dolayısıyla `MyProject.csproj` başvuruları projeleri B ve C ve bu projeler başvuru D, E ve F, ardından B, C D E ve F dosyalarından pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-314">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="9a5bc-315">Başvuruda bulunulan bir proje içeriyorsa, bir `.nuspec` sonra kendi, NuGet dosyasının başvurulan proje bunun yerine bir bağımlılık olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-315">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="9a5bc-316">Paket ve proje ayrıca yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-316">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="9a5bc-317">**Derleme Yapılandırması**: varsayılan olarak, varsayılan derleme yapılandırması proje dosyasında genellikle ayarlanmış NuGet kullanır *hata ayıklama*.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-317">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="9a5bc-318">Farklı bir yapı yapılandırma dosyaları gibi paketlemek için *sürüm*, kullanın `-properties` yapılandırma seçeneğiyle:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-318">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="9a5bc-319">**Simgeler**: hata ayıklayıcı paket kodunuzda adım adım tüketicilerin izin simgeleri eklemek için kullanın `-Symbols` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-319">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="9a5bc-320">Test paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-320">Testing package installation</span></span>

<span data-ttu-id="9a5bc-321">Bir paket yayımlamadan önce genellikle bir paket bir projeye yükleme işlemi test etmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-321">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="9a5bc-322">Testleri olduğundan emin olun mutlaka tüm şunun kendi doğru yerde projedeki dosyaları.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-322">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="9a5bc-323">Visual Studio'da veya normal kullanarak komut satırında el ile yüklemeleri komutunu sınayabilirsiniz [yükleme adımlarını paketini](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-323">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="9a5bc-324">Otomatik test için temel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-324">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="9a5bc-325">Kopya `.nupkg` dosyasını bir yerel klasöre.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-325">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="9a5bc-326">Paket kaynaklarınızın kullanarak klasörü Ekle `nuget sources add -name <name> -source <path>` komutu (bkz [nuget kaynakları](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-326">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="9a5bc-327">Yalnızca bu yerel kaynağı kez verilen herhangi bir bilgisayarda ayarlamanız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-327">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="9a5bc-328">Bu kaynak kullanarak paketi yükleyin `nuget install <packageID> -source <name>` nerede `<name>` verilen kaynak adıyla eşleşen `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-328">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="9a5bc-329">Kaynağını belirterek, bu kaynak paketinin yüklü olduğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-329">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="9a5bc-330">Dosyaların doğru yüklü olduğunu denetlemek için dosya sistemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="9a5bc-330">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a5bc-331">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9a5bc-331">Next Steps</span></span>

<span data-ttu-id="9a5bc-332">Olan bir paketi oluşturduktan sonra bir `.nupkg` dosyası yayımlayarak, tercih ettiğiniz Galerisine açıklandığı gibi [yayımlama bir paketi](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9a5bc-332">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="9a5bc-333">Paketinizi yeteneklerini veya aksi halde aşağıdaki konularda açıklandığı gibi başka senaryoları destekleyecek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-333">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="9a5bc-334">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a5bc-334">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9a5bc-335">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-335">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9a5bc-336">Kaynak ve yapılandırma dosyaları dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-336">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="9a5bc-337">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="9a5bc-337">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9a5bc-338">Yayın öncesi sürümleri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-338">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="9a5bc-339">Son olarak, dikkat edilmesi gereken ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="9a5bc-339">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="9a5bc-340">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="9a5bc-340">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="9a5bc-341">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="9a5bc-341">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
