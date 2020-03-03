---
title: Evrensel Windows Platformu için NuGet paketleri oluşturma
description: İçindeki C#Evrensel Windows platformu için bir Windows çalışma zamanı bileşeni kullanarak NuGet paketleri oluşturmaya yönelik uçtan uca bir yönerge.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231807"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="eb5c4-103">UWP paketleri oluşturma (C#)</span><span class="sxs-lookup"><span data-stu-id="eb5c4-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="eb5c4-104">[Evrensel Windows platformu (UWP)](/windows/uwp) , Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="eb5c4-105">Bu modelde, UWP uygulamaları tüm cihazlarda ortak olan WinRT API 'Lerini ve ayrıca uygulamanın üzerinde çalıştığı cihaz ailesine özgü API 'Leri (Win32 ve .NET dahil) çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="eb5c4-106">Bu kılavuzda, hem yönetilen hem de yerel projelerde kullanılabilen C# UWP BILEŞENI (XAML denetimi dahil) Ile bir NuGet paketi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb5c4-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="eb5c4-107">Prerequisites</span></span>

1. <span data-ttu-id="eb5c4-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-108">Visual Studio 2019.</span></span> <span data-ttu-id="eb5c4-109">[VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz olarak 2019 Community Edition 'ı yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="eb5c4-110">NuGet CLı.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-110">NuGet CLI.</span></span> <span data-ttu-id="eb5c4-111">En son `nuget.exe` sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin, bunu istediğiniz konuma kaydederek (indirme işlemi doğrudan `.exe`).</span><span class="sxs-lookup"><span data-stu-id="eb5c4-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="eb5c4-112">Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="eb5c4-113">[Daha fazla ayrıntı](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="eb5c4-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="eb5c4-114">UWP Windows Çalışma Zamanı bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb5c4-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="eb5c4-115">Visual Studio 'da **dosya > yeni > proje**' yi seçin, "UWP c#" araması yapın, **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablonunu seçin, ileri ' ye tıklayın, adı ImageEnhancer olarak değiştirin ve Oluştur ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="eb5c4-116">İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Yeni UWP Windows Çalışma Zamanı bileşen projesi oluşturma](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="eb5c4-118">Çözüm Gezgini projeye sağ tıklayın, **> yeni öğe Ekle**' yi seçin, **şablonlu denetim**' i seçin, adı AwesomeImageControl.cs olarak değiştirin ve **Ekle**' ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleniyor](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="eb5c4-120">Çözüm Gezgini ' de projeye sağ tıklayın ve Özellikler ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="eb5c4-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="eb5c4-121">Özellikler sayfasında, **derleme** sekmesi ' ni seçin ve **XML belge dosyasını**etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![XML belge dosyalarını oluştur Evet olarak ayarlanıyor](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="eb5c4-123">Şimdi *çözüme* sağ tıklayın, **Batch Build**' i seçin, iletişim kutusundaki beş derleme kutusunu aşağıda gösterildiği gibi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="eb5c4-124">Bu, bir yapı yaparken, Windows 'un desteklediği her bir hedef sistem için tam bir yapıt kümesi üretmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Batch derlemesi](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="eb5c4-126">Toplu derleme iletişim kutusunda, projeyi doğrulamak ve NuGet paketi için ihtiyaç duyduğunuz çıkış dosyalarını oluşturmak için **Oluştur** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="eb5c4-127">Bu kılavuzda, paket için hata ayıklama yapıtlarını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="eb5c4-128">Hata ayıklama olmayan paket için, bunun yerine toplu derleme iletişim kutusunda sürüm seçeneklerini işaretleyin ve izleyen adımlarda ortaya çıkan sürüm klasörlerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="eb5c4-129">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="eb5c4-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="eb5c4-130">İlk `.nuspec` dosyasını oluşturmak için aşağıdaki üç adımı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="eb5c4-131">Aşağıdaki bölümlerde, diğer gerekli güncelleştirmelerde size rehberlik sağlanır.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="eb5c4-132">Bir komut istemi açın ve `ImageEnhancer.csproj` içeren klasöre gidin (Bu, çözüm dosyasının bulunduğu alt klasör olacaktır).</span><span class="sxs-lookup"><span data-stu-id="eb5c4-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="eb5c4-133">`ImageEnhancer.nuspec` oluşturmak için [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) komutunu çalıştırın (dosyanın adı `.csroj` dosyanın adından alınır):</span><span class="sxs-lookup"><span data-stu-id="eb5c4-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="eb5c4-134">`ImageEnhancer.nuspec` bir düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek, bunları bir düzenleyicide eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="eb5c4-135">$PropertyName $ değerlerinden hiçbirini bırakmayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="eb5c4-136">`<id>` değeri özellikle, nuget.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="eb5c4-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="eb5c4-137">Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="eb5c4-138">Ortak tüketim için oluşturulmuş paketler için, bu Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olmak üzere `<tags>` öğesine özel bir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="eb5c4-139">Windows meta verileri pakete ekleniyor</span><span class="sxs-lookup"><span data-stu-id="eb5c4-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="eb5c4-140">Windows Çalışma Zamanı bileşeni, diğer uygulamaların ve kitaplıkların bileşeni tüketmesini sağlayan, genel olarak kullanılabilir tüm türlerini açıklayan meta veriler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="eb5c4-141">Bu meta veriler, projeyi derlerken oluşturulan ve NuGet paketinize dahil etmeniz gereken bir. winmd dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="eb5c4-142">IntelliSense verilerine sahip bir XML dosyası aynı anda oluşturulmuştur ve de dahil edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="eb5c4-143">Aşağıdaki `<files>` düğümünü `.nuspec` dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="eb5c4-144">XAML içeriği ekleme</span><span class="sxs-lookup"><span data-stu-id="eb5c4-144">Adding XAML content</span></span>

<span data-ttu-id="eb5c4-145">Bileşeninizdeki XAML denetimini eklemek için, denetimin varsayılan şablonuna sahip XAML dosyasını (proje şablonu tarafından oluşturulan olarak) eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="eb5c4-146">Bu da `<files>` bölümüne gider:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="eb5c4-147">Yerel uygulama kitaplıklarını ekleme</span><span class="sxs-lookup"><span data-stu-id="eb5c4-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="eb5c4-148">Bileşeninizin içinde, ImageEnhancer türünün Çekirdek mantığı, her bir hedef çalışma zamanı (ARM, ARM64, x86 ve x64) için oluşturulan çeşitli `ImageEnhancer.winmd` derlemelerindeki yerel kodda bulunur.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="eb5c4-149">Bunları pakete eklemek için, `<files>` bölümünde ilişkili. pri kaynak dosyalarıyla birlikte bunlara başvurun:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="eb5c4-150">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="eb5c4-150">Final .nuspec</span></span>

<span data-ttu-id="eb5c4-151">Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada tekrar YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="eb5c4-152">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="eb5c4-152">Package the component</span></span>

<span data-ttu-id="eb5c4-153">Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlanmış `.nuspec` ile [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) komutunu çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="eb5c4-154">Bu, `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="eb5c4-155">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="eb5c4-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![ImageEnhancer paketini gösteren NuGet Paket Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="eb5c4-157">`.nupkg` dosyası, farklı uzantılı yalnızca bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="eb5c4-158">Ayrıca, paket içeriğini inceleyebilir, sonra `.nupkg` `.zip`olarak değiştirebilir, ancak paketi nuget.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="eb5c4-159">Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="eb5c4-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="eb5c4-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="eb5c4-160">Related topics</span></span>

- [<span data-ttu-id="eb5c4-161">. nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="eb5c4-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="eb5c4-162">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="eb5c4-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="eb5c4-163">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb5c4-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="eb5c4-164">Çoklu .NET Framework sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="eb5c4-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="eb5c4-165">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="eb5c4-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="eb5c4-166">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb5c4-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
