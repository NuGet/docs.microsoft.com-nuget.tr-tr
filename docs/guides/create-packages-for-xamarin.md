---
title: Visual Studio 2017 veya 2019 ile Xamarin (iOS, Android ve Windows için) için NuGet paketleri oluşturma
description: İOS, Android ve Windows 'da yerel API 'Ler kullanan Xamarin için NuGet paketleri oluşturmaya yönelik uçtan uca bir anlatım.
author: JonDouglas
ms.author: jodou
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fdabeeac57ca12716f6ed2614d036f1623407b20
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774220"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Visual Studio 2017 veya 2019 ile Xamarin için paketler oluşturma

Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows 'da yerel API 'Ler kullanan kod içerir. Bu, basit olsa da, geliştiricilerin ortak bir API yüzey alanı aracılığıyla bir PCL veya .NET Standard kitaplıklarından paketi kullanmasına izin vermek tercih edilir.

Bu kılavuzda, iOS, Android ve Windows 'da mobil projelerde kullanılabilecek platformlar arası bir NuGet paketi oluşturmak için Visual Studio 2017 veya 2019 kullanın.

1. [Önkoşullar](#prerequisites)
1. [Proje yapısı ve soyutlama kodu oluşturma](#create-the-project-structure-and-abstraction-code)
1. [Platforma özgü kodunuzu yazma](#write-your-platform-specific-code)
1. [. Nuspec dosyasını oluşturun ve güncelleştirin](#create-and-update-the-nuspec-file)
1. [Bileşeni paketleme](#package-the-component)
1. [İlgili konular](#related-topics)

## <a name="prerequisites"></a>Ön koşullar

1. Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2017 veya 2019. Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz. UWP ve Xamarin araçlarını dahil etmek için özel bir yüklemeyi seçin ve uygun seçenekleri kontrol edin.
1. NuGet CLı. En son nuget.exe sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin, bunu istediğiniz bir konuma kaydederek yükleyin. Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

> [!Note]
> nuget.exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısı ve soyutlama kodu oluşturma

1. Visual Studio için [platformlar arası .NET Standard eklentisi şablonları uzantısını](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirip çalıştırın. Bu şablonlar, Bu izlenecek yol için gerekli proje yapısını oluşturmayı kolaylaştırır.
1. Visual Studio 2017 ' de, **dosya > yeni > proje**' yi arayın, `Plugin` **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin, adı logginglibrary olarak değiştirin ve Tamam ' a tıklayın.

    ![VS 2017 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

    Visual Studio 2019 ' de, **dosya > yeni > proje**' yi arayın, `Plugin` **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin ve ileri ' ye tıklayın.

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject19-Part1.png)

    Adı LoggingLibrary olarak değiştirip oluştur ' a tıklayın.

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) yapılandırması](media/CrossPlatform-NewProject19-Part2.png)

Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki paylaşılan proje içerir:

- `ILoggingLibrary`Dosyasında yer alan proje, `ILoggingLibrary.shared.cs` bileşenin genel ARABIRIMINI (API yüzey alanı) tanımlar. Bu, kitaplığınızın arabirimini tanımladığınız yerdir.
- Diğer paylaşılan proje, `CrossLoggingLibrary.shared.cs` çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulacak içindeki kodu içerir. Genellikle bu dosyayı değiştirmeniz gerekmez.
- Her biri gibi platforma özgü projeler, `LoggingLibrary.android.cs` arabirimin ilgili `LoggingLibraryImplementation.cs` (vs 2017) veya `LoggingLibrary.<PLATFORM>.cs` (vs 2019) dosyalarında yerel bir uygulamasını içerir. Bu, kitaplığınızın kodunu oluşturduğunuz yerdir.

Varsayılan olarak, projenin ILoggingLibrary.shared.cs dosyası `ILoggingLibrary` bir arabirim tanımı içerir, ancak hiçbir yöntem yoktur. Bu izlenecek yolun amaçları doğrultusunda, `Log` aşağıdaki gibi bir yöntem ekleyin:

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

## <a name="write-your-platform-specific-code"></a>Platforma özgü kodunuzu yazma

Arabirimin ve yöntemlerinin platforma özgü bir uygulamasını uygulamak için `ILoggingLibrary` aşağıdakileri yapın:

1. `LoggingLibraryImplementation.cs`Her platform projesinin (vs 2017) veya `LoggingLibrary.<PLATFORM>.cs` (vs 2019) dosyasını açın ve gerekli kodu ekleyin. Örneğin ( `Android` Platform projesini kullanarak):

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

1. Desteklemek istediğiniz her platform için bu uygulamayı projelerde tekrarlayın.
1. Çözüme sağ tıklayın ve işinizi denetlemek ve daha sonra paketettiğiniz yapıtları oluşturmak için **çözüm oluştur** ' u seçin. Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **NuGet paketlerini geri yükle** ' yi seçin ve yeniden derleyin.

> [!Note]
> Visual Studio 2019 kullanıyorsanız, **NuGet paketlerini geri yükle** ' yi seçmeden ve yeniden oluşturmaya çalışmadan önce, sürümünü `MSBuild.Sdk.Extras` ' de olarak değiştirmeniz gerekir `2.0.54` `LoggingLibrary.csproj` . Bu dosyaya yalnızca önce projeye sağ tıklayıp (çözümün altında) ve `Unload Project` sonra, kaldırılan projeye sağ tıklayıp ' ı seçerek erişebilirsiniz `Edit LoggingLibrary.csproj` .

> [!Note]
> İOS için derlemek için, Visual Studio için [Xamarin. iOS 'A giriş bölümünde](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi, Visual Studio 'ya bağlı ağa bağlı bir Mac gereklidir. Kullanılabilir bir Mac yoksa, Configuration Manager 'daki iOS projesi seçimini kaldırın (yukarıdaki 3. adım).

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

1. Bir komut istemi açın, `LoggingLibrary` dosyanın altında bir düzey olan klasöre gidin `.sln` ve `spec` ilk dosyayı oluşturmak için NuGet komutunu çalıştırın `Package.nuspec` :

    ```cli
    nuget spec
    ```

1. Bu dosyayı olarak yeniden adlandırın `LoggingLibrary.nuspec` ve bir düzenleyicide açın.
1. YOUR_NAME, uygun bir değerle değiştirerek, aşağıdaki dosyayla eşleşecek şekilde güncelleştirin. `<id>`Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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
> Paket sürümünüzü ile sonekine `-alpha` `-beta` veya `-rc` paketinizi ön sürüm olarak işaretlemek için yayın öncesi sürümler hakkında daha fazla bilgi için [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.

### <a name="add-reference-assemblies"></a>Başvuru derlemeleri Ekle

Platforma özgü başvuru derlemelerini dahil etmek için, aşağıdaki `<files>` öğesine `LoggingLibrary.nuspec` desteklenen platformlarınız için uygun olan öğesine ekleyin:

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
> DLL ve XML dosyalarının adlarını kısaltmak için, belirli bir projeye sağ tıklayın, **kitaplık** sekmesini seçin ve derleme adlarını değiştirin.

### <a name="add-dependencies"></a>Bağımlılık Ekle

Yerel uygulamalar için belirli bağımlılıklarınız varsa, bu `<dependencies>` öğeyi `<group>` belirtmek için öğeleri ile kullanın, örneğin:

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

Örneğin, aşağıdaki, IAP hedefi için bir bağımlılık olarak ıtextsharp olarak ayarlanır:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Final. nuspec

Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada yeniden YOUR_NAME uygun bir değerle değiştirilmelidir:

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

## <a name="package-the-component"></a>Bileşeni paketleme

`.nuspec`Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlandığında, komutunu çalıştırmaya hazırsınız demektir `pack` :

```cli
nuget pack LoggingLibrary.nuspec
```

Bu işlem oluşturacaktır `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` . Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![LoggingLibrary paketini gösteren NuGet Paket Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg`Dosya, yalnızca farklı bir uzantıya sahip BIR ZIP dosyasıdır. Paket içeriğini de inceleyebilir, ancak öğesini olarak değiştirebilir, `.nupkg` `.zip` ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
