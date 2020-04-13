---
title: Visual Studio 2015 ile .NET Standardı ve .NET Framework NuGet Paketleri Oluşturun
description: NuGet 3.x ve Visual Studio 2015'i kullanarak .NET Standard ve .NET Framework NuGet paketlerini oluşturmanın uçtan uca bir walkthrough'u.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380720"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturun

**Not:** Visual Studio 2017 ,.NET Standart kitaplıkları geliştirmek için önerilir. Visual Studio 2015 işe yarayabilir ancak .NET Core aracı yalnızca Önizleme durumuna getirildi. NuGet 4.x+ ve Visual Studio 2017 ile çalışmak için [Visual Studio 2017 ile bir paket oluşturun ve yayınlayın.](../quickstart/create-and-publish-a-package-using-visual-studio.md)

[.NET Standart Kitaplığı,](/dotnet/articles/standard/library) .NET'in tüm çalışma saatlerinde kullanıma sunulması amaçlanan .NET API'lerinin resmi bir belirtimidir ve böylece .NET ekosisteminde daha fazla tekdüzelik oluşturur. .NET Standart Kitaplığı, iş yükünden bağımsız olarak uygulanacak tüm .NET platformları için tek tip bir BCL (Taban Sınıf Kitaplığı) API'leri tanımlar. Geliştiricilerin tüm .NET çalışma saatlerinde kullanılabilir kod lar üretmesini sağlar ve paylaşılan koddaki platforma özgü koşullu derleme yönergelerini ortadan kaldırmazsa azaltır.

Bu kılavuz, .NET Standart Kitaplığı 1.4'u veya .NET Framework 4.6'yı hedefleyen bir paket ilerler. .NET Standart 1.4 kitaplığı .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core ve Mono/Xamarin genelinde çalışır. Ayrıntılar için [.NET Standart eşleme tablosuna](/dotnet/standard/net-standard#net-implementation-support) (.NET belgeleri) bakın. İsterseniz .NET Standart Kitaplığı'nın diğer sürümünü seçebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2015 Güncelleştirme 3
1. (.Sadece NET Standart) [.NET Çekirdek SDK](https://www.microsoft.com/net/download/)
1. NuGet CLI. nuget.exe'nin en son sürümünü [nuget.org/downloads](https://nuget.org/downloads)indirin ve seçtiğiniz bir konuma kaydedin. Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.

    > [!Note]
    > nuget.exe cli aracı kendisi değil, bir yükleyici, bu yüzden yerine çalışan tarayıcınızdan indirilen dosyayı kaydetmek için emin olun.

## <a name="create-the-class-library-project"></a>Sınıf kitaplığı projesini oluşturma

1. Visual Studio, **Dosya > Yeni > Projesi,** Visual **C# > Windows** düğümünü genişletin, Sınıf **Kitaplığı (Taşınabilir)** seçin, AppLogger adını değiştirin ve **Tamam'ı**seçin.

    ![Yeni sınıf kitaplık projesi oluşturma](media/NetStandard-NewProject.png)

1. Görünen **Taşınabilir Sınıf Kitaplığı Ekle** iletişim kutusunda, `.NET Framework 4.6` 'nin `ASP.NET Core 1.0`ve. (.NET Framework hedeflenebiliyorsanız, hangi seçeneklerin uygun olduğunu seçebilirsiniz.)

1. .NET Standard'ı hedefliyorsanız, `AppLogger (Portable)` Çözüm Gezgini'nde sağ tıklatın, **Özellikler'i**seçin, **Kitaplık** sekmesini seçin ve ardından **Hedefleme** bölümünde **Hedef .NET Platform Standardı'nı** seçin. Bu eylem onay ister, sonra açılır `.NET Standard 1.4` yerden (veya başka bir kullanılabilir sürümü) seçebilirsiniz:

    ![Hedefin .NET Standart 1.4'e ayarlanması](media/NetStandard-ChangeTarget.png)

1. **Yapı** sekmesine tıklayın, **Yapılandırmayı** `Release`değiştirin ve **XML dokümantasyon dosyası**için kutuyu işaretleyin.

1. Kodunuzu bileşene ekleyin, örneğin:

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

1. Yapılandırmayı Serbest Bırak'a ayarlayın, projeyi oluşturun ve Klasör içinde `bin\Release` DLL ve XML dosyalarının üretilip üretilmediğini denetleyin.

## <a name="create-and-update-the-nuspec-file"></a>.nuspec dosyasını oluşturma ve güncelleştirme

1. Komut istemini açın, klasör `AppLogger.csproj` içeren klasöre gidin `.sln` (dosyanın bulunduğu yerin `spec` bir alt `AppLogger.nuspec` düzeyi) ve ilk dosyayı oluşturmak için NuGet komutunu çalıştırın:

    ```cli
    nuget spec
    ```

1. Bir `AppLogger.nuspec` düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek aşağıdakilerle eşleşecek şekilde güncelleştirin. Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın. Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.

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

1. Dosyaya, `.nuspec` yani kitaplığın DLL'si ve IntelliSense XML dosyasına başvuru derlemeleri ekleyin:

    .NET Standard'ı hedefliyorsanız, girişler aşağıdakilere benzer görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework hedeflenenden, girişler aşağıdakilere benzer görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Çözüme sağ tıklayın ve paket için tüm dosyaları oluşturmak için **Çözüm Oluştur'u** seçin.

### <a name="declaring-dependencies"></a>Bağımlılıkları bildirme

Diğer NuGet paketlerine herhangi bir bağımlılığınız varsa, bildirimin `<dependencies>` `<group>` öğesindekileri öğelerle listele. Örneğin, NewtonSoft.Json 8.0.3 veya üzeri bir bağımlılık bildirmek için aşağıdakileri ekleyin:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Sürüm özniteliğinin *version* buradaki sözdizimi, 8.0.3 veya üzeri sürümün kabul edilebilir olduğunu gösterir. Farklı sürüm aralıkları belirtmek için [Paket sürümüne](../concepts/package-versioning.md)bakın.

### <a name="adding-a-readme"></a>Okuma meonu ekleme

Dosyanızı `readme.txt` oluşturun, proje kök klasörüne yerleştirin ve `.nuspec` dosyaya bakın:

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

Paket bir `readme.txt` projeye yüklendiğinde Visual Studio görüntülenir. Dosya,.NET Core projelerine yüklendiğinde veya bağımlılık olarak yüklenen paketler için gösterilmez.

## <a name="package-the-component"></a>Bileşeni paketle

Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:

```cli
nuget pack AppLogger.nuspec
```

Bu oluşturur. `AppLogger.YOUR_NAME.1.0.0.nupkg` Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletileyerek aşağıdaki içeriği görürsünüz (.NET Standardı için gösterilmiştir):

![NuGet Paket Explorer AppLogger paketini gösteriyor](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır. Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

Mac `pack` OS X'te Mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığını unutmayın. Mac'te, dosyadaki `.nuspec` Windows yol adlarını Unix stili yollara dönüştürmeniz gerekir.

## <a name="related-topics"></a>İlgili konular

- [.nuspec referans](../reference/nuspec.md)
- [Birden çok .NET çerçeve sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [MSBuild sahne ve hedeflerini bir pakete dahil et](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [.NET Standart Kütüphane belgeleri](/dotnet/articles/standard/library)
- [.NET Framework'den .NET Core'a taşıma](/dotnet/articles/core/porting/index)
