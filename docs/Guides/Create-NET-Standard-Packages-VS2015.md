---
title: "Visual Studio 2015 ile birlikte .NET standart NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "NuGet kullanarak .NET standart NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015."
keywords: "bir paket, .NET standart paketler, .NET standart eşleme tablosu oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c15ffd709856fc9d5b9a9fb2fe87c0029b82650d
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="9374e-104">Visual Studio 2015 ile .NET standart paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9374e-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="9374e-105">*Nuget'e geçerlidir 3.x. Bkz: [oluşturma ve Visual Studio 2017 paketiyle yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) NuGet 4.x+ ile çalışmak için.*</span><span class="sxs-lookup"><span data-stu-id="9374e-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="9374e-106">[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="9374e-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="9374e-107">.NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9374e-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="9374e-108">Tüm .NET çalışma zamanları arasında kullanılabilir ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldıran bir kod oluşturmak geliştiriciler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9374e-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="9374e-109">Bu kılavuzda .NET standart kitaplığı 1.4 hedefleyen bir NuGet paketi oluşturmada size anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9374e-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="9374e-110">Bu tür bir kitaplığı .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin çalışır.</span><span class="sxs-lookup"><span data-stu-id="9374e-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="9374e-111">Ayrıntılar için bkz [.NET standart eşleme tablosu](#net-standard-mapping-table) bu konuda daha sonra.</span><span class="sxs-lookup"><span data-stu-id="9374e-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9374e-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9374e-112">Prerequisites</span></span>

1. <span data-ttu-id="9374e-113">Visual Studio 2015 Güncelleştirme 3</span><span class="sxs-lookup"><span data-stu-id="9374e-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="9374e-114">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="9374e-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="9374e-115">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="9374e-115">NuGet CLI.</span></span> <span data-ttu-id="9374e-116">Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="9374e-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9374e-117">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9374e-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="9374e-118">nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="9374e-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="9374e-119">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="9374e-119">Create the class library project</span></span>

1. <span data-ttu-id="9374e-120">Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, select **sınıf kitaplığı (taşınabilir)**AppLogger için adı değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9374e-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Yeni sınıf kitaplığı proje oluşturma](media/NetStandard-NewProject.png)

