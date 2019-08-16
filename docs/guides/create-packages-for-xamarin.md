---
title: Visual Studio 2015 ile Xamarin (iOS, Android ve Windows için) için NuGet paketleri oluşturma
description: İOS, Android ve Windows 'da yerel API 'Ler kullanan Xamarin için NuGet paketleri oluşturmaya yönelik uçtan uca bir anlatım.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 927991429d8d4ce54aa35be3e450475a38141b11
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488907"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="54456-103">Visual Studio 2015 ile Xamarin’e yönelik paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="54456-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="54456-104">Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows 'da yerel API 'Ler kullanan kod içerir.</span><span class="sxs-lookup"><span data-stu-id="54456-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="54456-105">Bu, basit olsa da, geliştiricilerin ortak bir API yüzey alanı aracılığıyla bir PCL veya .NET Standard kitaplıklarından paketi kullanmasına izin vermek tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="54456-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="54456-106">Bu kılavuzda, Visual Studio 2015 ' u kullanarak iOS, Android ve Windows 'da mobil projelerde kullanılabilecek bir platformlar arası NuGet paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54456-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="54456-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="54456-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="54456-108">Proje yapısı ve soyutlama kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="54456-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="54456-109">Platforma özgü kodunuzu yazma</span><span class="sxs-lookup"><span data-stu-id="54456-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="54456-110">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="54456-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="54456-111">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="54456-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="54456-112">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="54456-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="54456-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="54456-113">Prerequisites</span></span>

