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
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Visual Studio 2015 ile Xamarin’e yönelik paketler oluşturma

Xamarin için bir paket, çalışma zamanı işletim sistemine bağlı olarak iOS, Android ve Windows 'da yerel API 'Ler kullanan kod içerir. Bu, basit olsa da, geliştiricilerin ortak bir API yüzey alanı aracılığıyla bir PCL veya .NET Standard kitaplıklarından paketi kullanmasına izin vermek tercih edilir.

Bu kılavuzda, Visual Studio 2015 ' u kullanarak iOS, Android ve Windows 'da mobil projelerde kullanılabilecek bir platformlar arası NuGet paketi oluşturun.

1. [Önkoşullar](#prerequisites)
1. [Proje yapısı ve soyutlama kodu oluşturma](#create-the-project-structure-and-abstraction-code)
1. [Platforma özgü kodunuzu yazma](#write-your-platform-specific-code)
1. [. Nuspec dosyasını oluşturun ve güncelleştirin](#create-and-update-the-nuspec-file)
1. [Bileşeni paketleme](#package-the-component)
1. [İlgili konular](#related-topics)

## <a name="prerequisites"></a>Önkoşullar

1. Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015. Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz. UWP ve Xamarin araçlarını dahil etmek için özel bir yüklemeyi seçin ve uygun seçenekleri kontrol edin.
1. NuGet CLı. NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin. Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

> [!Note]
> NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısı ve soyutlama kodu oluşturma

1. Visual Studio için [Xamarin şablonları uzantısı eklentisini](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) indirip çalıştırın. Bu şablonlar, Bu izlenecek yol için gerekli proje yapısını oluşturmayı kolaylaştırır.
1. Visual Studio 'da **Dosya > Yeni > proje**, arama `Plugin`, **Xamarin şablonu için eklentiyi** seçme, adı logginglibrary olarak değiştirme ve Tamam ' ı tıklatın.

    ![Visual Studio 'da yeni boş uygulama (Xamarin. Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

Elde edilen çözüm, platforma özgü çeşitli projelerle birlikte iki adet PCL projesi içerir:

- PCL adlı `Plugin.LoggingLibrary.Abstractions (Portable)`, bileşenin genel arabirimini (API yüzey alanı) tanımlar, bu `ILoggingLibrary` durumda arabirim ILoggingLibrary.cs dosyasında yer alır. Bu, kitaplığınızın arabirimini tanımladığınız yerdir.
- Diğer PCL `Plugin.LoggingLibrary (Portable)`, çalışma zamanında soyut arabirimin platforma özgü bir uygulamasını bulacak CrossLoggingLibrary.cs içinde kod içerir. Genellikle bu dosyayı değiştirmeniz gerekmez.
- Her biri gibi platforma özgü projeler `Plugin.LoggingLibrary.Android`, ilgili LoggingLibraryImplementation.cs dosyalarında arabirimin yerel bir uygulamasını içerir. Bu, kitaplığınızın kodunu oluşturduğunuz yerdir.

Varsayılan olarak, soyut olanaklar projesinin ILoggingLibrary.cs dosyası bir arabirim tanımı içerir, ancak hiçbir yöntem yoktur. Bu izlenecek yolun amaçları doğrultusunda, aşağıdaki gibi bir `Log` yöntem ekleyin:

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

## <a name="write-your-platform-specific-code"></a>Platforma özgü kodunuzu yazma

`ILoggingLibrary` Arabirimin ve yöntemlerinin platforma özgü bir uygulamasını uygulamak için aşağıdakileri yapın:

1. Her platform projesinin dosyasını açın ve gerekli kodu ekleyin. `LoggingLibraryImplementation.cs` Örneğin ( `Plugin.LoggingLibrary.Android` projeyi kullanarak):

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

1. Desteklemek istediğiniz her platform için bu uygulamayı projelerde tekrarlayın.
1. İOS projesine sağ tıklayın, **Özellikler**' i seçin, **derleme** sekmesine tıklayın ve "\Iphone" öğesini **çıkış yolundan** ve **XML belge dosyası** ayarlarından kaldırın. Bu, bu kılavuzda daha sonra kolaylık sağlaması için yeterlidir. Bitince dosyayı kaydedin.
1. Çözüme sağ tıklayın, **Configuration Manager...** öğesini seçin ve ardından, destekettiğiniz her platform için **Yapı** kutularını işaretleyin.
1. Çözüme sağ tıklayın ve işinizi denetlemek ve daha sonra paketettiğiniz yapıtları oluşturmak için **çözüm oluştur** ' u seçin. Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, bağımlılıkları yüklemek için **NuGet paketlerini geri yükle** ' yi seçin ve yeniden derleyin.

> [!Note]
> İOS için derlemek için, Visual Studio için [Xamarin. iOS 'A giriş bölümünde](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)açıklandığı gibi, Visual Studio 'ya bağlı ağa bağlı bir Mac gereklidir. Kullanılabilir bir Mac yoksa, Configuration Manager 'daki iOS projesi seçimini kaldırın (yukarıdaki 3. adım).

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

1. Bir `LoggingLibrary` komut istemi açın, `.sln` dosyanın altında bir düzey olan klasöre gidin ve ilk `Package.nuspec` dosyayı oluşturmak için NuGet `spec` komutunu çalıştırın:

    ```cli
    nuget spec
    ```

1. Bu dosyayı olarak `LoggingLibrary.nuspec` yeniden adlandırın ve bir düzenleyicide açın.
1. Dosyayı aşağıdaki ile eşleşecek şekilde güncelleştirin, YOUR_NAME değiştirerek uygun bir değerle değiştirin. Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). `<id>` Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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
> Paket `-alpha`sürümünüzü ile `-beta` sonekine veya `-rc` paketinizi ön sürüm olarak işaretlemek için yayın öncesi sürümler hakkında daha fazla bilgi için [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) kontrol edebilirsiniz.

### <a name="add-reference-assemblies"></a>Başvuru derlemeleri Ekle

Platforma özgü başvuru derlemelerini dahil etmek için, aşağıdaki `<files>` öğesine desteklenen platformlarınız için uygun olan `LoggingLibrary.nuspec` öğesine ekleyin:

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

Yerel uygulamalar için belirli bağımlılıklarınız varsa, bu `<dependencies>` öğeyi belirtmek için öğeleri ile `<group>` kullanın, örneğin:

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

## <a name="package-the-component"></a>Bileşeni paketleme

Pakete dahil etmeniz `.nuspec` gereken tüm dosyalara başvuran tamamlandığında, `pack` komutunu çalıştırmaya hazırsınız demektir:

```cli
nuget pack LoggingLibrary.nuspec
```

Bu işlem `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`oluşturacaktır. Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![LoggingLibrary paketini gösteren NuGet Paket Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` Dosya, yalnızca farklı bir uzantıya sahip bir ZIP dosyasıdır. Paket içeriğini `.nupkg` de inceleyebilir, ancak öğesini olarak `.zip`değiştirebilir, ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)