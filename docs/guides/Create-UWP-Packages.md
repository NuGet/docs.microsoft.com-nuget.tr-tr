---
title: Evrensel Windows platformu için NuGet paketleri oluşturma
description: Evrensel Windows platformu için bir Windows çalışma zamanı bileşeni kullanarak NuGet paketleri oluşturmanın bir uçtan uca kılavuz.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: a4c609b3390748099d85a73f7d168ebe4de2676a
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812950"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="bd8b5-103">UWP paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd8b5-103">Create UWP packages</span></span>

<span data-ttu-id="bd8b5-104">[Evrensel Windows Platformu (UWP)](https://developer.microsoft.com/windows) ortak bir uygulama platformu, Windows 10 çalıştıran her cihazda sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="bd8b5-105">Bu model içinde UWP uygulamaları tüm cihazlar için ortak bir WinRT API'leri hem de (Win32 ve .NET dahil) ve uygulamanın üzerinde çalıştığı cihaz ailesine özgü API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="bd8b5-106">Bu izlenecek yolda, hem yönetilen hem de yerel projeleri için kullanılabilir (bir XAML denetimi dahil) yerel UWP bileşeni ile bir NuGet paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd8b5-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bd8b5-107">Prerequisites</span></span>

1. <span data-ttu-id="bd8b5-108">Visual Studio 2017 veya Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="bd8b5-109">2017 Community edition ücretsiz yamasını [visualstudio.com](https://www.visualstudio.com/); Professional ve Enterprise sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="bd8b5-110">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-110">NuGet CLI.</span></span> <span data-ttu-id="bd8b5-111">En son sürümünü indirin `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme (indirme `.exe` doğrudan).</span><span class="sxs-lookup"><span data-stu-id="bd8b5-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="bd8b5-112">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="bd8b5-113">Bir UWP Windows çalışma zamanı bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd8b5-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="bd8b5-114">Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C++ > Windows > Evrensel** düğümünü **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablon ImageEnhancer için adı değiştirin ve Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="bd8b5-115">Hedef sürümü ve en düşük istendiğinde sürümü için varsayılan değerleri kabul.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Yeni bir UWP Windows çalışma zamanı bileşeni projesi oluşturma](media/UWP-NewProject.png)

1. <span data-ttu-id="bd8b5-117">Seçin Çözüm Gezgini'nde projeye sağ tıklayın **Ekle > Yeni öğe**, tıklayın **Visual C++ > XAML** düğümünü **şablonlu denetim**, adla değiştirin AwesomeImageControl.cpp seçeneğine tıklayıp **Ekle**:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Projeye yeni bir XAML şablonlu denetim öğe ekleme](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="bd8b5-119">Çözüm Gezgini'nde projeye sağ tıklayıp **özellikleri.**</span><span class="sxs-lookup"><span data-stu-id="bd8b5-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="bd8b5-120">Özellikler sayfasında genişletin **yapılandırma özellikleri > C/C++** tıklatıp **Çıkış dosyalarını**.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="bd8b5-121">Sağ taraftaki bölmede değerini değiştirin **XML belge dosyaları oluştur** Evet:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Ayarı Evet olarak XML belge dosyaları oluştur](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="bd8b5-123">Sağ tıklayın *çözüm* şimdi seçin **Toplu derleme**, aşağıda gösterildiği gibi iletişim kutusundaki üç hata ayıklama kutuları işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="bd8b5-124">Bu, bir derleme yaptığınızda, yapıtlar tam bir dizi her Windows destekleyen hedef sistemleri için oluşturduğunuz emin emin olur.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Toplu derleme](media/UWP-BatchBuild.png)

1. <span data-ttu-id="bd8b5-126">Toplu derleme iletişim ve tıklayın **derleme** proje doğrulamak ve NuGet paketi için gereksinim duyduğunuz çıktı dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="bd8b5-127">Bu izlenecek yolda paket için hata ayıklama yapıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="bd8b5-128">Hata ayıklama olmayan paketi için Toplu derleme iletişim kutusunda yayın seçenekleri yerine denetleyin ve sonuçta elde edilen sürüm klasörler, aşağıdaki adımları başvurun.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="bd8b5-129">Oluşturma ve güncelleştirme .nuspec dosyası</span><span class="sxs-lookup"><span data-stu-id="bd8b5-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="bd8b5-130">İlk oluşturmak için `.nuspec` dosya, aşağıdaki üç adımı yapın.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="bd8b5-131">Ardından aşağıdaki bölümlerde, diğer gerekli güncelleştirmeleri size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="bd8b5-132">Bir komut istemi açın ve klasör içeren dizine gidin `ImageEnhancer.vcxproj` (Bu çözüm dosyasının bulunduğu bir alt aşağıdaki olacaktır).</span><span class="sxs-lookup"><span data-stu-id="bd8b5-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="bd8b5-133">NuGet komutunu çalıştırarak `spec` oluşturmak için komutu `ImageEnhancer.nuspec` (adından dosyasının adı alınmış `.vcxproj` dosyası):</span><span class="sxs-lookup"><span data-stu-id="bd8b5-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="bd8b5-134">Açık `ImageEnhancer.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirmeniz YOUR_NAME uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="bd8b5-135">`<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="bd8b5-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="bd8b5-136">Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="bd8b5-137">Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi olarak, bu etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="bd8b5-138">Windows meta veri paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="bd8b5-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="bd8b5-139">Bir Windows çalışma zamanı bileşeni tüm diğer uygulamaları ve kitaplıkları bileşeni kullanma için mümkün kılar, genel kullanıma açık türleri açıklayan meta verileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="bd8b5-140">Bu meta veriler, projeyi derleyin ve NuGet paketle birlikte oluşturulduğu bir .winmd dosyası içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="bd8b5-141">IntelliSense verilerini içeren bir XML dosyası da aynı anda yerleşik olarak bulunur ve de eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="bd8b5-142">Aşağıdaki `<files>` düğüme `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="bd8b5-143">XAML İçerik ekleme</span><span class="sxs-lookup"><span data-stu-id="bd8b5-143">Adding XAML content</span></span>

<span data-ttu-id="bd8b5-144">Bir XAML bileşeniniz Generic.XAML'yi eklemeniz (proje şablonu tarafından oluşturulan gibi) bir denetim için varsayılan şablonu olan bir XAML dosyası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="bd8b5-145">Bu ayrıca gider `<files>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="bd8b5-146">Yerel uygulama kitaplıkları ekleme</span><span class="sxs-lookup"><span data-stu-id="bd8b5-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="bd8b5-147">Bileşeniniz çeşitli yer alan yerel kod ImageEnhancer türü çekirdek mantığını bulunduğu `ImageEnhancer.dll` her hedef çalışma zamanı (x 86 ve x64, ARM) için oluşturulan derlemeler.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="bd8b5-148">Bu paketi eklemek için bunları başvuru `<files>` ilişkili .pri kaynak dosyalarla birlikte bölümü:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="bd8b5-149">.Targets ekleme</span><span class="sxs-lookup"><span data-stu-id="bd8b5-149">Adding .targets</span></span>

<span data-ttu-id="bd8b5-150">Ardından, NuGet paketinizi tüketebilir C++ ve JavaScript projeleri, gerekli bütünleştirilmiş kod ve winmd dosyaları belirlemek için bir .targets dosyasında gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="bd8b5-151">(C# ve Visual Basic projeleri otomatik olarak bunu.) Aşağıdaki metni içine kopyalayarak bu dosyayı oluşturmak `ImageEnhancer.targets` ve aynı klasöre kaydedin `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="bd8b5-152">_Not_: Bu `.targets` dosya paket kimliği adıyla aynı olması gerekir (örneğin `<Id>` öğesinde `.nupspec` dosyası):</span><span class="sxs-lookup"><span data-stu-id="bd8b5-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="bd8b5-153">Daha sonra başvurmak `ImageEnhancer.targets` içinde `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="bd8b5-154">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="bd8b5-154">Final .nuspec</span></span>

<span data-ttu-id="bd8b5-155">Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden YOUR_NAME uygun bir değer ile değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="bd8b5-156">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="bd8b5-156">Package the component</span></span>

<span data-ttu-id="bd8b5-157">Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="bd8b5-158">Bu oluşturur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="bd8b5-159">Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:</span><span class="sxs-lookup"><span data-stu-id="bd8b5-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet paket Gezgini ImageEnhancer paket gösteriliyor](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="bd8b5-161">A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="bd8b5-162">Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bd8b5-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="bd8b5-163">Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bd8b5-163">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="bd8b5-164">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="bd8b5-164">Related topics</span></span>

- [<span data-ttu-id="bd8b5-165">.nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="bd8b5-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="bd8b5-166">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="bd8b5-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="bd8b5-167">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd8b5-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="bd8b5-168">Birden çok .NET Framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="bd8b5-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bd8b5-169">Bir pakete MSBuild özellikler ve hedefler</span><span class="sxs-lookup"><span data-stu-id="bd8b5-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="bd8b5-170">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd8b5-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
