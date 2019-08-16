---
title: Visual Studio 2015 ile .NET Standard ve .NET Framework NuGet paketleri oluşturma
description: NuGet 3. x ve Visual Studio 2015 kullanarak NuGet paketleri .NET Standard ve .NET Framework oluşturmaya yönelik uçtan uca bir anlatım.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 11dce27b93c3d09a2d27dc79f8d4fed86df879ba
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488982"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="aecbf-103">Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="aecbf-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="aecbf-104">**Not:** .NET Standard kitaplıklarını geliştirmek için Visual Studio 2017 önerilir.</span><span class="sxs-lookup"><span data-stu-id="aecbf-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="aecbf-105">Visual Studio 2015 çalışır, ancak .NET Core araçları yalnızca önizleme durumuna getirildi.</span><span class="sxs-lookup"><span data-stu-id="aecbf-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="aecbf-106">Bkz. NuGet 4. x + ve Visual Studio 2017 ile çalışmak için [Visual Studio 2017 ile bir paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) .</span><span class="sxs-lookup"><span data-stu-id="aecbf-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="aecbf-107">[.NET Standard kitaplığı](/dotnet/articles/standard/library) , .NET API 'lerinin tüm .NET çalışma zamanları üzerinde kullanılabilmesi amaçlanan ve bu sayede .net ekosisteminde daha büyük bir uyumluluk sağlamak amacıyla sunulan biçimsel bir belirtimdir.</span><span class="sxs-lookup"><span data-stu-id="aecbf-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="aecbf-108">.NET Standard kitaplığı, iş yüküyle bağımsız olarak uygulanacak tüm .NET platformları için tek bir BCL kümesi (temel sınıf kitaplığı) API 'Lerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="aecbf-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="aecbf-109">Geliştiricilerin tüm .NET çalışma zamanları genelinde kullanılabilir olan kodu üretmesini ve paylaşılan koddaki platforma özgü koşullu derleme yönergelerini ortadan kaldırmaması gerektiğini azaltmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="aecbf-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="aecbf-110">Bu kılavuzda, .NET Standard kitaplığı 1,4 ' i hedefleyen bir NuGet paketi veya 4,6 .NET Framework hedefleme bir paket oluşturma işlemi adım adım açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aecbf-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="aecbf-111">.NET Standard 1,4 kitaplığı .NET Framework 4.6.1, Evrensel Windows Platformu 10, .NET Core ve mono/Xamarin arasında çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aecbf-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="aecbf-112">Ayrıntılar için bkz. [.NET Standard eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.net belgeleri).</span><span class="sxs-lookup"><span data-stu-id="aecbf-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="aecbf-113">İsterseniz .NET Standard kitaplığının diğer sürümünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecbf-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aecbf-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aecbf-114">Prerequisites</span></span>

1. <span data-ttu-id="aecbf-115">Visual Studio 2015 Güncelleştirme 3</span><span class="sxs-lookup"><span data-stu-id="aecbf-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="aecbf-116">(Yalnızca .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="aecbf-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="aecbf-117">NuGet CLı.</span><span class="sxs-lookup"><span data-stu-id="aecbf-117">NuGet CLI.</span></span> <span data-ttu-id="aecbf-118">NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="aecbf-119">Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="aecbf-120">NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aecbf-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="aecbf-121">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aecbf-121">Create the class library project</span></span>

1. <span data-ttu-id="aecbf-122">Visual Studio 'da **dosya > yeni > projesi**,  **C# Visual > Windows** düğümünü genişletin, **sınıf kitaplığı (taşınabilir)** öğesini seçin, adı appgünlükçü olarak değiştirin ve **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Yeni sınıf kitaplığı projesi oluştur](media/NetStandard-NewProject.png)

