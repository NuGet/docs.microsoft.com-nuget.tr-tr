---
title: "Platformlar arası NuGet paketlerini (için iOS, Android ve Windows) oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "NuGet paketleri için Xamarin oluşturduğunuz bir uçtan uca kılavuz, iOS, Android ve Windows yerel API'leri kullanın."
keywords: "paketler Xamarin, platformlar arası paketleri için bir paket oluşturun"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8ee825a6299d7de375fd2f242cf456da13b777d9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="93b35-104">Platformlar arası paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="93b35-104">Create cross-platform packages</span></span>

<span data-ttu-id="93b35-105">Platformlar arası paket çalışma zamanı işletim sistemine bağlı iOS, Android ve Windows, yerel API'lerini kullanan kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="93b35-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="93b35-106">Bunu yapmak basit olmasına karşın, geliştiricilerin bir PCL paketinden kullanmasına izin vermek için tercih edilir veya ortak bir API üzerinden .NET standart kitaplıkları yüzey alanı.</span><span class="sxs-lookup"><span data-stu-id="93b35-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="93b35-107">Bu kılavuzda iOS, Android ve Windows mobil projelerinde kullanılan bir platformlar arası NuGet paketi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="93b35-107">In this walkthrough you'll create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="93b35-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="93b35-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="93b35-109">Proje yapısı ve Özet kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="93b35-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="93b35-110">Platforma özgü kod yazma</span><span class="sxs-lookup"><span data-stu-id="93b35-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="93b35-111">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="93b35-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="93b35-112">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="93b35-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="93b35-113">İlgili Konular</span><span class="sxs-lookup"><span data-stu-id="93b35-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="93b35-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="93b35-114">Pre-requisites</span></span>

