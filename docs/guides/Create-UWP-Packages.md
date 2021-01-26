---
title: Evrensel Windows Platformu için NuGet paketleri oluşturma
description: Evrensel Windows Platformu için bir Windows Çalışma Zamanı bileşeni kullanarak NuGet paketleri oluşturmaya yönelik uçtan uca bir yönerge.
author: JonDouglas
ms.author: jodou
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c077645508cb10e86b3ed1e1f2bf61adcd2013d9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774233"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="fe830-103">UWP paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe830-103">Create UWP packages</span></span>

<span data-ttu-id="fe830-104">[Evrensel Windows platformu (UWP)](https://developer.microsoft.com/windows) , Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe830-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="fe830-105">Bu modelde, UWP uygulamaları tüm cihazlarda ortak olan WinRT API 'Lerini ve ayrıca uygulamanın üzerinde çalıştığı cihaz ailesine özgü API 'Leri (Win32 ve .NET dahil) çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="fe830-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="fe830-106">Bu kılavuzda, hem yönetilen hem de yerel projelerde kullanılabilen yerel UWP bileşeni (XAML denetimi dahil) ile bir NuGet paketi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fe830-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe830-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe830-107">Prerequisites</span></span>

1. <span data-ttu-id="fe830-108">Visual Studio 2017 veya Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="fe830-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="fe830-109">[VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz olarak 2017 Community Edition 'ı yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe830-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="fe830-110">NuGet CLı.</span><span class="sxs-lookup"><span data-stu-id="fe830-110">NuGet CLI.</span></span> <span data-ttu-id="fe830-111">Nuget.org/downloads adresinden en son sürümünü `nuget.exe` indirin [](https://nuget.org/downloads)ve seçtiğiniz bir konuma kaydederek (indirme işlemi `.exe` doğrudan olur).</span><span class="sxs-lookup"><span data-stu-id="fe830-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="fe830-112">Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe830-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="fe830-113">UWP Windows Çalışma Zamanı bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe830-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="fe830-114">Visual Studio 'da **dosya > yeni > proje**' yi seçin, **Visual C++ > Windows > Universal** düğümünü genişletin, **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablonunu seçin, adı ImageEnhancer olarak değiştirin ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="fe830-115">İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.</span><span class="sxs-lookup"><span data-stu-id="fe830-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Yeni UWP Windows Çalışma Zamanı bileşen projesi oluşturma](media/UWP-NewProject.png)

1. <span data-ttu-id="fe830-117">Çözüm Gezgini ' de projeye sağ tıklayın, **> yeni öğe Ekle**' yi seçin, **Visual C++ > xaml** düğümüne tıklayın, **şablonlu denetim**' i seçin, adı awesomeımagecontrol. cpp olarak değiştirin ve **Ekle**' ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="fe830-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleniyor](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="fe830-119">Çözüm Gezgini ' de projeye sağ tıklayın ve Özellikler ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="fe830-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="fe830-120">Özellikler sayfasında, **C/C++ > yapılandırma özellikleri** ' ni genişletin ve **çıkış dosyaları**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="fe830-121">Sağdaki bölmede, **XML belgesi dosyaları oluştur** değerini Evet olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fe830-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![XML belge dosyalarını oluştur Evet olarak ayarlanıyor](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="fe830-123">Şimdi *çözüme* sağ tıklayın, **Batch Build**' i seçin, Iletişim kutusundaki üç hata ayıklama kutusunu aşağıda gösterildiği gibi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fe830-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="fe830-124">Bu, bir yapı yaparken, Windows 'un desteklediği her bir hedef sistem için tam bir yapıt kümesi üretmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe830-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Batch derlemesi](media/UWP-BatchBuild.png)

1. <span data-ttu-id="fe830-126">Toplu derleme iletişim kutusunda, projeyi doğrulamak ve NuGet paketi için ihtiyaç duyduğunuz çıkış dosyalarını oluşturmak için **Oluştur** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="fe830-127">Bu kılavuzda, paket için hata ayıklama yapıtlarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="fe830-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="fe830-128">Hata ayıklama olmayan paket için, bunun yerine toplu derleme iletişim kutusunda sürüm seçeneklerini işaretleyin ve izleyen adımlarda ortaya çıkan sürüm klasörlerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="fe830-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="fe830-129">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="fe830-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="fe830-130">İlk dosyayı oluşturmak için `.nuspec` aşağıdaki üç adımı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="fe830-131">Aşağıdaki bölümlerde, diğer gerekli güncelleştirmelerde size rehberlik sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fe830-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="fe830-132">Bir komut istemi açın ve içeren klasöre gidin `ImageEnhancer.vcxproj` (Bu, çözüm dosyasının bulunduğu alt klasör olacaktır).</span><span class="sxs-lookup"><span data-stu-id="fe830-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="fe830-133">`spec`Oluşturmak Için NuGet komutunu çalıştırın (dosyanın adı `ImageEnhancer.nuspec` dosyanın adından alınır `.vcxproj` ):</span><span class="sxs-lookup"><span data-stu-id="fe830-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="fe830-134">`ImageEnhancer.nuspec`Bir düzenleyicide açın ve uygun bir değerle YOUR_NAME değiştirerek aşağıdaki ile eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fe830-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="fe830-135">`<id>`Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="fe830-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="fe830-136">Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="fe830-137">Ortak tüketim için oluşturulmuş paketler için, `<tags>` Bu Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olmak üzere öğeye özel bir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fe830-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="fe830-138">Windows meta verileri pakete ekleniyor</span><span class="sxs-lookup"><span data-stu-id="fe830-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="fe830-139">Windows Çalışma Zamanı bileşeni, diğer uygulamaların ve kitaplıkların bileşeni tüketmesini sağlayan, genel olarak kullanılabilir tüm türlerini açıklayan meta veriler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fe830-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="fe830-140">Bu meta veriler, projeyi derlerken oluşturulan ve NuGet paketinize dahil etmeniz gereken bir. winmd dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="fe830-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="fe830-141">IntelliSense verilerine sahip bir XML dosyası aynı anda oluşturulmuştur ve de dahil edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fe830-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="fe830-142">Aşağıdaki `<files>` düğümü `.nuspec` dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fe830-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="fe830-143">XAML içeriği ekleme</span><span class="sxs-lookup"><span data-stu-id="fe830-143">Adding XAML content</span></span>

<span data-ttu-id="fe830-144">Bileşeninizdeki XAML denetimini eklemek için, denetimin varsayılan şablonuna sahip XAML dosyasını (proje şablonu tarafından oluşturulan olarak) eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe830-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="fe830-145">Bu da `<files>` bölümüne gider:</span><span class="sxs-lookup"><span data-stu-id="fe830-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="fe830-146">Yerel uygulama kitaplıklarını ekleme</span><span class="sxs-lookup"><span data-stu-id="fe830-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="fe830-147">Bileşeninizin içinde, ImageEnhancer türünün Çekirdek mantığı, `ImageEnhancer.dll` her bir hedef çalışma zamanı (ARM, x86 ve x64) için oluşturulan çeşitli derlemelerde yer alan yerel koddur.</span><span class="sxs-lookup"><span data-stu-id="fe830-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="fe830-148">Bunları pakete eklemek için, `<files>` ilgili. pri kaynak dosyalarıyla birlikte bu bölüme başvurun:</span><span class="sxs-lookup"><span data-stu-id="fe830-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="fe830-149">. Targets ekleniyor</span><span class="sxs-lookup"><span data-stu-id="fe830-149">Adding .targets</span></span>

<span data-ttu-id="fe830-150">Daha sonra, NuGet paketinizi kullanabilen C++ ve JavaScript projelerinin, gerekli derlemeyi ve winmd dosyalarını tanımlamak için bir. targets dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe830-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="fe830-151">(C# ve Visual Basic projeleri bunu otomatik olarak yapılır.) Aşağıdaki metni içine kopyalayarak bu dosyayı oluşturun `ImageEnhancer.targets` ve dosyayla aynı klasöre kaydedin `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fe830-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="fe830-152">_Note_: Bu `.targets` dosyanın paket kimliğiyle aynı adı olması gerekir (örneğin, `<Id>` `.nupspec` dosyadaki öğesi):</span><span class="sxs-lookup"><span data-stu-id="fe830-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="fe830-153">Ardından `ImageEnhancer.targets` , `.nuspec` dosyanıza başvurun:</span><span class="sxs-lookup"><span data-stu-id="fe830-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="fe830-154">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="fe830-154">Final .nuspec</span></span>

<span data-ttu-id="fe830-155">Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada yeniden YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="fe830-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="fe830-156">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="fe830-156">Package the component</span></span>

<span data-ttu-id="fe830-157">`.nuspec`Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlandığında, komutunu çalıştırmaya hazırsınız demektir `pack` :</span><span class="sxs-lookup"><span data-stu-id="fe830-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="fe830-158">Bu oluşturulur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="fe830-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="fe830-159">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fe830-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![ImageEnhancer paketini gösteren NuGet Paket Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="fe830-161">`.nupkg`Dosya, yalnızca farklı bir uzantıya sahip BIR ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="fe830-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="fe830-162">Paket içeriğini de inceleyebilir, ancak öğesini olarak değiştirebilir, `.nupkg` `.zip` ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fe830-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="fe830-163">Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="fe830-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="fe830-164">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="fe830-164">Related topics</span></span>

- [<span data-ttu-id="fe830-165">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="fe830-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="fe830-166">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="fe830-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="fe830-167">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe830-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="fe830-168">Çoklu .NET Framework sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="fe830-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fe830-169">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="fe830-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="fe830-170">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe830-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
