---
title: Visual Studio 2017 veya 2019 ile Xamarin (iOS, Android ve Windows için) için NuGet paketleri oluşturma
description: İOS, Android ve Windows 'da yerel API 'Ler kullanan Xamarin için NuGet paketleri oluşturmaya yönelik uçtan uca bir anlatım.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385700"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="6672b-103">Visual Studio 2017 veya 2019 ile Xamarin için paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="6672b-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="6672b-104">Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows 'da yerel API 'Ler kullanan kod içerir.</span><span class="sxs-lookup"><span data-stu-id="6672b-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="6672b-105">Bu, basit olsa da, geliştiricilerin ortak bir API yüzey alanı aracılığıyla bir PCL veya .NET Standard kitaplıklarından paketi kullanmasına izin vermek tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="6672b-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="6672b-106">Bu kılavuzda, iOS, Android ve Windows 'da mobil projelerde kullanılabilecek platformlar arası bir NuGet paketi oluşturmak için Visual Studio 2017 veya 2019 kullanın.</span><span class="sxs-lookup"><span data-stu-id="6672b-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="6672b-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6672b-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="6672b-108">Proje yapısı ve soyutlama kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6672b-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="6672b-109">Platforma özgü kodunuzu yazma</span><span class="sxs-lookup"><span data-stu-id="6672b-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="6672b-110">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="6672b-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="6672b-111">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="6672b-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="6672b-112">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="6672b-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="6672b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6672b-113">Prerequisites</span></span>

