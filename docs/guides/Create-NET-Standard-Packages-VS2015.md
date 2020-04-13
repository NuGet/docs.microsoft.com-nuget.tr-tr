---
title: Visual Studio 2015 ile .NET Standardı ve .NET Framework NuGet Paketleri Oluşturun
description: NuGet 3.x ve Visual Studio 2015'i kullanarak .NET Standard ve .NET Framework NuGet paketlerini oluşturmanın uçtan uca bir walkthrough'u.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380720"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="ec779-103">Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturun</span><span class="sxs-lookup"><span data-stu-id="ec779-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="ec779-104">**Not:** Visual Studio 2017 ,.NET Standart kitaplıkları geliştirmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="ec779-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="ec779-105">Visual Studio 2015 işe yarayabilir ancak .NET Core aracı yalnızca Önizleme durumuna getirildi.</span><span class="sxs-lookup"><span data-stu-id="ec779-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="ec779-106">NuGet 4.x+ ve Visual Studio 2017 ile çalışmak için [Visual Studio 2017 ile bir paket oluşturun ve yayınlayın.](../quickstart/create-and-publish-a-package-using-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ec779-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="ec779-107">[.NET Standart Kitaplığı,](/dotnet/articles/standard/library) .NET'in tüm çalışma saatlerinde kullanıma sunulması amaçlanan .NET API'lerinin resmi bir belirtimidir ve böylece .NET ekosisteminde daha fazla tekdüzelik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec779-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="ec779-108">.NET Standart Kitaplığı, iş yükünden bağımsız olarak uygulanacak tüm .NET platformları için tek tip bir BCL (Taban Sınıf Kitaplığı) API'leri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ec779-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="ec779-109">Geliştiricilerin tüm .NET çalışma saatlerinde kullanılabilir kod lar üretmesini sağlar ve paylaşılan koddaki platforma özgü koşullu derleme yönergelerini ortadan kaldırmazsa azaltır.</span><span class="sxs-lookup"><span data-stu-id="ec779-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="ec779-110">Bu kılavuz, .NET Standart Kitaplığı 1.4'u veya .NET Framework 4.6'yı hedefleyen bir paket ilerler.</span><span class="sxs-lookup"><span data-stu-id="ec779-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="ec779-111">.NET Standart 1.4 kitaplığı .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core ve Mono/Xamarin genelinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ec779-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="ec779-112">Ayrıntılar için [.NET Standart eşleme tablosuna](/dotnet/standard/net-standard#net-implementation-support) (.NET belgeleri) bakın.</span><span class="sxs-lookup"><span data-stu-id="ec779-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="ec779-113">İsterseniz .NET Standart Kitaplığı'nın diğer sürümünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec779-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec779-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ec779-114">Prerequisites</span></span>

1. <span data-ttu-id="ec779-115">Visual Studio 2015 Güncelleştirme 3</span><span class="sxs-lookup"><span data-stu-id="ec779-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="ec779-116">(.Sadece NET Standart) [.NET Çekirdek SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="ec779-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="ec779-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="ec779-117">NuGet CLI.</span></span> <span data-ttu-id="ec779-118">nuget.exe'nin en son sürümünü [nuget.org/downloads](https://nuget.org/downloads)indirin ve seçtiğiniz bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ec779-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="ec779-119">Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec779-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="ec779-120">nuget.exe cli aracı kendisi değil, bir yükleyici, bu yüzden yerine çalışan tarayıcınızdan indirilen dosyayı kaydetmek için emin olun.</span><span class="sxs-lookup"><span data-stu-id="ec779-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="ec779-121">Sınıf kitaplığı projesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec779-121">Create the class library project</span></span>

1. <span data-ttu-id="ec779-122">Visual Studio, **Dosya > Yeni > Projesi,** Visual **C# > Windows** düğümünü genişletin, Sınıf **Kitaplığı (Taşınabilir)** seçin, AppLogger adını değiştirin ve **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="ec779-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Yeni sınıf kitaplık projesi oluşturma](media/NetStandard-NewProject.png)

1. <span data-ttu-id="ec779-124">Görünen **Taşınabilir Sınıf Kitaplığı Ekle** iletişim kutusunda, `.NET Framework 4.6` 'nin `ASP.NET Core 1.0`ve.</span><span class="sxs-lookup"><span data-stu-id="ec779-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="ec779-125">(.NET Framework hedeflenebiliyorsanız, hangi seçeneklerin uygun olduğunu seçebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="ec779-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="ec779-126">.NET Standard'ı hedefliyorsanız, `AppLogger (Portable)` Çözüm Gezgini'nde sağ tıklatın, **Özellikler'i**seçin, **Kitaplık** sekmesini seçin ve ardından **Hedefleme** bölümünde **Hedef .NET Platform Standardı'nı** seçin.</span><span class="sxs-lookup"><span data-stu-id="ec779-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="ec779-127">Bu eylem onay ister, sonra açılır `.NET Standard 1.4` yerden (veya başka bir kullanılabilir sürümü) seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec779-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Hedefin .NET Standart 1.4'e ayarlanması](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="ec779-129">**Yapı** sekmesine tıklayın, **Yapılandırmayı** `Release`değiştirin ve **XML dokümantasyon dosyası**için kutuyu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="ec779-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="ec779-130">Kodunuzu bileşene ekleyin, örneğin:</span><span class="sxs-lookup"><span data-stu-id="ec779-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="ec779-131">Yapılandırmayı Serbest Bırak'a ayarlayın, projeyi oluşturun ve Klasör içinde `bin\Release` DLL ve XML dosyalarının üretilip üretilmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ec779-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="ec779-132">.nuspec dosyasını oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ec779-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="ec779-133">Komut istemini açın, klasör `AppLogger.csproj` içeren klasöre gidin `.sln` (dosyanın bulunduğu yerin `spec` bir alt `AppLogger.nuspec` düzeyi) ve ilk dosyayı oluşturmak için NuGet komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ec779-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="ec779-134">Bir `AppLogger.nuspec` düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek aşağıdakilerle eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ec779-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="ec779-135">Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın.</span><span class="sxs-lookup"><span data-stu-id="ec779-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="ec779-136">Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec779-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="ec779-137">Dosyaya, `.nuspec` yani kitaplığın DLL'si ve IntelliSense XML dosyasına başvuru derlemeleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ec779-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="ec779-138">.NET Standard'ı hedefliyorsanız, girişler aşağıdakilere benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="ec779-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="ec779-139">.NET Framework hedeflenenden, girişler aşağıdakilere benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="ec779-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="ec779-140">Çözüme sağ tıklayın ve paket için tüm dosyaları oluşturmak için **Çözüm Oluştur'u** seçin.</span><span class="sxs-lookup"><span data-stu-id="ec779-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="ec779-141">Bağımlılıkları bildirme</span><span class="sxs-lookup"><span data-stu-id="ec779-141">Declaring dependencies</span></span>

<span data-ttu-id="ec779-142">Diğer NuGet paketlerine herhangi bir bağımlılığınız varsa, bildirimin `<dependencies>` `<group>` öğesindekileri öğelerle listele.</span><span class="sxs-lookup"><span data-stu-id="ec779-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="ec779-143">Örneğin, NewtonSoft.Json 8.0.3 veya üzeri bir bağımlılık bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ec779-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="ec779-144">Sürüm özniteliğinin *version* buradaki sözdizimi, 8.0.3 veya üzeri sürümün kabul edilebilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec779-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="ec779-145">Farklı sürüm aralıkları belirtmek için [Paket sürümüne](../concepts/package-versioning.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="ec779-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="ec779-146">Okuma meonu ekleme</span><span class="sxs-lookup"><span data-stu-id="ec779-146">Adding a readme</span></span>

<span data-ttu-id="ec779-147">Dosyanızı `readme.txt` oluşturun, proje kök klasörüne yerleştirin ve `.nuspec` dosyaya bakın:</span><span class="sxs-lookup"><span data-stu-id="ec779-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="ec779-148">Paket bir `readme.txt` projeye yüklendiğinde Visual Studio görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ec779-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="ec779-149">Dosya,.NET Core projelerine yüklendiğinde veya bağımlılık olarak yüklenen paketler için gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="ec779-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="ec779-150">Bileşeni paketle</span><span class="sxs-lookup"><span data-stu-id="ec779-150">Package the component</span></span>

<span data-ttu-id="ec779-151">Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="ec779-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="ec779-152">Bu oluşturur. `AppLogger.YOUR_NAME.1.0.0.nupkg`</span><span class="sxs-lookup"><span data-stu-id="ec779-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="ec779-153">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletileyerek aşağıdaki içeriği görürsünüz (.NET Standardı için gösterilmiştir):</span><span class="sxs-lookup"><span data-stu-id="ec779-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet Paket Explorer AppLogger paketini gösteriyor](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ec779-155">Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ec779-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ec779-156">Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec779-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ec779-157">Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="ec779-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="ec779-158">Mac `pack` OS X'te Mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec779-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ec779-159">Mac'te, dosyadaki `.nuspec` Windows yol adlarını Unix stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec779-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ec779-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="ec779-160">Related topics</span></span>

- [<span data-ttu-id="ec779-161">.nuspec referans</span><span class="sxs-lookup"><span data-stu-id="ec779-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="ec779-162">Birden çok .NET çerçeve sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="ec779-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ec779-163">MSBuild sahne ve hedeflerini bir pakete dahil et</span><span class="sxs-lookup"><span data-stu-id="ec779-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="ec779-164">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec779-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ec779-165">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="ec779-165">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="ec779-166">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="ec779-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ec779-167">.NET Standart Kütüphane belgeleri</span><span class="sxs-lookup"><span data-stu-id="ec779-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ec779-168">.NET Framework'den .NET Core'a taşıma</span><span class="sxs-lookup"><span data-stu-id="ec779-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
