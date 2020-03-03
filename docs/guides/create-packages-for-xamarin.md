---
title: Visual Studio 2017 veya 2019 ile Xamarin (iOS, Android ve Windows için) için NuGet paketleri oluşturma
description: İOS, Android ve Windows 'da yerel API 'Ler kullanan Xamarin için NuGet paketleri oluşturmaya yönelik uçtan uca bir anlatım.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230908"
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

## <a name="prerequisites"></a>Önkoşullar

1. Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2017 veya 2019. Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz. UWP ve Xamarin araçlarını dahil etmek için özel bir yüklemeyi seçin ve uygun seçenekleri kontrol edin.
1. NuGet CLı. NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin. Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

> [!Note]
> NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısı ve soyutlama kodu oluşturma

1. Visual Studio için [platformlar arası .NET Standard eklentisi şablonları uzantısını](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirip çalıştırın. Bu şablonlar, Bu izlenecek yol için gerekli proje yapısını oluşturmayı kolaylaştırır.
1. Visual Studio 2017 ' de, **dosya > yeni > projesi**`Plugin`' ne tıklayın, **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin, adı logginglibrary olarak değiştirin ve Tamam ' a tıklayın.

    ![VS 2017 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

    Visual Studio 2019 ' de **> dosya yeni > projesi**`Plugin`arayın, **platformlar arası .NET Standard kitaplığı eklentisi** şablonunu seçin ve ileri ' ye tıklayın.

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject19-Part1.png)

    Adı LoggingLibrary olarak değiştirip oluştur ' a tıklayın.

    ![VS 2019 ' de yeni boş uygulama (Xamarin. Forms taşınabilir) yapılandırması](media/CrossPlatform-NewProject19-Part2.png)

Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki paylaşılan proje içerir:

- `ILoggingLibrary.shared.cs` dosyasında bulunan `ILoggingLibrary` projesi, bileşenin genel arabirimini (API yüzey alanı) tanımlar. Bu, kitaplığınızın arabirimini tanımladığınız yerdir.
- Diğer paylaşılan proje, çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulacak `CrossLoggingLibrary.shared.cs` kod içerir. Genellikle bu dosyayı değiştirmeniz gerekmez.
- `LoggingLibrary.android.cs`gibi platforma özgü projeler, her biri arabirimin ilgili `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyalarında yerel bir uygulamasını içerir. Bu, kitaplığınızın kodunu oluşturduğunuz yerdir.

Varsayılan olarak, `ILoggingLibrary` projesinin ILoggingLibrary.shared.cs dosyası bir arabirim tanımı içerir, ancak hiçbir yöntem yoktur. Bu izlenecek yolun amaçları doğrultusunda, aşağıdaki gibi bir `Log` yöntemi ekleyin:

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

`ILoggingLibrary` arabiriminin ve yöntemlerinin platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:

1. Her platform projesinin `LoggingLibraryImplementation.cs` (VS 2017) veya `LoggingLibrary.<PLATFORM>.cs` (VS 2019) dosyasını açın ve gerekli kodu ekleyin. Örneğin (`Android` platform projesini kullanarak):

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
> Visual Studio 2019 kullanıyorsanız, **NuGet paketlerini geri yükle** ' yi seçmeden ve yeniden oluşturmaya çalışmadan önce, `MSBuild.Sdk.Extras` sürümünü `LoggingLibrary.csproj``2.0.54` olarak değiştirmeniz gerekir. Bu dosyaya yalnızca önce projeye sağ tıklayıp (çözümün altında) ve `Unload Project`' yi seçerek erişilebilir projeye sağ tıklayıp `Edit LoggingLibrary.csproj`' i seçmeniz yeterlidir.

> [!Note]
> İOS için derlemek için, Visual Studio için [Xamarin. iOS 'A giriş bölümünde](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi, Visual Studio 'ya bağlı ağa bağlı bir Mac gereklidir. Kullanılabilir bir Mac yoksa, Configuration Manager 'daki iOS projesi seçimini kaldırın (yukarıdaki 3. adım).

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

1. Bir komut istemi açın, `.sln` dosyasının altında bir düzey `LoggingLibrary` klasöre gidin ve ilk `Package.nuspec` dosyasını oluşturmak için NuGet `spec` komutunu çalıştırın:

    ```cli
    nuget spec
    ```

1. Bu dosyayı `LoggingLibrary.nuspec` olarak yeniden adlandırın ve bir düzenleyicide açın.
1. YOUR_NAME, uygun bir değerle değiştirerek, aşağıdaki dosyayla eşleşecek şekilde güncelleştirin. `<id>` değeri özellikle, nuget.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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
> Paketi yayın öncesi sürümler hakkında daha fazla bilgi için, paket sürümünüzü `-alpha`, `-beta` veya `-rc` ön sürüm olarak işaretlemek üzere ön sürüm [sürümlerini](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.

### <a name="add-reference-assemblies"></a>Başvuru derlemeleri Ekle

Platforma özgü başvuru derlemelerini dahil etmek için, aşağıdaki `LoggingLibrary.nuspec` `<files>` öğesine desteklenen platformlarınız için uygun şekilde ekleyin:

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

Yerel uygulamalar için belirli bağımlılıklarınız varsa, bunları belirtmek için `<group>` öğeleriyle `<dependencies>` öğesini kullanın, örneğin:

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

Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada tekrar YOUR_NAME uygun bir değerle değiştirilmelidir:

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

Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlanmış `.nuspec` ile `pack` komutunu çalıştırmaya hazırsınız:

```cli
nuget pack LoggingLibrary.nuspec
```

Bu işlem `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`oluşturur. Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![LoggingLibrary paketini gösteren NuGet Paket Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` dosyası, farklı uzantılı yalnızca bir ZIP dosyasıdır. Ayrıca, paket içeriğini inceleyebilir, sonra `.nupkg` `.zip`olarak değiştirebilir, ancak paketi nuget.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