1. <span data-ttu-id="6672b-114">Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2017 veya 2019.</span><span class="sxs-lookup"><span data-stu-id="6672b-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="6672b-115">Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6672b-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="6672b-116">UWP ve Xamarin araçlarını dahil etmek için özel bir yüklemeyi seçin ve uygun seçenekleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="6672b-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="6672b-117">NuGet CLı.</span><span class="sxs-lookup"><span data-stu-id="6672b-117">NuGet CLI.</span></span> <span data-ttu-id="6672b-118">NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6672b-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="6672b-119">Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6672b-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="6672b-120">NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6672b-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="6672b-121">Proje yapısı ve soyutlama kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6672b-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="6672b-122">Visual Studio için [platformlar arası .NET Standard eklentisi şablonları uzantısını](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirip çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6672b-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="6672b-123">Bu şablonlar, Bu izlenecek yol için gerekli proje yapısını oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="6672b-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="6672b-124">Visual Studio 2017 ' de, **dosya > yeni > projesi**`Plugin`' ne tıklayın, **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin, adı logginglibrary olarak değiştirin ve Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![VS 2017 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="6672b-126">Visual Studio 2019 ' de **> dosya yeni > projesi**`Plugin`arayın, **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin ve ileri ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="6672b-128">Adı LoggingLibrary olarak değiştirip oluştur ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) yapılandırması](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="6672b-130">Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki paylaşılan proje içerir:</span><span class="sxs-lookup"><span data-stu-id="6672b-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="6672b-131">`ILoggingLibrary.shared.cs` dosyasında bulunan `ILoggingLibrary` projesi, bileşenin genel arabirimini (API yüzey alanı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6672b-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="6672b-132">Bu, kitaplığınızın arabirimini tanımladığınız yerdir.</span><span class="sxs-lookup"><span data-stu-id="6672b-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="6672b-133">Diğer paylaşılan proje, çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulacak `CrossLoggingLibrary.shared.cs` kod içerir.</span><span class="sxs-lookup"><span data-stu-id="6672b-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="6672b-134">Genellikle bu dosyayı değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6672b-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="6672b-135">`LoggingLibrary.android.cs`gibi platforma özgü projeler, kendi ilgili `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyalarındaki arabirimin yerel bir uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="6672b-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="6672b-136">Bu, kitaplığınızın kodunu oluşturduğunuz yerdir.</span><span class="sxs-lookup"><span data-stu-id="6672b-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="6672b-137">Varsayılan olarak, `ILoggingLibrary` projesinin ILoggingLibrary.shared.cs dosyası bir arabirim tanımı içerir, ancak hiçbir yöntem yoktur.</span><span class="sxs-lookup"><span data-stu-id="6672b-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="6672b-138">Bu izlenecek yolun amaçları doğrultusunda, aşağıdaki gibi bir `Log` yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6672b-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="6672b-139">Platforma özgü kodunuzu yazma</span><span class="sxs-lookup"><span data-stu-id="6672b-139">Write your platform-specific code</span></span>

<span data-ttu-id="6672b-140">`ILoggingLibrary` arabiriminin ve yöntemlerinin platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="6672b-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="6672b-141">Her platform projesinin `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyasını açın ve gerekli kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6672b-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="6672b-142">Örneğin (`Android` platform projesini kullanarak):</span><span class="sxs-lookup"><span data-stu-id="6672b-142">For example (using the `Android` platform project):</span></span>

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

1. <span data-ttu-id="6672b-143">Desteklemek istediğiniz her platform için bu uygulamayı projelerde tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="6672b-144">Çözüme sağ tıklayın ve işinizi denetlemek ve daha sonra paketettiğiniz yapıtları oluşturmak için **çözüm oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="6672b-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="6672b-145">Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **NuGet paketlerini geri yükle** ' yi seçin ve yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="6672b-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="6672b-146">Visual Studio 2019 kullanıyorsanız, **NuGet paketlerini geri yükle** ' yi seçmeden ve yeniden oluşturmaya çalışmadan önce, `MSBuild.Sdk.Extras` sürümünü `LoggingLibrary.csproj``2.0.54` olarak değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6672b-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="6672b-147">Bu dosyaya yalnızca önce projeye sağ tıklayıp (çözümün altında) ve `Unload Project`' yi seçerek erişilebilir projeye sağ tıklayıp `Edit LoggingLibrary.csproj`' i seçmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="6672b-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="6672b-148">İOS için derlemek için, Visual Studio için [Xamarin. iOS 'A giriş bölümünde](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi, Visual Studio 'ya bağlı ağa bağlı bir Mac gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6672b-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="6672b-149">Kullanılabilir bir Mac yoksa, Configuration Manager 'daki iOS projesi seçimini kaldırın (yukarıdaki 3. adım).</span><span class="sxs-lookup"><span data-stu-id="6672b-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="6672b-150">. Nuspec dosyasını oluşturun ve güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="6672b-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="6672b-151">Bir komut istemi açın, `.sln` dosyasının altında bir düzey `LoggingLibrary` klasöre gidin ve ilk `Package.nuspec` dosyasını oluşturmak için NuGet `spec` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6672b-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="6672b-152">Bu dosyayı `LoggingLibrary.nuspec` olarak yeniden adlandırın ve bir düzenleyicide açın.</span><span class="sxs-lookup"><span data-stu-id="6672b-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="6672b-153">YOUR_NAME, uygun bir değerle değiştirerek, aşağıdaki dosyayla eşleşecek şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6672b-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="6672b-154">`<id>` değeri özellikle, nuget.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın).</span><span class="sxs-lookup"><span data-stu-id="6672b-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="6672b-155">Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="6672b-156">Paketi yayın öncesi sürümler hakkında daha fazla bilgi için, paket sürümünüzü `-alpha`, `-beta` veya `-rc` ön sürüm olarak işaretlemek üzere ön sürüm [sürümlerini](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6672b-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="6672b-157">Başvuru derlemeleri Ekle</span><span class="sxs-lookup"><span data-stu-id="6672b-157">Add reference assemblies</span></span>

<span data-ttu-id="6672b-158">Platforma özgü başvuru derlemelerini dahil etmek için, aşağıdaki `LoggingLibrary.nuspec` `<files>` öğesine desteklenen platformlarınız için uygun şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6672b-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="6672b-159">DLL ve XML dosyalarının adlarını kısaltmak için, belirli bir projeye sağ tıklayın, **kitaplık** sekmesini seçin ve derleme adlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6672b-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="6672b-160">Bağımlılık Ekle</span><span class="sxs-lookup"><span data-stu-id="6672b-160">Add dependencies</span></span>

<span data-ttu-id="6672b-161">Yerel uygulamalar için belirli bağımlılıklarınız varsa, bunları belirtmek için `<group>` öğeleriyle `<dependencies>` öğesini kullanın, örneğin:</span><span class="sxs-lookup"><span data-stu-id="6672b-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="6672b-162">Örneğin, aşağıdaki, IAP hedefi için bir bağımlılık olarak ıtextsharp olarak ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="6672b-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="6672b-163">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="6672b-163">Final .nuspec</span></span>

<span data-ttu-id="6672b-164">Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada tekrar YOUR_NAME uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="6672b-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="6672b-165">Bileşeni paketleme</span><span class="sxs-lookup"><span data-stu-id="6672b-165">Package the component</span></span>

<span data-ttu-id="6672b-166">Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlanmış `.nuspec` ile `pack` komutunu çalıştırmaya hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="6672b-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="6672b-167">Bu işlem `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6672b-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="6672b-168">Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="6672b-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![LoggingLibrary paketini gösteren NuGet Paket Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="6672b-170">`.nupkg` dosyası, farklı uzantılı yalnızca bir ZIP dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6672b-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="6672b-171">Ayrıca, paket içeriğini inceleyebilir, sonra `.nupkg` `.zip`olarak değiştirebilir, ancak paketi nuget.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6672b-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="6672b-172">Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="6672b-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="6672b-173">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="6672b-173">Related topics</span></span>

- [<span data-ttu-id="6672b-174">Nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="6672b-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="6672b-175">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="6672b-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="6672b-176">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="6672b-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="6672b-177">Çoklu .NET Framework sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="6672b-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6672b-178">Bir pakete MSBuild props ve hedefleri dahil etme</span><span class="sxs-lookup"><span data-stu-id="6672b-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="6672b-179">Yerelleştirilmiş Paketler Oluşturma</span><span class="sxs-lookup"><span data-stu-id="6672b-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)