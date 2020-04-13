---
title: Evrensel Windows Platformu için NuGet Paketleri Oluşturun
description: C#'daki Evrensel Windows Platformu için Windows Runtime Bileşeni ni kullanarak NuGet paketleri oluşturmanın uçtan uca bir bölümü.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231807"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="098f7-103">UWP paketleri oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="098f7-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="098f7-104">[Evrensel Windows Platformu (UWP),](/windows/uwp) Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="098f7-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="098f7-105">Bu modelde, UWP uygulamaları hem tüm cihazlarda ortak olan WinRT API'lerini hem de uygulamanın çalıştırıldığı aygıt ailesine özgü API'leri (Win32 ve .NET dahil) arayabilir.</span><span class="sxs-lookup"><span data-stu-id="098f7-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="098f7-106">Bu izlenecek yolda, hem Yönetilen hem de Yerel projelerde kullanılabilecek bir C# UWP bileşenine (XAML denetimi dahil) sahip bir NuGet paketi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="098f7-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="098f7-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="098f7-107">Prerequisites</span></span>

1. <span data-ttu-id="098f7-108">Görsel Stüdyo 2019.</span><span class="sxs-lookup"><span data-stu-id="098f7-108">Visual Studio 2019.</span></span> <span data-ttu-id="098f7-109">2019 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/)ücretsiz olarak yükleyin; Profesyonel ve Kurumsal sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="098f7-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="098f7-110">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="098f7-110">NuGet CLI.</span></span> <span data-ttu-id="098f7-111">nuget.org/downloads en son `nuget.exe` [nuget.org/downloads](https://nuget.org/downloads)sürümünü indirin, seçtiğiniz bir konuma kaydedin `.exe` (indirme doğrudan).</span><span class="sxs-lookup"><span data-stu-id="098f7-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="098f7-112">Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="098f7-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="098f7-113">[Daha fazla ayrıntı](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="098f7-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="098f7-114">UWP Windows Runtime bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="098f7-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="098f7-115">Visual **Studio'> da, > "uwp**c#" araması, **Windows Runtime Bileşeni (Evrensel Windows)** şablonunu seçin, sonrakini tıklatın, adı ImageEnhancer olarak değiştirin ve Oluştur'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="098f7-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="098f7-116">İstendiğinde Hedef Sürüm ve Minimum Sürüm için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="098f7-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Yeni bir UWP Windows Runtime Bileşeni projesi oluşturma](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="098f7-118">Solution Explorer'da projeyi sağ tıklatın, **Yeni Öğe > Ekle'yi**seçin, **Şablon denetimini**seçin, AwesomeImageControl.cs adını değiştirin ve **Ekle'yi**tıklatın:</span><span class="sxs-lookup"><span data-stu-id="098f7-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Projeye yeni bir XAML Şablondenetim öğesi ekleme](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="098f7-120">Solution Explorer'da projeyi sağ tıklatın ve **Özellikler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="098f7-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="098f7-121">Özellikler sayfasında, **Yapı** sekmesini seçin ve **XML Belgedosyasını**etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="098f7-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![XML Belge Dosyalarını Evet'e Ayarlama](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="098f7-123">Şimdi *çözüme* sağ tıklayın, **Toplu Yapı'yı**seçin, iletişim kutusundaki beş yapı kutusunu aşağıda gösterildiği gibi işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="098f7-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="098f7-124">Bu, bir yapı yaptığınızda, Windows'un desteklediği hedef sistemlerin her biri için tam bir yapı kümesi oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="098f7-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Toplu Yapı](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="098f7-126">Toplu Yapı iletişim kutusunda ve projeyi doğrulamak ve NuGet paketi için ihtiyacınız olan çıktı dosyalarını oluşturmak için **Oluştur'u** tıklatın.</span><span class="sxs-lookup"><span data-stu-id="098f7-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="098f7-127">Bu gözden geçirme de paket için Hata Ayıklama yapıtlarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="098f7-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="098f7-128">Hata ayıklama paketi için, Toplu Yapı iletişim kutusundaki Sürüm seçeneklerini denetleyin ve ardından gelen Sürüm klasörlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="098f7-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="098f7-129">.nuspec dosyasını oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="098f7-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="098f7-130">İlk `.nuspec` dosyayı oluşturmak için aşağıdaki üç adımı yapın.</span><span class="sxs-lookup"><span data-stu-id="098f7-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="098f7-131">Ardından gelen bölümler daha sonra diğer gerekli güncelleştirmeler boyunca size rehberlik.</span><span class="sxs-lookup"><span data-stu-id="098f7-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="098f7-132">Bir komut istemi açın ve `ImageEnhancer.csproj` içeren klasöre gidin (bu çözüm dosyasının olduğu yerin altında bir alt klasör olacaktır).</span><span class="sxs-lookup"><span data-stu-id="098f7-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="098f7-133">Oluşturmak [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) `ImageEnhancer.nuspec` için komutu çalıştırın `.csroj` (dosyanın adı dosyanın adından alınır):</span><span class="sxs-lookup"><span data-stu-id="098f7-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="098f7-134">Bir `ImageEnhancer.nuspec` düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek aşağıdakilerle eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="098f7-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="098f7-135">$propertyName$ değerlerinden hiçbirini bırakmayın.</span><span class="sxs-lookup"><span data-stu-id="098f7-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="098f7-136">Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="098f7-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="098f7-137">Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="098f7-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="098f7-138">Genel tüketim için oluşturulmuş paketler için, `<tags>` bu etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, öğeye özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="098f7-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="098f7-139">Pakete Windows meta verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="098f7-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="098f7-140">Windows Runtime Bileşeni, genel kullanıma açık tüm türlerini açıklayan meta veriler gerektirir ve bu da diğer uygulamaların ve kitaplıkların bileşeni tüketmesini mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="098f7-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="098f7-141">Bu meta veriler, projeyi derlediğinizde oluşturulan ve NuGet paketinize eklenmesi gereken bir .winmd dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="098f7-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="098f7-142">IntelliSense verilerine sahip bir XML dosyası da aynı anda oluşturulur ve eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="098f7-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="098f7-143">`.nuspec` Dosyaya aşağıdaki `<files>` düğümü ekleyin:</span><span class="sxs-lookup"><span data-stu-id="098f7-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="098f7-144">XAML içeriği ekleme</span><span class="sxs-lookup"><span data-stu-id="098f7-144">Adding XAML content</span></span>

