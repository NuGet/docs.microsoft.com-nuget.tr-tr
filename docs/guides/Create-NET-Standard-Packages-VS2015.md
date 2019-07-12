---
title: Visual Studio 2015 ile .NET Standard ve .NET Framework NuGet paketleri oluşturma
description: NuGet kullanarak .NET Standard ve .NET Framework NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842450"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="9565b-103">Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9565b-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="9565b-104">**Not:** Visual Studio 2017, .NET standart kitaplıkları geliştirmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="9565b-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="9565b-105">Visual Studio 2015 çalışabilir ancak .NET Core araçları yalnızca önizleme duruma getirildi.</span><span class="sxs-lookup"><span data-stu-id="9565b-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="9565b-106">Bkz: [oluşturun ve Visual Studio 2017 ile paket yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) NuGet 4.x+ ve Visual Studio 2017 ile çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="9565b-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="9565b-107">[.NET Standard Kitaplığı](/dotnet/articles/standard/library) olduğu bir resmi belirtimi .NET API'lerini amaçlanan bu nedenle büyük gerekmemesi .NET ekosisteminde oluşturma tüm .NET çalışma zamanları, kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="9565b-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="9565b-108">.NET Standard kitaplığı BCL (temel sınıf kitaplığı) API kümesi, iş yükünü bağımsız uygulamak tüm .NET platformları için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9565b-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="9565b-109">Ancak, geliştiricilerin tüm .NET çalışma zamanı arasında kullanılabilir ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldıran bir kod üretmek etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="9565b-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="9565b-110">Bu kılavuzda, .NET Standard kitaplığı 1.4 hedefleyen bir NuGet paketi veya .NET Framework 4.6 targeting paketi oluşturma işlemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9565b-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="9565b-111">.NET Standard 1.4 kitaplığı, .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="9565b-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="9565b-112">Ayrıntılar için bkz [.NET Standard eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.NET belgeleri).</span><span class="sxs-lookup"><span data-stu-id="9565b-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="9565b-113">İsterseniz, diğer .NET Standard kitaplığı sürümünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9565b-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9565b-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9565b-114">Prerequisites</span></span>

1. <span data-ttu-id="9565b-115">Visual Studio 2015 Güncelleştirme 3</span><span class="sxs-lookup"><span data-stu-id="9565b-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="9565b-116">(Yalnızca .NET standard) [.NET core SDK'sı](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="9565b-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="9565b-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="9565b-117">NuGet CLI.</span></span> <span data-ttu-id="9565b-118">Nuget.exe en son sürümünü indirin [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="9565b-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9565b-119">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9565b-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="9565b-120">nuget.exe CLI aracı kendisini bir yükleyici dolayısıyla bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="9565b-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="9565b-121">Sınıf kitaplığı projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="9565b-121">Create the class library project</span></span>

1. <span data-ttu-id="9565b-122">Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C# > Windows** düğümünü **sınıf kitaplığı (taşınabilir)** AppLogger için adı değiştirin ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9565b-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Yeni sınıf kitaplığı projesi oluşturun](media/NetStandard-NewProject.png)

