---
title: nuget.exe CLI kullanarak bir NuGet paketi oluşturun
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428949"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="46990-103">nuget.exe CLI kullanarak bir paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="46990-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="46990-104">Paketiniz ne yaparsa yapsın veya hangi kodu içerse içersin, `dotnet.exe`bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene dönüştürmek için CLI araçlarından `nuget.exe` birini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="46990-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="46990-105">NuGet CLI araçlarını yüklemek için [NuGet istemci araçlarını yükleyin.](../install-nuget-client-tools.md)</span><span class="sxs-lookup"><span data-stu-id="46990-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="46990-106">Visual Studio'nun otomatik olarak bir CLI aracı içermediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46990-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="46990-107">Genellikle .NET Framework projeleri olan SDK tarzı olmayan projeler de bir paket oluşturmak için bu makalede açıklanan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="46990-108">Visual Studio ve `nuget.exe` CLI'yi kullanarak adım adım talimatlar için bir [.NET Framework paketi oluştur ve yayımla'ya](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="46990-109">[SDK stili biçimini](../resources/check-project-format.md)kullanan .NET Core ve .NET Standard projeleri ve diğer SDK tarzı projeler için [bkz.](creating-a-package-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="46990-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="46990-110">`packages.config` [PackageReference'a](../consume-packages/package-references-in-project-files.md)geçirilen projeler için [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.</span><span class="sxs-lookup"><span data-stu-id="46990-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="46990-111">Teknik olarak konuşursak, NuGet paketi, `.nupkg` uzantıyla birlikte yeniden adlandırılan ve içeriği belirli kurallarla eşleşen bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="46990-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="46990-112">Bu konu, bu kuralları karşılayan bir paket oluşturma nın ayrıntılı işlemini açıklar.</span><span class="sxs-lookup"><span data-stu-id="46990-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="46990-113">Ambalaj, paket olarak sunmak istediğiniz derlenmiş kod (derlemeler), semboller ve/veya diğer dosyalarla başlar (bkz. [Genel Bakış ve iş akışı).](overview-and-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="46990-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="46990-114">Derlenen derlemeleri ve paketleri eşit tutmak için proje dosyasındaki bilgilerden yararlanabilmekle birlikte, bu işlem pakete giren dosyaları derlemekten veya başka bir şekilde oluşturmaktan bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="46990-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="46990-115">Bu konu, Visual Studio 2017 ve daha yüksek sürümler ve NuGet 4.0+ kullanarak genellikle .NET Core ve .NET Standard projeleri dışındaki projeler olan SDK tarzı olmayan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="46990-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="46990-116">Hangi derlemelerin paketlenenene karar vereceğine karar verin</span><span class="sxs-lookup"><span data-stu-id="46990-116">Decide which assemblies to package</span></span>

<span data-ttu-id="46990-117">Genel amaçlı paketlerin çoğu, diğer geliştiricilerin kendi projelerinde kullanabilecekleri bir veya daha fazla derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="46990-118">Genel olarak, her derlemenin bağımsız olarak yararlı olması koşuluyla, NuGet paketi başına bir derleme olması en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="46990-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="46990-119">Örneğin, kendi başına `Utilities.dll` buna bağlı `Parser.dll`ve `Parser.dll` yararlı olan bir paketiniz varsa, her biri için bir paket oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46990-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="46990-120">Bunu yapmak, geliştiricilerin `Parser.dll` `Utilities.dll`'' den bağımsız olarak kullanmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="46990-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="46990-121">Kitaplığınız bağımsız olarak yararlı olmayan birden çok derlemeden oluşuyorsa, bunları tek bir pakette birleştirmek te sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="46990-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="46990-122">Önceki örneği kullanarak, `Parser.dll` yalnızca kullanılan `Utilities.dll`kod içeriyorsa, aynı pakette `Parser.dll` tutmak iyidir.</span><span class="sxs-lookup"><span data-stu-id="46990-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="46990-123">Benzer şekilde, `Utilities.dll` eğer `Utilities.resources.dll`bağlıdır , nerede tekrar ikincisi kendi başına yararlı değildir, o zaman aynı pakette her ikisini de koyun.</span><span class="sxs-lookup"><span data-stu-id="46990-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="46990-124">Kaynaklar aslında özel bir durum.</span><span class="sxs-lookup"><span data-stu-id="46990-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="46990-125">Bir paket projeye yüklendiğinde, NuGet otomatik olarak yerelleştirilmiş uydu derlemeleri olarak *excluding* kabul edildikleri için `.resources.dll` adı geçenler hariç olmak üzere paketin DL'lerine montaj başvuruları ekler (bkz. [yerelleştirilmiş paketler oluşturma).](creating-localized-packages.md)</span><span class="sxs-lookup"><span data-stu-id="46990-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="46990-126">Bu nedenle, aksi `.resources.dll` takdirde temel paket kodu içeren dosyalar için kullanmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="46990-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="46990-127">Kitaplığınız COM interop derlemeleri içeriyorsa, [COM interop derlemeleri ile paketleri oluştur'daki](author-packages-with-com-interop-assemblies.md)ek yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="46990-128">.nuspec dosyasının rolü ve yapısı</span><span class="sxs-lookup"><span data-stu-id="46990-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="46990-129">Hangi dosyaları paketlemek istediğinizi bildiğinizde, bir sonraki adım `.nuspec` XML dosyasında bir paket bildirimi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="46990-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="46990-130">Manifesto:</span><span class="sxs-lookup"><span data-stu-id="46990-130">The manifest:</span></span>

