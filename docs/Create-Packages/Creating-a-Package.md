---
title: "Bir NuGet paketi oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "Tasarlama ve dosyaları ve sürüm oluşturma gibi temel karar noktaları da dahil olmak üzere bir NuGet paketi oluşturma işlemi için ayrıntılı bir kılavuz."
keywords: "NuGet paket oluşturma, bir paket, nuspec bildirimi, NuGet paketi kuralları, NuGet Paket sürümü oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e7a2c4d02afb2387161c22fe5bd443eb0991ea8c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="4c94b-104">NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c94b-104">Creating NuGet packages</span></span>

<span data-ttu-id="4c94b-105">Konular paketinizi yaptığı veya ne kod içerir, kullandığınız `nuget.exe` işlevselliğini paylaşılan ve kullanılan bir bileşen herhangi bir sayıda diğer geliştiriciler tarafından halinde paketlemek için.</span><span class="sxs-lookup"><span data-stu-id="4c94b-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="4c94b-106">Yüklemek için `nuget.exe`, bkz: [NuGet CLI yükleme](../guides/Install-NuGet.md#nuget-cli).</span><span class="sxs-lookup"><span data-stu-id="4c94b-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="4c94b-107">Visual Studio otomatik olarak içermemesi Not `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="4c94b-108">Teknik olarak konuşarak bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olan `.nupkg` uzantısı ve içerikleri belirli kuralları eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="4c94b-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="4c94b-109">Bu konu, bu kuralları karşılayan paket oluşturma ayrıntılı işlemi açıklanır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="4c94b-110">Odaklanmış bir anlatım için başvurmak [oluşturma ve bir paket hızlı başlangıç yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="4c94b-111">Paketleme derlenmiş kod (derlemeler), simgeler ve/veya paket olarak teslim etmek istediğiniz diğer dosyaları şununla başlar (bkz [genel bakış ve iş akışı](Overview-and-Workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="4c94b-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="4c94b-112">Bu işlem derleme veya aksi halde pakete Git dosyalar oluşturma bağımsız, derlenmiş assemblines ve paketleri eşitlenmiş tutmak için bir proje dosyası'ndan kullanabilirsiniz ancak çizin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="4c94b-113">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="4c94b-113">In this topic:</span></span>

- [<span data-ttu-id="4c94b-114">Paketlemek için hangi derlemelerin karar verme</span><span class="sxs-lookup"><span data-stu-id="4c94b-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="4c94b-115">Rol ve yapısını `.nuspec` dosyası</span><span class="sxs-lookup"><span data-stu-id="4c94b-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="4c94b-116">[Oluşturma `.nuspec` dosya](#creating-the-nuspec-file) gelen:</span><span class="sxs-lookup"><span data-stu-id="4c94b-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="4c94b-117">Bir kurala dayalı çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="4c94b-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="4c94b-118">DLL derleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="4c94b-119">Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="4c94b-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="4c94b-120">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="4c94b-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="4c94b-121">Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="4c94b-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="4c94b-122">[Ayar paket türü](#setting-a-package-type) (NuGet 3.5 ve üstü)</span><span class="sxs-lookup"><span data-stu-id="4c94b-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="4c94b-123">Bir Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="4c94b-124">MSBuild özellik ve hedefleri bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="4c94b-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4c94b-125">COM birlikte çalışma derlemeleri içeren paketleri yazma</span><span class="sxs-lookup"><span data-stu-id="4c94b-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="4c94b-126">.Nupkg dosyasını oluşturmak için nuget paketi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4c94b-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="4c94b-127">Bu adımları çekirdek sonra başka bir yerde bu belgelerinde açıklandığı gibi çeşitli diğer özellikler dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c94b-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="4c94b-128">Bkz: [sonraki adımlar](#next-steps) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="4c94b-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="4c94b-129">Bu konu, Visual Studio 2017 ve NuGet 4.0 + kullanarak .NET Core projeleri dışında proje türleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="4c94b-130">.NET Core projelerdeki NuGet bilgileri kullanır. `.csproj` dosyasını doğrudan.</span><span class="sxs-lookup"><span data-stu-id="4c94b-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="4c94b-131">Ayrıntılar için bkz [oluşturma .NET standart paketlerle Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) ve [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="4c94b-132">Paketlemek için hangi derlemelerin karar verme</span><span class="sxs-lookup"><span data-stu-id="4c94b-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="4c94b-133">En genel amaçlı paketler diğer geliştiricilerin kendi projelerinde kullanabileceğiniz bir veya daha fazla derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="4c94b-134">Genel olarak, her derleme bağımsız olarak yararlıdır koşuluyla NuGet paketi, her bir derleme sağlamak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="4c94b-135">Örneğin, bir `Utilities.dll` , bağımlı `Parser.dll`, ve `Parser.dll` , kendi yararlıdır sonra her biri için bir paket oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c94b-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="4c94b-136">Böylece geliştiriciler verir `Parser.dll` bağımsız `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="4c94b-137">Ardından, kitaplık bağımsız olarak yararlı olmayan birden çok derlemelerinin oluşuyorsa, bir pakete birleştirmek sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="4c94b-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="4c94b-138">Önceki örnekte, kullanarak `Parser.dll` yalnızca kullanılan kodu içeren `Utilities.dll`, tutmak uygundur sonra `Parser.dll` aynı pakette.</span><span class="sxs-lookup"><span data-stu-id="4c94b-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="4c94b-139">Benzer şekilde, varsa `Utilities.dll` bağlıdır `Utilities.resources.dll`, burada yeniden ikinci her ikisinde de aynı paket put, kendi, kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="4c94b-140">Kaynak aslında, özel bir durum yok.</span><span class="sxs-lookup"><span data-stu-id="4c94b-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="4c94b-141">Bir paket bir projeye yüklendiğinde, NuGet paket DLL'leri derleme başvuruları otomatik olarak ekler. *hariç* adlandırıldığı o `.resources.dll` yerleştirilmiş yardımcı derlemeler (bkz: olarakkabulçünkü[ Yerelleştirilmiş paketleri oluşturma](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="4c94b-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="4c94b-142">Bu nedenle, kullanmaktan kaçının `.resources.dll` , aksi takdirde temel paket kodu içeren dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="4c94b-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="4c94b-143">Kitaplığınızı yönergeleri COM birlikte çalışma derlemeleri, ek izleme içeriyorsa [COM birlikte çalışma derlemeleri paketlerle yazma](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="4c94b-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="4c94b-144">Rol ve .nuspec dosyası yapısı</span><span class="sxs-lookup"><span data-stu-id="4c94b-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="4c94b-145">İstediğiniz paketlemek için hangi dosyaların öğrendikten sonra sonraki adım bir paket bildirimi oluşturma bir `.nuspec` XML dosyası.</span><span class="sxs-lookup"><span data-stu-id="4c94b-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="4c94b-146">Bildirim:</span><span class="sxs-lookup"><span data-stu-id="4c94b-146">The manifest:</span></span>

