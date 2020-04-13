---
title: Evrensel Windows Platformu için NuGet Paketleri Oluşturun
description: Evrensel Windows Platformu için Bir Windows Runtime Bileşeni kullanarak NuGet paketleri oluşturmanın uçtan uca bir gözden geçirme.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380758"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="7f3f5-103">UWP paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f3f5-103">Create UWP packages</span></span>

<span data-ttu-id="7f3f5-104">[Evrensel Windows Platformu (UWP),](https://developer.microsoft.com/windows) Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="7f3f5-105">Bu modelde, UWP uygulamaları hem tüm cihazlarda ortak olan WinRT API'lerini hem de uygulamanın çalıştırıldığı aygıt ailesine özgü API'leri (Win32 ve .NET dahil) arayabilir.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="7f3f5-106">Bu izlenecek yolda, hem Yönetilen hem de Yerel projelerde kullanılabilecek yerel uwp bileşenine (XAML denetimi dahil) sahip bir NuGet paketi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f3f5-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f3f5-107">Prerequisites</span></span>

1. <span data-ttu-id="7f3f5-108">Visual Studio 2017 veya Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="7f3f5-109">2017 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/)ücretsiz olarak yükleyin; Profesyonel ve Kurumsal sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="7f3f5-110">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-110">NuGet CLI.</span></span> <span data-ttu-id="7f3f5-111">nuget.org/downloads en son `nuget.exe` [nuget.org/downloads](https://nuget.org/downloads)sürümünü indirin, seçtiğiniz bir konuma kaydedin `.exe` (indirme doğrudan).</span><span class="sxs-lookup"><span data-stu-id="7f3f5-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="7f3f5-112">Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="7f3f5-113">UWP Windows Runtime bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f3f5-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="7f3f5-114">Visual **Studio'da, Yeni > Projesi > Dosya'yı**seçin, **Visual C++ > Windows > Evrensel** düğümünü genişletin, Windows **Runtime Bileşeni (Evrensel Windows)** şablonuna tıklayın, adı ImageEnhancer olarak değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="7f3f5-115">İstendiğinde Hedef Sürüm ve Minimum Sürüm için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Yeni bir UWP Windows Runtime Bileşeni projesi oluşturma](media/UWP-NewProject.png)