1. <span data-ttu-id="46990-131">Paketin içeriğini açıklar ve paketin kendisi dahildir.</span><span class="sxs-lookup"><span data-stu-id="46990-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="46990-132">Paketin oluşturulmasını hem sürücüler hem de NuGet'e paketi projeye nasıl yükleyeceklerine ilişkin talimat verir.</span><span class="sxs-lookup"><span data-stu-id="46990-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="46990-133">Örneğin, bildirim, NuGet'in ana paket yüklendiğinde bu bağımlılıkları da yükleyebileceği diğer paket bağımlılıklarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="46990-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="46990-134">Aşağıda açıklandığı gibi hem gerekli hem de isteğe bağlı özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="46990-135">Burada belirtilmeyen diğer özellikler de dahil olmak üzere tam ayrıntılar için [.nuspec başvurusuna](../reference/nuspec.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="46990-136">Gerekli özellikler:</span><span class="sxs-lookup"><span data-stu-id="46990-136">Required properties:</span></span>

- <span data-ttu-id="46990-137">Paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="46990-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="46990-138">*Major.Minor.Patch[-Soneki]* formunda *-Sonek* ön sürüm [sürümlerini](prerelease-packages.md) tanımlayan belirli bir sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="46990-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="46990-139">Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="46990-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="46990-140">Yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="46990-140">Author and owner information.</span></span>
- <span data-ttu-id="46990-141">Paketin uzun bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="46990-141">A long description of the package.</span></span>

<span data-ttu-id="46990-142">Yaygın isteğe bağlı özellikler:</span><span class="sxs-lookup"><span data-stu-id="46990-142">Common optional properties:</span></span>

