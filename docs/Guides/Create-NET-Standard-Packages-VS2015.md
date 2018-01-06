---
title: "Visual Studio 2015 ile birlikte .NET standart NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "NuGet kullanarak .NET standart NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015."
keywords: "bir paket, .NET standart paketler, .NET standart eşleme tablosu oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="b5ac9-104">Visual Studio 2015 ile .NET standart paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="b5ac9-105">*Nuget'e geçerlidir 3.x. Bkz: [oluşturma .NET standart paketlerle Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) NuGet 4.x+ ile çalışmak için.*</span><span class="sxs-lookup"><span data-stu-id="b5ac9-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="b5ac9-106">[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="b5ac9-107">.NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="b5ac9-108">Bunu tüm .NET çalışma zamanları arasında kullanılabilir PCLs üretmek için geliştiricilere olanak sağlar ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="b5ac9-109">Bu kılavuz .NET standart kitaplığı 1.4 hedefleyen bir nuget paketi oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="b5ac9-110">Bu, .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin çalışır.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="b5ac9-111">Ayrıntılar için bkz [.NET standart eşleme tablosu](#net-standard-mapping-table) bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="b5ac9-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5ac9-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="b5ac9-113">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="b5ac9-114">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="b5ac9-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="b5ac9-115">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="b5ac9-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="b5ac9-116">Ek Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b5ac9-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="b5ac9-117">.NET standart eşleme tablosu</span><span class="sxs-lookup"><span data-stu-id="b5ac9-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="b5ac9-118">İlgili Konular</span><span class="sxs-lookup"><span data-stu-id="b5ac9-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="b5ac9-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5ac9-119">Pre-requisites</span></span>

1. <span data-ttu-id="b5ac9-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-120">Visual Studio 2015.</span></span> <span data-ttu-id="b5ac9-121">Community edition ücretsiz yükleyin [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="b5ac9-122">.NET core: Install şablonları birlikte .NET Core ve diğer araçları Visual Studio 2015'ten [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="b5ac9-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="b5ac9-123">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-123">NuGet CLI.</span></span> <span data-ttu-id="b5ac9-124">Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="b5ac9-125">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="b5ac9-126">nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="b5ac9-127">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-127">Create the class library project</span></span>

1. <span data-ttu-id="b5ac9-128">Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, select **sınıf kitaplığı (taşınabilir)**AppLogger için adı değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Yeni sınıf kitaplığı proje oluşturma](media/NetStandard-NewProject.png)

1. <span data-ttu-id="b5ac9-130">İçinde **taşınabilir sınıf kitaplığı eklemek** görünen seçin iletişim `.NET Framework 4.6` ve `ASP.NET Core 1.0` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="b5ac9-131">Sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesini ve ardından **hedef .NET Platform standardını** içinde**Hedefleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="b5ac9-132">Bu daha sonra seçebileceğiniz onaylama için ister `.NET Standard 1.4` açılır:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Hedef .NET standart 1.4 ayarlama](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="b5ac9-134">Tıklayın **yapı** sekmesinde, değiştirmek **yapılandırma** için `Release`ve için kutuyu **XML belge dosyası**.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="b5ac9-135">Kodunuzu bileşenine örneğin ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="b5ac9-136">(Sürüm yapılandırmasıyla) projeyi oluşturun ve DLL ve XML dosyaları bin\Release klasör içinde üretilir denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="b5ac9-137">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="b5ac9-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="b5ac9-138">Bir komut istemi açın, içeren klasöre gidin `AppLogg.csproj` klasörü (bir düzey altındaki where `.sln` dosyası), NuGet çalıştırıp `spec` ilk oluşturmak için komutu `AppLogger.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="b5ac9-139">Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="b5ac9-140">`<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="b5ac9-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="b5ac9-141">Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata iletisi alırsınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="b5ac9-142">Başvuru derlemeleri eklemek `.nuspec` dosya, kitaplığın DLL ve IntelliSense XML dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="b5ac9-143">Çözüme sağ tıklayın ve seçin **yapı çözümü** bir paket için tüm dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="b5ac9-144">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="b5ac9-144">Package the component</span></span>

<span data-ttu-id="b5ac9-145">Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="b5ac9-146">Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="b5ac9-147">Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet paket AppLogger paket gösteren Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="b5ac9-149">A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="b5ac9-150">Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="b5ac9-151">Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b5ac9-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="b5ac9-152">Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="b5ac9-153">Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="b5ac9-154">Ek Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b5ac9-154">Additional options</span></span>

<span data-ttu-id="b5ac9-155">NuGet paket oluşturma için ek seçenekler içine aşağıdaki bölümlerde gidin:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="b5ac9-156">Bağımlılıklar bildirme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="b5ac9-157">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="b5ac9-158">MSBuild hedefleri ve özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="b5ac9-159">Yerelleştirilmiş paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="b5ac9-160">Bir benioku dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="b5ac9-161">Bağımlılıklar bildirme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-161">Declaring dependencies</span></span>

<span data-ttu-id="b5ac9-162">Diğer NuGet paketlerini bağımlılıkları varsa de listesinde `<dependencies>` öğeyle `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="b5ac9-163">Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya üstü bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="b5ac9-164">Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir ya da yukarıdaki kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="b5ac9-165">Farklı bir sürüm aralıklarını belirtmek için başvurmak [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b5ac9-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="b5ac9-166">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="b5ac9-167">.NET Framework'teki .NET standart 1.4 içinde kullanılabilir olmayan 4.6.2 bir API avantajlarından yararlanmak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="b5ac9-168">Bunu yapmak için öncelikle koşullu derleme veya paylaşılan projeleri kullanarak kitaplığı için .NET 4.6.2 derlendiğinden emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="b5ac9-169">(Visual Studio'da NetCore projesi oluşturun, tercih ettiğiniz framework birden çok framework bölümüne ekleyin, oluşturmak ve bunları kullanabileceğiniz ardından.) Ardından aşağıdaki gibi basit kurala dayalı çalışma dizini tekniği kullanarak paketi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="b5ac9-170">Projede kullanıcının kök klasörünü içeren, `.nuspec` adlı bir klasör oluşturun, dosya `lib`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="b5ac9-171">İçinde `lib`, desteklemek istediğiniz her platform için klasörleri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="b5ac9-172">İçinde `.nuspec` dosya, ekleme bir `files` düğümü altında `package` düğümü ve dosyaları başvurmak `lib` joker karakterleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="b5ac9-173">**Not:** belirteci değişikliklerini kurala dayalı çalışma dizini yaklaşımda desteklenmiyor, bu nedenle bunları hazır değer ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b5ac9-174">Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="b5ac9-175">Bu yöntemi kullanma hakkında daha fazla ayrıntı için bkz: [destekleyen birden çok .NET Framework sürümü](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="b5ac9-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="b5ac9-176">MSBuild hedefleri ve özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="b5ac9-177">Bazı durumlarda özel aracın veya işlemin derleme sırasında çalıştırma gibi paketinizi tüketen projelerine özel derleme hedefler ya da özellikleri eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="b5ac9-178">Dosyaları ekleyerek bunu bir `\build` aşağıdaki adımlarda açıklandığı gibi klasör.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="b5ac9-179">NuGet \build dosyalarıyla bir paketi yüklendiğinde, .targets ve .props dosyalarını işaret proje dosyasında bir MSBuild öğe ekler.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="b5ac9-180">Kullanırken `project.json`, hedefleri projeye eklenmez ancak kullanılabilir hale getirilir `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="b5ac9-181">Projeyi içeren klasörün içinde, `.nuspec` adlı bir klasör oluşturun, dosya `build`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="b5ac9-182">İçinde `build`, desteklenen her için klasörler oluşturmanız ve içinde bulunanlar yerleştirin, `.targets` ve `.props` dosyaları:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="b5ac9-183">İçinde `.nuspec` dosya, ekleme bir `files` düğümü altında `package` düğümü ve dosyaları başvurmak `build` joker karakterleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b5ac9-184">Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="b5ac9-185">Ek ayrıntılar için başvurmak [dahil MSBuild özellik ve paketteki hedefleri](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="b5ac9-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="b5ac9-186">Yerelleştirilmiş paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-186">Creating localized packages</span></span>

<span data-ttu-id="b5ac9-187">Yerelleştirilmiş sürümleri kitaplığınızın oluşturmak için farklı yerel ayarlar için ayrı paketleri oluşturmak veya tek bir paket içinde yerelleştirilmiş kaynak derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="b5ac9-188">Aşağıda, Almanca ve İtalyanca için ikinci yaklaşımı nasıl verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="b5ac9-189">Her hedef çerçeve klasörünün altında içinde `lib`, İngilizce varsayılan dışındaki desteklenen her dil için klasörleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="b5ac9-190">Bu klasörlerde kaynak derlemeler ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="b5ac9-191">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="b5ac9-192">İçinde `.nuspec` dosya, bu dosyaları başvuru `<files>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="b5ac9-193">Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="b5ac9-194">Bir benioku dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-194">Adding a readme</span></span>

<span data-ttu-id="b5ac9-195">Dahil ettiğinizde bir `readme.txt` paketi, Visual Studio kök dosyasında görüntüler, paket doğrudan yüklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="b5ac9-196">Bağımlılık olarak yüklü olan paketler için veya .NET Core projeleri için Benioku dosyaları gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="b5ac9-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="b5ac9-197">Bunu yapmak için oluşturmak, `readme.txt` dosya, bu proje kök klasöre yerleştirin ve kendisine başvuran `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5ac9-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="b5ac9-198">.NET standart eşleme tablosu</span><span class="sxs-lookup"><span data-stu-id="b5ac9-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="b5ac9-199">Platform adı</span><span class="sxs-lookup"><span data-stu-id="b5ac9-199">Platform Name</span></span> |<span data-ttu-id="b5ac9-200">Alias</span><span class="sxs-lookup"><span data-stu-id="b5ac9-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="b5ac9-201">.NET standart</span><span class="sxs-lookup"><span data-stu-id="b5ac9-201">.NET Standard</span></span> | <span data-ttu-id="b5ac9-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="b5ac9-202">netstandard</span></span>| <span data-ttu-id="b5ac9-203">1.0</span><span class="sxs-lookup"><span data-stu-id="b5ac9-203">1.0</span></span>| <span data-ttu-id="b5ac9-204">1.1</span><span class="sxs-lookup"><span data-stu-id="b5ac9-204">1.1</span></span>| <span data-ttu-id="b5ac9-205">1.2</span><span class="sxs-lookup"><span data-stu-id="b5ac9-205">1.2</span></span>| <span data-ttu-id="b5ac9-206">1.3</span><span class="sxs-lookup"><span data-stu-id="b5ac9-206">1.3</span></span>| <span data-ttu-id="b5ac9-207">1.4</span><span class="sxs-lookup"><span data-stu-id="b5ac9-207">1.4</span></span>| <span data-ttu-id="b5ac9-208">1,5</span><span class="sxs-lookup"><span data-stu-id="b5ac9-208">1.5</span></span>| <span data-ttu-id="b5ac9-209">1.6</span><span class="sxs-lookup"><span data-stu-id="b5ac9-209">1.6</span></span>|
|<span data-ttu-id="b5ac9-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b5ac9-210">.NET Core</span></span> | <span data-ttu-id="b5ac9-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="b5ac9-211">netcoreapp</span></span>| <span data-ttu-id="b5ac9-212">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-212">&#x2192;</span></span>| <span data-ttu-id="b5ac9-213">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-213">&#x2192;</span></span>| <span data-ttu-id="b5ac9-214">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-214">&#x2192;</span></span>| <span data-ttu-id="b5ac9-215">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-215">&#x2192;</span></span>| <span data-ttu-id="b5ac9-216">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-216">&#x2192;</span></span>| <span data-ttu-id="b5ac9-217">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-217">&#x2192;</span></span>| <span data-ttu-id="b5ac9-218">1.0</span><span class="sxs-lookup"><span data-stu-id="b5ac9-218">1.0</span></span>|
|<span data-ttu-id="b5ac9-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="b5ac9-219">.NET Framework</span></span>| <span data-ttu-id="b5ac9-220">NET</span><span class="sxs-lookup"><span data-stu-id="b5ac9-220">net</span></span>| <span data-ttu-id="b5ac9-221">4,5</span><span class="sxs-lookup"><span data-stu-id="b5ac9-221">4.5</span></span>| <span data-ttu-id="b5ac9-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="b5ac9-222">4.5.1</span></span>| <span data-ttu-id="b5ac9-223">4.6</span><span class="sxs-lookup"><span data-stu-id="b5ac9-223">4.6</span></span>| <span data-ttu-id="b5ac9-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="b5ac9-224">4.6.1</span></span>| <span data-ttu-id="b5ac9-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="b5ac9-225">4.6.2</span></span>| <span data-ttu-id="b5ac9-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="b5ac9-226">4.6.3</span></span>|
|<span data-ttu-id="b5ac9-227">Mono/Xamarin platformları</span><span class="sxs-lookup"><span data-stu-id="b5ac9-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="b5ac9-228">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-228">&#x2192;</span></span>| <span data-ttu-id="b5ac9-229">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-229">&#x2192;</span></span>| <span data-ttu-id="b5ac9-230">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-230">&#x2192;</span></span>| <span data-ttu-id="b5ac9-231">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-231">&#x2192;</span></span>| <span data-ttu-id="b5ac9-232">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-232">&#x2192;</span></span>| <span data-ttu-id="b5ac9-233">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-233">&#x2192;</span></span>|
|<span data-ttu-id="b5ac9-234">Evrensel Windows Platformu</span><span class="sxs-lookup"><span data-stu-id="b5ac9-234">Universal Windows Platform</span></span>| <span data-ttu-id="b5ac9-235">uap</span><span class="sxs-lookup"><span data-stu-id="b5ac9-235">uap</span></span>| <span data-ttu-id="b5ac9-236">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-236">&#x2192;</span></span>| <span data-ttu-id="b5ac9-237">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-237">&#x2192;</span></span>| <span data-ttu-id="b5ac9-238">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-238">&#x2192;</span></span>| <span data-ttu-id="b5ac9-239">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-239">&#x2192;</span></span>|<span data-ttu-id="b5ac9-240">10.0</span><span class="sxs-lookup"><span data-stu-id="b5ac9-240">10.0</span></span>|
|<span data-ttu-id="b5ac9-241">Windows</span><span class="sxs-lookup"><span data-stu-id="b5ac9-241">Windows</span></span>| <span data-ttu-id="b5ac9-242">Win</span><span class="sxs-lookup"><span data-stu-id="b5ac9-242">win</span></span>| <span data-ttu-id="b5ac9-243">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-243">&#x2192;</span></span>| <span data-ttu-id="b5ac9-244">8.0</span><span class="sxs-lookup"><span data-stu-id="b5ac9-244">8.0</span></span>| <span data-ttu-id="b5ac9-245">8.1</span><span class="sxs-lookup"><span data-stu-id="b5ac9-245">8.1</span></span>|
|<span data-ttu-id="b5ac9-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b5ac9-246">Windows Phone</span></span>| <span data-ttu-id="b5ac9-247">WPA</span><span class="sxs-lookup"><span data-stu-id="b5ac9-247">wpa</span></span>| <span data-ttu-id="b5ac9-248">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-248">&#x2192;</span></span>| <span data-ttu-id="b5ac9-249">& #x 2192;</span><span class="sxs-lookup"><span data-stu-id="b5ac9-249">&#x2192;</span></span>|<span data-ttu-id="b5ac9-250">8.1</span><span class="sxs-lookup"><span data-stu-id="b5ac9-250">8.1</span></span>|
|<span data-ttu-id="b5ac9-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b5ac9-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="b5ac9-252">WB</span><span class="sxs-lookup"><span data-stu-id="b5ac9-252">wp</span></span>| <span data-ttu-id="b5ac9-253">8.0</span><span class="sxs-lookup"><span data-stu-id="b5ac9-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="b5ac9-254">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="b5ac9-254">Related topics</span></span>

- [<span data-ttu-id="b5ac9-255">Nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="b5ac9-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="b5ac9-256">Simge paketleri</span><span class="sxs-lookup"><span data-stu-id="b5ac9-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="b5ac9-257">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b5ac9-258">Birden çok .NET Framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="b5ac9-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b5ac9-259">Bir pakete MSBuild özellik ve hedefler</span><span class="sxs-lookup"><span data-stu-id="b5ac9-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="b5ac9-260">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b5ac9-261">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="b5ac9-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b5ac9-262">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5ac9-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
