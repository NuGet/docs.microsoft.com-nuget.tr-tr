---
title: Bir NuGet paketi oluşturma
description: Ayrıntılı bir kılavuz tasarlama ve dosyaları ve sürüm oluşturma gibi temel karar noktaları da dahil olmak üzere bir NuGet paketi oluşturma işlemidir.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 37c2208f0942b12428dba9d664f25e7e4f3c0b72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547380"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="661f2-103">NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="661f2-103">Creating NuGet packages</span></span>

<span data-ttu-id="661f2-104">Paketiniz yapar veya hangi kod içeren olursa olsun, kullandığınız `nuget.exe` paylaşıldığı ve kullanılan bir bileşen herhangi bir sayıda diğer geliştiriciler tarafından bu işlevselliği paketlemek için.</span><span class="sxs-lookup"><span data-stu-id="661f2-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="661f2-105">Yüklenecek `nuget.exe`, bkz: [NuGet CLI yükleme](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="661f2-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="661f2-106">Visual Studio otomatik olarak içermez Not `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="661f2-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="661f2-107">Teknik terimlerle açıklamak gerekirse, bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğu `.nupkg` uzantısı ve içerikleri belirli kuralları eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="661f2-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="661f2-108">Bu konuda ayrıntılı bu kuralları karşılayan paket oluşturma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="661f2-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="661f2-109">Odaklanmış bir kılavuz için başvurmak [hızlı başlangıç: bir paketi oluşturma ve yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="661f2-110">Derlenmiş kodu (bütünleştirilmiş kodları), simge ve/veya bir paket olarak sunmak istediğiniz diğer dosyaları ile paketleme başlar (bkz [genel bakış ve iş akışı](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="661f2-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="661f2-111">Bu işlem, derleme veya derlenmiş bütünleştirilmiş kodların ve paketlerin eşitlenmiş şekilde tutmanızı sağlayacak bir proje dosyasında bilgilerden çizebilirsiniz ancak Aksi takdirde pakete Git dosyaları oluşturma bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="661f2-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="661f2-112">Bu konu, .NET Core projeleri Visual Studio 2017 ile NuGet 4.0 + dışında proje türleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="661f2-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="661f2-113">Bu .NET Core projelerinde, NuGet bilgileri proje dosyasında doğrudan kullanır.</span><span class="sxs-lookup"><span data-stu-id="661f2-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="661f2-114">Ayrıntılar için bkz [.NET standart paketleri oluşturma Visual Studio 2017 ile](../guides/create-net-standard-packages-vs2017.md) ve [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="661f2-115">Hangi derlemelerin paketini karar verme</span><span class="sxs-lookup"><span data-stu-id="661f2-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="661f2-116">En genel amaçlı paketleri diğer geliştiriciler kendi projelerinde kullanabileceğiniz bir veya daha fazla derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="661f2-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="661f2-117">Genel olarak, her derleme bağımsız olarak faydalı olması şartıyla, NuGet paket başına bir derleme en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="661f2-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="661f2-118">Örneğin, bir `Utilities.dll` , bağımlı `Parser.dll`, ve `Parser.dll` kendi yararlıdır ve ardından her biri için bir paket oluşturun.</span><span class="sxs-lookup"><span data-stu-id="661f2-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="661f2-119">Bunun yapılması geliştiricilerin kullanmasına olanak verir `Parser.dll` bağımsız `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="661f2-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="661f2-120">Ardından kitaplığınızı bağımsız olarak faydalı olmayan birden çok derlemelerinin oluşuyorsa, tek bir pakette birleştirip başlatılıyorsa sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="661f2-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="661f2-121">Önceki örnekte, kullanarak `Parser.dll` yalnızca kullanılan kodu içeren `Utilities.dll`, tutmak iyi ise `Parser.dll` aynı pakette.</span><span class="sxs-lookup"><span data-stu-id="661f2-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="661f2-122">Benzer şekilde, varsa `Utilities.dll` bağlıdır `Utilities.resources.dll`, burada yeniden ikinci hem de aynı paket yerleştirin, kendi, kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="661f2-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="661f2-123">Aslında bir özel durum kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="661f2-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="661f2-124">Bir projeye bir paketi yüklendiğinde, NuGet paket DLL'leri derleme başvurularını otomatik olarak ekler. *hariç* adlandırılmış olanlar `.resources.dll` yerelleştirilmiş yardımcı derlemeler (bkz: olarakkabuledilirçünkü[ Yerelleştirilmiş paketler oluşturma](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="661f2-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="661f2-125">Bu nedenle, kullanmaktan kaçının `.resources.dll` Aksi takdirde, gerekli paket kodu içeren dosyalar için.</span><span class="sxs-lookup"><span data-stu-id="661f2-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="661f2-126">COM birlikte çalışma derlemelerini, ek izleme kitaplığınızı yönergeleri içeriyorsa [COM birlikte çalışma derlemelerini paketlerle yazma](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="661f2-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="661f2-127">Rol ve .nuspec dosyası yapısı</span><span class="sxs-lookup"><span data-stu-id="661f2-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="661f2-128">Paket istediğiniz hangi dosyaların öğrendikten sonra sonraki adım bir paketi bildiriminde oluşturma bir `.nuspec` XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="661f2-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="661f2-129">Bildirim:</span><span class="sxs-lookup"><span data-stu-id="661f2-129">The manifest:</span></span>

