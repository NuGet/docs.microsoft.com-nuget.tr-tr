---
title: NuGet. exe CLı kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: e4223c25daa1c14c30de1ef063cd0f48df70c8b5
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564578"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="7193e-103">NuGet. exe CLı kullanarak paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="7193e-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="7193e-104">Paketinizin ne yaptığını veya hangi kodu içerdiğini bağımsız olarak, bu işlevselliği bir veya daha fazla geliştirici tarafından kullanılabilen bir bileşene `nuget.exe` paketlemek `dotnet.exe`için ya da CLI araçlarından birini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7193e-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="7193e-105">NuGet CLı araçları 'nı yüklemek için bkz. [NuGet istemci araçları 'Nı yüklemek](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="7193e-106">Visual Studio 'Nun otomatik olarak bir CLı aracı içermediği unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7193e-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="7193e-107">SDK olmayan stil projeleri için genellikle projeleri .NET Framework, bir paket oluşturmak için bu makalede açıklanan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7193e-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="7193e-108">Visual Studio ve `nuget.exe` CLI kullanarak adım adım yönergeler için bkz. [.NET Framework paketi oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="7193e-109">.NET Core .NET Standard ve [SDK stili biçimi](../resources/check-project-format.md)kullanan projeleri ve diğer SDK stili projeleri için, bkz. [DotNet CLI kullanarak bir NuGet paketi oluşturma](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="7193e-110">' Den `packages.config` [packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.</span><span class="sxs-lookup"><span data-stu-id="7193e-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="7193e-111">Teknik olarak, bir NuGet paketi yalnızca `.nupkg` uzantısıyla yeniden adlandırılan ve içeriği belirli kurallara uyan bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="7193e-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="7193e-112">Bu konuda, bu kuralları karşılayan bir paket oluşturmanın ayrıntılı süreci açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7193e-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="7193e-113">Paketleme, derlenmiş kod (derlemeler), semboller ve/veya paket olarak teslim etmek istediğiniz diğer dosyaları (bkz. [genel bakış ve iş akışı](overview-and-workflow.md)) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="7193e-114">Bu işlem, derlenmiş derlemeleri ve paketleri eşitlenmiş halde tutmak için bir proje dosyasındaki bilgilerden çizim yapabilmenize rağmen, derleme ' den bağımsız olan dosyaları derlemeden veya oluşturmadan bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="7193e-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="7193e-115">Bu konu SDK olmayan projeler için geçerlidir, genellikle .NET Core dışındaki projeler ve Visual Studio 2017 ve daha yeni sürümleri ve NuGet 4.0 + kullanan projeler .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="7193e-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="7193e-116">Hangi derlemelerin paketlenecek olduğuna karar verin</span><span class="sxs-lookup"><span data-stu-id="7193e-116">Decide which assemblies to package</span></span>

<span data-ttu-id="7193e-117">Genel amaçlı paketlerin çoğu, diğer geliştiricilerin kendi projelerinde kullanabileceği bir veya daha fazla derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="7193e-118">Genel olarak, her derlemenin bağımsız olarak yararlı olması şartıyla her bir derleme için tek bir derlemeye sahip olmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="7193e-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="7193e-119">Örneğin, `Utilities.dll` `Parser.dll`öğesine bağlı bir uygulamanız varsa ve `Parser.dll` kendi yararlıysa, her biri için bir paket oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7193e-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="7193e-120">Bunun yapılması, `Utilities.dll`geliştiricilerin bağımsız olarak `Parser.dll` kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="7193e-121">Kitaplığınız bağımsız olarak yararlı olmayan birden çok derlemeden oluşuyorsa, bunları tek bir pakette birleştirmek iyi olur.</span><span class="sxs-lookup"><span data-stu-id="7193e-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="7193e-122">Önceki örneği kullanarak, `Parser.dll` yalnızca tarafından `Utilities.dll`kullanılan kodu içeriyorsa, aynı pakette tutulması `Parser.dll` iyi olur.</span><span class="sxs-lookup"><span data-stu-id="7193e-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="7193e-123">Benzer şekilde, `Utilities.dll` ne olursa `Utilities.resources.dll`yapın, her ikisi de kendi üzerinde yararlı değildir ve her ikisini de aynı pakete koyun.</span><span class="sxs-lookup"><span data-stu-id="7193e-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="7193e-124">Kaynaklar aslında özel bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="7193e-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="7193e-125">Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'lerine derleme başvuruları ekler, `.resources.dll` çünkü yerelleştirilmiş uydu derlemeleri oldukları varsayılanlar (bkz. [yerelleştirilmiş oluşturma paketler](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="7193e-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="7193e-126">Bu nedenle, başka bir şekilde `.resources.dll` temel paket kodu içeren dosyalar için kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="7193e-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="7193e-127">Kitaplığınız COM birlikte çalışma derlemelerini içeriyorsa, [com birlikte çalışma Derlemeleriyle paket oluşturma](author-packages-with-com-interop-assemblies.md)' daki ek yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="7193e-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="7193e-128">. Nuspec dosyasının rolü ve yapısı</span><span class="sxs-lookup"><span data-stu-id="7193e-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="7193e-129">Hangi dosyaları paketlemek istediğinizi öğrendikten sonra, bir sonraki adım bir `.nuspec` XML dosyasında paket bildirimi oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="7193e-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="7193e-130">Bildirim:</span><span class="sxs-lookup"><span data-stu-id="7193e-130">The manifest:</span></span>

1. <span data-ttu-id="7193e-131">Paketin içeriğini açıklar ve pakete dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7193e-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="7193e-132">Hem paketin oluşturulmasını hem de paketin bir projeye nasıl yükleneceğine ilişkin NuGet 'e yöneltir.</span><span class="sxs-lookup"><span data-stu-id="7193e-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="7193e-133">Örneğin, bildirim diğer paket bağımlılıklarını tanımlar, bu da ana paket yüklendiğinde NuGet bu bağımlılıkları yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="7193e-134">Aşağıda açıklandığı gibi hem gerekli hem de isteğe bağlı özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="7193e-135">Burada bahsedilen diğer özellikler dahil olmak üzere tam Ayrıntılar için bkz [. nuspec başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="7193e-136">Gerekli Özellikler:</span><span class="sxs-lookup"><span data-stu-id="7193e-136">Required properties:</span></span>

- <span data-ttu-id="7193e-137">Paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7193e-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="7193e-138">*Birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md) tanımlar</span><span class="sxs-lookup"><span data-stu-id="7193e-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="7193e-139">Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="7193e-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="7193e-140">Yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7193e-140">Author and owner information.</span></span>
- <span data-ttu-id="7193e-141">Paketin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="7193e-141">A long description of the package.</span></span>

<span data-ttu-id="7193e-142">Ortak isteğe bağlı özellikler:</span><span class="sxs-lookup"><span data-stu-id="7193e-142">Common optional properties:</span></span>

- <span data-ttu-id="7193e-143">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="7193e-143">Release notes</span></span>
- <span data-ttu-id="7193e-144">Telif hakkı bilgileri</span><span class="sxs-lookup"><span data-stu-id="7193e-144">Copyright information</span></span>
- <span data-ttu-id="7193e-145">[Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi](../consume-packages/install-use-packages-visual-studio.md) için kısa bir açıklama</span><span class="sxs-lookup"><span data-stu-id="7193e-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="7193e-146">Yerel ayar KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="7193e-146">A locale ID</span></span>
- <span data-ttu-id="7193e-147">Proje URL 'SI</span><span class="sxs-lookup"><span data-stu-id="7193e-147">Project URL</span></span>
- <span data-ttu-id="7193e-148">Bir ifade veya dosya olarak lisans (`licenseUrl` kullanım dışı bırakılıyor, [ `license` nuspec meta veri öğesini](../reference/nuspec.md#license)kullanın)</span><span class="sxs-lookup"><span data-stu-id="7193e-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="7193e-149">Simge URL 'SI</span><span class="sxs-lookup"><span data-stu-id="7193e-149">An icon URL</span></span>
- <span data-ttu-id="7193e-150">Bağımlılıklar ve başvuru listeleri</span><span class="sxs-lookup"><span data-stu-id="7193e-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="7193e-151">Galeri aramalarında yardımcı olan Etiketler</span><span class="sxs-lookup"><span data-stu-id="7193e-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="7193e-152">Aşağıda, özellikleri açıklayan açıklamalar içeren tipik bir ( `.nuspec` ancak kurgusal) dosya verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7193e-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

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

<span data-ttu-id="7193e-153">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. [Packages. config](../reference/packages-config.md) ve [Package sürümü oluşturma](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="7193e-154">Ayrıca, `include` öğe`dependency` üzerindeki ve `exclude` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan yüzeylerden yüzey mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7193e-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="7193e-155">Bkz [. nuspec başvurusu-bağımlılıklar](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="7193e-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="7193e-156">Bildirim bundan oluşturulan pakete eklendiğinden, var olan paketleri inceleyerek istediğiniz sayıda ek örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="7193e-157">İyi bir kaynak, bilgisayarınızdaki *genel paketler* klasörüdür ve aşağıdaki komut tarafından döndürülen konumudur:</span><span class="sxs-lookup"><span data-stu-id="7193e-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="7193e-158">Herhangi bir *package\version* klasörüne gidin, `.nupkg` dosyayı bir `.zip` dosyaya kopyalayın, `.nuspec` sonra dosyayı açın `.zip` ve içinde inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7193e-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="7193e-159">Visual Studio projesinden `.nuspec` bir oluştururken, bildirim, paket oluşturulduğunda projedeki bilgilerle değiştirilmiş belirteçleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="7193e-160">Bkz. [Visual Studio projesinden. nuspec oluşturma](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="7193e-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="7193e-161">. Nuspec dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7193e-161">Create the .nuspec file</span></span>

<span data-ttu-id="7193e-162">Komple bir bildirim oluşturmak, genellikle aşağıdaki yöntemlerden biri `.nuspec` kullanılarak oluşturulan temel bir dosya ile başlar:</span><span class="sxs-lookup"><span data-stu-id="7193e-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="7193e-163">Kural tabanlı çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="7193e-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="7193e-164">Derleme DLL 'SI</span><span class="sxs-lookup"><span data-stu-id="7193e-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="7193e-165">Bir Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="7193e-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="7193e-166">Varsayılan değerlere sahip yeni dosya</span><span class="sxs-lookup"><span data-stu-id="7193e-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="7193e-167">Ardından dosyayı el ile düzenleyerek son pakette istediğiniz içeriğin tam olarak oluşturulmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="7193e-168">Oluşturulan `.nuspec` dosyalar, `nuget pack` paketini komutuyla oluşturmadan önce değiştirilmesi gereken yer tutucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="7193e-169">Herhangi bir yer tutucu içeriyorsa `.nuspec` , bu komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7193e-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="7193e-170">Kural tabanlı çalışma dizininden</span><span class="sxs-lookup"><span data-stu-id="7193e-170">From a convention-based working directory</span></span>

<span data-ttu-id="7193e-171">Bir NuGet paketi yalnızca `.nupkg` uzantısıyla yeniden adlandırılmış bir ZIP dosyası olduğundan, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmak ve ardından `.nuspec` dosyayı doğrudan bu yapıyla oluşturmak daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="7193e-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="7193e-172">Komut daha sonra bu klasör yapısındaki tüm dosyaları otomatik olarak ekler (ile `.`başlayan tüm klasörler hariç) ve özel dosyaları aynı yapıda tutmanıza olanak sağlar. `nuget pack`</span><span class="sxs-lookup"><span data-stu-id="7193e-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="7193e-173">Bu yaklaşımın avantajı, pakete dahil etmek istediğiniz dosyaları (Bu konunun ilerleyen kısımlarında açıklandığı gibi) belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7193e-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="7193e-174">Yapı işleminizin pakete giden tam klasör yapısını oluşturması, aksi takdirde bir projenin parçası olmayan diğer dosyaları kolayca dahil edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7193e-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="7193e-175">Hedef projeye eklenmesi gereken içerik ve kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="7193e-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="7193e-176">PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="7193e-176">PowerShell scripts</span></span>
- <span data-ttu-id="7193e-177">Bir projedeki mevcut yapılandırma ve kaynak kod dosyalarına dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="7193e-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="7193e-178">Klasör kuralları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7193e-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="7193e-179">Klasör</span><span class="sxs-lookup"><span data-stu-id="7193e-179">Folder</span></span> | <span data-ttu-id="7193e-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7193e-180">Description</span></span> | <span data-ttu-id="7193e-181">Paket yüklendikten sonra gerçekleştirilecek eylem</span><span class="sxs-lookup"><span data-stu-id="7193e-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7193e-182">Asıl</span><span class="sxs-lookup"><span data-stu-id="7193e-182">(root)</span></span> | <span data-ttu-id="7193e-183">Readme. txt konumu</span><span class="sxs-lookup"><span data-stu-id="7193e-183">Location for readme.txt</span></span> | <span data-ttu-id="7193e-184">Paket yüklendiğinde, Visual Studio paket kökünde bir Readme. txt dosyası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7193e-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="7193e-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="7193e-185">lib/{tfm}</span></span> | <span data-ttu-id="7193e-186">Verilen hedef`.dll`çerçeve bilinen adı (`.xml`TFI) için bütünleştirilmiş`.pdb`kod (), belge () ve sembol () dosyaları</span><span class="sxs-lookup"><span data-stu-id="7193e-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="7193e-187">Derlemeler derleme ve çalışma zamanı için başvurular olarak eklenir; `.xml` ve`.pdb` proje klasörlerine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="7193e-188">Bkz. çerçeve hedefine özgü alt klasörler oluşturmak için [birden çok hedef çerçeve destekleme](supporting-multiple-target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="7193e-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="7193e-189">ref/{tfd}</span><span class="sxs-lookup"><span data-stu-id="7193e-189">ref/{tfm}</span></span> | <span data-ttu-id="7193e-190">Verilen hedef`.dll`çerçeve bilinen adı (TFI) için bütünleştirilmiş kod () ve sembol (`.pdb`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="7193e-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="7193e-191">Derlemeler yalnızca derleme süresi için başvuru olarak eklenir; Bu nedenle proje bin klasörüne hiçbir şey kopyalanmayacak.</span><span class="sxs-lookup"><span data-stu-id="7193e-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="7193e-192">zamanları</span><span class="sxs-lookup"><span data-stu-id="7193e-192">runtimes</span></span> | <span data-ttu-id="7193e-193">Mimariye özgü bütünleştirilmiş kod (`.dll`), simge (`.pdb`) ve yerel kaynak (`.pri`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="7193e-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="7193e-194">Derlemeler yalnızca çalışma zamanı için başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7193e-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="7193e-195">Karşılık gelen derleme zamanı derlemesini sağlamak için klasörü altında `AnyCPU` `/ref/{tfm}` her zaman karşılık gelen (TFE) özel bütünleştirilmiş kod olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7193e-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="7193e-196">Bkz. [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="7193e-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="7193e-197">içerik</span><span class="sxs-lookup"><span data-stu-id="7193e-197">content</span></span> | <span data-ttu-id="7193e-198">Rastgele dosyalar</span><span class="sxs-lookup"><span data-stu-id="7193e-198">Arbitrary files</span></span> | <span data-ttu-id="7193e-199">İçerikler proje köküne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7193e-199">Contents are copied to the project root.</span></span> <span data-ttu-id="7193e-200">**İçerik** klasörünü, son olarak paketi tüketen hedef uygulamanın kökü olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="7193e-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="7193e-201">Paketin uygulamanın */Images* klasörüne görüntü eklemesi için, paketin *içerik/görüntüler* klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7193e-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="7193e-202">derleme</span><span class="sxs-lookup"><span data-stu-id="7193e-202">build</span></span> | <span data-ttu-id="7193e-203">*(3. x +)* MSBuild `.targets` ve `.props` dosyalar</span><span class="sxs-lookup"><span data-stu-id="7193e-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="7193e-204">Projeye otomatik olarak ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="7193e-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="7193e-205">Buildmultihedefleme</span><span class="sxs-lookup"><span data-stu-id="7193e-205">buildMultiTargeting</span></span> | <span data-ttu-id="7193e-206">*(4.0 +)* Platformlar `.targets` arası `.props` hedefleme için MSBuild ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="7193e-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="7193e-207">Projeye otomatik olarak ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="7193e-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="7193e-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="7193e-208">buildTransitive</span></span> | <span data-ttu-id="7193e-209">*(5.0 +)* Herhangi `.targets` bir `.props` tüketen projeye geçişli olarak akan MSBuild ve dosyalar.</span><span class="sxs-lookup"><span data-stu-id="7193e-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="7193e-210">Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası.</span><span class="sxs-lookup"><span data-stu-id="7193e-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="7193e-211">Projeye otomatik olarak ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="7193e-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="7193e-212">araçlar</span><span class="sxs-lookup"><span data-stu-id="7193e-212">tools</span></span> | <span data-ttu-id="7193e-213">Paket Yöneticisi konsolundan erişilebilen PowerShell betikleri ve programları</span><span class="sxs-lookup"><span data-stu-id="7193e-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="7193e-214">Klasör, yalnızca Paket Yöneticisi Konsolu `PATH` için ortam değişkenine eklenir ( `PATH` özellikle, proje oluşturulurken MSBuild için ayarlanan as kümesine uygulanmaz). `tools`</span><span class="sxs-lookup"><span data-stu-id="7193e-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="7193e-215">Klasör yapınız herhangi bir sayıda hedef çerçeve için herhangi bir sayıda derleme içerebildiğinden, bu yöntem birden çok çerçeveyi destekleyen paketler oluştururken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7193e-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="7193e-216">Herhangi bir durumda, istenen klasör yapısına sahip olduktan sonra `.nuspec` dosyayı oluşturmak için bu klasörde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7193e-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="7193e-217">Yine, oluşturulan `.nuspec` , klasör yapısındaki dosyalara açık başvuru içermez.</span><span class="sxs-lookup"><span data-stu-id="7193e-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="7193e-218">NuGet, Paket oluşturulduğu zaman otomatik olarak tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="7193e-219">Bununla birlikte, bildirimin diğer bölümlerinde yer tutucu değerlerini de düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7193e-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="7193e-220">Bir derleme DLL 'sinden</span><span class="sxs-lookup"><span data-stu-id="7193e-220">From an assembly DLL</span></span>

<span data-ttu-id="7193e-221">Derlemeden bir paket oluşturduğunuzda, aşağıdaki komutu kullanarak derlemedeki meta verilerden bir `.nuspec` dosya oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7193e-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="7193e-222">Bu formun kullanılması, bildirimdeki bazı yer tutucuları derlemedeki belirli değerlerle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7193e-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="7193e-223">Örneğin, `<id>` özelliği derleme adına ayarlanır ve `<version>` derleme sürümü olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7193e-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="7193e-224">Ancak bildirimde bulunan diğer özellikler, derlemede eşleşen değerlere sahip değildir ve bu nedenle yine de yer tutucu içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="7193e-225">Visual Studio projesinden</span><span class="sxs-lookup"><span data-stu-id="7193e-225">From a Visual Studio project</span></span>

<span data-ttu-id="7193e-226">Bu projeye `.nuspec` yüklenmiş olan `.csproj` diğer `.vbproj` paketlere otomatik olarak bağımlılık olarak başvurulduğundan, veya dosyasından bir oluşturma işlemi kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="7193e-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="7193e-227">Aşağıdaki komutu, proje dosyasıyla aynı klasörde kullanmanız yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="7193e-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="7193e-228">Elde edilen `<project-name>.nuspec` dosya, zaten yüklenmiş olan diğer paketlere yönelik başvurular da dahil olmak üzere, paketleme sırasında değişen *belirteçleri* , projedeki değerlerle birlikte içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="7193e-229">*. Nuspec*içine dahil edilecek paket bağımlılıklarınız varsa, kullanın `nuget pack`ve. nuspec dosyasını oluşturulan *. nupkg* dosyasından alın.</span><span class="sxs-lookup"><span data-stu-id="7193e-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="7193e-230">Örneğin, aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7193e-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="7193e-231">Belirteç, proje özelliğinin her `$` iki tarafında da semboller tarafından sınırlandırılır.</span><span class="sxs-lookup"><span data-stu-id="7193e-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="7193e-232">Örneğin, `<id>` bu şekilde oluşturulan bir bildirimin değeri, genellikle aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="7193e-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="7193e-233">Bu belirteç, paket zamanında proje `AssemblyName` dosyasındaki değerle değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7193e-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="7193e-234">Proje değerlerinin `.nuspec` belirteçlere tam eşlemesi için, [değiştirme belirteçleri başvurusuna](../reference/nuspec.md#replacement-tokens)bakın.</span><span class="sxs-lookup"><span data-stu-id="7193e-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="7193e-235">Belirteçler, projeyi güncelleştirmediğiniz gibi önemli değerleri, `.nuspec` içindeki sürüm numarası gibi güncelleştirmek zorunda kalduymasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="7193e-236">(İsterseniz belirteçleri, her zaman değişmez değerlerle değiştirebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="7193e-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="7193e-237">Visual Studio projesinden çalışırken, daha sonra [. nupkg dosyasını oluşturmak için NuGet paketini çalıştırma](#run-nuget-pack-to-generate-the-nupkg-file) bölümünde açıklandığı gibi, bir Visual Studio projesinden çalışırken kullanılabilecek birkaç ek paketleme seçeneği olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7193e-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="7193e-238">Çözüm düzeyi paketler</span><span class="sxs-lookup"><span data-stu-id="7193e-238">Solution-level packages</span></span>

<span data-ttu-id="7193e-239">*Yalnızca NuGet 2. x. NuGet 3.0 + ' da kullanılamaz.*</span><span class="sxs-lookup"><span data-stu-id="7193e-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="7193e-240">NuGet 2. x, Paket Yöneticisi konsolu için araçlar veya ek komutlar ( `tools` klasörün içeriği) yükleyen, ancak başvuru, içerik veya özelleştirmeleri hiçbir projeye ekleme çözümden.</span><span class="sxs-lookup"><span data-stu-id="7193e-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="7193e-241">Bu tür paketler doğrudan `lib`, `content`veya `build` klasörlerinde hiçbir dosya içermez ve bağımlılıklarından hiçbirinin ilgili `lib`, `content`veya `build` klasörlerinde dosyaları yoktur.</span><span class="sxs-lookup"><span data-stu-id="7193e-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="7193e-242">NuGet, çözüm düzeyindeki paketleri proje `packages.config` `packages.config` dosyası yerine `.nuget` klasöründe bulunan bir dosyada izler.</span><span class="sxs-lookup"><span data-stu-id="7193e-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="7193e-243">Varsayılan değerlere sahip yeni dosya</span><span class="sxs-lookup"><span data-stu-id="7193e-243">New file with default values</span></span>

<span data-ttu-id="7193e-244">Aşağıdaki komut, uygun dosya yapısıyla başlayabilmenizi sağlayan yer tutucuları olan varsayılan bir bildirim oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7193e-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="7193e-245">Paket adını \<\>atlarsanız, elde edilen dosya olur `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7193e-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="7193e-246">Gibi bir ad `Contoso.Utility.UsefulStuff`sağlarsanız, dosya olur `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="7193e-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="7193e-247">Sonuç `.nuspec` olarak, `projectUrl`gibi değerler için yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="7193e-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="7193e-248">Son `.nupkg` dosyayı oluşturmak için dosyayı kullanmadan önce düzenlendiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7193e-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="7193e-249">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarla</span><span class="sxs-lookup"><span data-stu-id="7193e-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="7193e-250">Paket tanımlayıcısı (`<id>` öğe) ve sürüm numarası (`<version>` öğe), pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından, bildirimdeki en önemli iki değerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="7193e-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="7193e-251">**Paket tanımlayıcısı için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="7193e-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="7193e-252">**Benzersizlik**: Tanımlayıcının nuget.org genelinde benzersiz olması veya paketi barındırdığı bir galeri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7193e-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="7193e-253">Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın.</span><span class="sxs-lookup"><span data-stu-id="7193e-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="7193e-254">Çakışmaları önlemek için iyi bir model, tanımlayıcı `Contoso.`ilk parçası olarak şirketinizin adını kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="7193e-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="7193e-255">**Ad alanı benzeri adlar**: Kısa çizgi yerine nokta gösterimini kullanarak .NET 'teki ad alanlarına benzer bir model izleyin.</span><span class="sxs-lookup"><span data-stu-id="7193e-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="7193e-256">Örneğin, `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` veya yerinekullanın.`Contoso_Utility_UsefulStuff`</span><span class="sxs-lookup"><span data-stu-id="7193e-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="7193e-257">Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.</span><span class="sxs-lookup"><span data-stu-id="7193e-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="7193e-258">**Örnek paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, ' de `.Sample` `Contoso.Utility.UsefulStuff.Sample`olduğu gibi, tanımlayıcıda bir sonek olarak iliştirme.</span><span class="sxs-lookup"><span data-stu-id="7193e-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="7193e-259">(Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7193e-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="7193e-260">Klasöründe, örnek kodu içinde `\Samples\Contoso.Utility.UsefulStuff.Sample`olarak adlandırılan `\Samples\<identifier>` bir klasörde düzenleyin. `content`</span><span class="sxs-lookup"><span data-stu-id="7193e-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="7193e-261">**Paket sürümü için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="7193e-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="7193e-262">Genel olarak, paketin sürümünü kitaplıkla eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7193e-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="7193e-263">Bu, [Hangi derlemelerin paketlenecek olduğuna karar verirken](#decide-which-assemblies-to-package)daha önce açıklandığı gibi, bir paketi tek bir derlemeyle sınırlandırdığınızda bu basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="7193e-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="7193e-264">Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7193e-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="7193e-265">Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../concepts/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7193e-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="7193e-266">Aşağıdaki kısa blog gönderisi serisi, sürüm oluşturmayı anlamak için de yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="7193e-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="7193e-267">Bölüm 1: DLL Hell 'i alma</span><span class="sxs-lookup"><span data-stu-id="7193e-267">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="7193e-268">Bölüm 2: Çekirdek algoritması</span><span class="sxs-lookup"><span data-stu-id="7193e-268">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="7193e-269">Bölüm 3: Bağlama yeniden yönlendirmeleri aracılığıyla birleşme</span><span class="sxs-lookup"><span data-stu-id="7193e-269">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="7193e-270">Benioku dosyası ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="7193e-270">Add a readme and other files</span></span>

<span data-ttu-id="7193e-271">Pakete dahil edilecek dosyaları doğrudan belirtmek `<files>` için, `.nuspec` `<metadata>` dosyasında etiketini *takip* eden düğümünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="7193e-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="7193e-272">Kural tabanlı çalışma dizini yaklaşımını kullanırken Readme. txt dosyasını paket köküne ve `content` klasördeki diğer içeriklere yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="7193e-273">Bildirimde `<file>` hiçbir öğe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7193e-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="7193e-274">Paket kökünde adlı `readme.txt` bir dosyayı dahil ettiğinizde, Visual Studio Paketi doğrudan yükledikten hemen sonra bu dosyanın içeriğini düz metin olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7193e-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="7193e-275">(Benioku dosyaları, bağımlılıklar olarak yüklenen paketler için gösterilmez).</span><span class="sxs-lookup"><span data-stu-id="7193e-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="7193e-276">Örneğin, HtmlAgilityPack paketinin Benioku dosyası şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="7193e-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için Benioku dosyası görüntüleme](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="7193e-278">Dosyada boş `<files>` bir düğüm `lib` eklerseniz, NuGet, pakette bulunan ve bu klasördeki diğer içerikleri içermez. `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="7193e-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="7193e-279">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="7193e-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="7193e-280">Bazı durumlarda, özel bir araç veya derleme sırasında işlem çalıştırma gibi paketinizi kullanan projelere özel yapı hedefleri veya özellikler eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="7193e-281">Bu, dosyaları `<package_id>.targets` forma veya `<package_id>.props` ( `Contoso.Utility.UsefulStuff.targets`gibi) projenin klasörü içine yerleştirerek yapabilirsiniz. `\build`</span><span class="sxs-lookup"><span data-stu-id="7193e-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="7193e-282">Kök `\build` klasördeki dosyalar tüm hedef çerçeveler için uygun kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="7193e-283">Çerçeveye özgü dosyalar sağlamak için, önce bunları aşağıdaki gibi uygun alt klasörlere yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="7193e-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="7193e-284">Ardından dosyada, `<files>` düğümdeki bu dosyalara başvurduğunuzdan emin olun: `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="7193e-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="7193e-285">Bir paketteki MSBuild props ve hedefleri de dahil olmak üzere [NuGet 2,5 ile birlikte sunulmuştur](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). bu nedenle, paketi kullanmak `minClientVersion="2.5"` için gereken en `metadata` düşük NuGet istemci sürümünü göstermek için özniteliğini öğesine eklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="7193e-286">NuGet dosyaları içeren `\build` bir paket yüklediğinde `.targets` , ve `.props` dosyalarını gösteren proje `<Import>` dosyasına MSBuild öğeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="7193e-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="7193e-287">(`.props` proje dosyasının en üstüne eklenir; `.targets` en alta eklenir.) Her hedef çerçeve için `<Import>` ayrı bir koşullu MSBuild öğesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="7193e-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="7193e-288">Çapraz `.props` çerçeve `.targets` hedefleme için MSBuild ve dosyalar `\buildMultiTargeting` klasöre yerleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="7193e-289">Paket yüklemesi sırasında, NuGet ilgili `<Import>` öğeleri koşul ile proje dosyasına ekler; hedef Framework ayarlanmadı (MSBuild özelliği `$(TargetFramework)` boş olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="7193e-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="7193e-290">NuGet 3. x ile, hedefleri projeye eklenmez, ancak bunun yerine `{projectName}.nuget.g.targets` ve `{projectName}.nuget.g.props`ile kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="7193e-291">. Nupkg dosyasını oluşturmak için NuGet paketini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7193e-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="7193e-292">Bir bütünleştirilmiş kod veya kural tabanlı çalışma dizini kullanırken, `nuget pack` `.nuspec` dosyanıza çalıştırarak, özel dosya adı ile değiştirerek `<project-name>` bir paket oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7193e-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="7193e-293">Bir Visual Studio projesi kullanırken, proje dosyasını `nuget pack` otomatik olarak yükleyen `.nuspec` ve proje dosyasındaki değerleri kullanarak onun içindeki belirteçleri değiştiren proje dosyası ile çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7193e-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="7193e-294">Projenin belirteç değerlerinin kaynağı olduğundan, belirteç değişikliği için proje dosyasını doğrudan kullanmak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7193e-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="7193e-295">`nuget pack` Bir`.nuspec` dosya ile kullanırsanız belirteç değiştirme gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="7193e-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="7193e-296">Her durumda, `nuget pack` `.git` veya `.hg`gibi bir noktayla başlayan klasörleri dışlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="7193e-297">NuGet, `.nuspec` dosyada düzeltilmesi gereken herhangi bir hata olup olmadığını gösterir (bildirimin yer tutucu değerlerini değiştirme gibi).</span><span class="sxs-lookup"><span data-stu-id="7193e-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="7193e-298">Başarılı `nuget pack` olduktan sonra, [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi uygun bir galeride yayımlayacağınız bir `.nupkg` dosyanız vardır.</span><span class="sxs-lookup"><span data-stu-id="7193e-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="7193e-299">Paketi oluşturduktan sonra, [Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracında açmak için yararlı bir yol.</span><span class="sxs-lookup"><span data-stu-id="7193e-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="7193e-300">Bu, paket içeriklerinin ve bildiriminin grafik görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="7193e-301">Ayrıca, elde edilen `.nupkg` dosyayı bir `.zip` dosya olarak yeniden adlandırabilir ve içeriğini doğrudan keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="7193e-302">Ek seçenekler</span><span class="sxs-lookup"><span data-stu-id="7193e-302">Additional options</span></span>

<span data-ttu-id="7193e-303">Dosyaları dışlamak, bildirimdeki sürüm numarasını geçersiz kılmak ve `nuget pack` diğer özelliklerin yanı sıra çıkış klasörünü değiştirmek için ile çeşitli komut satırı anahtarlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="7193e-304">Tüm liste için, [paket komut başvurusuna](../reference/cli-reference/cli-ref-pack.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7193e-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="7193e-305">Aşağıdaki seçenekler, Visual Studio projeleriyle yaygın olarak karşılaşılan birkaç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="7193e-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="7193e-306">**Başvurulan projeler**: Proje diğer projelere başvuruyorsa, bu `-IncludeReferencedProjects` seçeneği kullanarak başvurulan projeleri paketin parçası olarak veya bağımlılıklar olarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7193e-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="7193e-307">Bu içerme işlemi özyinelemeli `MyProject.csproj` olduğundan, b ve c projeleri ve bu projeler D, e ve f 'ye başvuruyorsa, b, C, D, E ve f 'ye ait dosyalar pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="7193e-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="7193e-308">Başvurulan bir proje kendi `.nuspec` dosyasını içeriyorsa, NuGet bu başvurulan projeyi bunun yerine bağımlılık olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="7193e-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="7193e-309">Bu projeyi ayrı ayrı paketleyip yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7193e-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="7193e-310">**Derleme yapılandırması**: Varsayılan olarak, NuGet proje dosyasında varsayılan derleme yapılandırma kümesini kullanır, genellikle *hata ayıklayın*.</span><span class="sxs-lookup"><span data-stu-id="7193e-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="7193e-311">*Yayın*gibi farklı bir derleme yapılandırmasından dosyaları paketetmek için, bu `-properties` seçeneği yapılandırmayla birlikte kullanın:</span><span class="sxs-lookup"><span data-stu-id="7193e-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="7193e-312">**Semboller**: tüketicilerin hata ayıklayıcıdaki paket kodunuzda ilerlemenize izin veren sembolleri dahil etmek için şu `-Symbols` seçeneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7193e-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="7193e-313">Test paketi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="7193e-313">Test package installation</span></span>

<span data-ttu-id="7193e-314">Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="7193e-315">Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="7193e-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="7193e-316">Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="7193e-317">Otomatikleştirilmiş test için temel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7193e-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="7193e-318">`.nupkg` Dosyayı yerel bir klasöre kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7193e-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="7193e-319">`nuget sources add -name <name> -source <path>` Komutunu kullanarak, klasörü paket kaynaklarınıza ekleyin (bkz. [NuGet kaynakları](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="7193e-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="7193e-320">Bu yerel kaynağı yalnızca belirli bir bilgisayarda bir kez ayarlamanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7193e-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="7193e-321">Bu kaynaktan paketi, kaynağına verildiği `nuget install <packageID> -source <name>` `nuget sources`şekilde kaynağınızın `<name>` adıyla eşleşen yeri kullanarak yükler.</span><span class="sxs-lookup"><span data-stu-id="7193e-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="7193e-322">Kaynağı belirtmek paketin o kaynaktan yalnızca yüklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7193e-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="7193e-323">Dosyaların doğru şekilde yüklenip yüklenmediğini denetlemek için dosya sisteminizi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7193e-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7193e-324">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="7193e-324">Next Steps</span></span>

<span data-ttu-id="7193e-325">Bir `.nupkg` dosya olan bir paket oluşturduktan sonra, bir [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7193e-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="7193e-326">Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7193e-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="7193e-327">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="7193e-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7193e-328">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="7193e-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7193e-329">Kaynak ve yapılandırma dosyalarının dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="7193e-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="7193e-330">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="7193e-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="7193e-331">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="7193e-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="7193e-332">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="7193e-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="7193e-333">COM birlikte çalışma Derlemeleriyle paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="7193e-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="7193e-334">Son olarak, bilmeniz için ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="7193e-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="7193e-335">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="7193e-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="7193e-336">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="7193e-336">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