1. <span data-ttu-id="54456-114">Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="54456-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="54456-115">Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54456-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="54456-116">UWP ve Xamarin araçlarını dahil etmek için özel bir yüklemeyi seçin ve uygun seçenekleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="54456-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="54456-117">NuGet CLı.</span><span class="sxs-lookup"><span data-stu-id="54456-117">NuGet CLI.</span></span> <span data-ttu-id="54456-118">NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="54456-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="54456-119">Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="54456-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="54456-120">NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="54456-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="54456-121">Proje yapısı ve soyutlama kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="54456-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="54456-122">Visual Studio için [Xamarin şablonları uzantısı eklentisini](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirip çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54456-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="54456-123">Bu şablonlar, Bu izlenecek yol için gerekli proje yapısını oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="54456-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="54456-124">Visual Studio 'da **Dosya > Yeni > proje**, arama `Plugin`, **Xamarin şablonu için eklentiyi** seçme, adı logginglibrary olarak değiştirme ve Tamam ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="54456-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio 'da yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

<span data-ttu-id="54456-126">Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki adet PCL projesi içerir:</span><span class="sxs-lookup"><span data-stu-id="54456-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="54456-127">PCL adlı `Plugin.LoggingLibrary.Abstractions (Portable)`, bileşenin genel arabirimini (API yüzey alanı) tanımlar, bu `ILoggingLibrary` durumda arabirim ILoggingLibrary.cs dosyasında yer alır.</span><span class="sxs-lookup"><span data-stu-id="54456-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="54456-128">Bu, kitaplığınızın arabirimini tanımladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="54456-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="54456-129">Diğer PCL `Plugin.LoggingLibrary (Portable)`, çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulacak CrossLoggingLibrary.cs içinde kod içerir.</span><span class="sxs-lookup"><span data-stu-id="54456-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="54456-130">Genellikle bu dosyayı değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="54456-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="54456-131">Her biri gibi platforma özgü projeler `Plugin.LoggingLibrary.Android`, ilgili LoggingLibraryImplementation.cs dosyalarında arabirimin yerel bir uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="54456-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="54456-132">Bu, kitaplığınızın kodunu oluşturduğunuz yerdir.</span><span class="sxs-lookup"><span data-stu-id="54456-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="54456-133">Varsayılan olarak, soyut olanaklar projesinin ILoggingLibrary.cs dosyası bir arabirim tanımı içerir, ancak hiçbir yöntem yoktur.</span><span class="sxs-lookup"><span data-stu-id="54456-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="54456-134">Bu izlenecek yolun amaçları doğrultusunda, aşağıdaki gibi bir `Log` yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="54456-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="54456-135">Platforma özgü kodunuzu yazma</span><span class="sxs-lookup"><span data-stu-id="54456-135">Write your platform-specific code</span></span>

<span data-ttu-id="54456-136">`ILoggingLibrary` Arabirimin ve yöntemlerinin platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="54456-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="54456-137">Her platform projesinin dosyasını açın ve gerekli kodu ekleyin. `LoggingLibraryImplementation.cs`</span><span class="sxs-lookup"><span data-stu-id="54456-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="54456-138">Örneğin ( `Plugin.LoggingLibrary.Android` projeyi kullanarak):</span><span class="sxs-lookup"><span data-stu-id="54456-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

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

1. <span data-ttu-id="54456-139">Desteklemek istediğiniz her platform için bu uygulamayı projelerde tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="54456-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="54456-140">İOS projesine sağ tıklayın, **Özellikler**' i seçin, **derleme** sekmesine tıklayın ve "\Iphone" öğesini **çıkış yolundan** ve **XML belge dosyası** ayarlarından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="54456-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="54456-141">Bu, bu kılavuzda daha sonra kolaylık sağlaması için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="54456-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="54456-142">Bitince dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="54456-142">Save the file when done.</span></span>
1. <span data-ttu-id="54456-143">Çözüme sağ tıklayın, **Configuration Manager...** öğesini seçin ve ardından, destekettiğiniz her platform için **Yapı** kutularını işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="54456-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="54456-144">Çözüme sağ tıklayın ve işinizi denetlemek ve daha sonra paketettiğiniz yapıtları oluşturmak için **çözüm oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="54456-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="54456-145">Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **NuGet paketlerini geri yükle** ' yi seçin ve yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="54456-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="54456-146">İOS için derlemek için, Visual Studio için [Xamarin. iOS 'A giriş bölümünde](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi, Visual Studio 'ya bağlı ağa bağlı bir Mac gereklidir.</span><span class="sxs-lookup"><span data-stu-id="54456-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="54456-147">Kullanılabilir bir Mac yoksa, Configuration Manager 'daki iOS projesi seçimini kaldırın (yukarıdaki 3. adım).</span><span class="sxs-lookup"><span data-stu-id="54456-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="54456-148">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="54456-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="54456-149">Bir `LoggingLibrary` komut istemi açın, `.sln` dosyanın altında bir düzey olan klasöre gidin ve ilk `Package.nuspec` dosyayı oluşturmak için NuGet `spec` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="54456-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="54456-150">Bu dosyayı olarak `LoggingLibrary.nuspec` yeniden adlandırın ve bir düzenleyicide açın.</span><span class="sxs-lookup"><span data-stu-id="54456-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="54456-151">Dosyayı aşağıdaki ile eşleşecek şekilde güncelleştirin, YOUR_NAME değiştirerek uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54456-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="54456-152">Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). `<id>`</span><span class="sxs-lookup"><span data-stu-id="54456-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="54456-153">Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="54456-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="54456-154">Paket `-alpha`sürümünüzü ile `-beta` sonekine veya `-rc` paketinizi ön sürüm olarak işaretlemek için yayın öncesi sürümler hakkında daha fazla bilgi için [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54456-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="54456-155">Başvuru derlemeleri Ekle</span><span class="sxs-lookup"><span data-stu-id="54456-155">Add reference assemblies</span></span>

<span data-ttu-id="54456-156">Platforma özgü başvuru derlemelerini dahil etmek için, aşağıdaki `<files>` öğesine desteklenen platformlarınız için uygun olan `LoggingLibrary.nuspec` öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="54456-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="54456-157">DLL ve XML dosyalarının adlarını kısaltmak için, belirli bir projeye sağ tıklayın, **kitaplık** sekmesini seçin ve derleme adlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54456-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="54456-158">Bağımlılık Ekle</span><span class="sxs-lookup"><span data-stu-id="54456-158">Add dependencies</span></span>

<span data-ttu-id="54456-159">Yerel uygulamalar için belirli bağımlılıklarınız varsa, bu `<dependencies>` öğeyi belirtmek için öğeleri ile `<group>` kullanın, örneğin:</span><span class="sxs-lookup"><span data-stu-id="54456-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="54456-160">Örneğin, aşağıdaki, IAP hedefi için bir bağımlılık olarak ıtextsharp olarak ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="54456-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="54456-161">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="54456-161">Final .nuspec</span></span>

<span data-ttu-id="54456-162">Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada yeniden YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="54456-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="54456-163">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="54456-163">Package the component</span></span>

<span data-ttu-id="54456-164">Pakete dahil etmeniz `.nuspec` gereken tüm dosyalara başvuran tamamlandığında, `pack` komutunu çalıştırmaya hazırsınız demektir:</span><span class="sxs-lookup"><span data-stu-id="54456-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="54456-165">Bu işlem `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="54456-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="54456-166">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="54456-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![LoggingLibrary paketini gösteren NuGet Paket Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="54456-168">`.nupkg` Dosya, yalnızca farklı bir uzantıya sahip bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="54456-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="54456-169">Paket içeriğini `.nupkg` de inceleyebilir, ancak öğesini olarak `.zip`değiştirebilir, ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="54456-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="54456-170">Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="54456-170">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="54456-171">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="54456-171">Related topics</span></span>

- [<span data-ttu-id="54456-172">Nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="54456-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="54456-173">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="54456-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="54456-174">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="54456-174">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="54456-175">Çoklu .NET Framework sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="54456-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="54456-176">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="54456-176">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="54456-177">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="54456-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)