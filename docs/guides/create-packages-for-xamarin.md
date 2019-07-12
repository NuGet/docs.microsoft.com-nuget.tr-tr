---
title: (İOS, Android ve Windows için) Xamarin ile Visual Studio 2015 için NuGet paketleri oluşturma
description: Xamarin için NuGet paketleri oluşturmak üzere bir uçtan uca izlenecek yol, iOS, Android ve Windows üzerinde yerel API'lerini kullanın.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 81f78de02d9b6510f195e04c78436e38f9b7353d
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842417"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Visual Studio 2015 ile Xamarin’e yönelik paketler oluşturma

Bir paket için Xamarin iOS, Android ve Windows, yerel API'lerin çalışma zamanı işletim sistemine bağlı olarak kullanan kod içerir. Bunu yapmak basit olsa da, .NET standart kitaplıkları aracılığıyla ortak bir API yüzey ya da geliştiriciler bir PCL paketinden kullanmasına izin vermek için tercih edilir.

Bu izlenecek yolda, kullandığınız Visual Studio 2015 iOS, Android ve Windows mobil projeleri kullanılabilir platformlar arası bir NuGet paketi oluşturun.

1. [Önkoşullar](#prerequisites)
1. [Proje yapısını ve Özet kodu oluşturma](#create-the-project-structure-and-abstraction-code)
1. [Platforma özgü kod yazma](#write-your-platform-specific-code)
1. [Oluşturma ve güncelleştirme .nuspec dosyası](#create-and-update-the-nuspec-file)
1. [Paket bileşeni](#package-the-component)
1. [İlgili Konular](#related-topics)

## <a name="prerequisites"></a>Önkoşullar

1. Evrensel Windows Platformu (UWP) ve Xamarin ile Visual Studio 2015. Yamasını ücretsiz Community edition [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz. UWP ve Xamarin araçları dahil etmek için bir özel yükleme seçeneğini belirleyin ve uygun seçeneklerini işaretleyin.
1. NuGet CLI. Nuget.exe en son sürümünü indirin [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme. Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

> [!Note]
> nuget.exe CLI aracı kendisini bir yükleyici dolayısıyla bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.

## <a name="create-the-project-structure-and-abstraction-code"></a>Proje yapısını ve Özet kodu oluşturma

1. İndirme ve çalıştırma [Xamarin Şablonları uzantısı için eklenti](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) Visual Studio için. Bu şablonlar Bu izlenecek yol için gerekli proje yapısını oluşturmak kolaylaştıracak.
1. Visual Studio'da **Dosya > Yeni > Proje**, arama `Plugin`seçin **Xamarin için eklentisi** şablon LoggingLibrary için adı değiştirin ve Tamam'a tıklayın.

    ![Visual Studio'da yeni bir boş uygulama (Xamarin.Forms taşınabilir) projesine](media/CrossPlatform-NewProject.png)

Sonuçta elde edilen çözümü ile çeşitli platforma özgü projeleri birlikte iki PCL projeleri içerir:

- Adlı PCL `Plugin.LoggingLibrary.Abstractions (Portable)`, bu durumda bileşenin genel arabirimi (API yüzey alanı) tanımlar `ILoggingLibrary` ILoggingLibrary.cs dosyasında yer alan arabirimi. Arayüzü kitaplığınıza tanımladığınız budur.
- Diğer PCL `Plugin.LoggingLibrary (Portable)`, platforma özel uygulanışı soyut arabirimi çalışma zamanında bulur CrossLoggingLibrary.cs kodunu içerir. Genellikle bu dosyayı değiştirmek gerekmez.
- Gibi platforma özgü projeleri `Plugin.LoggingLibrary.Android`, her içeren ilgili LoggingLibraryImplementation.cs dosyalarına arabiriminde yerel bir uygulama içerir. Kitaplığınızın kodu, oluşturduğunuz budur.

Varsayılan olarak, arabirim tanımı, ancak hiçbir yöntemleri soyutlama projenin ILoggingLibrary.cs dosyası içerir. Bu izlenecek yolda amacı doğrultusunda, ekleme bir `Log` yöntemini aşağıdaki şekilde:

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

Platforma özel uygulanışı uygulamak için `ILoggingLibrary` arabirimi ve yöntemlerinin, aşağıdakileri yapın:

1. Açık `LoggingLibraryImplementation.cs` dosya her platform için proje ve gerekli kodu eklemek. Örneğin (kullanarak `Plugin.LoggingLibrary.Android` Proje):

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

1. Bu uygulama projelerindeki desteklemek istediğiniz her platform için yineleyin.
1. İOS projesine sağ tıklayın, **özellikleri**, tıklayın **derleme** sekmesini tıklatın ve "\iPhone" kaldırma **çıkış yolu** ve **XML belge dosyası**  ayarları. Bu kılavuzda daha sonra kolaylık olması için yalnızca budur. İşiniz bittiğinde dosyayı kaydedin.
1. Çözüme sağ tıklayın, **Configuration Manager...** ve **derleme** PCLs ve destekleyen her platform için kutuları.
1. Çözüme sağ tıklayıp **Çözümü Derle** iş denetleyin ve sonraki paketini yapıları üretmek için. Eksik başvurular hakkında hataları alırsanız, çözüme sağ tıklayın, **NuGet paketlerini geri yükle** bağımlılıklarını yükleyin ve yeniden oluşturun.

> [!Note]
> İOS için oluşturmak için bir ağa bağlı Mac üzerinde açıklandığı gibi Visual Studio'ya bağlı gereksinim [Visual Studio için Xamarin.ios'a giriş](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Kullanılabilir Mac yoksa, Yapılandırma Yöneticisi'nin (yukarıdaki adım 3) iOS projesi temizleyin.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturma ve güncelleştirme .nuspec dosyası

1. Bir komut istemi açın ve gidin `LoggingLibrary` nerede aşağıda bir düzey klasör `.sln` dosyası olduğunu ve NuGet komutunu çalıştırarak `spec` ilk oluşturmak için komut `Package.nuspec` dosyası:

    ```cli
    nuget spec
    ```

1. Bu dosyayı yeniden adlandır `LoggingLibrary.nuspec` ve bir düzenleyicide açın.
1. Aşağıdaki ile eşleşecek şekilde dosyasını güncelleştirme YOUR_NAME uygun bir değerle değiştirin. `<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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
> Paket sürümünüzle sonekine sahip `-alpha`, `-beta` veya `-rc` paketinizi yayın öncesi olarak işaretlemek için denetleme [yayın öncesi sürümleri](../create-packages/prerelease-packages.md) yayın öncesi sürümleri hakkında daha fazla bilgi.

### <a name="add-reference-assemblies"></a>Başvuru bütünleştirilmiş kodları Ekle

Platforma özgü başvuru bütünleştirilmiş kodları eklemek için aşağıdaki ekleyin `<files>` öğesinin `LoggingLibrary.nuspec` , desteklenen platformlar için uygun şekilde:

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
> DLL ve XML dosyalarının adlarını kısaltmak için herhangi bir proje üzerinde select sağ **Kitaplığı** sekme ve derleme adları değiştirin.

### <a name="add-dependencies"></a>Bağımlılıkları ekleyin

Yerel uygulamaları için belirli bağımlılıkları varsa, `<dependencies>` öğeyle `<group>` öğeleri, örneğin belirtmek için:

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

Örneğin, aşağıdaki iTextSharp UAP hedefi için bağımlılık olarak ayarlayabilirsiniz:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Son .nuspec

Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden YOUR_NAME uygun bir değer ile değiştirilmelidir:

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

Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:

```cli
nuget pack LoggingLibrary.nuspec
```

Bu işlem oluşturur `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:

![NuGet paket Gezgini LoggingLibrary paket gösteriliyor](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır. Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.

Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok .NET Framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellikler ve hedefler](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)