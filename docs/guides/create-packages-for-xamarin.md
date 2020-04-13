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
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Visual Studio 2017 veya 2019 ile Xamarin için paketler oluşturun

Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows'da yerel API'leri kullanan kod lar içerir. Bunu yapmak kolay olsa da, geliştiricilerin paketi bir PCL veya .NET Standart kitaplıklarından ortak bir API yüzey alanı üzerinden tüketmesine izin vermek tercih edilir.

Bu walkthrough'ta Visual Studio 2017 veya 2019'u kullanarak iOS, Android ve Windows'daki mobil projelerde kullanılabilecek bir çapraz platform NuGet paketi oluşturursunuz.

1. [Ön koşullar](#prerequisites)
1. [Proje yapısını ve soyutlama kodunu oluşturma](#create-the-project-structure-and-abstraction-code)
1. [Platforma özel kodunuzu yazın](#write-your-platform-specific-code)
1. [.nuspec dosyasını oluşturma ve güncelleştirme](#create-and-update-the-nuspec-file)
1. [Bileşeni paketle](#package-the-component)
1. [İlgili konular](#related-topics)

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017 veya 2019, Universal Windows Platform (UWP) ve Xamarin ile birlikte. Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/)ücretsiz olarak yükleyin; Profesyonel ve Kurumsal sürümleri de kullanabilirsiniz, tabii ki. UWP ve Xamarin araçlarını eklemek için Özel yükleme'yi seçin ve uygun seçenekleri denetleyin.
1. NuGet CLI. nuget.exe'nin en son sürümünü [nuget.org/downloads](https://nuget.org/downloads)indirin ve seçtiğiniz bir konuma kaydedin. Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.

> [!Note]
> nuget.exe cli aracı kendisi değil, bir yükleyici, bu yüzden yerine çalışan tarayıcınızdan indirilen dosyayı kaydetmek için emin olun.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısını ve soyutlama kodunu oluşturma

1. Visual Studio için [Çapraz Platform .NET Standart Eklenti Şablonları uzantısını](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirin ve çalıştırın. Bu şablonlar, bu gözden geçirme için gerekli proje yapısını oluşturmayı kolaylaştırır.
1. Visual Studio 2017'de, Dosya > `Plugin`New > **Projesi**, ara , Çapraz Platform **.NET Standart Kitaplık Eklentisi** şablonunu seçin, adınızı LoggingLibrary olarak değiştirin ve Tamam'ı tıklatın.

    ![VS 2017'de Yeni Boş Uygulama (Xamarin.Forms Portable) projesi](media/CrossPlatform-NewProject.png)

    Visual Studio 2019'da, Dosya > `Plugin`New > **Project**, ara , Çapraz Platform **.NET Standart Kitaplık Eklentisi** şablonunu seçin ve İleri'yi tıklatın.

    ![VS 2019'da Yeni Boş Uygulama (Xamarin.Forms Portable) projesi](media/CrossPlatform-NewProject19-Part1.png)

    Adı Günlük Kitaplığı olarak değiştirin ve Oluştur'u tıklatın.

    ![VS 2019'da Yeni Boş Uygulama (Xamarin.Forms Portable) yapılandırması](media/CrossPlatform-NewProject19-Part2.png)

Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki Paylaşılan proje içerir:

- `ILoggingLibrary.shared.cs` Dosyada bulunan `ILoggingLibrary` proje, bileşenin ortak arabirimini (API yüzey alanı) tanımlar. Burası kitaplığınız için arabirimi tanımladığınız yerdir.
- Diğer Paylaşılan proje, `CrossLoggingLibrary.shared.cs` çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulabilen kod içerir. Genellikle bu dosyayı değiştirmeniz gerekmez.
- Platforma özgü projeler, `LoggingLibrary.android.cs`her biri kendi `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyalarında arabirimin yerel bir uygulamasını içerir. Burası kitaplığınızın kodunu oluşturduğunuz yer.

Varsayılan olarak, `ILoggingLibrary` projenin ILoggingLibrary.shared.cs dosyası bir arabirim tanımı içerir, ancak yöntem içermez. Bu gözden geçirme nin amaçları `Log` için aşağıdaki gibi bir yöntem ekleyin:

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

## <a name="write-your-platform-specific-code"></a>Platforma özel kodunuzu yazın

Arabirimin ve yöntemlerinin `ILoggingLibrary` platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:

1. Her `LoggingLibraryImplementation.cs` platform projesinin (VS `LoggingLibrary.<PLATFORM>.cs` 2017) veya (VS 2019) dosyasını açın ve gerekli kodu ekleyin. Örneğin `Android` (platform projesini kullanarak):

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

1. Desteklemek istediğiniz her platform için projelerde bu uygulamayı yineleyin.
1. Çözüme sağ tıklayın ve çalışmanızı kontrol etmek ve bir sonraki paketlediğiniz yapıları üretmek için **Çözüm Oluştur'u** seçin. Eksik başvurular hakkında hatalar alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **Paketleri Geri Yükle'yi** seçin ve yeniden oluşturun.

> [!Note]
> Visual Studio 2019'u kullanıyorsanız, **NuGet Paketlerini Geri Yükle'yi** seçmeden `MSBuild.Sdk.Extras` ve `2.0.54` `LoggingLibrary.csproj`yeniden oluşturmaya çalışmadan önce, 'in sürümünü değiştirmeniz gerekir. Bu dosyaya yalnızca ilk sağ tıklayarak (çözümün altında) ve sonra `Unload Project`boşaltılan projeye sağ tıklayıp . `Edit LoggingLibrary.csproj`

> [!Note]
> iOS için oluşturmak için Visual [Studio için Xamarin.iOS'a Giriş'te](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi Visual Studio'ya bağlı ağ bağlantılı bir Mac'e ihtiyacınız var. Kullanılabilir bir Mac'inyoksa, iOS projesini yapılandırma yöneticisinden temizleyin (yukarıdaki adım 3).

## <a name="create-and-update-the-nuspec-file"></a>.nuspec dosyasını oluşturma ve güncelleştirme

1. Komut istemini açın, `LoggingLibrary` `.sln` dosyanın bulunduğu seviyenin altındaki klasöre gidin ve `spec` ilk `Package.nuspec` dosyayı oluşturmak için NuGet komutunu çalıştırın:

    ```cli
    nuget spec
    ```

1. Bu dosyayı `LoggingLibrary.nuspec` yeniden adlandırın ve bir editörde açın.
1. Dosyayı aşağıdakilerle eşleşecek şekilde güncelleştirin ve YOUR_NAME uygun bir değerle değiştirin. Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.

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
> Paket sürümünüzü `-alpha`ön sürüm olarak `-beta` `-rc` işaretleyebilir veya ön sürüm olarak işaretlemek için, ön sürüm sürümleri hakkında daha fazla bilgi için [ön sürüm sürümlerini](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.

### <a name="add-reference-assemblies"></a>Referans derlemeleri ekleme

Platforma özgü başvuru derlemelerini eklemek için, `<files>` desteklenen `LoggingLibrary.nuspec` platformlar için uygun olan öğesine aşağıdakileri ekleyin:

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
> DLL ve XML dosyalarının adlarını kısaltmak için, belirli bir projeye sağ tıklayın, **Kitaplık** sekmesini seçin ve derleme adlarını değiştirin.

### <a name="add-dependencies"></a>Bağımlılıkekleme

Yerel uygulamalar için belirli bağımlılıklarınız varsa, bunları belirtmek için `<dependencies>` öğeleri içeren `<group>` öğeyi kullanın, örneğin:

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

Örneğin, aşağıdaki uap hedefi için bir bağımlılık olarak iTextSharp ayarlar:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Son .nuspec

Son `.nuspec` dosyanız şimdi aşağıdaki gibi görünmelidir ve yine YOUR_NAME uygun bir değerle değiştirilmelidir:

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

## <a name="package-the-component"></a>Bileşeni paketle

Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:

```cli
nuget pack LoggingLibrary.nuspec
```

Bu oluşturur. `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletmek, aşağıdaki içeriği görürsünüz:

![NuGet Paket Gezgini LoggingLibrary paketini gösteriyor](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır. Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [Nuspec Referans](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Çoklu .NET Framework Sürümlerini Destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [MSBuild sahne ve hedeflerini bir pakete dahil et](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
