---
title: Visual Studio 2015 ile birlikte .NET standart ve .NET Framework NuGet paketleri oluşturma
description: NuGet kullanarak .NET standart ve .NET Framework NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: a77d977b2abc4cfd8be48e97e4c811e68e09bd61
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015 ile .NET standart ve .NET Framework paketleri oluşturma

**Not:** .NET standart kitaplıkları geliştirmek için Visual Studio 2017 önerilir. Visual Studio 2015 çalışabilir ancak .NET Core araç yalnızca önizleme duruma getirildi. Bkz: [oluşturma ve Visual Studio 2017 paketiyle yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) NuGet 4.x+ ve Visual Studio 2017 çalışma.

[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması. .NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar. Tüm .NET çalışma zamanları arasında kullanılabilir ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldıran bir kod oluşturmak geliştiriciler sağlar.

Bu kılavuzda .NET standart kitaplığı 1.4 hedefleyen bir NuGet paketi veya .NET Framework 4.6 hedefleyen bir paket oluşturma konusunda anlatılmaktadır. Bir .NET standart 1.4 kitaplığı .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin çalışır. Ayrıntılar için bkz [.NET standart eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.NET belge). İsterseniz, başka bir sürümünü .NET standart kitaplığı seçebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2015 Güncelleştirme 3
1. (Yalnızca .NET standart) [.NET core SDK](https://www.microsoft.com/net/download/)
1. NuGet CLI. Nuget.exe en son sürümünü indirme [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme. Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

    > [!Note]
    > nuget.exe CLI aracı kendisini bir yükleyici nedenle bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.

## <a name="create-the-class-library-project"></a>Sınıf kitaplığı proje oluşturma

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, select **sınıf kitaplığı (taşınabilir)** AppLogger için adı değiştirin ve seçin **Tamam**.

    ![Yeni sınıf kitaplığı proje oluşturma](media/NetStandard-NewProject.png)

1. İçinde **taşınabilir sınıf kitaplığı eklemek** görünür, iletişim için seçenekleri seçin `.NET Framework 4.6` ve `ASP.NET Core 1.0`. (.NET Framework'ü hedefleme, hangi seçenekleri uygun seçebilirsiniz.)

1. .NET standardını hedefleyen, sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesini ve ardından **hedef .NET Platform standardını** içinde **hedefleme** bölümü. Daha sonra seçebileceğiniz onaylama için bu eylem ister `.NET Standard 1.4` (veya başka bir kullanılabilir sürüm) açılır:

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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Yapılandırması yayın olarak ayarlanmış, projeyi oluşturun ve DLL ve XML dosyaları içinde üretilir denetleyin `bin\Release` klasör.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturun ve .nuspec dosyası güncelleştirin

1. Bir komut istemi açın, içeren klasöre gidin `AppLogger.csproj` klasörü (bir düzey altındaki where `.sln` dosyası), NuGet çalıştırıp `spec` ilk oluşturmak için komutu `AppLogger.nuspec` dosyası:

    ```cli
    nuget spec
    ```

1. Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin. `<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Başvuru derlemeleri eklemek `.nuspec` dosya, kitaplığın DLL ve IntelliSense XML dosyası:

    .NET standardını hedefleyen girişleri aşağıdakine benzer görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework'ü hedefleme girişleri aşağıdakine benzer görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Çözüme sağ tıklayın ve seçin **yapı çözümü** bir paket için tüm dosyaları oluşturmak için.

### <a name="declaring-dependencies"></a>Bağımlılıklar bildirme

Diğer NuGet paketlerini bağımlılıkları varsa, bildirim de listesinde `<dependencies>` öğeyle `<group>` öğeleri. Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya üstü bildirmek için aşağıdakileri ekleyin:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir ya da yukarıdaki kabul edilebilir. Farklı bir sürüm aralıklarını belirtmek için başvurmak [paket sürüm](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Bir benioku dosyası ekleme

Oluştur, `readme.txt` dosya, bu proje kök klasöre yerleştirin ve kendisine başvuran `.nuspec` dosyası:

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

Visual Studio görüntü `readme.txt` paket bir projeye yüklü olduğunda. Dosya, .NET Core projelerine veya bağımlılık olarak yüklü olan paketleri yüklendiğinde gösterilmez.

## <a name="package-the-component"></a>Paket bileşeni

Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:

```cli
nuget pack AppLogger.nuspec
```

Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`. Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, (.NET standart için gösterilen) aşağıdaki içeriğe bakın:

![NuGet paket AppLogger paket gösteren Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır. Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.

Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz. Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.

## <a name="related-topics"></a>İlgili konular

- [.nuspec başvurusu](../reference/nuspec.md)
- [Birden çok .NET framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellik ve hedefler](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [.NET standart kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core için .NET Framework'bağlantı noktası oluşturma](/dotnet/articles/core/porting/index)