1. <span data-ttu-id="9374e-122">İçinde **taşınabilir sınıf kitaplığı eklemek** görünen seçin iletişim `.NET Framework 4.6` ve `ASP.NET Core 1.0` seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="9374e-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="9374e-123">Sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesini ve ardından **hedef .NET Platform standardını** içinde**Hedefleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9374e-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="9374e-124">Bu daha sonra seçebileceğiniz onaylama için ister `.NET Standard 1.4` açılır:</span><span class="sxs-lookup"><span data-stu-id="9374e-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Hedef .NET standart 1.4 ayarlama](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="9374e-126">Tıklayın **yapı** sekmesinde, değiştirmek **yapılandırma** için `Release`ve için kutuyu **XML belge dosyası**.</span><span class="sxs-lookup"><span data-stu-id="9374e-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="9374e-127">Kodunuzu bileşenine örneğin ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9374e-127">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="9374e-128">Yapılandırması yayın olarak ayarlanmış, projeyi oluşturun ve DLL ve XML dosyaları içinde üretilir denetleyin `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="9374e-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9374e-129">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="9374e-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9374e-130">Bir komut istemi açın, içeren klasöre gidin `AppLogger.csproj` klasörü (bir düzey altındaki where `.sln` dosyası), NuGet çalıştırıp `spec` ilk oluşturmak için komutu `AppLogger.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="9374e-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```cli
nuget spec
```

1. <span data-ttu-id="9374e-131">Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9374e-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9374e-132">`<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="9374e-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="9374e-133">Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9374e-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
    <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="9374e-134">Başvuru derlemeleri eklemek `.nuspec` dosya, kitaplığın DLL ve IntelliSense XML dosyası:</span><span class="sxs-lookup"><span data-stu-id="9374e-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="9374e-135">Çözüme sağ tıklayın ve seçin **yapı çözümü** bir paket için tüm dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="9374e-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="9374e-136">Bağımlılıklar bildirme</span><span class="sxs-lookup"><span data-stu-id="9374e-136">Declaring dependencies</span></span>

<span data-ttu-id="9374e-137">Diğer NuGet paketlerini bağımlılıkları varsa, bildirim de listesinde `<dependencies>` öğeyle `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="9374e-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="9374e-138">Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya üstü bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9374e-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="9374e-139">Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir ya da yukarıdaki kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="9374e-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="9374e-140">Farklı bir sürüm aralıklarını belirtmek için başvurmak [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9374e-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="9374e-141">Bir benioku dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="9374e-141">Adding a readme</span></span>

<span data-ttu-id="9374e-142">Oluştur, `readme.txt` dosya, bu proje kök klasöre yerleştirin ve kendisine başvuran `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="9374e-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="9374e-143">Visual Studio görüntü `readme.txt` paket bir projeye yüklü olduğunda.</span><span class="sxs-lookup"><span data-stu-id="9374e-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="9374e-144">Dosya, .NET Core projelerine veya bağımlılık olarak yüklü olan paketleri yüklendiğinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="9374e-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="9374e-145">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="9374e-145">Package the component</span></span>

<span data-ttu-id="9374e-146">Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="9374e-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="9374e-147">Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9374e-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9374e-148">Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:</span><span class="sxs-lookup"><span data-stu-id="9374e-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet paket AppLogger paket gösteren Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9374e-150">A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="9374e-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9374e-151">Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9374e-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9374e-152">Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9374e-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="9374e-153">Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9374e-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9374e-154">Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="9374e-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="9374e-155">.NET standart eşleme tablosu</span><span class="sxs-lookup"><span data-stu-id="9374e-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="9374e-156">Platform adı</span><span class="sxs-lookup"><span data-stu-id="9374e-156">Platform Name</span></span> | <span data-ttu-id="9374e-157">Alias</span><span class="sxs-lookup"><span data-stu-id="9374e-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="9374e-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="9374e-158">.NET Standard</span></span> | <span data-ttu-id="9374e-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="9374e-159">netstandard</span></span> | <span data-ttu-id="9374e-160">1.0</span><span class="sxs-lookup"><span data-stu-id="9374e-160">1.0</span></span> | <span data-ttu-id="9374e-161">1.1</span><span class="sxs-lookup"><span data-stu-id="9374e-161">1.1</span></span> | <span data-ttu-id="9374e-162">1.2</span><span class="sxs-lookup"><span data-stu-id="9374e-162">1.2</span></span> | <span data-ttu-id="9374e-163">1.3</span><span class="sxs-lookup"><span data-stu-id="9374e-163">1.3</span></span> | <span data-ttu-id="9374e-164">1.4</span><span class="sxs-lookup"><span data-stu-id="9374e-164">1.4</span></span> | <span data-ttu-id="9374e-165">1,5</span><span class="sxs-lookup"><span data-stu-id="9374e-165">1.5</span></span> | <span data-ttu-id="9374e-166">1.6</span><span class="sxs-lookup"><span data-stu-id="9374e-166">1.6</span></span> |
| <span data-ttu-id="9374e-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9374e-167">.NET Core</span></span> | <span data-ttu-id="9374e-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="9374e-168">netcoreapp</span></span> | <span data-ttu-id="9374e-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-169">&#x2192;</span></span> | <span data-ttu-id="9374e-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-170">&#x2192;</span></span> | <span data-ttu-id="9374e-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-171">&#x2192;</span></span> | <span data-ttu-id="9374e-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-172">&#x2192;</span></span> | <span data-ttu-id="9374e-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-173">&#x2192;</span></span> | <span data-ttu-id="9374e-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-174">&#x2192;</span></span> | <span data-ttu-id="9374e-175">1.0</span><span class="sxs-lookup"><span data-stu-id="9374e-175">1.0</span></span> |
| <span data-ttu-id="9374e-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9374e-176">.NET Framework</span></span> | <span data-ttu-id="9374e-177">net</span><span class="sxs-lookup"><span data-stu-id="9374e-177">net</span></span> | <span data-ttu-id="9374e-178">4,5</span><span class="sxs-lookup"><span data-stu-id="9374e-178">4.5</span></span> | <span data-ttu-id="9374e-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="9374e-179">4.5.1</span></span> | <span data-ttu-id="9374e-180">4.6</span><span class="sxs-lookup"><span data-stu-id="9374e-180">4.6</span></span> | <span data-ttu-id="9374e-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="9374e-181">4.6.1</span></span> | <span data-ttu-id="9374e-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="9374e-182">4.6.2</span></span> | <span data-ttu-id="9374e-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="9374e-183">4.6.3</span></span> |
| <span data-ttu-id="9374e-184">Mono/Xamarin platformları</span><span class="sxs-lookup"><span data-stu-id="9374e-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="9374e-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-185">&#x2192;</span></span> | <span data-ttu-id="9374e-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-186">&#x2192;</span></span> | <span data-ttu-id="9374e-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-187">&#x2192;</span></span> | <span data-ttu-id="9374e-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-188">&#x2192;</span></span> | <span data-ttu-id="9374e-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-189">&#x2192;</span></span> | <span data-ttu-id="9374e-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-190">&#x2192;</span></span> |
| <span data-ttu-id="9374e-191">Evrensel Windows Platformu</span><span class="sxs-lookup"><span data-stu-id="9374e-191">Universal Windows Platform</span></span> | <span data-ttu-id="9374e-192">uap</span><span class="sxs-lookup"><span data-stu-id="9374e-192">uap</span></span> | <span data-ttu-id="9374e-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-193">&#x2192;</span></span> | <span data-ttu-id="9374e-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-194">&#x2192;</span></span> | <span data-ttu-id="9374e-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-195">&#x2192;</span></span> | <span data-ttu-id="9374e-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-196">&#x2192;</span></span> |<span data-ttu-id="9374e-197">10.0</span><span class="sxs-lookup"><span data-stu-id="9374e-197">10.0</span></span> |
| <span data-ttu-id="9374e-198">Windows</span><span class="sxs-lookup"><span data-stu-id="9374e-198">Windows</span></span> | <span data-ttu-id="9374e-199">Win</span><span class="sxs-lookup"><span data-stu-id="9374e-199">win</span></span>| <span data-ttu-id="9374e-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-200">&#x2192;</span></span> | <span data-ttu-id="9374e-201">8.0</span><span class="sxs-lookup"><span data-stu-id="9374e-201">8.0</span></span> | <span data-ttu-id="9374e-202">8.1</span><span class="sxs-lookup"><span data-stu-id="9374e-202">8.1</span></span> |
| <span data-ttu-id="9374e-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9374e-203">Windows Phone</span></span> | <span data-ttu-id="9374e-204">wpa</span><span class="sxs-lookup"><span data-stu-id="9374e-204">wpa</span></span>| <span data-ttu-id="9374e-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-205">&#x2192;</span></span>| <span data-ttu-id="9374e-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="9374e-206">&#x2192;</span></span> | <span data-ttu-id="9374e-207">8.1</span><span class="sxs-lookup"><span data-stu-id="9374e-207">8.1</span></span> |
| <span data-ttu-id="9374e-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="9374e-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="9374e-209">wp</span><span class="sxs-lookup"><span data-stu-id="9374e-209">wp</span></span> | <span data-ttu-id="9374e-210">8.0</span><span class="sxs-lookup"><span data-stu-id="9374e-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="9374e-211">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="9374e-211">Related topics</span></span>

- [<span data-ttu-id="9374e-212">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="9374e-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9374e-213">Birden çok .NET framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="9374e-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9374e-214">Bir pakete MSBuild özellik ve hedefler</span><span class="sxs-lookup"><span data-stu-id="9374e-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9374e-215">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="9374e-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9374e-216">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="9374e-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9374e-217">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9374e-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9374e-218">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="9374e-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9374e-219">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9374e-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
