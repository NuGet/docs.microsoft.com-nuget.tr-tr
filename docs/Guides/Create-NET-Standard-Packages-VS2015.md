---
title: "Visual Studio 2015 ile birlikte .NET standart NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "NuGet kullanarak .NET standart NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015."
keywords: "bir paket, .NET standart paketler, .NET standart eşleme tablosu oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 24089eba93d80dca32632a8c1e174aef849ee72d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Visual Studio 2015 ile .NET standart paketleri oluşturma

*Nuget'e geçerlidir 3.x. Bkz: [oluşturma .NET standart paketlerle Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) NuGet 4.x+ ile çalışmak için.*

[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması. .NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar. Bunu tüm .NET çalışma zamanları arasında kullanılabilir PCLs üretmek için geliştiricilere olanak sağlar ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldırır.

Bu kılavuz .NET standart kitaplığı 1.4 hedefleyen bir nuget paketi oluşturmada size yol gösterir. Bu, .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin çalışır. Ayrıntılar için bkz [.NET standart eşleme tablosu](#net-standard-mapping-table) bu konuda daha sonra.

1. [Ön koşullar](#pre-requisites)
1. [Sınıf kitaplığı proje oluşturma](#create-the-class-library-project)
1. [Oluşturun ve .nuspec dosyası güncelleştirin](#create-and-update-the-nuspec-file)
1. [Paket bileşeni](#package-the-component)
1. [Ek Seçenekler](#additional-options)
1. [.NET standart eşleme tablosu](#net-standard-mapping-table)
1. [İlgili Konular](#related-topics)

## <a name="pre-requisites"></a>Ön koşullar

1. Visual Studio 2015. Community edition ücretsiz yükleyin [visualstudio.com](https://www.visualstudio.com/); Elbette Professional ve Enterprise sürümleri de kullanabilirsiniz.
1. .NET core: Install şablonları birlikte .NET Core ve diğer araçları Visual Studio 2015'ten [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. NuGet CLI. Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme. Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

> [!Note]
> nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.

## <a name="create-the-class-library-project"></a>Sınıf kitaplığı proje oluşturma

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, select **sınıf kitaplığı (taşınabilir)**AppLogger için adı değiştirin ve Tamam'ı tıklatın.

    ![Yeni sınıf kitaplığı proje oluşturma](media/NetStandard-NewProject.png)

1. İçinde **taşınabilir sınıf kitaplığı eklemek** görünen seçin iletişim `.NET Framework 4.6` ve `ASP.NET Core 1.0` seçenekleri.

1. Sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesini ve ardından **hedef .NET Platform standardını** içinde**Hedefleme** bölümü. Bu daha sonra seçebileceğiniz onaylama için ister `.NET Standard 1.4` açılır:

    ![Hedef .NET standart 1.4 ayarlama](media/NetStandard-ChangeTarget.png)

1. Tıklayın **yapı** sekmesinde, değiştirmek **yapılandırma** için `Release`ve için kutuyu **XML belge dosyası**.

1. Kodunuzu bileşenine örneğin ekleyin:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. (Sürüm yapılandırmasıyla) projeyi oluşturun ve DLL ve XML dosyaları bin\Release klasör içinde üretilir denetleyin.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturun ve .nuspec dosyası güncelleştirin

1. Bir komut istemi açın, içeren klasöre gidin `AppLogg.csproj` klasörü (bir düzey altındaki where `.sln` dosyası), NuGet çalıştırıp `spec` ilk oluşturmak için komutu `AppLogger.nuspec` dosyası:

```cli
nuget spec
```

1. Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin. `<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata iletisi alırsınız unutmayın.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Başvuru derlemeleri eklemek `.nuspec` dosya, kitaplığın DLL ve IntelliSense XML dosyası:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Çözüme sağ tıklayın ve seçin **yapı çözümü** bir paket için tüm dosyaları oluşturmak için.

## <a name="package-the-component"></a>Paket bileşeni

Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:

```cli
nuget pack AppLogger.nuspec
```

Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`. Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriği görürsünüz:

![NuGet paket AppLogger paket gösteren Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır. Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.

Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz. Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.

## <a name="additional-options"></a>Ek Seçenekler

NuGet paket oluşturma için ek seçenekler içine aşağıdaki bölümlerde gidin:

- [Bağımlılıklar bildirme](#declaring-dependencies)
- [Birden çok hedef çerçeveyi destekleme](#supporting-multiple-target-frameworks)
- [MSBuild hedefleri ve özellik ekleme](#adding-targets-and-props-for-msbuild)
- [Yerelleştirilmiş paketleri oluşturma](#creating-localized-packages)
- [Bir benioku dosyası ekleme](#adding-a-readme)

### <a name="declaring-dependencies"></a>Bağımlılıklar bildirme

Diğer NuGet paketlerini bağımlılıkları varsa de listesinde `<dependencies>` öğeyle `<group>` öğeleri. Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya üstü bildirmek için aşağıdakileri ekleyin:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir ya da yukarıdaki kabul edilebilir. Farklı bir sürüm aralıklarını belirtmek için başvurmak [paket sürüm](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Birden çok hedef çerçeveyi destekleme

.NET Framework'teki .NET standart 1.4 içinde kullanılabilir olmayan 4.6.2 bir API avantajlarından yararlanmak istediğiniz varsayalım. Bunu yapmak için öncelikle koşullu derleme veya paylaşılan projeleri kullanarak kitaplığı için .NET 4.6.2 derlendiğinden emin olmak gerekir. (Visual Studio'da NetCore projesi oluşturun, tercih ettiğiniz framework birden çok framework bölümüne ekleyin, oluşturmak ve bunları kullanabileceğiniz ardından.) Ardından aşağıdaki gibi basit kurala dayalı çalışma dizini tekniği kullanarak paketi oluşturun:

1. Projede kullanıcının kök klasörünü içeren, `.nuspec` adlı bir klasör oluşturun, dosya `lib`.
1. İçinde `lib`, desteklemek istediğiniz her platform için klasörleri oluşturun:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. İçinde `.nuspec` dosya, ekleme bir `files` düğümü altında `package` düğümü ve dosyaları başvurmak `lib` joker karakterleri kullanma. **Not:** belirteci değişikliklerini kurala dayalı çalışma dizini yaklaşımda desteklenmiyor, bu nedenle bunları hazır değer ile değiştirin:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.spec`.

Bu yöntemi kullanma hakkında daha fazla ayrıntı için bkz: [destekleyen birden çok .NET Framework sürümü](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild hedefleri ve özellik ekleme

Bazı durumlarda özel aracın veya işlemin derleme sırasında çalıştırma gibi paketinizi tüketen projelerine özel derleme hedefler ya da özellikleri eklemek isteyebilirsiniz. Dosyaları ekleyerek bunu bir `\build` aşağıdaki adımlarda açıklandığı gibi klasör. NuGet \build dosyalarıyla bir paketi yüklendiğinde, .targets ve .props dosyalarını işaret proje dosyasında bir MSBuild öğe ekler.

1. Projeyi içeren klasörün içinde, `.nuspec` adlı bir klasör oluşturun, dosya `build`.

1. İçinde `build`, desteklenen her için klasörler oluşturmanız ve içinde bulunanlar yerleştirin, `.targets` ve `.props` dosyaları:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. İçinde `.nuspec` dosya, ekleme bir `files` düğümü altında `package` düğümü ve dosyaları başvurmak `build` joker karakterleri kullanma.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.nuspec`.

Ek ayrıntılar için başvurmak [dahil MSBuild özellik ve paketteki hedefleri](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).

### <a name="creating-localized-packages"></a>Yerelleştirilmiş paketleri oluşturma

Yerelleştirilmiş sürümleri kitaplığınızın oluşturmak için farklı yerel ayarlar için ayrı paketleri oluşturmak veya tek bir paket içinde yerelleştirilmiş kaynak derlemeleri içerir. Aşağıda, Almanca ve İtalyanca için ikinci yaklaşımı nasıl verilmiştir:

1. Her hedef çerçeve klasörünün altında içinde `lib`, İngilizce varsayılan dışındaki desteklenen her dil için klasörleri oluşturun. Bu klasörlerde kaynak derlemeler ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz. Örneğin:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. İçinde `.nuspec` dosya, bu dosyaları başvuru `<files>` düğümü:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Kullanarak yeniden paketi oluşturma `nuget pack AppLogger.nuspec`.

### <a name="adding-a-readme"></a>Bir benioku dosyası ekleme

Dahil ettiğinizde bir `readme.txt` paketi, Visual Studio kök dosyasında görüntüler, paket doğrudan yüklendiğinde.

> [!Note]
> Bağımlılık olarak yüklü olan paketler için veya .NET Core projeleri için Benioku dosyaları gösterilmez.

Bunu yapmak için oluşturmak, `readme.txt` dosya, bu proje kök klasöre yerleştirin ve kendisine başvuran `.nuspec` dosyası:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

## <a name="net-standard-mapping-table"></a>.NET standart eşleme tablosu

|Platform adı |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1,5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4,5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Mono/Xamarin platformları| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|Evrensel Windows Platformu| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| Win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|

## <a name="related-topics"></a>İlgili konular

- [Nuspec başvurusu](../schema/nuspec.md)
- [Simge paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok .NET Framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellik ve hedefler](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
- [.NET standart kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core için .NET Framework'bağlantı noktası oluşturma](/dotnet/articles/core/porting/index)
