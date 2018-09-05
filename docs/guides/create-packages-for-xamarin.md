---
title: (İOS, Android ve Windows için) Xamarin ile Visual Studio 2015 için NuGet paketleri oluşturma
description: Xamarin için NuGet paketleri oluşturmak üzere bir uçtan uca izlenecek yol, iOS, Android ve Windows üzerinde yerel API'lerini kullanın.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: c43f4e80d456214ca354e136db6419a95fc797a0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551914"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="291eb-103">Visual Studio 2015 ile Xamarin'e yönelik paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="291eb-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="291eb-104">Bir paket için Xamarin iOS, Android ve Windows, yerel API'lerin çalışma zamanı işletim sistemine bağlı olarak kullanan kod içerir.</span><span class="sxs-lookup"><span data-stu-id="291eb-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="291eb-105">Bunu yapmak basit olsa da, .NET standart kitaplıkları aracılığıyla ortak bir API yüzey ya da geliştiriciler bir PCL paketinden kullanmasına izin vermek için tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="291eb-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="291eb-106">Bu izlenecek yolda, kullandığınız Visual Studio 2015 iOS, Android ve Windows mobil projeleri kullanılabilir platformlar arası bir NuGet paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="291eb-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="291eb-107">Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="291eb-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="291eb-108">Proje yapısını ve Özet kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="291eb-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="291eb-109">Platforma özgü kod yazma</span><span class="sxs-lookup"><span data-stu-id="291eb-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="291eb-110">Oluşturma ve güncelleştirme .nuspec dosyası</span><span class="sxs-lookup"><span data-stu-id="291eb-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="291eb-111">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="291eb-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="291eb-112">İlgili Konular</span><span class="sxs-lookup"><span data-stu-id="291eb-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="291eb-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="291eb-113">Prerequisites</span></span>

