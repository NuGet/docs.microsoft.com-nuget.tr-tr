---
title: Visual Studio 2015 ile .NET Standard ve .NET Framework NuGet paketleri oluşturma
description: NuGet kullanarak .NET Standard ve .NET Framework NuGet paketleri oluşturma bir uçtan uca Kılavuz 3.x ve Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 7b1ccfbede4cec53cee3ec7d1c023e4c5be60bf0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545919"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturma

**Not:** Visual Studio 2017, .NET standart kitaplıkları geliştirmek için önerilir. Visual Studio 2015 çalışabilir ancak .NET Core araçları yalnızca önizleme duruma getirildi. Bkz: [oluşturun ve Visual Studio 2017 ile paket yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) NuGet 4.x+ ve Visual Studio 2017 ile çalışmak için.

[.NET Standard Kitaplığı](/dotnet/articles/standard/library) olduğu bir resmi belirtimi .NET API'lerini amaçlanan bu nedenle büyük gerekmemesi .NET ekosisteminde oluşturma tüm .NET çalışma zamanları, kullanılabilir olması. .NET Standard kitaplığı BCL (temel sınıf kitaplığı) API kümesi, iş yükünü bağımsız uygulamak tüm .NET platformları için tanımlar. Ancak, geliştiricilerin tüm .NET çalışma zamanı arasında kullanılabilir ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldıran bir kod üretmek etkinleştirir.

Bu kılavuzda, .NET Standard kitaplığı 1.4 hedefleyen bir NuGet paketi veya .NET Framework 4.6 targeting paketi oluşturma işlemini gösterir. .NET Standard 1.4 kitaplığı, .NET Framework 4.6.1, Evrensel Windows platformu 10, .NET Core ve Mono/Xamarin arasında çalışır. Ayrıntılar için bkz [.NET Standard eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.NET belgeleri). İsterseniz, diğer .NET Standard kitaplığı sürümünü seçebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2015 Güncelleştirme 3
1. (Yalnızca .NET standard) [.NET core SDK'sı](https://www.microsoft.com/net/download/)
1. NuGet CLI. Nuget.exe en son sürümünü indirin [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme. Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

    > [!Note]
    > nuget.exe CLI aracı kendisini bir yükleyici dolayısıyla bunu çalıştırmak yerine tarayıcınızdan indirilen dosyayı kaydettiğinizden emin olur.

## <a name="create-the-class-library-project"></a>Sınıf kitaplığı projesi oluşturun

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C# > Windows** düğümünü **sınıf kitaplığı (taşınabilir)** AppLogger için adı değiştirin ve seçin **Tamam**.

    ![Yeni sınıf kitaplığı projesi oluşturun](media/NetStandard-NewProject.png)

1. İçinde **taşınabilir sınıf kitaplığı Ekle** görüntülenen iletişim seçmek için seçenekleri `.NET Framework 4.6` ve `ASP.NET Core 1.0`. (.NET Framework'ü hedefleyen, hangi seçenekleri uygun seçebilirsiniz.)

1. .NET Standard hedefleme, sağ `AppLogger (Portable)` Çözüm Gezgini'nde seçin **özellikleri**seçin **Kitaplığı** sekmesine ve ardından seçin **hedef .NET Platform standardını** içinde **hedefleme** bölümü. Bu eylem, onay sonrasında seçebilirsiniz, ister `.NET Standard 1.4` (veya başka bir kullanılabilir sürüm) açılan:

    ![Hedef .NET Standard 1.4 için ayarlama](media/NetStandard-ChangeTarget.png)

1. Tıklayarak **derleme** sekmesinde, **yapılandırma** için `Release`ve kutusunu işaretlemeniz **XML belge dosyası**.

1. Örneğin, kodunuzu bileşene ekleyin:

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

1. Yapılandırması yayın olarak ayarlanmış, projeyi derleyin ve DLL ve XML dosyaları içinde üretildiğini denetleyin `bin\Release` klasör.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturma ve güncelleştirme .nuspec dosyası

1. Bir komut istemi açın, klasör içeren dizine gidin `AppLogger.csproj` klasörü (bir düzey altındaki nerede `.sln` dosyasıdır), NuGet çalıştırıp `spec` ilk oluşturmak için komut `AppLogger.nuspec` dosya:

    ```cli
    nuget spec
    ```

1. Açık `AppLogger.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirmeniz YOUR_NAME uygun bir değerle değiştirin. `<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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

1. Başvuru bütünleştirilmiş kodları için ekleme `.nuspec` kitaplığının DLL ve IntelliSense XML dosyasının dosya:

    .NET Standard hedefleme, girişleri aşağıdakine benzer şekilde görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework'ü hedefleyen girişleri aşağıdaki gibi görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Çözüme sağ tıklayıp **Çözümü Derle** paket için tüm dosyaları oluşturmak için.

### <a name="declaring-dependencies"></a>Bağımlılıkları bildirme

Diğer NuGet paketleri üzerinde bağımlılıkları varsa, bu bildirim, liste `<dependencies>` öğeyle `<group>` öğeleri. Örneğin, bir bağımlılık NewtonSoft.Json 8.0.3 veya sonraki sürümlere bildirmek için aşağıdakileri ekleyin:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Söz dizimi *sürüm* özniteliği burada bu sürümü 8.0.3 gösterir veya üstü kabul edilebilir. Farklı sürüm aralıklarını belirtmek için başvurmak [Paket sürümü oluşturma](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Benioku dosyası ekleme

Oluşturma, `readme.txt` dosyası, proje kök klasörüne yerleştirin ve buna başvuran `.nuspec` dosyası:

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

Visual Studio görüntü `readme.txt` paketini projeye yüklü olduğunda. Dosya, .NET Core projeleri veya bağımlılık olarak yüklenen paketler yüklediğinizde gösterilmez.

## <a name="package-the-component"></a>Paket bileşeni

Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:

```cli
nuget pack AppLogger.nuspec
```

Bu oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg`. Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, (.NET Standard için gösterilen) aşağıdaki içeriğe bakın:

![NuGet paket Gezgini AppLogger paket gösteriliyor](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır. Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.

Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../create-packages/publish-a-package.md).

Unutmayın `pack` Mac OS X üzerinde Mono 4.4.2 gerektirir ve Linux sistemlerinde çalışmaz. Mac bilgisayarlarda, Windows yol adları olarak da dönüştürmelisiniz `.nuspec` UNIX stili yollara dosya.

## <a name="related-topics"></a>İlgili konular

- [.nuspec başvurusu](../reference/nuspec.md)
- [Birden çok .NET framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellikler ve hedefler](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [.NET standard kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core ile .NET Framework'ten taşıma](/dotnet/articles/core/porting/index)
