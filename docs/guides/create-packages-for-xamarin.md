---
title: Visual Studio 2017 veya 2019 ile Xamarin (iOS, Android ve Windows için) için NuGet Paketleri Oluşturun
description: iOS, Android ve Windows'da yerel API'leri kullanan Xamarin için NuGet paketleri oluşturmanın uçtan uca bir walkthrough'u.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230908"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="5d639-103">Visual Studio 2017 veya 2019 ile Xamarin için paketler oluşturun</span><span class="sxs-lookup"><span data-stu-id="5d639-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="5d639-104">Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows'da yerel API'leri kullanan kod lar içerir.</span><span class="sxs-lookup"><span data-stu-id="5d639-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="5d639-105">Bunu yapmak kolay olsa da, geliştiricilerin paketi bir PCL veya .NET Standart kitaplıklarından ortak bir API yüzey alanı üzerinden tüketmesine izin vermek tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="5d639-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="5d639-106">Bu walkthrough'ta Visual Studio 2017 veya 2019'u kullanarak iOS, Android ve Windows'daki mobil projelerde kullanılabilecek bir çapraz platform NuGet paketi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5d639-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="5d639-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5d639-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="5d639-108">Proje yapısını ve soyutlama kodunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d639-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="5d639-109">Platforma özel kodunuzu yazın</span><span class="sxs-lookup"><span data-stu-id="5d639-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="5d639-110">.nuspec dosyasını oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5d639-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="5d639-111">Bileşeni paketle</span><span class="sxs-lookup"><span data-stu-id="5d639-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="5d639-112">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="5d639-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="5d639-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5d639-113">Prerequisites</span></span>