<span data-ttu-id="098f7-145">Bileşeninize bir XAML denetimi eklemek için, denetim için varsayılan şablona sahip XAML dosyasını eklemeniz gerekir (proje şablonu tarafından oluşturulan gibi).</span><span class="sxs-lookup"><span data-stu-id="098f7-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="098f7-146">Bu da `<files>` bölümünde gider:</span><span class="sxs-lookup"><span data-stu-id="098f7-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="098f7-147">Yerel uygulama kitaplıklarını ekleme</span><span class="sxs-lookup"><span data-stu-id="098f7-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="098f7-148">Bileşeniniz içinde, ImageEnhancer türünün temel mantığı, her hedef çalışma `ImageEnhancer.winmd` zamanı (ARM, ARM64, x86 ve x64) için oluşturulan çeşitli derlemelerde bulunan yerel koddadır.</span><span class="sxs-lookup"><span data-stu-id="098f7-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="098f7-149">Bunları pakete eklemek için, ilişkili `<files>` .pri kaynak dosyalarıyla birlikte bölüme başvurun:</span><span class="sxs-lookup"><span data-stu-id="098f7-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="098f7-150">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="098f7-150">Final .nuspec</span></span>

<span data-ttu-id="098f7-151">Son `.nuspec` dosyanız şimdi aşağıdaki gibi görünmelidir ve yine YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="098f7-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="098f7-152">Bileşeni paketle</span><span class="sxs-lookup"><span data-stu-id="098f7-152">Package the component</span></span>

<span data-ttu-id="098f7-153">Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="098f7-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="098f7-154">Bu oluşturur. `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`</span><span class="sxs-lookup"><span data-stu-id="098f7-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="098f7-155">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletmek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="098f7-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Paket Explorer ImageEnhancer paketini gösteriyor](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="098f7-157">Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="098f7-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="098f7-158">Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="098f7-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="098f7-159">Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="098f7-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="098f7-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="098f7-160">Related topics</span></span>

- [<span data-ttu-id="098f7-161">.nuspec Başvuru</span><span class="sxs-lookup"><span data-stu-id="098f7-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="098f7-162">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="098f7-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="098f7-163">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="098f7-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="098f7-164">Çoklu .NET Framework Sürümlerini Destekleme</span><span class="sxs-lookup"><span data-stu-id="098f7-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="098f7-165">MSBuild sahne ve hedeflerini bir pakete dahil et</span><span class="sxs-lookup"><span data-stu-id="098f7-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="098f7-166">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="098f7-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