1. <span data-ttu-id="9565b-124">İçinde **taşınabilir sınıf kitaplığı Ekle** görüntülenen iletişim seçmek için seçenekleri `.NET Framework 4.6` ve `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="9565b-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="9565b-125">(.NET Framework'ü hedefleyen, hangi seçenekleri uygun seçebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9565b-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="9565b-126">.NET Standard hedefleme, sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesine ve ardından seçin **hedef .NET Platform standardını** içinde **hedefleme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9565b-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="9565b-127">Bu eylem, onay sonrasında seçebilirsiniz, ister `.NET Standard 1.4` (veya başka bir kullanılabilir sürüm) açılan:</span><span class="sxs-lookup"><span data-stu-id="9565b-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Hedef .NET Standard 1.4 için ayarlama](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="9565b-129">Tıklayarak **derleme** sekmesinde, **yapılandırma** için `Release`ve kutusunu işaretlemeniz **XML belge dosyası**.</span><span class="sxs-lookup"><span data-stu-id="9565b-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="9565b-130">Örneğin, kodunuzu bileşene ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9565b-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="9565b-131">Yapılandırması yayın olarak ayarlanmış, projeyi derleyin ve DLL ve XML dosyaları içinde üretildiğini denetleyin `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="9565b-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9565b-132">Oluşturma ve güncelleştirme .nuspec dosyası</span><span class="sxs-lookup"><span data-stu-id="9565b-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9565b-133">Bir komut istemi açın, klasör içeren dizine gidin `AppLogger.csproj` klasörü (bir düzey altındaki nerede `.sln` dosyasıdır), NuGet çalıştırıp `spec` ilk oluşturmak için komut `AppLogger.nuspec` dosya:</span><span class="sxs-lookup"><span data-stu-id="9565b-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9565b-134">Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirmeniz YOUR_NAME uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9565b-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9565b-135">`<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="9565b-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="9565b-136">Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9565b-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="9565b-137">Başvuru bütünleştirilmiş kodları için ekleme `.nuspec` kitaplığının DLL ve IntelliSense XML dosyasının dosya:</span><span class="sxs-lookup"><span data-stu-id="9565b-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="9565b-138">.NET Standard hedefleme, girişleri aşağıdakine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="9565b-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="9565b-139">.NET Framework'ü hedefleyen girişleri aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9565b-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="9565b-140">Çözüme sağ tıklayıp **Çözümü Derle** paket için tüm dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="9565b-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="9565b-141">Bağımlılıkları bildirme</span><span class="sxs-lookup"><span data-stu-id="9565b-141">Declaring dependencies</span></span>

<span data-ttu-id="9565b-142">Diğer NuGet paketleri üzerinde bağımlılıkları varsa, bu bildirim, liste `<dependencies>` öğeyle `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="9565b-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="9565b-143">Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya sonraki sürümlere bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9565b-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="9565b-144">Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir veya üstü kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="9565b-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="9565b-145">Farklı sürüm aralıklarını belirtmek için başvurmak [Paket sürümü oluşturma](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9565b-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="9565b-146">Benioku dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="9565b-146">Adding a readme</span></span>

<span data-ttu-id="9565b-147">Oluşturma, `readme.txt` dosyası, proje kök klasörüne yerleştirin ve buna başvuran `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="9565b-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="9565b-148">Visual Studio görüntü `readme.txt` paketini projeye yüklü olduğunda.</span><span class="sxs-lookup"><span data-stu-id="9565b-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="9565b-149">Dosya, .NET Core projeleri veya bağımlılık olarak yüklenen paketler yüklediğinizde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="9565b-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="9565b-150">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="9565b-150">Package the component</span></span>

<span data-ttu-id="9565b-151">Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="9565b-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="9565b-152">Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9565b-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9565b-153">Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, (.NET Standard için gösterilen) aşağıdaki içeriğe bakın:</span><span class="sxs-lookup"><span data-stu-id="9565b-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet paket Gezgini AppLogger paket gösteriliyor](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9565b-155">A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="9565b-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9565b-156">Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9565b-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9565b-157">Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9565b-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="9565b-158">Unutmayın `pack` Mac OS X üzerinde Mono 4.4.2 gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9565b-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9565b-159">Mac bilgisayarlarda, Windows yol adları olarak da dönüştürmelisiniz `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="9565b-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9565b-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="9565b-160">Related topics</span></span>

- [<span data-ttu-id="9565b-161">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="9565b-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9565b-162">Birden çok .NET framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="9565b-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9565b-163">Bir pakete MSBuild özellikler ve hedefler</span><span class="sxs-lookup"><span data-stu-id="9565b-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9565b-164">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="9565b-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9565b-165">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="9565b-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9565b-166">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9565b-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9565b-167">.NET standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="9565b-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9565b-168">.NET Core ile .NET Framework'ten taşıma</span><span class="sxs-lookup"><span data-stu-id="9565b-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