1. <span data-ttu-id="93b35-115">Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="93b35-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="93b35-116">Community edition ücretsiz yükleyin [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93b35-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="93b35-117">UWP ve Xamarin Araçları eklemek için bir özel yükleme seçeneğini belirleyin ve uygun seçenekleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="93b35-118">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="93b35-118">NuGet CLI.</span></span> <span data-ttu-id="93b35-119">Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme.</span><span class="sxs-lookup"><span data-stu-id="93b35-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="93b35-120">Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="93b35-121">nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.</span><span class="sxs-lookup"><span data-stu-id="93b35-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="93b35-122">Proje yapısı ve Özet kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="93b35-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="93b35-123">İndirme ve çalıştırma [Xamarin Şablonları uzantısı eklentisi](https://visualstudiogallery.msdn.microsoft.com/afead421-3fbf-489a-a4e8-4a244ecdbb1e) Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="93b35-123">Download and run the [Plugin for Xamarin Templates extension](https://visualstudiogallery.msdn.microsoft.com/afead421-3fbf-489a-a4e8-4a244ecdbb1e) for Visual Studio.</span></span> <span data-ttu-id="93b35-124">Bu şablonlar bu kılavuz için gerekli Proje yapısı oluşturmak kolaylaştıracak.</span><span class="sxs-lookup"><span data-stu-id="93b35-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="93b35-125">Visual Studio'da **Dosya > Yeni > Proje**, arama `Plugin`seçin **xamarin eklentisi** şablonu adı için LoggingLibrary değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="93b35-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio'da yeni boş uygulama (Xamarin.Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

<span data-ttu-id="93b35-127">Sonuçta elde edilen çözüm çeşitli platforma özgü projeleri birlikte iki PCL projeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="93b35-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="93b35-128">Adlı PCL `Plugin.LoggingLibrary.Abstractions (Portable)`, bu durumda bileşenin ortak arabirimi (API yüzey alanını) tanımlar `ILoggingLibrary` ILoggingLibrary.cs dosyasında yer alan arabirimi.</span><span class="sxs-lookup"><span data-stu-id="93b35-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="93b35-129">Arabirim kitaplığınıza tanımladığınız budur.</span><span class="sxs-lookup"><span data-stu-id="93b35-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="93b35-130">Diğer PCL `Plugin.LoggingLibrary (Portable)`, çalışma zamanında soyut arabiriminin bir platforma özgü uygulamasını bulun CrossLoggingLibrary.cs kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="93b35-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="93b35-131">Genellikle, bu dosyayı değiştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="93b35-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="93b35-132">Platforma özgü projeleri, gibi `Plugin.LoggingLibrary.Android`, her içeren ilgili LoggingLibraryImplementation.cs dosyalarına arabiriminde yerel bir uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="93b35-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="93b35-133">Kitaplığınızın kodu nereye oluşturacağınız budur.</span><span class="sxs-lookup"><span data-stu-id="93b35-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="93b35-134">Varsayılan olarak, arabirim tanımı, ancak hiçbir yöntemi soyutlamalar projesinin ILoggingLibrary.cs dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="93b35-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="93b35-135">Bu kılavuzda amaçları doğrultusunda eklemek bir `Log` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="93b35-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="93b35-136">Platforma özgü kod yazma</span><span class="sxs-lookup"><span data-stu-id="93b35-136">Write your platform-specific code</span></span>

<span data-ttu-id="93b35-137">Platforma özgü uyarlamasını uygulamak için `ILoggingLibrary` arabirimi ve yöntemlerinden, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="93b35-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="93b35-138">Açık `LoggingLibraryImplementation.cs` dosya her platform için proje ve gerekli kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="93b35-139">Örneğin (kullanarak `Plugin.LoggingLibrary.Android` Proje):</span><span class="sxs-lookup"><span data-stu-id="93b35-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

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

1. <span data-ttu-id="93b35-140">Bu uygulama projelerinde desteklemek istediğiniz her platform için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="93b35-141">İOS projesine sağ tıklayın, **özellikleri**, tıklatın **yapı** sekmesini tıklatın ve "\iPhone" kaldırma **çıkış yolu** ve **XML belge dosyası**  ayarlar.</span><span class="sxs-lookup"><span data-stu-id="93b35-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="93b35-142">Bu kılavuzda daha sonra kolaylık sağlamak için yalnızca budur.</span><span class="sxs-lookup"><span data-stu-id="93b35-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="93b35-143">İşiniz bittiğinde dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="93b35-143">Save the file when done.</span></span>
1. <span data-ttu-id="93b35-144">Çözüme sağ tıklayın, seçin **Configuration Manager...** ve denetleme **yapı** PCLs ve destekleyen her platform için kutuları.</span><span class="sxs-lookup"><span data-stu-id="93b35-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="93b35-145">Çözüme sağ tıklayın ve seçin **yapı çözümü** çalışmanızı iade etme ve sonraki paketini yapıları üretmek için.</span><span class="sxs-lookup"><span data-stu-id="93b35-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="93b35-146">Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, seçin **NuGet paketleri geri** bağımlılıkları yükler ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93b35-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="93b35-147">İOS için oluşturmak için Visual Studio için açıklandığı gibi bağlı ağa bağlı bir Mac gereksinim [Visual Studio Xamarin.iOS için giriş](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="93b35-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="93b35-148">Kullanılabilir bir Mac yoksa, Yapılandırma Yöneticisi'ni (yukarıdaki adım 3) IOS projede temizleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="93b35-149">Oluşturun ve .nuspec dosyası güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="93b35-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="93b35-150">Bir komut istemi açıp `LoggingLibrary` where bir düzeyin klasörü `.sln` dosyası olduğunu ve NuGet çalıştırın `spec` ilk oluşturmak için komutu `Package.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="93b35-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="93b35-151">Bu dosyayı yeniden adlandırmak `LoggingLibrary.nuspec` ve bir düzenleyicide açın.</span><span class="sxs-lookup"><span data-stu-id="93b35-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="93b35-152">Aşağıdaki ile eşleşecek şekilde dosyasını güncelleştirme adiniz uygun bir değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="93b35-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="93b35-153">`<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="93b35-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="93b35-154">Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata iletisi alırsınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="93b35-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
> <span data-ttu-id="93b35-155">Paket sürümü ile soneki `-alpha`, `-beta` veya `-rc` paketinizi yayın öncesi olarak işaretlemek için kontrol [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) yayın öncesi sürümleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="93b35-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="93b35-156">Başvuru derlemeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="93b35-156">Add reference assemblies</span></span>

<span data-ttu-id="93b35-157">Platforma özgü başvuru derlemeleri eklemek için aşağıdakileri ekleyin `<files>` öğesinin `LoggingLibrary.nuspec` , desteklenen platformlar için uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="93b35-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="93b35-158">DLL ve XML dosyalarının adlarını kısaltmak için tüm verilen projeye, select sağ tıklayın **Kitaplığı** sekmesinde ve derleme adları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="93b35-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>


### <a name="add-dependencies"></a><span data-ttu-id="93b35-159">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="93b35-159">Add dependencies</span></span>

<span data-ttu-id="93b35-160">Yerel uygulamaları için belirli bağımlılıkları varsa, `<dependencies>` öğeyle `<group>` öğeleri, örneğin belirtin:</span><span class="sxs-lookup"><span data-stu-id="93b35-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="93b35-161">Örneğin, aşağıdaki iTextSharp UAP hedef için bağımlılık olarak ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="93b35-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="93b35-162">Son .nuspec</span><span class="sxs-lookup"><span data-stu-id="93b35-162">Final .nuspec</span></span>

<span data-ttu-id="93b35-163">Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden adiniz uygun bir değerle değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="93b35-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="93b35-164">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="93b35-164">Package the component</span></span>

<span data-ttu-id="93b35-165">Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="93b35-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="93b35-166">Bu oluşturur `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="93b35-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="93b35-167">Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="93b35-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet paket LoggingLibrary paket gösteren Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="93b35-169">A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="93b35-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="93b35-170">Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="93b35-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>


<span data-ttu-id="93b35-171">Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="93b35-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="93b35-172">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="93b35-172">Related topics</span></span>

- [<span data-ttu-id="93b35-173">Nuspec başvurusu</span><span class="sxs-lookup"><span data-stu-id="93b35-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="93b35-174">Simge paketleri</span><span class="sxs-lookup"><span data-stu-id="93b35-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="93b35-175">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="93b35-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="93b35-176">Birden çok .NET Framework sürümleri destekleme</span><span class="sxs-lookup"><span data-stu-id="93b35-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="93b35-177">MSBuild özellik ve hedefleri bir pakete dahil etme</span><span class="sxs-lookup"><span data-stu-id="93b35-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="93b35-178">Yerelleştirilmiş paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="93b35-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)