1. <span data-ttu-id="291eb-114">Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="291eb-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="291eb-115">Yamasını ücretsiz Community edition [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="291eb-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="291eb-116">UWP ve Xamarin araçları dahil etmek için bir özel yükleme seçeneğini belirleyin ve uygun seçeneklerini işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="291eb-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="291eb-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="291eb-117">NuGet CLI.</span></span> <span data-ttu-id="291eb-118">Nuget.exe en son sürümünü indirin [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="291eb-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="291eb-119">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="291eb-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="291eb-120">nuget.exe CLI aracı kendisini bir yükleyici dolayısıyla bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="291eb-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="291eb-121">Proje yapısını ve Özet kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="291eb-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="291eb-122">İndirme ve çalıştırma [Xamarin Şablonları uzantısı için eklenti](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="291eb-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="291eb-123">Bu şablonlar Bu izlenecek yol için gerekli proje yapısını oluşturmak kolaylaştıracak.</span><span class="sxs-lookup"><span data-stu-id="291eb-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="291eb-124">Visual Studio'da **Dosya > Yeni > Proje**, arama `Plugin`seçin **Xamarin için eklentisi** şablon LoggingLibrary için adı değiştirin ve Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="291eb-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio'da yeni bir boş uygulama (Xamarin.Forms taşınabilir) projesine](media/CrossPlatform-NewProject.png)

<span data-ttu-id="291eb-126">Sonuçta elde edilen çözümü ile çeşitli platforma özgü projeleri birlikte iki PCL projeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="291eb-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="291eb-127">Adlı PCL `Plugin.LoggingLibrary.Abstractions (Portable)`, bu durumda bileşenin genel arabirimi (API yüzey alanı) tanımlar `ILoggingLibrary` ILoggingLibrary.cs dosyasında yer alan arabirimi.</span><span class="sxs-lookup"><span data-stu-id="291eb-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="291eb-128">Arayüzü kitaplığınıza tanımladığınız budur.</span><span class="sxs-lookup"><span data-stu-id="291eb-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="291eb-129">Diğer PCL `Plugin.LoggingLibrary (Portable)`, platforma özel uygulanışı soyut arabirimi çalışma zamanında bulur CrossLoggingLibrary.cs kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="291eb-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="291eb-130">Genellikle bu dosyayı değiştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="291eb-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="291eb-131">Gibi platforma özgü projeleri `Plugin.LoggingLibrary.Android`, her içeren ilgili LoggingLibraryImplementation.cs dosyalarına arabiriminde yerel bir uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="291eb-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="291eb-132">Kitaplığınızın kodu, oluşturduğunuz budur.</span><span class="sxs-lookup"><span data-stu-id="291eb-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="291eb-133">Varsayılan olarak, arabirim tanımı, ancak hiçbir yöntemleri soyutlama projenin ILoggingLibrary.cs dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="291eb-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="291eb-134">Bu izlenecek yolda amacı doğrultusunda, ekleme bir `Log` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="291eb-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="291eb-135">Platforma özgü kod yazma</span><span class="sxs-lookup"><span data-stu-id="291eb-135">Write your platform-specific code</span></span>

<span data-ttu-id="291eb-136">Platforma özel uygulanışı uygulamak için `ILoggingLibrary` arabirimi ve yöntemlerinin, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="291eb-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="291eb-137">Açık `LoggingLibraryImplementation.cs` dosya her platform için proje ve gerekli kodu eklemek.</span><span class="sxs-lookup"><span data-stu-id="291eb-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="291eb-138">Örneğin (kullanarak `Plugin.LoggingLibrary.Android` Proje):</span><span class="sxs-lookup"><span data-stu-id="291eb-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="291eb-139">Bu uygulama projelerindeki desteklemek istediğiniz her platform için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="291eb-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="291eb-140">İOS projesine sağ tıklayın, **özellikleri**, tıklayın **derleme** sekmesini tıklatın ve "\iPhone" kaldırma **çıkış yolu** ve **XML belge dosyası**  ayarları.</span><span class="sxs-lookup"><span data-stu-id="291eb-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="291eb-141">Bu kılavuzda daha sonra kolaylık olması için yalnızca budur.</span><span class="sxs-lookup"><span data-stu-id="291eb-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="291eb-142">İşiniz bittiğinde dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="291eb-142">Save the file when done.</span></span>
1. <span data-ttu-id="291eb-143">Çözüme sağ tıklayın, **Configuration Manager...** ve **derleme** PCLs ve destekleyen her platform için kutuları.</span><span class="sxs-lookup"><span data-stu-id="291eb-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="291eb-144">Çözüme sağ tıklayıp **Çözümü Derle** iş denetleyin ve sonraki paketini yapıları üretmek için.</span><span class="sxs-lookup"><span data-stu-id="291eb-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="291eb-145">Eksik başvurular hakkında hataları alırsanız, çözüme sağ tıklayın, **NuGet paketlerini geri yükle** bağımlılıklarını yükleyin ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="291eb-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="291eb-146">İOS için oluşturmak için bir ağa bağlı Mac üzerinde açıklandığı gibi Visual Studio'ya bağlı gereksinim [Visual Studio için Xamarin.ios'a giriş](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="291eb-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="291eb-147">Kullanılabilir Mac yoksa, Yapılandırma Yöneticisi'nin (yukarıdaki adım 3) iOS projesi temizleyin.</span><span class="sxs-lookup"><span data-stu-id="291eb-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="291eb-148">Oluşturma ve güncelleştirme .nuspec dosyası</span><span class="sxs-lookup"><span data-stu-id="291eb-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="291eb-149">Bir komut istemi açın ve gidin `LoggingLibrary` nerede aşağıda bir düzey klasör `.sln` dosyası olduğunu ve NuGet komutunu çalıştırarak `spec` ilk oluşturmak için komut `Package.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="291eb-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="291eb-150">Bu dosyayı yeniden adlandır `LoggingLibrary.nuspec` ve bir düzenleyicide açın.</span><span class="sxs-lookup"><span data-stu-id="291eb-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="291eb-151">Aşağıdaki ile eşleşecek şekilde dosyasını güncelleştirme YOUR_NAME uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="291eb-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="291eb-152">`<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="291eb-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="291eb-153">Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="291eb-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="291eb-154">Paket sürümünüzle sonekine sahip `-alpha`, `-beta` veya `-rc` paketinizi yayın öncesi olarak işaretlemek için denetleme [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) yayın öncesi sürümleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="291eb-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="291eb-155">Başvuru bütünleştirilmiş kodları Ekle</span><span class="sxs-lookup"><span data-stu-id="291eb-155">Add reference assemblies</span></span>

<span data-ttu-id="291eb-156">Platforma özgü başvuru bütünleştirilmiş kodları eklemek için aşağıdaki ekleyin `<files>` öğesinin `LoggingLibrary.nuspec` , desteklenen platformlar için uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="291eb-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="291eb-157">DLL ve XML dosyalarının adlarını kısaltmak için herhangi bir proje üzerinde select sağ **Kitaplığı** sekme ve derleme adları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="291eb-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="291eb-158">Bağımlılıkları ekleyin</span><span class="sxs-lookup"><span data-stu-id="291eb-158">Add dependencies</span></span>

<span data-ttu-id="291eb-159">Yerel uygulamaları için belirli bağımlılıkları varsa, `<dependencies>` öğeyle `<group>` öğeleri, örneğin belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="291eb-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="291eb-160">Örneğin, aşağıdaki iTextSharp UAP hedefi için bağımlılık olarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="291eb-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="291eb-161">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="291eb-161">Final .nuspec</span></span>

<span data-ttu-id="291eb-162">Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden YOUR_NAME uygun bir değer ile değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="291eb-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="291eb-163">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="291eb-163">Package the component</span></span>

<span data-ttu-id="291eb-164">Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="291eb-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="291eb-165">Bu işlem oluşturur `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="291eb-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="291eb-166">Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:</span><span class="sxs-lookup"><span data-stu-id="291eb-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet paket Gezgini LoggingLibrary paket gösteriliyor](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="291eb-168">A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="291eb-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="291eb-169">Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="291eb-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="291eb-170">Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="291eb-170">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="291eb-171">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="291eb-171">Related topics</span></span>

- [<span data-ttu-id="291eb-172">Nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="291eb-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="291eb-173">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="291eb-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="291eb-174">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="291eb-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="291eb-175">Birden çok .NET Framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="291eb-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="291eb-176">MSBuild özellikler ve hedefler bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="291eb-176">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="291eb-177">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="291eb-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)