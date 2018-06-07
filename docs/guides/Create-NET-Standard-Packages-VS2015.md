---
title: Visual Studio 2015 ile birlikte .NET standart ve .NET Framework NuGet paketleri oluşturma
description: NuGet kullanarak .NET standart ve .NET Framework NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: c66e782ea5d4e9e2a9585d8301dc2a1b2e8c72b9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818740"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="40155-103">Visual Studio 2015 ile .NET standart ve .NET Framework paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="40155-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="40155-104">**Not:** .NET standart kitaplıkları geliştirmek için Visual Studio 2017 önerilir.</span><span class="sxs-lookup"><span data-stu-id="40155-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="40155-105">Visual Studio 2015 çalışabilir ancak .NET Core araç yalnızca önizleme duruma getirildi.</span><span class="sxs-lookup"><span data-stu-id="40155-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="40155-106">Bkz: [oluşturma ve Visual Studio 2017 paketiyle yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) NuGet 4.x+ ve Visual Studio 2017 çalışma.</span><span class="sxs-lookup"><span data-stu-id="40155-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="40155-107">[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="40155-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="40155-108">.NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="40155-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="40155-109">Tüm .NET çalışma zamanları arasında kullanılabilir ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldıran bir kod oluşturmak geliştiriciler sağlar.</span><span class="sxs-lookup"><span data-stu-id="40155-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="40155-110">Bu kılavuzda .NET standart kitaplığı 1.4 hedefleyen bir NuGet paketi veya .NET Framework 4.6 hedefleyen bir paket oluşturma konusunda anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="40155-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="40155-111">Bir .NET standart 1.4 kitaplığı .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin çalışır.</span><span class="sxs-lookup"><span data-stu-id="40155-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="40155-112">Ayrıntılar için bkz [.NET standart eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.NET belge).</span><span class="sxs-lookup"><span data-stu-id="40155-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="40155-113">İsterseniz, başka bir sürümünü .NET standart kitaplığı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40155-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40155-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="40155-114">Prerequisites</span></span>

1. <span data-ttu-id="40155-115">Visual Studio 2015 Güncelleştirme 3</span><span class="sxs-lookup"><span data-stu-id="40155-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="40155-116">(Yalnızca .NET standart) [.NET core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="40155-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="40155-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="40155-117">NuGet CLI.</span></span> <span data-ttu-id="40155-118">Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="40155-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="40155-119">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="40155-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="40155-120">nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="40155-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="40155-121">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="40155-121">Create the class library project</span></span>

1. <span data-ttu-id="40155-122">Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, select **sınıf kitaplığı (taşınabilir)** AppLogger için adı değiştirin ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="40155-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Yeni sınıf kitaplığı proje oluşturma](media/NetStandard-NewProject.png)

1. <span data-ttu-id="40155-124">İçinde **taşınabilir sınıf kitaplığı eklemek** görünür, iletişim için seçenekleri seçin `.NET Framework 4.6` ve `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="40155-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="40155-125">(.NET Framework'ü hedefleme, hangi seçenekleri uygun seçebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="40155-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="40155-126">.NET standardını hedefleyen, sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesini ve ardından **hedef .NET Platform standardını** içinde **hedefleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="40155-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="40155-127">Daha sonra seçebileceğiniz onaylama için bu eylem ister `.NET Standard 1.4` (veya başka bir kullanılabilir sürüm) açılır:</span><span class="sxs-lookup"><span data-stu-id="40155-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Hedef .NET standart 1.4 ayarlama](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="40155-129">Tıklayın **yapı** sekmesinde, değiştirmek **yapılandırma** için `Release`ve için kutuyu **XML belge dosyası**.</span><span class="sxs-lookup"><span data-stu-id="40155-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="40155-130">Kodunuzu bileşenine örneğin ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40155-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="40155-131">Yapılandırması yayın olarak ayarlanmış, projeyi oluşturun ve DLL ve XML dosyaları içinde üretilir denetleyin `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="40155-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="40155-132">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="40155-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="40155-133">Bir komut istemi açın, içeren klasöre gidin `AppLogger.csproj` klasörü (bir düzey altındaki where `.sln` dosyası), NuGet çalıştırıp `spec` ilk oluşturmak için komutu `AppLogger.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40155-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="40155-134">Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="40155-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="40155-135">`<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="40155-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="40155-136">Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="40155-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="40155-137">Başvuru derlemeleri eklemek `.nuspec` dosya, kitaplığın DLL ve IntelliSense XML dosyası:</span><span class="sxs-lookup"><span data-stu-id="40155-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="40155-138">.NET standardını hedefleyen girişleri aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="40155-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="40155-139">.NET Framework'ü hedefleme girişleri aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="40155-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="40155-140">Çözüme sağ tıklayın ve seçin **yapı çözümü** bir paket için tüm dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="40155-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="40155-141">Bağımlılıklar bildirme</span><span class="sxs-lookup"><span data-stu-id="40155-141">Declaring dependencies</span></span>

<span data-ttu-id="40155-142">Diğer NuGet paketlerini bağımlılıkları varsa, bildirim de listesinde `<dependencies>` öğeyle `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="40155-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="40155-143">Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya üstü bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40155-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="40155-144">Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir ya da yukarıdaki kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="40155-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="40155-145">Farklı bir sürüm aralıklarını belirtmek için başvurmak [paket sürüm](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="40155-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="40155-146">Bir benioku dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="40155-146">Adding a readme</span></span>

<span data-ttu-id="40155-147">Oluştur, `readme.txt` dosya, bu proje kök klasöre yerleştirin ve kendisine başvuran `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40155-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="40155-148">Visual Studio görüntü `readme.txt` paket bir projeye yüklü olduğunda.</span><span class="sxs-lookup"><span data-stu-id="40155-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="40155-149">Dosya, .NET Core projelerine veya bağımlılık olarak yüklü olan paketleri yüklendiğinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="40155-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="40155-150">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="40155-150">Package the component</span></span>

<span data-ttu-id="40155-151">Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="40155-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="40155-152">Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="40155-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="40155-153">Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, (.NET standart için gösterilen) aşağıdaki içeriğe bakın:</span><span class="sxs-lookup"><span data-stu-id="40155-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet paket AppLogger paket gösteren Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="40155-155">A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="40155-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="40155-156">Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="40155-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="40155-157">Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="40155-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="40155-158">Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="40155-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="40155-159">Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="40155-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="40155-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="40155-160">Related topics</span></span>

- [<span data-ttu-id="40155-161">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="40155-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="40155-162">Birden çok .NET framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="40155-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="40155-163">Bir pakete MSBuild özellik ve hedefler</span><span class="sxs-lookup"><span data-stu-id="40155-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="40155-164">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="40155-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="40155-165">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="40155-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="40155-166">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="40155-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="40155-167">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="40155-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="40155-168">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="40155-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