1. <span data-ttu-id="aecbf-124">Görüntülenen **taşınabilir sınıf kitaplığı Ekle** iletişim kutusunda `.NET Framework 4.6` ve `ASP.NET Core 1.0`seçeneklerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="aecbf-125">(.NET Framework hedefliyorsanız, uygun seçenekleri belirleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="aecbf-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="aecbf-126">.NET Standard hedefliyorsanız, Çözüm Gezgini ' a sağ `AppLogger (Portable)` tıklayın, **Özellikler**' i seçin, **kitaplık** sekmesini seçin ve **hedefleme** bölümünde **hedef .NET platformu standardı** ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="aecbf-127">Bu eylem, açılan listeden (veya başka bir kullanılabilir sürümü `.NET Standard 1.4` ) seçebileceğiniz onay ister.</span><span class="sxs-lookup"><span data-stu-id="aecbf-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Hedef .NET Standard 1,4 olarak ayarlanıyor](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="aecbf-129">**Derleme** sekmesine tıklayın, **yapılandırmayı** olarak `Release`değiştirin ve **XML belge dosyası**kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="aecbf-130">Kodunuzu bileşene ekleyin, örneğin:</span><span class="sxs-lookup"><span data-stu-id="aecbf-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="aecbf-131">Yapılandırmayı serbest olarak ayarlayın, projeyi derleyin ve dll ve XML dosyalarının `bin\Release` klasör içinde üretildiğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="aecbf-132">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="aecbf-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="aecbf-133">Bir komut istemi `AppLogger.csproj` açın, klasörü içeren klasöre gidin ( `.sln` dosyanın altında bir düzey) ve ilk `AppLogger.nuspec` dosyayı oluşturmak için NuGet `spec` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="aecbf-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="aecbf-134">Bir `AppLogger.nuspec` düzenleyicide açın ve YOUR_NAME ile eşleşecek şekilde güncelleştirin ve uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="aecbf-135">Değer, özellikle de NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın. `<id>`</span><span class="sxs-lookup"><span data-stu-id="aecbf-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="aecbf-136">Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aecbf-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="aecbf-137">Kitaplık dll ve IntelliSense XML `.nuspec` dosyası gibi başvuru derlemelerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aecbf-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="aecbf-138">.NET Standard hedefliyorsanız, girdiler aşağıdakine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="aecbf-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="aecbf-139">.NET Framework hedefliyorsanız, girdiler aşağıdakine benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="aecbf-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="aecbf-140">Çözüme sağ tıklayın ve paketin tüm dosyalarını oluşturmak için **çözümü oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="aecbf-141">Bağımlılıkları bildirme</span><span class="sxs-lookup"><span data-stu-id="aecbf-141">Declaring dependencies</span></span>

<span data-ttu-id="aecbf-142">Diğer NuGet paketlerinde herhangi bir bağımlılıklarınız varsa, bu öğeleri, öğelerin bulunduğu `<dependencies>` `<group>` bildirimin öğesinde listeleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="aecbf-143">Örneğin, NewtonSoft. JSON 8.0.3 veya üzeri bir bağımlılık bildirmek için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aecbf-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="aecbf-144">Burada *Sürüm* özniteliğinin sözdizimi, 8.0.3 veya üzeri sürümünün kabul edilebilir olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="aecbf-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="aecbf-145">Farklı sürüm aralıkları belirtmek için [paket sürümü oluşturma](../concepts/package-versioning.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="aecbf-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="aecbf-146">Benioku ekleme</span><span class="sxs-lookup"><span data-stu-id="aecbf-146">Adding a readme</span></span>

<span data-ttu-id="aecbf-147">Dosyanızı oluşturun, proje kök klasörüne yerleştirin ve bu `.nuspec` dosyaya başvurun: `readme.txt`</span><span class="sxs-lookup"><span data-stu-id="aecbf-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="aecbf-148">Visual Studio, `readme.txt` paket bir projeye yüklendiğinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aecbf-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="aecbf-149">Dosya .NET Core projelerine yüklendiğinde veya bağımlılık olarak yüklenen paketler için gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="aecbf-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="aecbf-150">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="aecbf-150">Package the component</span></span>

<span data-ttu-id="aecbf-151">Pakete dahil etmeniz `.nuspec` gereken tüm dosyalara başvuran tamamlandığında, `pack` komutunu çalıştırmaya hazırsınız demektir:</span><span class="sxs-lookup"><span data-stu-id="aecbf-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="aecbf-152">Bu oluşturulur `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="aecbf-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="aecbf-153">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek, aşağıdaki içerikleri görürsünüz (.NET Standard için gösterilmektedir):</span><span class="sxs-lookup"><span data-stu-id="aecbf-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Appgünlükçü paketini gösteren NuGet Paket Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="aecbf-155">`.nupkg` Dosya, yalnızca farklı bir uzantıya sahip bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="aecbf-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="aecbf-156">Paket içeriğini `.nupkg` de inceleyebilir, ancak öğesini olarak `.zip`değiştirebilir, ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aecbf-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="aecbf-157">Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="aecbf-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="aecbf-158">Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına not edin. `pack`</span><span class="sxs-lookup"><span data-stu-id="aecbf-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="aecbf-159">Mac 'te Ayrıca, `.nuspec` dosyadaki Windows yol adlarını UNIX stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aecbf-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="aecbf-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="aecbf-160">Related topics</span></span>

- [<span data-ttu-id="aecbf-161">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="aecbf-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="aecbf-162">Birden çok .NET Framework sürümünü destekleme</span><span class="sxs-lookup"><span data-stu-id="aecbf-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="aecbf-163">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="aecbf-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="aecbf-164">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="aecbf-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="aecbf-165">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="aecbf-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="aecbf-166">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="aecbf-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="aecbf-167">.NET Standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="aecbf-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="aecbf-168">.NET Framework .NET Core 'a taşıma</span><span class="sxs-lookup"><span data-stu-id="aecbf-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