1. <span data-ttu-id="5d639-114">Visual Studio 2017 veya 2019, Universal Windows Platform (UWP) ve Xamarin ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="5d639-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="5d639-115">Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/)ücretsiz olarak yükleyin; Profesyonel ve Kurumsal sürümleri de kullanabilirsiniz, tabii ki.</span><span class="sxs-lookup"><span data-stu-id="5d639-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="5d639-116">UWP ve Xamarin araçlarını eklemek için Özel yükleme'yi seçin ve uygun seçenekleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5d639-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="5d639-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="5d639-117">NuGet CLI.</span></span> <span data-ttu-id="5d639-118">nuget.exe'nin en son sürümünü [nuget.org/downloads](https://nuget.org/downloads)indirin ve seçtiğiniz bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5d639-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="5d639-119">Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5d639-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="5d639-120">nuget.exe cli aracı kendisi değil, bir yükleyici, bu yüzden yerine çalışan tarayıcınızdan indirilen dosyayı kaydetmek için emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d639-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="5d639-121">Proje yapısını ve soyutlama kodunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d639-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="5d639-122">Visual Studio için [Çapraz Platform .NET Standart Eklenti Şablonları uzantısını](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5d639-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="5d639-123">Bu şablonlar, bu gözden geçirme için gerekli proje yapısını oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5d639-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="5d639-124">Visual Studio 2017'de, Dosya > `Plugin`New > **Projesi**, ara , Çapraz Platform **.NET Standart Kitaplık Eklentisi** şablonunu seçin, adınızı LoggingLibrary olarak değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5d639-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![VS 2017'de Yeni Boş Uygulama (Xamarin.Forms Portable) projesi](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="5d639-126">Visual Studio 2019'da, Dosya > `Plugin`New > **Project**, ara , Çapraz Platform **.NET Standart Kitaplık Eklentisi** şablonunu seçin ve İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5d639-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![VS 2019'da Yeni Boş Uygulama (Xamarin.Forms Portable) projesi](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="5d639-128">Adı Günlük Kitaplığı olarak değiştirin ve Oluştur'u tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5d639-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![VS 2019'da Yeni Boş Uygulama (Xamarin.Forms Portable) yapılandırması](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="5d639-130">Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki Paylaşılan proje içerir:</span><span class="sxs-lookup"><span data-stu-id="5d639-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="5d639-131">`ILoggingLibrary.shared.cs` Dosyada bulunan `ILoggingLibrary` proje, bileşenin ortak arabirimini (API yüzey alanı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5d639-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="5d639-132">Burası kitaplığınız için arabirimi tanımladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="5d639-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="5d639-133">Diğer Paylaşılan proje, `CrossLoggingLibrary.shared.cs` çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulabilen kod içerir.</span><span class="sxs-lookup"><span data-stu-id="5d639-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="5d639-134">Genellikle bu dosyayı değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5d639-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="5d639-135">Platforma özgü projeler, `LoggingLibrary.android.cs`her biri kendi `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyalarında arabirimin yerel bir uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="5d639-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="5d639-136">Burası kitaplığınızın kodunu oluşturduğunuz yer.</span><span class="sxs-lookup"><span data-stu-id="5d639-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="5d639-137">Varsayılan olarak, `ILoggingLibrary` projenin ILoggingLibrary.shared.cs dosyası bir arabirim tanımı içerir, ancak yöntem içermez.</span><span class="sxs-lookup"><span data-stu-id="5d639-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="5d639-138">Bu gözden geçirme nin amaçları `Log` için aşağıdaki gibi bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d639-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="5d639-139">Platforma özel kodunuzu yazın</span><span class="sxs-lookup"><span data-stu-id="5d639-139">Write your platform-specific code</span></span>

<span data-ttu-id="5d639-140">Arabirimin ve yöntemlerinin `ILoggingLibrary` platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5d639-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="5d639-141">Her `LoggingLibraryImplementation.cs` platform projesinin (VS `LoggingLibrary.<PLATFORM>.cs` 2017) veya (VS 2019) dosyasını açın ve gerekli kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5d639-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="5d639-142">Örneğin `Android` (platform projesini kullanarak):</span><span class="sxs-lookup"><span data-stu-id="5d639-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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

1. <span data-ttu-id="5d639-143">Desteklemek istediğiniz her platform için projelerde bu uygulamayı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5d639-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="5d639-144">Çözüme sağ tıklayın ve çalışmanızı kontrol etmek ve bir sonraki paketlediğiniz yapıları üretmek için **Çözüm Oluştur'u** seçin.</span><span class="sxs-lookup"><span data-stu-id="5d639-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="5d639-145">Eksik başvurular hakkında hatalar alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **Paketleri Geri Yükle'yi** seçin ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5d639-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="5d639-146">Visual Studio 2019'u kullanıyorsanız, **NuGet Paketlerini Geri Yükle'yi** seçmeden `MSBuild.Sdk.Extras` ve `2.0.54` `LoggingLibrary.csproj`yeniden oluşturmaya çalışmadan önce, 'in sürümünü değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d639-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="5d639-147">Bu dosyaya yalnızca ilk sağ tıklayarak (çözümün altında) ve sonra `Unload Project`boşaltılan projeye sağ tıklayıp . `Edit LoggingLibrary.csproj`</span><span class="sxs-lookup"><span data-stu-id="5d639-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="5d639-148">iOS için oluşturmak için Visual [Studio için Xamarin.iOS'a Giriş'te](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi Visual Studio'ya bağlı ağ bağlantılı bir Mac'e ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="5d639-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="5d639-149">Kullanılabilir bir Mac'inyoksa, iOS projesini yapılandırma yöneticisinden temizleyin (yukarıdaki adım 3).</span><span class="sxs-lookup"><span data-stu-id="5d639-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="5d639-150">.nuspec dosyasını oluşturma ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5d639-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="5d639-151">Komut istemini açın, `LoggingLibrary` `.sln` dosyanın bulunduğu seviyenin altındaki klasöre gidin ve `spec` ilk `Package.nuspec` dosyayı oluşturmak için NuGet komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5d639-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="5d639-152">Bu dosyayı `LoggingLibrary.nuspec` yeniden adlandırın ve bir editörde açın.</span><span class="sxs-lookup"><span data-stu-id="5d639-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="5d639-153">Dosyayı aşağıdakilerle eşleşecek şekilde güncelleştirin ve YOUR_NAME uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5d639-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="5d639-154">Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="5d639-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="5d639-155">Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5d639-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="5d639-156">Paket sürümünüzü `-alpha`ön sürüm olarak `-beta` `-rc` işaretleyebilir veya ön sürüm olarak işaretlemek için, ön sürüm sürümleri hakkında daha fazla bilgi için [ön sürüm sürümlerini](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d639-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="5d639-157">Referans derlemeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="5d639-157">Add reference assemblies</span></span>

<span data-ttu-id="5d639-158">Platforma özgü başvuru derlemelerini eklemek için, `<files>` desteklenen `LoggingLibrary.nuspec` platformlar için uygun olan öğesine aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d639-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="5d639-159">DLL ve XML dosyalarının adlarını kısaltmak için, belirli bir projeye sağ tıklayın, **Kitaplık** sekmesini seçin ve derleme adlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5d639-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="5d639-160">Bağımlılıkekleme</span><span class="sxs-lookup"><span data-stu-id="5d639-160">Add dependencies</span></span>

<span data-ttu-id="5d639-161">Yerel uygulamalar için belirli bağımlılıklarınız varsa, bunları belirtmek için `<dependencies>` öğeleri içeren `<group>` öğeyi kullanın, örneğin:</span><span class="sxs-lookup"><span data-stu-id="5d639-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="5d639-162">Örneğin, aşağıdaki uap hedefi için bir bağımlılık olarak iTextSharp ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5d639-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="5d639-163">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="5d639-163">Final .nuspec</span></span>

<span data-ttu-id="5d639-164">Son `.nuspec` dosyanız şimdi aşağıdaki gibi görünmelidir ve yine YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="5d639-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2018</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="5d639-165">Bileşeni paketle</span><span class="sxs-lookup"><span data-stu-id="5d639-165">Package the component</span></span>

<span data-ttu-id="5d639-166">Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="5d639-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="5d639-167">Bu oluşturur. `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`</span><span class="sxs-lookup"><span data-stu-id="5d639-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="5d639-168">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletmek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="5d639-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Paket Gezgini LoggingLibrary paketini gösteriyor](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="5d639-170">Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5d639-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="5d639-171">Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5d639-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="5d639-172">Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="5d639-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="5d639-173">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="5d639-173">Related topics</span></span>

- [<span data-ttu-id="5d639-174">Nuspec Referans</span><span class="sxs-lookup"><span data-stu-id="5d639-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="5d639-175">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="5d639-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="5d639-176">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="5d639-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="5d639-177">Çoklu .NET Framework Sürümlerini Destekleme</span><span class="sxs-lookup"><span data-stu-id="5d639-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="5d639-178">MSBuild sahne ve hedeflerini bir pakete dahil et</span><span class="sxs-lookup"><span data-stu-id="5d639-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="5d639-179">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d639-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