1. <span data-ttu-id="7f3f5-117">Solution Explorer'da projeyi sağ tıklatın, **Yeni Öğe> ekle'yi**seçin, **Visual C++ > XAML** düğümünü tıklatın, **Şablon denetim'i**seçin, adını AwesomeImageControl.cpp olarak değiştirin ve **Ekle'yi**tıklatın:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Projeye yeni bir XAML Şablondenetim öğesi ekleme](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="7f3f5-119">Solution Explorer'da projeyi sağ tıklatın ve **Özellikler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="7f3f5-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="7f3f5-120">Özellikler sayfasında, **Yapılandırma Özelliklerini C/C++ >** genişletin ve Çıktı **Dosyaları'nı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="7f3f5-121">Sağdaki bölmede, **XML Belge Dosyaları Oluştur** değerini Evet olarak değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![XML Belge Dosyalarını Evet'e Ayarlama](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="7f3f5-123">Şimdi *çözüme* sağ tıklayın, **Toplu Yapı'yı**seçin, iletişim kutusundaki üç Hata Ayıklama kutusunu aşağıda gösterildiği gibi kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="7f3f5-124">Bu, bir yapı yaptığınızda, Windows'un desteklediği hedef sistemlerin her biri için tam bir yapı kümesi oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Toplu Yapı](media/UWP-BatchBuild.png)

1. <span data-ttu-id="7f3f5-126">Toplu Yapı iletişim kutusunda ve projeyi doğrulamak ve NuGet paketi için ihtiyacınız olan çıktı dosyalarını oluşturmak için **Oluştur'u** tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="7f3f5-127">Bu gözden geçirme de paket için Hata Ayıklama yapıtlarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="7f3f5-128">Hata ayıklama paketi için, Toplu Yapı iletişim kutusundaki Sürüm seçeneklerini denetleyin ve ardından gelen Sürüm klasörlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7f3f5-129">.nuspec dosyasını oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="7f3f5-130">İlk `.nuspec` dosyayı oluşturmak için aşağıdaki üç adımı yapın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="7f3f5-131">Ardından gelen bölümler daha sonra diğer gerekli güncelleştirmeler boyunca size rehberlik.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="7f3f5-132">Bir komut istemi açın ve `ImageEnhancer.vcxproj` içeren klasöre gidin (bu çözüm dosyasının olduğu yerin altında bir alt klasör olacaktır).</span><span class="sxs-lookup"><span data-stu-id="7f3f5-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="7f3f5-133">Oluşturmak `spec` `ImageEnhancer.nuspec` için NuGet komutunu çalıştırın `.vcxproj` (dosyanın adı dosyanın adından alınır):</span><span class="sxs-lookup"><span data-stu-id="7f3f5-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="7f3f5-134">Bir `ImageEnhancer.nuspec` düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek aşağıdakilerle eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7f3f5-135">Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="7f3f5-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="7f3f5-136">Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="7f3f5-137">Genel tüketim için oluşturulmuş paketler için, `<tags>` bu etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, öğeye özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="7f3f5-138">Pakete Windows meta verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="7f3f5-139">Windows Runtime Bileşeni, genel kullanıma açık tüm türlerini açıklayan meta veriler gerektirir ve bu da diğer uygulamaların ve kitaplıkların bileşeni tüketmesini mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="7f3f5-140">Bu meta veriler, projeyi derlediğinizde oluşturulan ve NuGet paketinize eklenmesi gereken bir .winmd dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="7f3f5-141">IntelliSense verilerine sahip bir XML dosyası da aynı anda oluşturulur ve eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="7f3f5-142">`.nuspec` Dosyaya aşağıdaki `<files>` düğümü ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="7f3f5-143">XAML içeriği ekleme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-143">Adding XAML content</span></span>

<span data-ttu-id="7f3f5-144">Bileşeninize bir XAML denetimi eklemek için, denetim için varsayılan şablona sahip XAML dosyasını eklemeniz gerekir (proje şablonu tarafından oluşturulan gibi).</span><span class="sxs-lookup"><span data-stu-id="7f3f5-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="7f3f5-145">Bu da `<files>` bölümünde gider:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="7f3f5-146">Yerel uygulama kitaplıklarını ekleme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="7f3f5-147">Bileşeniniz içinde, ImageEnhancer türünün temel mantığı, her hedef çalışma `ImageEnhancer.dll` zamanı (ARM, x86 ve x64) için oluşturulan çeşitli derlemelerde bulunan yerel koddadır.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="7f3f5-148">Bunları pakete eklemek için, ilişkili `<files>` .pri kaynak dosyalarıyla birlikte bölüme başvurun:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="7f3f5-149">.targets ekleme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-149">Adding .targets</span></span>

<span data-ttu-id="7f3f5-150">Ardından, NuGet paketinizi tüketebilecek C++ ve JavaScript projeleri, gerekli derleme ve winmd dosyalarını tanımlamak için bir .targets dosyasına ihtiyaç duyar.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="7f3f5-151">(C# ve Visual Basic projeleri bunu otomatik olarak yapar.) Aşağıdaki metni kopyalayarak bu dosyayı oluşturun `ImageEnhancer.targets` ve dosyayla `.nuspec` aynı klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="7f3f5-152">_Not_: `.targets` Bu dosyanın paket kimliğiyle aynı adla (örn. `<Id>` `.nupspec` dosyadaki öğe) olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="7f3f5-153">Ardından dosyanıza `ImageEnhancer.targets` `.nuspec` bakın:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="7f3f5-154">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="7f3f5-154">Final .nuspec</span></span>

<span data-ttu-id="7f3f5-155">Son `.nuspec` dosyanız şimdi aşağıdaki gibi görünmelidir ve yine YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="7f3f5-156">Bileşeni paketle</span><span class="sxs-lookup"><span data-stu-id="7f3f5-156">Package the component</span></span>

<span data-ttu-id="7f3f5-157">Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="7f3f5-158">Bu oluşturur. `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`</span><span class="sxs-lookup"><span data-stu-id="7f3f5-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7f3f5-159">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletmek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7f3f5-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Paket Explorer ImageEnhancer paketini gösteriyor](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7f3f5-161">Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7f3f5-162">Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7f3f5-163">Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="7f3f5-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="7f3f5-164">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="7f3f5-164">Related topics</span></span>

- [<span data-ttu-id="7f3f5-165">.nuspec Başvuru</span><span class="sxs-lookup"><span data-stu-id="7f3f5-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="7f3f5-166">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="7f3f5-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="7f3f5-167">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="7f3f5-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7f3f5-168">Çoklu .NET Framework Sürümlerini Destekleme</span><span class="sxs-lookup"><span data-stu-id="7f3f5-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7f3f5-169">MSBuild sahne ve hedeflerini bir pakete dahil et</span><span class="sxs-lookup"><span data-stu-id="7f3f5-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7f3f5-170">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f3f5-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