1. <span data-ttu-id="661f2-130">Paket içeriğini açıklar ve kendisi paket içerisine dâhil.</span><span class="sxs-lookup"><span data-stu-id="661f2-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="661f2-131">Sürücü paketi oluşturmaya ve NuGet paketini projeye yükle konusunda bildirir.</span><span class="sxs-lookup"><span data-stu-id="661f2-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="661f2-132">Örneğin, ana paket yüklendiğinde bu bağımlılıkların NuGet de yükleyebilir, bildirim diğer Paket bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="661f2-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="661f2-133">Aşağıda açıklandığı gibi gerekli ve isteğe bağlı özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="661f2-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="661f2-134">Burada, geçmeyen diğer özellikler dahil olmak üzere tam Ayrıntılar için bkz. [.nuspec başvuru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="661f2-135">Gerekli özellikler:</span><span class="sxs-lookup"><span data-stu-id="661f2-135">Required properties:</span></span>

- <span data-ttu-id="661f2-136">Paket tanımlayıcısı paketini barındıran galeri arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="661f2-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="661f2-137">Belirli bir sürüm numarasını biçiminde *ana.İkincil.yama [-soneki]* burada *-soneki* tanımlayan [yayın öncesi sürümleri](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="661f2-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="661f2-138">Her paket başlık (gibi nuget.org) konak üzerindeki görünür</span><span class="sxs-lookup"><span data-stu-id="661f2-138">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="661f2-139">Yazar ve sahibi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="661f2-139">Author and owner information.</span></span>
- <span data-ttu-id="661f2-140">Paketinin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="661f2-140">A long description of the package.</span></span>

<span data-ttu-id="661f2-141">Ortak isteğe bağlı özellikler:</span><span class="sxs-lookup"><span data-stu-id="661f2-141">Common optional properties:</span></span>

- <span data-ttu-id="661f2-142">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="661f2-142">Release notes</span></span>
- <span data-ttu-id="661f2-143">Telif hakkı bilgileri</span><span class="sxs-lookup"><span data-stu-id="661f2-143">Copyright information</span></span>
- <span data-ttu-id="661f2-144">Kısa bir açıklaması için [Visual Studio'da Paket Yöneticisi UI](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="661f2-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="661f2-145">Bir yerel ayar kimliği</span><span class="sxs-lookup"><span data-stu-id="661f2-145">A locale ID</span></span>
- <span data-ttu-id="661f2-146">Giriş sayfası ve lisans URL'leri</span><span class="sxs-lookup"><span data-stu-id="661f2-146">Home page and license URLs</span></span>
- <span data-ttu-id="661f2-147">Simge URL'si</span><span class="sxs-lookup"><span data-stu-id="661f2-147">An icon URL</span></span>
- <span data-ttu-id="661f2-148">Bağımlılıklar ve başvuru listeleri</span><span class="sxs-lookup"><span data-stu-id="661f2-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="661f2-149">Galeri Arama Yardımcısı etiketleri</span><span class="sxs-lookup"><span data-stu-id="661f2-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="661f2-150">Verilmiştir (ancak kurgusal) tipik bir `.nuspec` dosyasıyla özelliklerini açıklayan bir yorum:</span><span class="sxs-lookup"><span data-stu-id="661f2-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="661f2-151">Bağımlılıkları bildirme ve sürüm numaraları belirtme hakkında daha fazla bilgi için bkz [Paket sürümü oluşturma](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="661f2-152">Ayrıca surface varlıklara doğrudan paketindeki bağımlılıklardan kullanarak mümkündür `include` ve `exclude` üzerinde öznitelikleri `dependency` öğesi.</span><span class="sxs-lookup"><span data-stu-id="661f2-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="661f2-153">Bkz: [.nuspec başvuru - bağımlılıkları](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="661f2-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="661f2-154">Bildirim oluşturulan paketteki dahil olduğundan, mevcut paketleri inceleyerek herhangi bir sayıda ek örnekler bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="661f2-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="661f2-155">İyi bir kaynaktır *genel paketleri* bilgisayarınızdaki konumunu aşağıdaki komutu tarafından döndürülen klasörü:</span><span class="sxs-lookup"><span data-stu-id="661f2-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="661f2-156">Tüm Git *package\version* klasörü, kopyalama `.nupkg` dosyasını bir `.zip` dosya ve ardından, `.zip` inceleyin ve dosya `.nuspec` içindeki.</span><span class="sxs-lookup"><span data-stu-id="661f2-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="661f2-157">Oluştururken bir `.nuspec` bir Visual Studio projesinden bildirim paketi oluşturulduğunda, projeden bilgileriyle değiştirilir belirteçleri içerir.</span><span class="sxs-lookup"><span data-stu-id="661f2-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="661f2-158">Bkz: [.nuspec bir Visual Studio projesi oluşturma](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="661f2-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="661f2-159">.Nuspec dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="661f2-159">Creating the .nuspec file</span></span>

<span data-ttu-id="661f2-160">Tam bir bildirim oluşturmak genellikle başlar ile temel bir `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan dosya:</span><span class="sxs-lookup"><span data-stu-id="661f2-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="661f2-161">Kural tabanlı bir çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="661f2-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="661f2-162">Bir derlemeyi DLL</span><span class="sxs-lookup"><span data-stu-id="661f2-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="661f2-163">Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="661f2-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="661f2-164">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="661f2-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="661f2-165">Böylece son pakette istediğiniz tam içeriği açıklar, ardından dosyayı el ile düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="661f2-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="661f2-166">Oluşturulan `.nuspec` dosyaları içeren paket ile oluşturmadan önce değiştirilmelidir yer tutucuları `nuget pack` komutu.</span><span class="sxs-lookup"><span data-stu-id="661f2-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="661f2-167">Komutu, başarısız `.nuspec` herhangi bir yer tutucu içerir.</span><span class="sxs-lookup"><span data-stu-id="661f2-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="661f2-168">Bir kural tabanlı çalışma dizinine</span><span class="sxs-lookup"><span data-stu-id="661f2-168">From a convention-based working directory</span></span>

<span data-ttu-id="661f2-169">Bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğundan `.nupkg` uzantısı, genellikle kolay yöntemi, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmak oluşturup `.nuspec` dosyasını doğrudan, yapı.</span><span class="sxs-lookup"><span data-stu-id="661f2-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="661f2-170">`nuget pack` Komut daha sonra otomatik olarak ekler tüm dosyaları bu klasör yapısındaki (ile başlayan tüm klasörler hariç `.`, aynı yapı içinde özel dosyaları tutmak izin verme).</span><span class="sxs-lookup"><span data-stu-id="661f2-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="661f2-171">Bu yaklaşımın avantajı (Bu konunun ilerleyen kısımlarında açıklandığı gibi) paket içerisine dâhil etmek istediğiniz dosyaları bildiriminde belirtmeniz gerekmez ' dir.</span><span class="sxs-lookup"><span data-stu-id="661f2-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="661f2-172">Yalnızca yapı işleminizi pakete giden tam bir klasör yapısını oluşturmak olabilir ve gelecekteki bir kolayca Aksi takdirde bir projenin parçası olmayabilir diğer dosyaları dahil edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="661f2-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="661f2-173">Hedef projeye eklenen içerik ve kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="661f2-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="661f2-174">PowerShell betikleri (NuGet içinde desteklenmeyen NuGet 2.x yükleme betikleri de dahil edebilirsiniz kullanılan paketler 3.x ve üzeri).</span><span class="sxs-lookup"><span data-stu-id="661f2-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="661f2-175">Bir projede var olan yapılandırma ve kaynak kodu dosyalarına dönüştürmeler.</span><span class="sxs-lookup"><span data-stu-id="661f2-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="661f2-176">Klasör kuralları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="661f2-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="661f2-177">Klasör</span><span class="sxs-lookup"><span data-stu-id="661f2-177">Folder</span></span> | <span data-ttu-id="661f2-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="661f2-178">Description</span></span> | <span data-ttu-id="661f2-179">Paket yükleme sonrasında eylem</span><span class="sxs-lookup"><span data-stu-id="661f2-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="661f2-180">(kök)</span><span class="sxs-lookup"><span data-stu-id="661f2-180">(root)</span></span> | <span data-ttu-id="661f2-181">Readme.txt konumu</span><span class="sxs-lookup"><span data-stu-id="661f2-181">Location for readme.txt</span></span> | <span data-ttu-id="661f2-182">Paket yüklenirken visual Studio Paket kök dizininde readme.txt dosyasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="661f2-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="661f2-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="661f2-183">lib/{tfm}</span></span> | <span data-ttu-id="661f2-184">Derleme (`.dll`), belgeleri (`.xml`) ve simgesi (`.pdb`) dosyaları belirtilen hedef çerçeve adı (TFM) için</span><span class="sxs-lookup"><span data-stu-id="661f2-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="661f2-185">Derlemelere başvurular eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="661f2-185">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="661f2-186">Bkz: [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md) framework hedef özgü alt klasörler oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="661f2-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="661f2-187">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="661f2-187">runtimes</span></span> | <span data-ttu-id="661f2-188">Mimariye özel derleme (`.dll`), sembol (`.pdb`) ve yerel kaynak (`.pri`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="661f2-188">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="661f2-189">Derlemelere başvurular eklenir; diğer dosyalar, proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="661f2-189">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="661f2-190">Bkz: [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-190">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="661f2-191">içerik</span><span class="sxs-lookup"><span data-stu-id="661f2-191">content</span></span> | <span data-ttu-id="661f2-192">Rastgele dosyalar</span><span class="sxs-lookup"><span data-stu-id="661f2-192">Arbitrary files</span></span> | <span data-ttu-id="661f2-193">İçeriği, proje kök dizinine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="661f2-193">Contents are copied to the project root.</span></span> <span data-ttu-id="661f2-194">Düşünün **içeriği** nihai olarak Paketle tüketen hedef uygulamanın kök klasör.</span><span class="sxs-lookup"><span data-stu-id="661f2-194">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="661f2-195">Uygulamanın resim ekleme paket için */görüntüleri* klasörü, paketin içinde yerleştirin *içeriği/görüntülerinden* klasör.</span><span class="sxs-lookup"><span data-stu-id="661f2-195">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="661f2-196">derleme</span><span class="sxs-lookup"><span data-stu-id="661f2-196">build</span></span> | <span data-ttu-id="661f2-197">MSBuild `.targets` ve `.props` dosyaları</span><span class="sxs-lookup"><span data-stu-id="661f2-197">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="661f2-198">Proje dosyasına otomatik olarak eklenen veya `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="661f2-198">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="661f2-199">araçlar</span><span class="sxs-lookup"><span data-stu-id="661f2-199">tools</span></span> | <span data-ttu-id="661f2-200">PowerShell betikleri ve programları Paket Yöneticisi konsolunda erişilebilir</span><span class="sxs-lookup"><span data-stu-id="661f2-200">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="661f2-201">`tools` Klasör eklenir `PATH` yalnızca Paket Yöneticisi konsolu için ortam değişkenini (özellikle *değil* için `PATH` projeyi derlerken MSBuild için belirlenen).</span><span class="sxs-lookup"><span data-stu-id="661f2-201">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="661f2-202">Herhangi bir sayıda hedef çerçeveleri için derlemeler herhangi bir sayıda klasör yapınız içerebileceğinden, bu yöntem, birden çok çerçeveyi destekleyen bir paket oluştururken gereklidir</span><span class="sxs-lookup"><span data-stu-id="661f2-202">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="661f2-203">Herhangi bir durumda, istenen klasör yapısı yerinde olduktan sonra bu klasörde oluşturmak için aşağıdaki komutu çalıştırın `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="661f2-203">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="661f2-204">Yeniden oluşturulan `.nuspec` klasörü yapısı içinde dosyaların açık başvuru içeriyor.</span><span class="sxs-lookup"><span data-stu-id="661f2-204">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="661f2-205">Paketi oluşturulduğunda NuGet tüm dosyaları otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="661f2-205">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="661f2-206">Ancak bildirimin diğer bölümlerinde yer tutucu değerlerini düzenlemek yine.</span><span class="sxs-lookup"><span data-stu-id="661f2-206">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="661f2-207">Bir derleme DLL</span><span class="sxs-lookup"><span data-stu-id="661f2-207">From an assembly DLL</span></span>

<span data-ttu-id="661f2-208">Basit durumda da, bir derlemeden bir paket oluşturma oluşturabileceğiniz bir `.nuspec` aşağıdaki komutu kullanarak derleme içindeki meta veri dosyası:</span><span class="sxs-lookup"><span data-stu-id="661f2-208">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="661f2-209">Bu formu kullanarak bazı yer tutucuları bildiriminde derlemesinden belirli değerlerle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="661f2-209">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="661f2-210">Örneğin, `<id>` özelliği, derleme adı için ayarlanır ve `<version>` derleme sürüme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="661f2-210">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="661f2-211">Diğer özellikleri bildiriminde ancak yoksa eşleşen değerler derlemedeki olmalı ve yine de bu nedenle yer tutucular içermelidir.</span><span class="sxs-lookup"><span data-stu-id="661f2-211">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="661f2-212">Visual Studio projesinden</span><span class="sxs-lookup"><span data-stu-id="661f2-212">From a Visual Studio project</span></span>

<span data-ttu-id="661f2-213">Oluşturma bir `.nuspec` gelen bir `.csproj` veya `.vbproj` dosya, bu projeye yüklü diğer paketleri otomatik bağımlılıkları başvurulduğu için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="661f2-213">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="661f2-214">Sadece proje dosyası ile aynı klasörde aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="661f2-214">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="661f2-215">Ortaya çıkan `<project-name>.nuspec` dosyasını içeren *belirteçleri* , yerini paketleme zamanında projesinden zaten yüklenmiş olan diğer tüm paketler için başvuruları dahil olmak üzere değerlerle.</span><span class="sxs-lookup"><span data-stu-id="661f2-215">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="661f2-216">Bir belirteç tarafından ayrılmış `$` simgeler iki tarafındaki proje özelliği.</span><span class="sxs-lookup"><span data-stu-id="661f2-216">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="661f2-217">Örneğin, `<id>` bu şekilde genellikle oluşturulan bildirim değeri şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="661f2-217">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="661f2-218">Bu belirteç ile değiştirilir `AssemblyName` zaman paketleme sırasında proje dosyasından değer.</span><span class="sxs-lookup"><span data-stu-id="661f2-218">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="661f2-219">Proje değerlerinin tam eşlemesi için `.nuspec` belirteçlerini bkz [değiştirme belirteçleri başvuru](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="661f2-219">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="661f2-220">Belirteçleri hafifletmek, sürüm numarası gibi önemli değerleri güncelleştirmek gerek `.nuspec` projeyi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="661f2-220">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="661f2-221">(Her zaman belirteçleri değişmez değer değerlerle isterseniz değiştirebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="661f2-221">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="661f2-222">Kullanılabilir olduğundan emin birkaç ek paketleme seçenekleri bir Visual Studio projesinde çalışırken açıklandığı Not [.nupkg dosyası oluşturmak için nuget paketi](#running-nuget-pack-to-generate-the-nupkg-file) daha sonra.</span><span class="sxs-lookup"><span data-stu-id="661f2-222">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="661f2-223">Çözüm düzeyinde paketleri</span><span class="sxs-lookup"><span data-stu-id="661f2-223">Solution-level packages</span></span>

<span data-ttu-id="661f2-224">*NuGet 2.x yalnızca. NuGet 3.0 + kullanılamaz.*</span><span class="sxs-lookup"><span data-stu-id="661f2-224">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="661f2-225">NuGet 2.x desteklenen araçlar veya ek komutlar için Paket Yöneticisi konsolu yükleyen bir çözüm düzeyinde paket kavramı (içeriğini `tools` klasör), başvurular, içerik, eklenemiyor veya yapı özelleştirmeleri için herhangi bir projeyi ancak Çözüm.</span><span class="sxs-lookup"><span data-stu-id="661f2-225">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="661f2-226">Yok, doğrudan dosyalarında gibi paketlerin içeren `lib`, `content`, veya `build` klasörleri ve bağımlılıklarını hiçbiri sahip kendi ilgili dosyalarında `lib`, `content`, veya `build` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="661f2-226">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="661f2-227">NuGet parçaları çözüm düzeyinde paketleri yüklü bir `packages.config` dosyası `.nuget` projenin yerine klasör `packages.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="661f2-227">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="661f2-228">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="661f2-228">New file with default values</span></span>

<span data-ttu-id="661f2-229">Aşağıdaki komut varsayılan bildirimi yer tutucularını, uygun dosya yapısı ile Başlat sağlayan oluşturur:</span><span class="sxs-lookup"><span data-stu-id="661f2-229">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="661f2-230">Atlarsanız \<paket adı\>, sonuçta elde edilen dosya `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="661f2-230">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="661f2-231">Gibi bir ad verin, `Contoso.Utility.UsefulStuff`, dosya `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="661f2-231">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="661f2-232">Ortaya çıkan `.nuspec` ister değerler için yer tutucular içerir `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="661f2-232">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="661f2-233">En son oluşturmak amacıyla kullanmadan önce dosyayı düzenlemek mutlaka `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="661f2-233">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="661f2-234">Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="661f2-234">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="661f2-235">Paket tanımlayıcısı (`<id>` öğesi) ve sürüm numarasını (`<version>` öğesi) pakette yer alan tam kodu, benzersiz şekilde tanımlamak için iki en önemli bildirim değerler.</span><span class="sxs-lookup"><span data-stu-id="661f2-235">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="661f2-236">**Paket tanımlayıcısı için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="661f2-236">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="661f2-237">**Benzersizlik**: tanımlayıcı nuget.org veya hangi galeri paketi barındıran arasında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="661f2-237">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="661f2-238">Bir tanımlayıcının karar vermeden önce uygun galeri adı zaten kullanımda olup olmadığını denetlemek için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="661f2-238">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="661f2-239">Çakışmaları önlemek için iyi bir desen şirket adınızı tanımlayıcısı ilk parçası olarak gibi kullanmaktır `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="661f2-239">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="661f2-240">**Namespace benzeri adları**: .NET, kısa çizgi yerine nokta gösterimi kullanılarak ad alanları için benzer bir desen izleyin.</span><span class="sxs-lookup"><span data-stu-id="661f2-240">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="661f2-241">Örneğin, `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="661f2-241">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="661f2-242">Paket tanımlayıcısı kod içinde kullanılan ad alanları eşleştiğinde tüketiciler de yararlı.</span><span class="sxs-lookup"><span data-stu-id="661f2-242">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="661f2-243">**Örnek paketleri**: bir paket nasıl başka bir paket ekleme kullanılacağını gösteren örnek kod üretir, `.Sample` soneki olarak da tanımlayıcı olarak `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="661f2-243">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="661f2-244">(Örnek paketinin Elbette diğer paketi bir bağımlılık yoktur.) Örnek paketi oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="661f2-244">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="661f2-245">İçinde `content` klasör adında bir klasör örnek kodda düzenleme `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="661f2-245">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="661f2-246">**Paket sürümü için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="661f2-246">**Best practices for the package version:**</span></span>

- <span data-ttu-id="661f2-247">Genel olarak, bu kesinlikle gerekli olmasa da kitaplığı eşleşecek şekilde paketin sürümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="661f2-247">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="661f2-248">Bir paketi tek bir derleme sınırladığınızda ibarettir daha önce açıklandığı gibi budur [pakete hangi derlemelerin karar](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="661f2-248">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="661f2-249">Genel olarak, kendi NuGet Paket sürümü ile derleme sürümlerini bağımlılıkları çözümlenirken anlaştığından emin unutmayın.</span><span class="sxs-lookup"><span data-stu-id="661f2-249">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="661f2-250">Standart sürüm şeması kullanırken, NuGet sürüm oluşturma kuralları açıklandığı şekilde dikkate aldığınızdan emin olun [Paket sürümü oluşturma](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-250">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="661f2-251">Aşağıdaki bir dizi kısa blog gönderileri da sürüm anlamak yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="661f2-251">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="661f2-252">1. Bölüm: Alma DLL cehennemi üzerinde</span><span class="sxs-lookup"><span data-stu-id="661f2-252">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="661f2-253">2. Bölüm: Çekirdek algoritması</span><span class="sxs-lookup"><span data-stu-id="661f2-253">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="661f2-254">3. Bölüm: bağlama yönlendirmeleri aracılığıyla birleştirme</span><span class="sxs-lookup"><span data-stu-id="661f2-254">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="661f2-255">Ayar paket türü</span><span class="sxs-lookup"><span data-stu-id="661f2-255">Setting a package type</span></span>

<span data-ttu-id="661f2-256">NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="661f2-256">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="661f2-257">NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere, bir tür ile işaretlenmemiş paketleri varsayılan `Dependency` türü.</span><span class="sxs-lookup"><span data-stu-id="661f2-257">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="661f2-258">`Dependency` türü paketler, kitaplıkları ve uygulamaları için derleme veya çalışma zamanı varlıklar eklemek ve (uyumlu olduklarından varsayılarak) herhangi bir proje türü yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="661f2-258">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="661f2-259">`DotnetCliTool` tür paketlerin uzantıları [.NET CLI](/dotnet/articles/core/tools/index) ve komut satırından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="661f2-259">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="661f2-260">Bu paketler, yalnızca .NET Core projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="661f2-260">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="661f2-261">Bu proje başına uzantılar hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="661f2-261">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="661f2-262">Özel tür paketleri paket kimliği olarak aynı biçimi kurallara uyan bir rastgele tür tanımlayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="661f2-262">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="661f2-263">Dışında herhangi türdeki `Dependency` ve `DotnetCliTool`, ancak Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="661f2-263">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="661f2-264">Paket türlerinin ayarlanır `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="661f2-264">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="661f2-265">Geriye dönük için en iyi uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine NuGet varsayılarak türü yok, bu tür üzerinde yararlanmayı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="661f2-265">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="661f2-266">`.nuspec`: Paket türü içinde göstermek bir `packageTypes\packageType` düğümünde `<metadata>` öğesi:</span><span class="sxs-lookup"><span data-stu-id="661f2-266">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="661f2-267">Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="661f2-267">Adding a readme and other files</span></span>

<span data-ttu-id="661f2-268">Pakete dahil edilecek dosyalar doğrudan belirtmek için kullanın `<files>` düğümünde `.nuspec` dosyası, hangi *izleyen* `<metadata>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="661f2-268">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="661f2-269">Çalışma dizini kural tabanlı yaklaşım kullanırken, readme.txt paket kök ve diğer içeriği yerleştirebilirsiniz `content` klasör.</span><span class="sxs-lookup"><span data-stu-id="661f2-269">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="661f2-270">Hayır `<file>` bildiriminde öğeler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="661f2-270">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="661f2-271">Adlı bir dosya dahil ettiğinizde `readme.txt` paket kök dizininde, Visual Studio, dosyanın içeriğini düz metin olarak hemen paket doğrudan yüklendikten sonra görüntüler.</span><span class="sxs-lookup"><span data-stu-id="661f2-271">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="661f2-272">(Benioku dosyaları bağımlılıkların yüklü paketler için görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="661f2-272">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="661f2-273">Örneğin, işte HtmlAgilityPack paketinin Benioku dosyasını nasıl görünür:</span><span class="sxs-lookup"><span data-stu-id="661f2-273">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için bir benioku dosyası görüntüsü](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="661f2-275">Boş bir eklerseniz `<files>` düğümünde `.nuspec` dosya, NuGet içermez herhangi bir içerik paketinde ne olduğunu dışında `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="661f2-275">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="661f2-276">MSBuild özellikler ve hedefler bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="661f2-276">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="661f2-277">Bazı durumlarda, derleme sırasında bir özel araç veya işlemin çalıştırma gibi paketinizi kullanan projelerdeki özel yapı hedefleri veya özellikleri eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="661f2-277">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="661f2-278">Dosya biçiminde yerleştirerek bunu `<package_id>.targets` veya `<package_id>.props` (gibi `Contoso.Utility.UsefulStuff.targets`) içinde `\build` proje klasörü.</span><span class="sxs-lookup"><span data-stu-id="661f2-278">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="661f2-279">Kök dosyaları `\build` için tüm çerçeveleri hedef klasörü uygun değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="661f2-279">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="661f2-280">Çerçeveye özgü dosyaları sağlamak için önce aşağıdaki gibi uygun bir alt kategorilerindekiler yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="661f2-280">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="661f2-281">Ardından `.nuspec` dosya, bu dosyalara başvurmak mutlaka `<files>` düğüm:</span><span class="sxs-lookup"><span data-stu-id="661f2-281">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="661f2-282">Bir paket içinde MSBuild özellikler ve hedefler dahil edildi [NuGet 2.5 ile sunulan](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), bu nedenle eklemeniz önerilir `minClientVersion="2.5"` özniteliğini `metadata` öğesi için gereken en düşük NuGet istemci sürümü belirtmek için paketi kullanır.</span><span class="sxs-lookup"><span data-stu-id="661f2-282">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="661f2-283">NuGet paketi ile yüklendiğinde `\build` dosyaları, MSBuild ekler `<Import>` işaret proje dosyasındaki öğeleri `.targets` ve `.props` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="661f2-283">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="661f2-284">(`.props` ; proje dosyasının en üstüne eklenir `.targets` altına eklenir.) Ayrı bir koşullu MSBuild `<Import>` öğesi, her hedef çerçeve için eklenir.</span><span class="sxs-lookup"><span data-stu-id="661f2-284">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="661f2-285">MSBuild `.props` ve `.targets` arası framework'ü hedefleyen yerleştirilebilir için dosyaları `\buildCrossTargeting` klasör.</span><span class="sxs-lookup"><span data-stu-id="661f2-285">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="661f2-286">Buna karşılık gelen NuGet paketi yüklemesi sırasında ekler `<Import>` öğeleri hedef Framework'ü ayarlı değil koşuluyla, proje dosyasına (MSBuild özelliğini `$(TargetFramework)` boş olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="661f2-286">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="661f2-287">İle NuGet 3.x hedefleri projeye eklenmez ancak bunun yerine kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="661f2-287">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="661f2-288">COM birlikte çalışma derlemelerini paketlerle yazma</span><span class="sxs-lookup"><span data-stu-id="661f2-288">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="661f2-289">COM birlikte çalışma derlemelerini içeren paketleri uygun bir içermelidir [hedefler dosyası](#including-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` PackageReference biçimini kullanan projeler için meta veriler eklenir.</span><span class="sxs-lookup"><span data-stu-id="661f2-289">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="661f2-290">Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, bu meta veriler, açıkça hedefler dosyası ekler.</span><span class="sxs-lookup"><span data-stu-id="661f2-290">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="661f2-291">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adınızla ve katıştırılmış, değiştirilmesini olan derleme birleşimini kullanın `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="661f2-291">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="661f2-292">(Ayrıca bkz: [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek.)</span><span class="sxs-lookup"><span data-stu-id="661f2-292">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="661f2-293">Kullanırken dikkat `packages.config` yönetim biçimi paketlerinden derlemelerine başvurular ekleme oluyor NuGet ve Visual Studio için COM birlikte çalışma derlemeleri denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasındaki true.</span><span class="sxs-lookup"><span data-stu-id="661f2-293">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="661f2-294">Bu durumda geçersiz kılınmış hedeflerdir.</span><span class="sxs-lookup"><span data-stu-id="661f2-294">In this case the targets are overriden.</span></span>

<span data-ttu-id="661f2-295">Ayrıca, varsayılan olarak [derleme varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="661f2-295">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="661f2-296">Geçişli bağımlılık gelen bir projeden projeye başvuru olarak çekildiğinde burada iş farklı bir şekilde açıklandığı yazılan paketler.</span><span class="sxs-lookup"><span data-stu-id="661f2-296">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="661f2-297">Paket kullanıcısı PrivateAssets varsayılan değer, derleme içermeyecek şekilde değiştirerek akmasına izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="661f2-297">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="661f2-298">Nuget paketi .nupkg dosyası oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="661f2-298">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="661f2-299">Bir derleme veya kural tabanlı çalışma dizinini kullanarak, bir paket çalıştırarak oluşturun `nuget pack` ile `.nuspec` değiştirerek, dosya `<project-name>` , belirli bir dosya adına sahip:</span><span class="sxs-lookup"><span data-stu-id="661f2-299">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="661f2-300">Visual Studio projesi kullanırken çalıştırmak `nuget pack` proje dosyanız ile otomatik olarak yükleyen projenin `.nuspec` dosya ve proje dosyasında değerleri kullanarak içindeki herhangi bir belirteç değiştirir:</span><span class="sxs-lookup"><span data-stu-id="661f2-300">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="661f2-301">Proje dosyasını kullanarak doğrudan proje kaynak belirteci değerler olduğundan belirteç değiştirme için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="661f2-301">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="661f2-302">Belirteç değiştirme kullanırsanız testler bulunmuyor `nuget pack` ile bir `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="661f2-302">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="661f2-303">Tüm durumlarda `nuget pack` gibi bir noktayla başlayan klasörleri dışlar `.git` veya `.hg`.</span><span class="sxs-lookup"><span data-stu-id="661f2-303">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="661f2-304">NuGet, herhangi bir hata olup olmadığını gösteren `.nuspec` bildiriminde yer tutucu değerlerini değiştirmek unutarak gibi düzeltilmesi gereken bir dosya.</span><span class="sxs-lookup"><span data-stu-id="661f2-304">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="661f2-305">Bir kez `nuget pack` başarılı, sahip olduğunuz bir `.nupkg` açıklandığı gibi uygun bir Galeriye yayımlayabilirsiniz dosya [bir paket yayımlama](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-305">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="661f2-306">Bir paket oluşturma açılır olduktan sonra incelemek için kullanışlı bir yol [paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="661f2-306">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="661f2-307">Bu, paket içeriğini ve bildirimi grafik bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="661f2-307">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="661f2-308">Ayrıca sonuç yeniden adlandırabilirsiniz `.nupkg` dosyasını bir `.zip` dosya ve doğrudan içeriğini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="661f2-308">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="661f2-309">Ek Seçenekler</span><span class="sxs-lookup"><span data-stu-id="661f2-309">Additional options</span></span>

<span data-ttu-id="661f2-310">Çeşitli komut satırı anahtarları ile kullanabileceğiniz `nuget pack` dosyaları hariç tutmak, sürüm numarasını bildiriminde geçersiz kılma ve yanı sıra başka özellikler çıkış klasörüne değiştirin.</span><span class="sxs-lookup"><span data-stu-id="661f2-310">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="661f2-311">Tam bir listesi için başvurmak [paketi komut başvurusu](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-311">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="661f2-312">Visual Studio projeleriyle ortak olan birkaç aşağıdaki seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="661f2-312">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="661f2-313">**Başvurulan projeler**: projenin diğer projelerden başvuruda bulunuyorsa, başvurulan projeler paketinin bir parçası olarak veya bağımlılıkları ekleyebilirsiniz `-IncludeReferencedProjects` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="661f2-313">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="661f2-314">Bu ekleme işlemi özyinelemelidir dolayısıyla `MyProject.csproj` başvuruları projeleri B ve C ve bu projelerde başvuru D, E ve F, ardından B, C, D, E ve F dosyalarından pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="661f2-314">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="661f2-315">Başvurulan proje içeriyorsa, bir `.nuspec` dosya, kendi sonra nuget başvurulan proje bunun yerine bir bağımlılık olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="661f2-315">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="661f2-316">Paket ve bu projeyi ayrı ayrı yayımlama gerekir.</span><span class="sxs-lookup"><span data-stu-id="661f2-316">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="661f2-317">**Derleme Yapılandırması**: varsayılan olarak, NuGet genellikle proje dosyasında ayarlanmış varsayılan derleme yapılandırmasını kullanır. *hata ayıklama*.</span><span class="sxs-lookup"><span data-stu-id="661f2-317">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="661f2-318">Farklı bir derleme yapılandırma dosyaları gibi paketlenecek *yayın*, kullanın `-properties` yapılandırma seçeneğiyle:</span><span class="sxs-lookup"><span data-stu-id="661f2-318">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="661f2-319">**Semboller**: hata ayıklayıcı paket kodunuzda adım adım tüketicilerin izin simgeleri eklemek için kullanın `-Symbols` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="661f2-319">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="661f2-320">Test paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="661f2-320">Testing package installation</span></span>

<span data-ttu-id="661f2-321">Bir paket yayımlamadan önce genellikle bir projeye bir paket yükleme işlemini test etmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="661f2-321">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="661f2-322">Testleri emin mutlaka tüm düştüğünden kendi doğru yerde proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="661f2-322">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="661f2-323">Yüklemelerini el ile normal kullanarak komut satırında veya Visual Studio'da test edebilirsiniz [paketini yükleme adımlarını](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-323">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="661f2-324">Otomatik test için temel işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="661f2-324">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="661f2-325">Kopyalama `.nupkg` dosyasını bir yerel klasöre.</span><span class="sxs-lookup"><span data-stu-id="661f2-325">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="661f2-326">Paket kaynaklarınızı kullanarak klasör eklemek `nuget sources add -name <name> -source <path>` komut (bkz [nuget kaynakları](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="661f2-326">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="661f2-327">Yalnızca gereksinim duyduğunuz Not Bu yerel kaynak herhangi belirli bir bilgisayarda bir kez ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="661f2-327">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="661f2-328">Bu kaynağı kullanarak paketi yükleyin `nuget install <packageID> -source <name>` burada `<name>` için belirtilen kaynak adıyla eşleşen `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="661f2-328">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="661f2-329">Kaynağını belirterek, bu kaynak paketin yüklendiğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="661f2-329">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="661f2-330">Dosyaları düzgün yüklendiğini kontrol etmek için dosya sisteminize inceleyin.</span><span class="sxs-lookup"><span data-stu-id="661f2-330">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="661f2-331">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="661f2-331">Next Steps</span></span>

<span data-ttu-id="661f2-332">Olan bir paketi oluşturduktan sonra bir `.nupkg` dosyasını yayımlayabilirsiniz, tercih ettiğiniz Galerisine üzerinde açıklandığı [bir paket yayımlama](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="661f2-332">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="661f2-333">Paketiniz yeteneklerini genişletmek veya aksi halde aşağıdaki konularda açıklandığı gibi başka senaryoları destekleyecek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="661f2-333">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="661f2-334">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="661f2-334">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="661f2-335">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="661f2-335">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="661f2-336">Kaynak ve yapılandırma dosyalarını dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="661f2-336">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="661f2-337">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="661f2-337">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="661f2-338">Yayın öncesi sürümleri</span><span class="sxs-lookup"><span data-stu-id="661f2-338">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="661f2-339">Son olarak, dikkat edilmesi gereken ek paket türü vardır:</span><span class="sxs-lookup"><span data-stu-id="661f2-339">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="661f2-340">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="661f2-340">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="661f2-341">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="661f2-341">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