- <span data-ttu-id="46990-143">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="46990-143">Release notes</span></span>
- <span data-ttu-id="46990-144">Telif hakkı bilgileri</span><span class="sxs-lookup"><span data-stu-id="46990-144">Copyright information</span></span>
- <span data-ttu-id="46990-145">[Visual Studio'da Paket Yöneticisi UI](../consume-packages/install-use-packages-visual-studio.md) için kısa bir açıklama</span><span class="sxs-lookup"><span data-stu-id="46990-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="46990-146">Yerel kimlik</span><span class="sxs-lookup"><span data-stu-id="46990-146">A locale ID</span></span>
- <span data-ttu-id="46990-147">Proje URL'si</span><span class="sxs-lookup"><span data-stu-id="46990-147">Project URL</span></span>
- <span data-ttu-id="46990-148">İfade veya dosya olarak`licenseUrl` lisans (amortismana uymaktadır, [ `license` nuspec meta veri öğesini](../reference/nuspec.md#license)kullanın )</span><span class="sxs-lookup"><span data-stu-id="46990-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="46990-149">Simge URL'si</span><span class="sxs-lookup"><span data-stu-id="46990-149">An icon URL</span></span>
- <span data-ttu-id="46990-150">Bağımlılıklar ve referanslar listeleri</span><span class="sxs-lookup"><span data-stu-id="46990-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="46990-151">Galeri aramalarına yardımcı olan etiketler</span><span class="sxs-lookup"><span data-stu-id="46990-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="46990-152">Aşağıdaki özellikleri açıklayan yorumlar ile tipik `.nuspec` (ama hayali) bir dosya:</span><span class="sxs-lookup"><span data-stu-id="46990-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

<span data-ttu-id="46990-153">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılı bilgi için [packages.config](../reference/packages-config.md) ve [Package sürümüne](../concepts/package-versioning.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="46990-154">Ayrıca, öğedeki `include` öznitelikleri ve `exclude` öznitelikleri kullanarak varlıkları doğrudan paketteki bağımlılıklardan yüzeye çıkarmak da mümkündür. `dependency`</span><span class="sxs-lookup"><span data-stu-id="46990-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="46990-155">[Bkz..nuspec Başvuru - Bağımlılıklar](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="46990-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="46990-156">Bildirim, oluşturulan pakete dahil olduğundan, varolan paketleri inceleyerek istediğiniz sayıda ek örnek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="46990-157">İyi bir kaynak, bilgisayarınızdaki *genel paketler* klasörüdür ve konumu aşağıdaki komutla döndürülür:</span><span class="sxs-lookup"><span data-stu-id="46990-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="46990-158">Herhangi bir *paket\sürüm* klasörüne `.nupkg` gidin, `.zip` dosyayı bir `.zip` dosyaya `.nuspec` kopyalayın, sonra dosyayı açın ve dosyanın içini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="46990-159">Bir Visual `.nuspec` Studio projesinden bir oluşturma yaparken, bildirim, paket oluşturulduğunda projedeki bilgilerle değiştirilen belirteçler içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="46990-160">Bkz. [Bir Visual Studio projesinden .nuspec oluşturma.](#from-a-visual-studio-project)</span><span class="sxs-lookup"><span data-stu-id="46990-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="46990-161">.nuspec dosyasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="46990-161">Create the .nuspec file</span></span>

<span data-ttu-id="46990-162">Tam bir bildirim oluşturma genellikle `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan temel bir dosya ile başlar:</span><span class="sxs-lookup"><span data-stu-id="46990-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="46990-163">Kongre tabanlı çalışma dizini</span><span class="sxs-lookup"><span data-stu-id="46990-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="46990-164">Bir montaj DLL</span><span class="sxs-lookup"><span data-stu-id="46990-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="46990-165">Görsel Stüdyo projesi</span><span class="sxs-lookup"><span data-stu-id="46990-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="46990-166">Varsayılan değerlere sahip yeni dosya</span><span class="sxs-lookup"><span data-stu-id="46990-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="46990-167">Daha sonra, son pakette istediğiniz içeriği tam olarak açıklayabilmek için dosyayı elle düzenlemeniz.</span><span class="sxs-lookup"><span data-stu-id="46990-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="46990-168">Oluşturulan `.nuspec` `nuget pack` dosyalar, komutla paketi oluşturmadan önce değiştirilmesi gereken yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="46990-169">Herhangi bir yer `.nuspec` tutucu içeriyorsa bu komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="46990-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="46990-170">Sözleşme tabanlı çalışma dizininden</span><span class="sxs-lookup"><span data-stu-id="46990-170">From a convention-based working directory</span></span>

<span data-ttu-id="46990-171">NuGet paketi `.nupkg` yalnızca uzantıyla yeniden adlandırılabilen bir ZIP dosyası olduğundan, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmak `.nuspec` ve ardından dosyayı doğrudan bu yapıdan oluşturmak genellikle en kolayıdır.</span><span class="sxs-lookup"><span data-stu-id="46990-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="46990-172">Komut `nuget pack` daha sonra otomatik olarak bu klasör yapısına tüm dosyaları `.`ekler (ile başlayan tüm klasörler hariç , aynı yapıda özel dosyaları tutmak için izin).</span><span class="sxs-lookup"><span data-stu-id="46990-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="46990-173">Bu yaklaşımın avantajı, pakete hangi dosyaları eklemek istediğinizi (bu konuda daha sonra açıklandığı gibi) bildirimde belirtmeniz gerekmemelidir.</span><span class="sxs-lookup"><span data-stu-id="46990-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="46990-174">Yapı işleminizin pakete giren tam klasör yapısını oluşturmasını sağlayabilir ve aksi takdirde projenin parçası olmayan diğer dosyaları kolayca ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46990-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="46990-175">Hedef projeye enjekte edilmesi gereken içerik ve kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="46990-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="46990-176">PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="46990-176">PowerShell scripts</span></span>
- <span data-ttu-id="46990-177">Projedeki varolan yapılandırma ve kaynak kodu dosyalarına dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="46990-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="46990-178">Klasör kuralları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="46990-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="46990-179">Klasör</span><span class="sxs-lookup"><span data-stu-id="46990-179">Folder</span></span> | <span data-ttu-id="46990-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="46990-180">Description</span></span> | <span data-ttu-id="46990-181">Paket yükleme üzerine eylem</span><span class="sxs-lookup"><span data-stu-id="46990-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46990-182">(kök)</span><span class="sxs-lookup"><span data-stu-id="46990-182">(root)</span></span> | <span data-ttu-id="46990-183">readme.txt için konum</span><span class="sxs-lookup"><span data-stu-id="46990-183">Location for readme.txt</span></span> | <span data-ttu-id="46990-184">Visual Studio, paket yüklendiğinde paket kökünde bir readme.txt dosyası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="46990-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="46990-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="46990-185">lib/{tfm}</span></span> | <span data-ttu-id="46990-186">Verilen`.dll`Hedef Çerçeve`.xml`Takma (TFM) için Derleme ( ), belgeler ve sembol (`.pdb`) dosyaları</span><span class="sxs-lookup"><span data-stu-id="46990-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="46990-187">Derleme için referans olarak derleme ve çalışma zamanı olarak derleme derleme ler eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="46990-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="46990-188">Bkz. Çerçeve hedefe özgü alt klasörler oluşturmak için [birden çok hedef çerçeveyi destekleme.](supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="46990-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="46990-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="46990-189">ref/{tfm}</span></span> | <span data-ttu-id="46990-190">Verilen`.dll`Hedef Çerçeve`.pdb`Takma (TFM) için Montaj ( ), ve sembol ( ) dosyaları</span><span class="sxs-lookup"><span data-stu-id="46990-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="46990-191">Derlemeler yalnızca derleme süresi için referans olarak eklenir; Böylece hiçbir şey proje kutusu klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="46990-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="46990-192">Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="46990-192">runtimes</span></span> | <span data-ttu-id="46990-193">Mimariye özgü`.dll`derleme (`.pdb`), sembolü`.pri`( ), ve yerel kaynak ( ) dosyaları</span><span class="sxs-lookup"><span data-stu-id="46990-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="46990-194">Derlemeler yalnızca çalışma süresi için başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="46990-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="46990-195">Her zaman ilgili derleme zaman `AnyCPU` derlemesağlamak `/ref/{tfm}` için klasör altında karşılık gelen (TFM) özel bir derleme olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="46990-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="46990-196">Bkz. [Birden çok hedef çerçeveyi destekleme.](supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="46990-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="46990-197">content</span><span class="sxs-lookup"><span data-stu-id="46990-197">content</span></span> | <span data-ttu-id="46990-198">Rasgele dosyalar</span><span class="sxs-lookup"><span data-stu-id="46990-198">Arbitrary files</span></span> | <span data-ttu-id="46990-199">İçerikler proje köküne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="46990-199">Contents are copied to the project root.</span></span> <span data-ttu-id="46990-200">**İçerik** klasörünü, sonuçta paketi tüketen hedef uygulamanın kökü olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="46990-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="46990-201">Paketin uygulamanın */images* klasörüne bir resim eklemesini sağlamak için, paketin *içerik/resim* klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="46990-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="46990-202">derleme</span><span class="sxs-lookup"><span data-stu-id="46990-202">build</span></span> | <span data-ttu-id="46990-203">*(3.x+)* MSBuild `.targets` `.props` ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="46990-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="46990-204">Projeye otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="46990-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="46990-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="46990-205">buildMultiTargeting</span></span> | <span data-ttu-id="46990-206">*(4.0+)* MSBuild `.targets` `.props` ve çerçeveler arası hedefleme için dosyalar</span><span class="sxs-lookup"><span data-stu-id="46990-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="46990-207">Projeye otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="46990-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="46990-208">buildGeçişive</span><span class="sxs-lookup"><span data-stu-id="46990-208">buildTransitive</span></span> | <span data-ttu-id="46990-209">*(5.0+)* MSBuild `.targets` `.props` ve herhangi bir tüketen projeye geçişli olarak akan dosyalar.</span><span class="sxs-lookup"><span data-stu-id="46990-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="46990-210">[Özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="46990-211">Projeye otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="46990-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="46990-212">araçlar</span><span class="sxs-lookup"><span data-stu-id="46990-212">tools</span></span> | <span data-ttu-id="46990-213">Powershell komut dosyaları ve programlara Package Manager Konsolu'ndan erişilebiliyor</span><span class="sxs-lookup"><span data-stu-id="46990-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="46990-214">Klasör `tools` yalnızca Paket `PATH` Yöneticisi Konsolu için ortam değişkenine *not* eklenir `PATH` (özellikle, projeyi oluştururken MSBuild için ayarlanan aküme değil).</span><span class="sxs-lookup"><span data-stu-id="46990-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="46990-215">Klasör yapınız herhangi bir sayıda hedef çerçeve için herhangi bir sayıda derleme içerebileceğinden, birden çok çerçeveyi destekleyen paketler oluştururken bu yöntem gereklidir.</span><span class="sxs-lookup"><span data-stu-id="46990-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="46990-216">Her durumda, istediğiniz klasör yapısını yerleştirdikten sonra, dosyayı oluşturmak için `.nuspec` bu klasörde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46990-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="46990-217">Yine, oluşturulan `.nuspec` klasör yapısında dosyalara açık başvurular içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="46990-218">Paket oluşturulduğunda NuGet tüm dosyaları otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="46990-219">Ancak, yine de bildirimin diğer bölümlerinde yer tutucu değerlerini de yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46990-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="46990-220">Bir montaj DLL gönderen</span><span class="sxs-lookup"><span data-stu-id="46990-220">From an assembly DLL</span></span>

<span data-ttu-id="46990-221">Derlemeden paket oluşturma basit durumda, aşağıdaki komutu `.nuspec` kullanarak derlemedeki meta verilerden bir dosya oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46990-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="46990-222">Bu formu kullanmak, bildirimdeki birkaç yer tutucunun yerine derlemeden belirli değerler le birlikte çıkar.</span><span class="sxs-lookup"><span data-stu-id="46990-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="46990-223">Örneğin, `<id>` özellik derleme adına ayarlanır ve `<version>` derleme sürümüne ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="46990-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="46990-224">Ancak, bildirimdeki diğer özellikler derlemede eşleşen değerlere sahip değildir ve bu nedenle yine de yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="46990-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="46990-225">Görsel Stüdyo projesinden</span><span class="sxs-lookup"><span data-stu-id="46990-225">From a Visual Studio project</span></span>

<span data-ttu-id="46990-226">Bu `.nuspec` projeye `.csproj` yüklenen `.vbproj` diğer paketler otomatik olarak bağımlılık olarak başvurulduğundan, bir veya dosyadan bir dosya oluşturmak uygundur.</span><span class="sxs-lookup"><span data-stu-id="46990-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="46990-227">Proje dosyasıyla aynı klasörde aşağıdaki komutu kullanmanız yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="46990-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="46990-228">Ortaya çıkan `<project-name>.nuspec` dosya, paketleme sırasında projedeki değerlerle değiştirilen *belirteçler* içerir ve bu belirteçler, önceden yüklenmiş diğer paketlere yapılan atıflar da dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="46990-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="46990-229">*.nuspec'e*eklemek için paket bağımlılıklarınız `nuget pack`varsa, bunun yerine kullanın ve *.nuspec* dosyasını oluşturulan *.nupkg* dosyasının içinden alın.</span><span class="sxs-lookup"><span data-stu-id="46990-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="46990-230">Örneğin, aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="46990-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="46990-231">Bir belirteç, `$` proje özelliğinin her iki tarafındaki sembollerle sınırlandırılır.</span><span class="sxs-lookup"><span data-stu-id="46990-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="46990-232">Örneğin, bu `<id>` şekilde oluşturulan bir bildirimdeki değer genellikle aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="46990-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="46990-233">Bu belirteç, paketleme `AssemblyName` sırasında proje dosyasındaki değerle değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="46990-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="46990-234">Proje değerlerinin `.nuspec` belirteçlere tam eşlenemi [için, Yedek Belirteçler başvurusuna](../reference/nuspec.md#replacement-tokens)bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="46990-235">Belirteçler, projeyi `.nuspec` güncellediğiniz sürüm numarası gibi önemli değerleri güncelleştirmegereksinimini giderir.</span><span class="sxs-lookup"><span data-stu-id="46990-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="46990-236">(İstenirse belirteçleri her zaman gerçek değerlerle değiştirebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="46990-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="46990-237">Bir Visual Studio projesinde [çalışırken,.nupkg dosyasını](#run-nuget-pack-to-generate-the-nupkg-file) daha sonra oluşturmak için Running nuget paketinde açıklandığı gibi birkaç ek paketleme seçeneği nin mevcut olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46990-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="46990-238">Çözüm düzeyinde paketler</span><span class="sxs-lookup"><span data-stu-id="46990-238">Solution-level packages</span></span>

<span data-ttu-id="46990-239">*NuGet 2.x sadece. NuGet 3.0+ adresinde kullanılamaz.*</span><span class="sxs-lookup"><span data-stu-id="46990-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="46990-240">NuGet 2.x, Paket Yöneticisi Konsolu `tools` (klasörün içeriği) için araçlar veya ek komutlar yükleyen, ancak çözümdeki herhangi bir projeye referans, içerik eklemeyen veya özelleştirmeler oluşturmayan çözüm düzeyinde bir paket kavramını desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="46990-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="46990-241">Bu tür paketler `lib`doğrudan , `content`, `build` veya klasörlerinde hiçbir dosya içermez ve `lib`bağımlılıklarının hiçbirinde ilgili , `content`veya `build` klasörlerinde dosya bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="46990-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="46990-242">NuGet, yüklü çözüm düzeyi paketlerini `packages.config` projenin `.nuget` `packages.config` dosyası yerine klasördeki bir dosyada izler.</span><span class="sxs-lookup"><span data-stu-id="46990-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="46990-243">Varsayılan değerlere sahip yeni dosya</span><span class="sxs-lookup"><span data-stu-id="46990-243">New file with default values</span></span>

<span data-ttu-id="46990-244">Aşağıdaki komut, uygun dosya yapısıyla başlamanızı sağlayan yer tutucularla varsayılan bir bildirim oluşturur:</span><span class="sxs-lookup"><span data-stu-id="46990-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="46990-245">Paket adını \<\>atlarsanız, ortaya çıkan dosya `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="46990-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="46990-246">Gibi bir ad `Contoso.Utility.UsefulStuff`sağlarsanız, dosya `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="46990-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="46990-247">Elde edilen `.nuspec` yer tutucular. `projectUrl`</span><span class="sxs-lookup"><span data-stu-id="46990-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="46990-248">Son `.nupkg` dosyayı oluşturmak için kullanmadan önce dosyayı yeniden oluşturduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="46990-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="46990-249">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="46990-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="46990-250">Paket tanımlayıcısı (öğe)`<id>` ve sürüm numarası`<version>` (öğe) pakette bulunan tam kodu benzersiz olarak tanımladıkları için bildirimdeki en önemli iki değerdir.</span><span class="sxs-lookup"><span data-stu-id="46990-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="46990-251">**Paket tanımlayıcısı için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="46990-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="46990-252">**Teklik**: Tanımlayıcı, nuget.org veya pakete ev sahipliği yapan galeride benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="46990-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="46990-253">Tanımlayıcıya karar vermeden önce, adın zaten kullanIlip kullanılmadığını kontrol etmek için ilgili galeride arama yapın.</span><span class="sxs-lookup"><span data-stu-id="46990-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="46990-254">Çakışmaları önlemek için, iyi bir desen gibi tanımlayıcının ilk bölümü olarak şirket `Contoso.`adınızı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="46990-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="46990-255">**Ad alanı benzeri adlar**: Tire yerine nokta gösterimi kullanarak .NET'teki ad boşluklarına benzer bir desen izleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="46990-256">Örneğin, kullanmak `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`veya .</span><span class="sxs-lookup"><span data-stu-id="46990-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="46990-257">Tüketiciler, paket tanımlayıcısı kodda kullanılan ad alanlarıyla eşleştiğinde de yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="46990-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="46990-258">**Örnek Paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir `.Sample` örnek kod paketi üretirseniz, tanımlayıcıya sonek `Contoso.Utility.UsefulStuff.Sample`olarak iliştirin.</span><span class="sxs-lookup"><span data-stu-id="46990-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="46990-259">(Örnek paket elbette diğer pakete bağımlı olacaktır.) Örnek bir paket oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="46990-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="46990-260">Klasörde, `content` örnek kodu ' da `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`adlandırılan bir klasörde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="46990-261">**Paket sürümü için en iyi uygulamalar:**</span><span class="sxs-lookup"><span data-stu-id="46990-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="46990-262">Genel olarak, bu kesinlikle gerekli olmasa da, kitaplık maç için paketin sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="46990-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="46990-263">Bu, bir paketi tek bir derlemeyle sınırladığınızda, [hangi derlemelerin paketlenecene karar](#decide-which-assemblies-to-package)verirken açıklandığı gibi basit bir konudur.</span><span class="sxs-lookup"><span data-stu-id="46990-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="46990-264">Genel olarak, NuGet'in derleme sürümlerini değil, bağımlılıkları çözerken paket sürümleriyle ilgili olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46990-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="46990-265">Standart olmayan bir sürüm şeması kullanırken, [Paket sürümde](../concepts/package-versioning.md)açıklandığı gibi NuGet sürüm kurallarını dikkate almayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46990-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="46990-266">Kısa blog gönderileri aşağıdaki dizi de sürüm anlamak için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="46990-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="46990-267">Bölüm 1: DLL Hell alma</span><span class="sxs-lookup"><span data-stu-id="46990-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="46990-268">Bölüm 2: Çekirdek algoritması</span><span class="sxs-lookup"><span data-stu-id="46990-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="46990-269">Bölüm 3: Bağlayıcı Yönlendirmelerle Birleşme</span><span class="sxs-lookup"><span data-stu-id="46990-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="46990-270">Okuma mem ve diğer dosyalar ekleme</span><span class="sxs-lookup"><span data-stu-id="46990-270">Add a readme and other files</span></span>

<span data-ttu-id="46990-271">Pakete dahil olacak dosyaları doğrudan belirtmek `<files>` için, `.nuspec` `<metadata>` etiketi *izleyen* dosyadaki düğümü kullanın:</span><span class="sxs-lookup"><span data-stu-id="46990-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="46990-272">Kural tabanlı çalışma dizini yaklaşımını kullanırken, readme.txt'yi paket köküne ve `content` diğer içeriğe klasöre yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="46990-273">Bildirimde hiçbir öğe gerekli değildir. `<file>`</span><span class="sxs-lookup"><span data-stu-id="46990-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="46990-274">Paket köküne bir `readme.txt` dosya eklediğinizde, Visual Studio paketi doğrudan yükledikten hemen sonra dosyanın içeriğini düz metin olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="46990-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="46990-275">(Bağımlılık olarak yüklenen paketler için Okuma dosyaları görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="46990-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="46990-276">Örneğin, HtmlAgilityPack paketinin okuma sı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="46990-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme üzerine NuGet paketi için okuma dosyasının görüntülenmesi](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="46990-278">Dosyaya boş `<files>` bir düğüm eklerseniz, NuGet `lib` pakete klasördekinden başka içerik eklemez. `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="46990-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="46990-279">MSBuild sahne ve hedeflerini bir pakete dahil et</span><span class="sxs-lookup"><span data-stu-id="46990-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="46990-280">Bazı durumlarda, paketinizi tüketen projelere (örneğin, yapı sırasında özel bir araç veya işlem çalıştırmak gibi) özel yapı hedefleri veya özellikleri eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="46990-281">`<package_id>.targets` Bunu, dosyaları projeye `<package_id>.props` veya (örneğin) `Contoso.Utility.UsefulStuff.targets`proje `\build` klasörüne yerleştirerek yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="46990-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="46990-282">Kök `\build` klasördeki dosyalar tüm hedef çerçeveler için uygun kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="46990-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="46990-283">Çerçeveye özgü dosyaları sağlamak için, öncelikle bunları aşağıdakiler gibi uygun alt klasörlere yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="46990-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="46990-284">Daha sonra `.nuspec` dosyada, `<files>` düğümdeki bu dosyalara başvurup bakın:</span><span class="sxs-lookup"><span data-stu-id="46990-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="46990-285">Bir pakette MSBuild sahne ve hedefleri dahil [NuGet 2.5 ile tanıtıldı](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), `minClientVersion="2.5"` bu nedenle `metadata` paketi tüketmek için gerekli minimum NuGet istemci sürümü belirtmek için, öğeözeklemek için tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="46990-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="46990-286">NuGet `\build` dosyaları içeren bir paket yüklediğinde, `<Import>` proje dosyasına `.props` ve `.targets` dosyaları işaret eden MSBuild öğeleri ni ekler.</span><span class="sxs-lookup"><span data-stu-id="46990-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="46990-287">(`.props` proje dosyasının üst kısmında eklenir; `.targets` alt kısmında eklenir.) Her hedef çerçeve `<Import>` için ayrı bir koşullu MSBuild öğesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="46990-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="46990-288">MSBuild `.props` `.targets` ve çerçeveler arası hedefleme dosyaları `\buildMultiTargeting` klasöre yerleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="46990-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="46990-289">Paket yükleme sırasında NuGet, `<Import>` hedef çerçevenin ayarlanmadığını (MSBuild özelliğinin `$(TargetFramework)` boş olması gerekir) koşuluyla proje dosyasına karşılık gelen öğeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="46990-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="46990-290">NuGet 3.x ile hedefler projeye eklenmez, bunun `{projectName}.nuget.g.targets` yerine `{projectName}.nuget.g.props`kullanılabilir hale getirilir ve .</span><span class="sxs-lookup"><span data-stu-id="46990-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="46990-291">.nupkg dosyasını oluşturmak için nuget paketini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="46990-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="46990-292">Bir derleme veya kural tabanlı çalışma dizini kullanırken, `nuget pack` dosyanızla `.nuspec` birlikte `<project-name>` çalışarak, belirli dosya adınızı değiştirerek bir paket oluşturun:</span><span class="sxs-lookup"><span data-stu-id="46990-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="46990-293">Visual Studio projesi kullanırken, proje `nuget pack` `.nuspec` dosyasını otomatik olarak yükleyen ve proje dosyasındaki değerleri kullanarak içindeki belirteçleri değiştiren proje dosyanızla çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="46990-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="46990-294">Proje belirteç değerlerinin kaynağı olduğundan, proje dosyasının doğrudan belirteç değişimi için kullanılması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="46990-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="46990-295">Bir `nuget pack` `.nuspec` dosyayla kullanırsanız belirteç değiştirme gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="46990-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="46990-296">Her durumda, `nuget pack` bir dönemle başlayan klasörleri hariç `.git` `.hg`tutar, örneğin.</span><span class="sxs-lookup"><span data-stu-id="46990-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="46990-297">NuGet, `.nuspec` dosyada düzeltmesi gereken (örneğin, bildirimdeki yer tutucu değerlerini değiştirmeyi unutmagibi) herhangi bir hata olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="46990-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="46990-298">Başarılı `nuget pack` olduktan sonra, `.nupkg` [Paketi Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi uygun bir galeride yayımlayabileceğiniz bir dosyanız vardır.</span><span class="sxs-lookup"><span data-stu-id="46990-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="46990-299">Bir paketi oluşturduktan sonra incelemenin yararlı bir yolu, [paketi Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracında açmaktır.</span><span class="sxs-lookup"><span data-stu-id="46990-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="46990-300">Bu, paket içeriğinin ve manifestosunun grafiksel bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="46990-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="46990-301">Ayrıca, ortaya çıkan `.nupkg` dosyayı bir `.zip` dosyaya yeniden adlandırabilir ve içeriğini doğrudan keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="46990-302">Ek seçenekler</span><span class="sxs-lookup"><span data-stu-id="46990-302">Additional options</span></span>

<span data-ttu-id="46990-303">Dosyaları hariç tutmak, bildirimdeki `nuget pack` sürüm numarasını geçersiz kılmak ve diğer özelliklerin yanı sıra çıktı klasörünü değiştirmek için çeşitli komut satırı anahtarlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="46990-304">Tam liste için paket [komutu başvurusuna](../reference/cli-reference/cli-ref-pack.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="46990-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="46990-305">Aşağıdaki seçenekler Visual Studio projeleri ile ortak birkaçıdır:</span><span class="sxs-lookup"><span data-stu-id="46990-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="46990-306">**Başvurulan projeler**: Proje diğer projelere başvuruyorsa, başvurulan projeleri paketin bir parçası olarak `-IncludeReferencedProjects` veya bağımlılık olarak, seçeneği kullanarak ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46990-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="46990-307">Bu ekleme işlemi özyinelemelidir, `MyProject.csproj` bu nedenle başvurular B ve C projeleri yse ve bu projeler D, E ve F'ye başvuruyorsa, B, C, D, E ve F'den dosyalar pakete dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="46990-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="46990-308">Başvurulan bir `.nuspec` proje kendi dosyasını içeriyorsa, NuGet başvurulan projeyi bağımlılık olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="46990-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="46990-309">Bu projeyi ayrı olarak paketlemeniz ve yayınlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="46990-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="46990-310">**Yapı yapılandırması**: NuGet varsayılan olarak proje dosyasındaki varsayılan yapı yapılandırma kümesini kullanır, genellikle *Hata Ayıklama.*</span><span class="sxs-lookup"><span data-stu-id="46990-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="46990-311">*Sürüm*gibi farklı bir yapı yapılandırmasından dosyaları `-properties` paketlemek için yapılandırma seçeneğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="46990-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="46990-312">**Semboller**: tüketicilerin paket kodunuzu hata ayıklayıcıya eklemesine olanak `-Symbols` tanıyan sembolleri eklemek için aşağıdaki seçeneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="46990-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="46990-313">Test paketi kurulumu</span><span class="sxs-lookup"><span data-stu-id="46990-313">Test package installation</span></span>

<span data-ttu-id="46990-314">Paket yayımlamadan önce, genellikle bir projeye paket yükleme işlemini sınamak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="46990-315">Testler, zorunlu dosyaların tümünden inin projedeki doğru yerlerinde sonunun olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="46990-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="46990-316">Yüklemeleri Visual Studio'da veya komut satırında normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="46990-317">Otomatik sınama için temel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="46990-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="46990-318">Dosyayı `.nupkg` yerel bir klasöre kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="46990-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="46990-319">Komutu kullanarak `nuget sources add -name <name> -source <path>` klasörü paket kaynaklarınıza ekleyin [(nuget kaynaklarına](../reference/cli-reference/cli-ref-sources.md)bakın).</span><span class="sxs-lookup"><span data-stu-id="46990-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="46990-320">Bu yerel kaynağı herhangi bir bilgisayarda yalnızca bir kez ayarlamanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46990-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="46990-321">Verilen kaynağınızın adı `nuget install <packageID> -source <name>` ile `<name>` eşleşen bir yerde kullanarak `nuget sources`paketi o kaynaktan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="46990-322">Kaynağın belirtilmesi, paketin tek başına o kaynaktan yüklenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="46990-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="46990-323">Dosyaların doğru yüklenmesini denetlemek için dosya sisteminizi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="46990-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46990-324">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="46990-324">Next Steps</span></span>

<span data-ttu-id="46990-325">Bir dosya olan bir `.nupkg` paket oluşturduktan sonra, paketi [Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi istediğiniz galeride yayınlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46990-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="46990-326">Ayrıca paketinizin yeteneklerini genişletmek veya aşağıdaki konularda açıklandığı gibi diğer senaryoları desteklemek de isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46990-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="46990-327">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="46990-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="46990-328">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="46990-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="46990-329">Kaynak ve yapılandırma dosyalarının dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="46990-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="46990-330">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="46990-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="46990-331">Ön sürüm sürümleri</span><span class="sxs-lookup"><span data-stu-id="46990-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="46990-332">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="46990-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="46990-333">COM interop montajları ile paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="46990-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="46990-334">Son olarak, dikkat edilmesi gereken ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="46990-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="46990-335">Yerli Paketler</span><span class="sxs-lookup"><span data-stu-id="46990-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="46990-336">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="46990-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
