---
title: (İçin iOS, Android ve Windows) Xamarin ile Visual Studio 2015 için NuGet paketlerini oluşturma | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: NuGet paketleri için Xamarin oluşturduğunuz bir uçtan uca kılavuz, iOS, Android ve Windows yerel API'leri kullanın.
keywords: paketler Xamarin, platformlar arası paketleri için bir paket oluşturun
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e101ca2d124a19d2cf758776717b3680aa5bbdd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Xamarin ile Visual Studio 2015 için paketler oluşturma

Bir paket xamarin çalışma zamanı işletim sistemine bağlı iOS, Android ve Windows, yerel API'lerini kullanan kodu içerir. Bunu yapmak basit olmasına karşın, geliştiricilerin bir PCL paketinden kullanmasına izin vermek için tercih edilir veya ortak bir API üzerinden .NET standart kitaplıkları yüzey alanı.

Kullandığınız bu kılavuzda, Visual Studio 2015 iOS, Android ve Windows mobil projelerinde kullanılan bir platformlar arası NuGet paketi oluşturun.

1. [Önkoşulları](#prerequisites)
1. [Proje yapısı ve Özet kodu oluşturma](#create-the-project-structure-and-abstraction-code)
1. [Platforma özgü kod yazma](#write-your-platform-specific-code)
1. [Oluşturun ve .nuspec dosyası güncelleştirin](#create-and-update-the-nuspec-file)
1. [Paket bileşeni](#package-the-component)
1. [İlgili Konular](#related-topics)

## <a name="prerequisites"></a>Önkoşullar

1. Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015. Community edition ücretsiz yükleyin [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz. UWP ve Xamarin Araçları eklemek için bir özel yükleme seçeneğini belirleyin ve uygun seçenekleri denetleyin.
1. NuGet CLI. Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme. Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

> [!Note]
> nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısı ve Özet kodu oluşturma

1. İndirme ve çalıştırma [Xamarin Şablonları uzantısı eklentisi](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) Visual Studio için. Bu şablonlar bu kılavuz için gerekli Proje yapısı oluşturmak kolaylaştıracak.
1. Visual Studio'da **Dosya > Yeni > Proje**, arama `Plugin`seçin **xamarin eklentisi** şablonu adı için LoggingLibrary değiştirin ve Tamam'ı tıklatın.

    ![Visual Studio'da yeni boş uygulama (Xamarin.Forms taşınabilir) projesi](media/CrossPlatform-NewProject.png)

Sonuçta elde edilen çözüm çeşitli platforma özgü projeleri birlikte iki PCL projeleri içerir:

- Adlı PCL `Plugin.LoggingLibrary.Abstractions (Portable)`, bu durumda bileşenin ortak arabirimi (API yüzey alanını) tanımlar `ILoggingLibrary` ILoggingLibrary.cs dosyasında yer alan arabirimi. Arabirim kitaplığınıza tanımladığınız budur.
- Diğer PCL `Plugin.LoggingLibrary (Portable)`, çalışma zamanında soyut arabiriminin bir platforma özgü uygulamasını bulun CrossLoggingLibrary.cs kodunu içerir. Genellikle, bu dosyayı değiştirmek gerekmez.
- Platforma özgü projeleri, gibi `Plugin.LoggingLibrary.Android`, her içeren ilgili LoggingLibraryImplementation.cs dosyalarına arabiriminde yerel bir uygulama içerir. Burada kitaplığınızın kodu derleme budur.

Varsayılan olarak, arabirim tanımı, ancak hiçbir yöntemi soyutlamalar projesinin ILoggingLibrary.cs dosyası içerir. Bu kılavuzda amaçları doğrultusunda eklemek bir `Log` yöntemini aşağıdaki şekilde:

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

## <a name="write-your-platform-specific-code"></a>Platforma özgü kod yazma

Platforma özgü uyarlamasını uygulamak için `ILoggingLibrary` arabirimi ve yöntemlerinden, aşağıdakileri yapın:

1. Açık `LoggingLibraryImplementation.cs` dosya her platform için proje ve gerekli kodu ekleyin. Örneğin (kullanarak `Plugin.LoggingLibrary.Android` Proje):

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

1. Bu uygulama projelerinde desteklemek istediğiniz her platform için yineleyin.
1. İOS projesine sağ tıklayın, **özellikleri**, tıklatın **yapı** sekmesini tıklatın ve "\iPhone" kaldırma **çıkış yolu** ve **XML belge dosyası**  ayarlar. Bu kılavuzda daha sonra kolaylık sağlamak için yalnızca budur. İşiniz bittiğinde dosyayı kaydedin.
1. Çözüme sağ tıklayın, seçin **Configuration Manager...** ve denetleme **yapı** PCLs ve destekleyen her platform için kutuları.
1. Çözüme sağ tıklayın ve seçin **yapı çözümü** çalışmanızı iade etme ve sonraki paketini yapıları üretmek için. Eksik başvurular hakkında hata alırsanız, çözüme sağ tıklayın, seçin **NuGet paketleri geri** bağımlılıkları yükler ve yeniden oluşturun.

> [!Note]
> İOS için oluşturmak için Visual Studio için açıklandığı gibi bağlı ağa bağlı bir Mac gereksinim [Visual Studio Xamarin.iOS için giriş](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Kullanılabilir bir Mac yoksa, Yapılandırma Yöneticisi'ni (yukarıdaki adım 3) IOS projede temizleyin.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturun ve .nuspec dosyası güncelleştirin

1. Bir komut istemi açıp `LoggingLibrary` where bir düzeyin klasörü `.sln` dosyası olduğunu ve NuGet çalıştırın `spec` ilk oluşturmak için komutu `Package.nuspec` dosyası:

    ```cli
    nuget spec
    ```

1. Bu dosyayı yeniden adlandırmak `LoggingLibrary.nuspec` ve bir düzenleyicide açın.
1. Aşağıdaki ile eşleşecek şekilde dosyasını güncelleştirme adiniz uygun bir değerle değiştirin. `<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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
> Paket sürümü ile soneki `-alpha`, `-beta` veya `-rc` paketinizi yayın öncesi olarak işaretlemek için kontrol [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) yayın öncesi sürümleri hakkında daha fazla bilgi için.

### <a name="add-reference-assemblies"></a>Başvuru derlemeleri ekleme

Platforma özgü başvuru derlemeleri eklemek için aşağıdakileri ekleyin `<files>` öğesinin `LoggingLibrary.nuspec` , desteklenen platformlar için uygun şekilde:

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
> DLL ve XML dosyalarının adlarını kısaltmak için tüm verilen projeye, select sağ tıklayın **Kitaplığı** sekmesinde ve derleme adları değiştirin.

### <a name="add-dependencies"></a>Bağımlılıkları ekleyin.

Yerel uygulamaları için belirli bağımlılıkları varsa, `<dependencies>` öğeyle `<group>` öğeleri, örneğin belirtin:

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

Örneğin, aşağıdaki iTextSharp UAP hedef için bağımlılık olarak ayarlamanız gerekir:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Son .nuspec

Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden adiniz uygun bir değerle değiştirilmelidir:

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

## <a name="package-the-component"></a>Paket bileşeni

Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:

```cli
nuget pack LoggingLibrary.nuspec
```

Bu oluşturur `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:

![NuGet paket LoggingLibrary paket gösteren Gezgini](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır. Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.

Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok .NET Framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [MSBuild özellik ve hedefleri bir pakete dahil etme](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)