1. <span data-ttu-id="4c94b-147">Paketin içeriği açıklar ve kendisi paketine dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="4c94b-148">Her iki paket oluşturmayı sürücüleri ve paket bir projeye yüklemeye nasıl NuGet bildirir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="4c94b-149">Örneğin, ana paketi yüklendiğinde NuGet bu bağımlılıkları da yükleyebilirsiniz, bildirim diğer Paket bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4c94b-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="4c94b-150">Aşağıda açıklandığı gibi gerekli ve isteğe bağlı özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="4c94b-151">Burada, geçmeyen diğer özellikleri de dahil olmak üzere, tam Ayrıntılar için bkz: [.nuspec başvuru](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="4c94b-152">Gerekli özellikleri:</span><span class="sxs-lookup"><span data-stu-id="4c94b-152">Required properties:</span></span>

- <span data-ttu-id="4c94b-153">Paket tanımlayıcısı paketini barındıran galeri arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="4c94b-154">Belirli bir sürüm numarasını biçiminde *Major.Minor.Patch [-soneki]* nerede *-soneki* tanımlayan [yayın öncesi sürümleri](Prerelease-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="4c94b-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="4c94b-155">Gerektiği gibi (gibi nuget.org) ana bilgisayardaki paket başlığı görüntülenir</span><span class="sxs-lookup"><span data-stu-id="4c94b-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="4c94b-156">Yazar ve sahibi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4c94b-156">Author and owner information.</span></span>
- <span data-ttu-id="4c94b-157">Paket, uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="4c94b-157">A long description of the package.</span></span>

<span data-ttu-id="4c94b-158">Ortak isteğe bağlı özellikleri:</span><span class="sxs-lookup"><span data-stu-id="4c94b-158">Common optional properties:</span></span>

- <span data-ttu-id="4c94b-159">Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="4c94b-159">Release notes</span></span>
- <span data-ttu-id="4c94b-160">Telif hakkı bilgileri</span><span class="sxs-lookup"><span data-stu-id="4c94b-160">Copyright information</span></span>
- <span data-ttu-id="4c94b-161">Kısa bir açıklaması [Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi](../Tools/Package-Manager-UI.md)</span><span class="sxs-lookup"><span data-stu-id="4c94b-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="4c94b-162">Yerel ayar kimliği</span><span class="sxs-lookup"><span data-stu-id="4c94b-162">A locale ID</span></span>
- <span data-ttu-id="4c94b-163">Giriş sayfası ve lisans URL'leri</span><span class="sxs-lookup"><span data-stu-id="4c94b-163">Home page and license URLs</span></span>
- <span data-ttu-id="4c94b-164">Bir simge URL'si</span><span class="sxs-lookup"><span data-stu-id="4c94b-164">An icon URL</span></span>
- <span data-ttu-id="4c94b-165">Bağımlılıklar ve başvurular listesi</span><span class="sxs-lookup"><span data-stu-id="4c94b-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="4c94b-166">Galeri aramalarda yardımcı etiketleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="4c94b-167">Tipik bir (ancak kurgusal) aşağıdadır `.nuspec` özelliklerini açıklayan yorumlarla dosyası:</span><span class="sxs-lookup"><span data-stu-id="4c94b-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
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

<span data-ttu-id="4c94b-168">Bağımlılıklar bildirme ve sürüm numaralarını belirtme hakkında daha fazla bilgi için bkz: [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="4c94b-169">Ayrıca yüzey varlıklarına bağımlılıkları doğrudan paketindeki gelen kullanarak mümkündür `include` ve `exclude` üzerinde öznitelikleri `dependency` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4c94b-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="4c94b-170">Bkz: [.nuspec başvuru - bağımlılıkları](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="4c94b-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="4c94b-171">Bildirim oluşturulan paketinde yer aldığından herhangi bir sayıda ek örnekler mevcut paketleri inceleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c94b-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="4c94b-172">İyi bir kaynak konumu aşağıdaki komutu tarafından döndürülen makinenizde genel paket önbelleğidir:</span><span class="sxs-lookup"><span data-stu-id="4c94b-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="4c94b-173">Tüm gidin *package\version* klasörü, kopya `.nupkg` dosyasını bir `.zip` dosya sonra açmak `.zip` dosya ve inceleyin `.nuspec` içindeki.</span><span class="sxs-lookup"><span data-stu-id="4c94b-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="4c94b-174">Oluştururken bir `.nuspec` bir Visual Studio projesinden paketi yapılandırıldığında projeden bilgilerle değiştirilir belirteçleri bildirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are be replaced with information from the project when the package is built.</span></span> <span data-ttu-id="4c94b-175">Bkz: [.nuspec bir Visual Studio projesi oluşturma](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="4c94b-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="4c94b-176">.Nuspec dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c94b-176">Creating the .nuspec file</span></span>

<span data-ttu-id="4c94b-177">Tam bildirim genellikle oluşturma başlar ile temel bir `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan dosyası:</span><span class="sxs-lookup"><span data-stu-id="4c94b-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="4c94b-178">Bir kurala dayalı çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="4c94b-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="4c94b-179">DLL derleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="4c94b-180">Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="4c94b-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="4c94b-181">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="4c94b-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="4c94b-182">Böylece son paketinde istediğiniz tam içeriğini açıklayan, sonra dosyayı el ile düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="4c94b-183">Oluşturulan `.nuspec` dosyalarını paket ile oluşturmadan önce değiştirilmelidir yer tutucuları içeren `nuget pack` komutu.</span><span class="sxs-lookup"><span data-stu-id="4c94b-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="4c94b-184">Komutu, başarısız `.nuspec` herhangi yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="4c94b-185">Bir kurala dayalı çalışma dizininden</span><span class="sxs-lookup"><span data-stu-id="4c94b-185">From a convention-based working directory</span></span>

<span data-ttu-id="4c94b-186">Bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğundan `.nupkg` uzantısı, kendi genellikle en kolay dosya sisteminde istediğiniz klasör yapısını oluşturun ardından oluşturma `.nuspec` yapıyı doğrudan dosyasından.</span><span class="sxs-lookup"><span data-stu-id="4c94b-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="4c94b-187">`nuget pack` Komut sonra otomatik olarak ekler tüm dosyaları bu klasör yapısındaki (ile başlayan tüm klasörleri hariç `.`, aynı yapısında özel dosyaları tutmak izin vererek).</span><span class="sxs-lookup"><span data-stu-id="4c94b-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="4c94b-188">Bu yaklaşımın avantajı, hangi dosyaların paketin içinde (Bu konunun ilerleyen bölümlerinde açıklandığı gibi) dahil etmek istediğiniz bildiriminde belirtmeniz gerekmez ' dir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="4c94b-189">Pakete gider tam klasör yapısı oluşturmak, oluşturma işlemi yalnızca olabilir ve bir projenin parçası Aksi durumda olmayabilir diğer dosyaları kolayca ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c94b-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="4c94b-190">Hedef projeye eklenen içerik ve kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="4c94b-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="4c94b-191">PowerShell komut dosyaları (NuGet içinde desteklenmeyen 2.x yükleme betikleri de dahil edebilirsiniz NuGet kullanılan paketler 3.x ve üzeri).</span><span class="sxs-lookup"><span data-stu-id="4c94b-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="4c94b-192">Projede mevcut yapılandırma ve kaynak kodu dosyaları için dönüştürmeleri.</span><span class="sxs-lookup"><span data-stu-id="4c94b-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="4c94b-193">Klasör kuralları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4c94b-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="4c94b-194">Klasör</span><span class="sxs-lookup"><span data-stu-id="4c94b-194">Folder</span></span> | <span data-ttu-id="4c94b-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4c94b-195">Description</span></span> | <span data-ttu-id="4c94b-196">Paketi Yükle üzerine gerçekleştirilecek eylemi</span><span class="sxs-lookup"><span data-stu-id="4c94b-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c94b-197">(kök)</span><span class="sxs-lookup"><span data-stu-id="4c94b-197">(root)</span></span> | <span data-ttu-id="4c94b-198">Readme.txt konumu</span><span class="sxs-lookup"><span data-stu-id="4c94b-198">Location for readme.txt</span></span> | <span data-ttu-id="4c94b-199">Paketi yüklendiğinde, visual Studio Paketi kök dizininde readme.txt dosyasına görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="4c94b-200">LIB / {tfm}</span><span class="sxs-lookup"><span data-stu-id="4c94b-200">lib/{tfm}</span></span> | <span data-ttu-id="4c94b-201">Derleme (`.dll`), belgeleri (`.xml`) ve simge (`.pdb`) dosyaları belirtilen hedef Framework bilinen ad (TFM) için</span><span class="sxs-lookup"><span data-stu-id="4c94b-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="4c94b-202">Derlemeleri başvuru olarak eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="4c94b-203">Bkz: [birden çok hedef çerçeveyi destekleyen](Supporting-Multiple-Target-Frameworks.md) framework hedef özgü alt klasörleri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4c94b-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="4c94b-204">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="4c94b-204">runtimes</span></span> | <span data-ttu-id="4c94b-205">Mimariye özel derleme (`.dll`), simge (`.pdb`) ve yerel kaynak (`.pri`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="4c94b-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="4c94b-206">Derlemeleri başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="4c94b-207">Bkz: [birden çok hedef çerçeveyi destekleyen](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="4c94b-208">içerik</span><span class="sxs-lookup"><span data-stu-id="4c94b-208">content</span></span> | <span data-ttu-id="4c94b-209">İsteğe bağlı dosyalar</span><span class="sxs-lookup"><span data-stu-id="4c94b-209">Arbitrary files</span></span> | <span data-ttu-id="4c94b-210">İçeriği proje kök dizinine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-210">Contents are copied to the project root.</span></span> <span data-ttu-id="4c94b-211">Düşünün **içerik** sonuçta paket tüketir hedef uygulama kökü olarak klasör.</span><span class="sxs-lookup"><span data-stu-id="4c94b-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="4c94b-212">Paketi uygulamanın bir görüntüsünü Ekle olmasını */görüntüleri* klasörü, paketin içinde yerleştirin *içeriği/görüntüleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="4c94b-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="4c94b-213">derleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-213">build</span></span> | <span data-ttu-id="4c94b-214">MSBuild `.targets` ve `.props` dosyaları</span><span class="sxs-lookup"><span data-stu-id="4c94b-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="4c94b-215">Proje dosyasına otomatik olarak eklenen (NuGet 2.x) veya `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="4c94b-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="4c94b-216">araçlar</span><span class="sxs-lookup"><span data-stu-id="4c94b-216">tools</span></span> | <span data-ttu-id="4c94b-217">PowerShell komut dosyaları ve programları Paket Yöneticisi Konsolu'ndan erişilebilir</span><span class="sxs-lookup"><span data-stu-id="4c94b-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="4c94b-218">`tools` Klasörü eklenen `PATH` yalnızca Paket Yöneticisi konsolu için ortam değişkeni (özellikle *değil* için `PATH` projesi oluştururken MSBuild için belirlenen).</span><span class="sxs-lookup"><span data-stu-id="4c94b-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="4c94b-219">Klasör yapısı herhangi bir sayıda hedef çerçeve için derlemeleri herhangi bir sayıda içerdiğinden bu yöntem, birden çok çerçeveyi destekleyen paket oluştururken gereklidir</span><span class="sxs-lookup"><span data-stu-id="4c94b-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="4c94b-220">İstenen klasör yapısı yerinde olduktan sonra oluşturmak için bu klasörde herhangi bir durumda, aşağıdaki komutu çalıştırın `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="4c94b-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="4c94b-221">Yeniden oluşturulan `.nuspec` dosyaları klasörü yapısı içinde hiçbir açık başvurular içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4c94b-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="4c94b-222">Paketi oluştururken NuGet tüm dosyaları otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="4c94b-223">Hala bildiriminin diğer bölümlerinde yer tutucu değerlerini ancak düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="4c94b-224">Bir derlemeyi DLL</span><span class="sxs-lookup"><span data-stu-id="4c94b-224">From an assembly DLL</span></span>

<span data-ttu-id="4c94b-225">Bir derlemeye ait bir paket oluşturma en basit durumda, oluşturduğunuz bir `.nuspec` aşağıdaki komutu kullanarak derleme meta dosyası:</span><span class="sxs-lookup"><span data-stu-id="4c94b-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="4c94b-226">Bu formu kullanarak derlemesinden belirli değerleri içeren birkaç yer tutucuları bildiriminde yerini alır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="4c94b-227">Örneğin, `<id>` özelliği, derleme adı için ayarlanır ve `<version>` derleme sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="4c94b-228">Diğer özellikler bildiriminde ancak yoksa eşleşen değerleri bütünleştirilmiş ve hala böylece yer tutucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="4c94b-229">Bir Visual Studio Proje</span><span class="sxs-lookup"><span data-stu-id="4c94b-229">From a Visual Studio project</span></span>

<span data-ttu-id="4c94b-230">Oluşturma bir `.nuspec` gelen bir `.csproj` veya `.vbproj` bu projeye yüklü diğer paketleri otomatik olarak bağımlılıklar olarak başvurulduğundan dosya uygun.</span><span class="sxs-lookup"><span data-stu-id="4c94b-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="4c94b-231">Yalnızca proje dosyası ile aynı klasörde aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4c94b-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="4c94b-232">Elde edilen `<project-name>.nuspec` dosyasını içeren *belirteçleri* , yerini paketleme zaman önceden yüklenmiş olan diğer Paketlerine yönelik başvuruları dahil olmak üzere projeden değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="4c94b-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="4c94b-233">Bir belirteç virgülle ayrılan `$` proje özelliği her iki tarafında simgeler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="4c94b-234">Örneğin, `<id>` bu şekilde genellikle oluşturulan bildiriminde değer şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="4c94b-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="4c94b-235">Bu belirteç ile değiştirilir `AssemblyName` zaman sevk adresindeki Proje dosyasından değeri.</span><span class="sxs-lookup"><span data-stu-id="4c94b-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="4c94b-236">Proje değerlerin tam eşlemesi için `.nuspec` belirteçleri bkz [değiştirme belirteçleri başvuru](../schema/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="4c94b-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="4c94b-237">Belirteçleri hafifletmek, sürüm numarası gibi önemli değerleri güncelleştirmek gerek `.nuspec` proje güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="4c94b-238">(Her zaman belirteçleri değişmez değerler ile isterseniz değiştirebileceğiniz).</span><span class="sxs-lookup"><span data-stu-id="4c94b-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="4c94b-239">Kullanılabilir olduğundan emin birkaç ek paketleme seçenekleri bir Visual Studio projesinden çalışırken açıklandığı gibi Not [.nupkg dosyasını oluşturmak için nuget paketi çalıştıran](#running-nuget-pack-to-generate-the-nupkg-file) daha sonra.</span><span class="sxs-lookup"><span data-stu-id="4c94b-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="4c94b-240">Çözüm düzeyi paketleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-240">Solution-level packages</span></span>

<span data-ttu-id="4c94b-241">*NuGet yalnızca 2.x. NuGet 3.0 + kullanılamaz.*</span><span class="sxs-lookup"><span data-stu-id="4c94b-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="4c94b-242">NuGet 2.x desteklenen araçları veya ek komutlar için Paket Yöneticisi konsolu yükleyen bir çözüm düzeyi paket kavramı (içeriğini `tools` klasör), başvurular, içerik, eklemeyin veya hiçbir projede özelleştirmeleri yapı ancak çözümü.</span><span class="sxs-lookup"><span data-stu-id="4c94b-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="4c94b-243">Kendi doğrudan hiçbir dosyaları gibi paketlerin içeren `lib`, `content`, veya `build` klasörlerin ve bağımlılıklarını hiçbiri sahip kendi ilgili dosyalarında `lib`, `content`, veya `build` klasörler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="4c94b-244">NuGet parçaları çözüm düzeyi paketlerinde yüklü bir `packages.config` dosyasını `.nuget` projenin yerine klasör `packages.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="4c94b-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="4c94b-245">Varsayılan değerlerle yeni dosya</span><span class="sxs-lookup"><span data-stu-id="4c94b-245">New file with default values</span></span>

<span data-ttu-id="4c94b-246">Aşağıdaki komut bir varsayılan bildirimi yer tutucularını, uygun dosya yapısıyla başlayın sağlayan oluşturur:</span><span class="sxs-lookup"><span data-stu-id="4c94b-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="4c94b-247">Atlarsanız \<paket adı\>, sonuçta elde edilen dosya `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="4c94b-248">Bir ad gibi sağlarsanız, `Contoso.Utility.UsefulStuff`, dosya `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="4c94b-249">Elde edilen `.nuspec` değerleri ister için yer tutucuları içeren `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="4c94b-250">En son oluşturmak amacıyla kullanmadan önce dosyayı düzenlemek mutlaka `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="4c94b-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="4c94b-251">Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="4c94b-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="4c94b-252">Paket tanımlayıcısı (`<id>` öğesi) ve uygulamanın sürüm numarasını (`<version>` öğesi) benzersiz şekilde pakette yer alan tam kodu belirttikleri iki en önemli bildiriminde değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="4c94b-253">**Paket tanımlayıcısı için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="4c94b-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="4c94b-254">**Benzersizlik**: tanımlayıcısı nuget.org veya ne olursa olsun galeri paketi barındıran arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="4c94b-255">Üzerinde bir tanımlayıcı karar vermeden önce ad zaten kullanımda olup olmadığını denetlemek için uygulanabilir galeri arayın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="4c94b-256">Çakışmaları önlemek için iyi bir desen şirket adınızı tanımlayıcı ilk parçası olarak gibi kullanmaktır `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="4c94b-257">**Namespace benzeri adları**: .NET, kısa çizgi yerine noktalı gösterim kullanılarak ad alanları için benzer bir yol izler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="4c94b-258">Örneğin, `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="4c94b-259">Paket tanımlayıcısı kod içinde kullanılan ad alanları eşleştiğinde tüketicileri de yararlı.</span><span class="sxs-lookup"><span data-stu-id="4c94b-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="4c94b-260">**Örnek paketler**: başka bir paket kullanmak için iliştirmek nasıl gösteren örnek kod paketi oluşturmak, `.Sample` giriş olarak tanımlayıcısına soneki olarak `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="4c94b-261">(Örnek paketi Elbette başka bir paketi bir bağımlılık gerekir.) Bir örnek paket oluştururken, daha önce açıklanan kurala dayalı çalışma dizini yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="4c94b-262">İçinde `content` klasör adında bir klasör örnek kodda düzenleme `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="4c94b-263">**Paket sürümü için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="4c94b-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="4c94b-264">Genel olarak, bu kesinlikle gerekli olmasa da kitaplığı eşleşecek şekilde paketin sürümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="4c94b-265">Bir paketi tek bir derleme sınırladığınızda atmaktan daha önce açıklandığı gibi budur [hangi derlemelerin pakete karar](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="4c94b-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="4c94b-266">Genel olarak, bağımlılıkları, derleme sürümlerini çözülürken kendisini NuGet paketi sürümleri ile ilgilenir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="4c94b-267">Standart sürüm düzeni kullanırken açıklandığı şekilde NuGet sürüm kuralları dikkate aldığınızdan emin olun [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="4c94b-268">Kısa blog gönderileri aşağıdaki bir dizi ayrıca sürüm anlaşılması yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="4c94b-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="4c94b-269">1. Kısım: Alma DLL cehennemi üzerinde</span><span class="sxs-lookup"><span data-stu-id="4c94b-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="4c94b-270">2. Kısım: Çekirdek algoritması</span><span class="sxs-lookup"><span data-stu-id="4c94b-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="4c94b-271">3. Kısım: bağlama yeniden yönlendirmeleri aracılığıyla Birleştirici</span><span class="sxs-lookup"><span data-stu-id="4c94b-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="4c94b-272">Ayar paket türü</span><span class="sxs-lookup"><span data-stu-id="4c94b-272">Setting a package type</span></span>

<span data-ttu-id="4c94b-273">NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="4c94b-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="4c94b-274">NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere bir türü ile işaretli olmayan paketler için varsayılan değer `Dependency` türü.</span><span class="sxs-lookup"><span data-stu-id="4c94b-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="4c94b-275">`Dependency`türü paketleri kitaplıkları ve uygulamalar için derleme veya çalışma zamanı varlıklar ekleyin ve (uyumlu olduğu varsayılarak) herhangi bir proje türü yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="4c94b-276">`DotnetCliTool`türü paketlerdir uzantıları [.NET CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index) ve komut satırından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="4c94b-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="4c94b-277">Gibi paketlerin, yalnızca .NET çekirdeği projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="4c94b-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="4c94b-278">Bu proje başına uzantıları hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="4c94b-278">More details about these per-project extensions are available in the  [.NET Core extensibility](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="4c94b-279">DotnetCliTool paket yüklendikten sonra Visual Studio pakette yerleştirir `project.json` `tools` yerine düğümü `dependencies` düğümü.</span><span class="sxs-lookup"><span data-stu-id="4c94b-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="4c94b-280">Özel tür paketleri paket kimlikleri ile aynı biçimi kurallara uyan bir rastgele türü tanımlayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="4c94b-281">Herhangi türdeki dışında `Dependency` ve `DotnetCliTool`, ancak, Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.</span><span class="sxs-lookup"><span data-stu-id="4c94b-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="4c94b-282">Paket türleri kümesinde ya da `.nuspec` dosya veya `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="4c94b-283">Her iki durumda da, geriye doğru için en iyisidir Uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine bu türü tür varsayılarak NuGet üzerinde yararlanmayı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="4c94b-284">`.nuspec`: İçinde paket türünü gösteren bir `packageTypes\packageType` düğümü altında `<metadata>` öğe:</span><span class="sxs-lookup"><span data-stu-id="4c94b-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

- <span data-ttu-id="4c94b-285">`project.json`: İçinde paket türünü gösteren bir `packOptions.packageType` özelliği json:</span><span class="sxs-lookup"><span data-stu-id="4c94b-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="4c94b-286">Bir Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-286">Adding a readme and other files</span></span>

<span data-ttu-id="4c94b-287">Doğrudan pakete eklenecek dosyaları belirtmek için kullanın `<files>` düğümünde `.nuspec` dosyası, hangi *izleyen* `<metadata>` etiketi:</span><span class="sxs-lookup"><span data-stu-id="4c94b-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="4c94b-288">Çalışma dizini kurala dayalı yaklaşım kullanırken, readme.txt paket kök ve diğer içerik yerleştirebilirsiniz `content` klasör.</span><span class="sxs-lookup"><span data-stu-id="4c94b-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="4c94b-289">Hayır `<file>` öğeleridir bildiriminde gerekli.</span><span class="sxs-lookup"><span data-stu-id="4c94b-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="4c94b-290">Adlı bir dosya eklediğinizde `readme.txt` paket kök, Visual Studio bu dosyanın içeriğini düz metin olarak hemen paketi doğrudan yüklendikten sonra görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="4c94b-291">(Benioku dosyaları bağımlılıklar olarak yüklenen paketler için görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="4c94b-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="4c94b-292">Örneğin, işte nasıl HtmlAgilityPack paketi için Benioku görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="4c94b-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için Benioku dosyasını görüntüleme](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="4c94b-294">Boş bir eklerseniz `<files>` düğümünde `.nuspec` dosyası NuGet içermez herhangi bir içerik paketinde ne olduğunu dışında `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="4c94b-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="4c94b-295">MSBuild özellik ve hedefleri bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="4c94b-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="4c94b-296">Bazı durumlarda, özel araç veya işlem sırasında derleme çalıştırma gibi paketinizi tüketen projelerine özel derleme hedefler ya da özellikleri eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c94b-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="4c94b-297">Dosya biçiminde girerek bunu `<package_id>.targets` veya `<package_id>.props` (gibi `Contoso.Utility.UsefulStuff.targets`) içinde `\build` projenin klasör.</span><span class="sxs-lookup"><span data-stu-id="4c94b-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="4c94b-298">Kök dosyalarında `\build` tüm çerçeveler hedef için klasör uygun değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="4c94b-299">Çerçeveye özel dosyaları sağlamak için önce aşağıdaki gibi uygun alt içinde bulunanlar koyun:</span><span class="sxs-lookup"><span data-stu-id="4c94b-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="4c94b-300">Ardından `.nuspec` dosya, bu dosyaları başvurmak mutlaka `<files>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="4c94b-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
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

<span data-ttu-id="4c94b-301">Zaman 2.x ile bir pakete yükler NuGet `\build` dosyaları, bir MSBuild ekler `<Import>` işaret proje dosyasındaki öğeleri `.targets` ve `.props` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4c94b-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="4c94b-302">(`.props` proje dosyası; en üstte eklenir `.targets` altındaki eklenir.)</span><span class="sxs-lookup"><span data-stu-id="4c94b-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="4c94b-303">NuGet ile 3.x hedefleri projeye eklenmez ancak bunun yerine kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="4c94b-304">COM birlikte çalışma derlemeleri paketlerle yazma</span><span class="sxs-lookup"><span data-stu-id="4c94b-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="4c94b-305">COM birlikte çalışma derlemeleri içeren paketleri uygun bir içermelidir [hedefler dosyası](#including-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` meta veri PackageReference biçimini kullanarak projelerine eklenir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="4c94b-306">Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, hedefler dosyası bu meta verileri açıkça ekler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="4c94b-307">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adı ve katıştırılmış, değiştirerek olan derleme oluşan bir bileşim kullanmanız `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="4c94b-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="4c94b-308">(Ayrıca bkz. [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek için.)</span><span class="sxs-lookup"><span data-stu-id="4c94b-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="4c94b-309">Kullanırken dikkat edin `packages.config` başvuru biçimi'nın paketlerinden derlemeler başvuruları ekleme neden olan NuGet ve Visual Studio COM birlikte çalışma derlemeleri için denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasında true.</span><span class="sxs-lookup"><span data-stu-id="4c94b-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="4c94b-310">Bu durumda hedefleri kılınmadı ' dir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="4c94b-311">Ayrıca, varsayılan olarak [yapı varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="4c94b-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="4c94b-312">Projeyi project başvurusundan geçişli bağımlılık olarak çekildiğinde burada iş farklı bir şekilde açıklandığı gibi yazılan paketler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="4c94b-313">Paket tüketici yapı içermeyecek şekilde PrivateAssets varsayılan değerini değiştirerek akmasına izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c94b-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="4c94b-314">.Nupkg dosyasını oluşturmak için nuget paketi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4c94b-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="4c94b-315">Bir derlemeyi ya da kurala dayalı çalışma dizini kullanarak, bir paket çalıştırarak oluşturduğunuzda `nuget pack` ile `.nuspec` dosya, değiştirme `<manifest-name>` , belirli dosya adı:</span><span class="sxs-lookup"><span data-stu-id="4c94b-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="4c94b-316">Visual Studio projesi kullanırken çalıştırmak `nuget pack` , proje dosyası ile otomatik olarak yükleyen projenin `.nuspec` dosya ve proje dosyasında değerleri kullanarak içinde herhangi bir belirtece değiştirir:</span><span class="sxs-lookup"><span data-stu-id="4c94b-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="4c94b-317">Proje dosyası kullanarak doğrudan proje simge değerlerini kaynağı olduğundan belirteci yapabilmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="4c94b-318">Belirteç değiştirme olmayacak kullanırsanız `nuget pack` ile bir `.nuspec` dosyası.</span><span class="sxs-lookup"><span data-stu-id="4c94b-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="4c94b-319">Tüm durumlarda `nuget pack` gibi bir noktayla başlayan klasörleri dışlar `.git` veya `.hg`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="4c94b-320">NuGet gösteren herhangi bir hata olup olmadığını `.nuspec` bildiriminde yer tutucu değerlerini değiştirmek işlerle gibi düzeltilmesi gereken dosya.</span><span class="sxs-lookup"><span data-stu-id="4c94b-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="4c94b-321">Bir kez `nuget pack` başarılı, sahip olduğunuz bir `.nupkg` açıklandığı gibi uygun bir Galeriye yayımlayabilirsiniz dosya [yayımlama bir paketi](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="4c94b-322">İçinde açmak için oluşturma tamamlandıktan sonra bir paket incelemek için kullanışlı bir yol [paket Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracı.</span><span class="sxs-lookup"><span data-stu-id="4c94b-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="4c94b-323">Bu paket içeriğini ve onun bildirimi grafik bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c94b-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="4c94b-324">Elde edilen adlandırabilirsiniz `.nupkg` dosyasını bir `.zip` dosya ve içeriğini doğrudan inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="4c94b-325">Ek Seçenekler</span><span class="sxs-lookup"><span data-stu-id="4c94b-325">Additional options</span></span>

<span data-ttu-id="4c94b-326">Çeşitli komut satırı anahtarları ile kullanabileceğiniz `nuget pack` dosyaları hariç tutmak, bildiriminde sürüm numarası geçersiz kılmak ve diğer özellikler arasında çıkış klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="4c94b-327">Tam bir listesi için bkz [pack komut başvurusu](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="4c94b-328">Aşağıdaki seçenekler, birkaç Visual Studio projeleri ile ortak şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4c94b-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="4c94b-329">**Projeleri başvurulan**: Proje diğer projeler başvuruyorsa, başvurulan projeleri paketinin bir parçası olarak ya da bağımlılık, kullanarak ekleyebileceğiniz `-IncludeReferencedProjects` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="4c94b-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="4c94b-330">Bu ekleme işlemi yinelemelidir dolayısıyla `MyProject.csproj` başvuruları projeleri B ve C ve bu projeler başvuru D, E ve F, ardından B, C D E ve F dosyalarından pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="4c94b-331">Başvuruda bulunulan bir proje içeriyorsa, bir `.nuspec` sonra kendi, NuGet dosyasının başvurulan proje bunun yerine bir bağımlılık olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="4c94b-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="4c94b-332">Paket ve proje ayrıca yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c94b-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="4c94b-333">**Derleme Yapılandırması**: varsayılan olarak, varsayılan derleme yapılandırması proje dosyasında genellikle ayarlanmış NuGet kullanır *hata ayıklama*.</span><span class="sxs-lookup"><span data-stu-id="4c94b-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="4c94b-334">Farklı bir yapı yapılandırma dosyaları gibi paketlemek için *sürüm*, kullanın `-properties` yapılandırma seçeneğiyle:</span><span class="sxs-lookup"><span data-stu-id="4c94b-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="4c94b-335">**Simgeler**: hata ayıklayıcı paket kodunuzda adım adım tüketicilerin izin simgeleri eklemek için kullanın `-Symbols` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="4c94b-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="4c94b-336">Test paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-336">Testing package installation</span></span>

<span data-ttu-id="4c94b-337">Bir paket yayımlamadan önce genellikle bir paket bir projeye yükleme işlemi test etmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4c94b-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="4c94b-338">Testleri olduğundan emin olun mutlaka tüm şunun kendi doğru yerde projedeki dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4c94b-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="4c94b-339">Visual Studio'da veya normal kullanarak komut satırında el ile yüklemeleri komutunu sınayabilirsiniz [yükleme adımlarını paketini](../Quickstart/Use-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="4c94b-340">Otomatik test için temel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4c94b-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="4c94b-341">Kopya `.nupkg` dosyasını bir yerel klasöre.</span><span class="sxs-lookup"><span data-stu-id="4c94b-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="4c94b-342">Paket kaynaklarınızın kullanarak klasörü Ekle `nuget sources -name <name> -source <path>` komutu (bkz [nuget kaynakları](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="4c94b-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="4c94b-343">Yalnızca bu yerel kaynağı kez verilen herhangi bir bilgisayarda ayarlamanız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4c94b-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="4c94b-344">Bu kaynak kullanarak paketi yükleyin `nuget install <packageID> -source <name>` nerede `<name>` verilen kaynak adıyla eşleşen `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="4c94b-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="4c94b-345">Kaynağını belirterek, bu kaynak paketinin yüklü olduğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c94b-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="4c94b-346">Dosyaların doğru yüklü olduğunu denetlemek için dosya sistemini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4c94b-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c94b-347">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4c94b-347">Next Steps</span></span>

<span data-ttu-id="4c94b-348">Olan bir paketi oluşturduktan sonra bir `.nupkg` dosyası yayımlayarak, tercih ettiğiniz Galerisine açıklandığı gibi [yayımlama bir paketi](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4c94b-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="4c94b-349">Paketinizi yeteneklerini veya aksi halde aşağıdaki konularda açıklandığı gibi başka senaryoları destekleyecek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c94b-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="4c94b-350">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c94b-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4c94b-351">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="4c94b-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4c94b-352">Kaynak ve yapılandırma dosyaları dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="4c94b-353">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="4c94b-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4c94b-354">Yayın öncesi sürümleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="4c94b-355">Son olarak, dikkat edilmesi gereken ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="4c94b-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="4c94b-356">Yerel Paketleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="4c94b-357">Simge paketleri</span><span class="sxs-lookup"><span data-stu-id="4c94b-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
