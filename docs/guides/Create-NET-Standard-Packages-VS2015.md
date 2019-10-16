---
title: Visual Studio 2015 ile .NET Standard ve .NET Framework NuGet paketleri oluşturma
description: NuGet 3. x ve Visual Studio 2015 kullanarak NuGet paketleri .NET Standard ve .NET Framework oluşturmaya yönelik uçtan uca bir anlatım.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380720"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015 ile .NET Standard ve .NET Framework paketleri oluşturma

**Note:** .NET Standard kitaplıklarını geliştirmek için Visual Studio 2017 önerilir. Visual Studio 2015 çalışır, ancak .NET Core araçları yalnızca önizleme durumuna getirildi. Bkz. NuGet 4. x + ve Visual Studio 2017 ile çalışmak için [Visual Studio 2017 ile bir paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md) .

[.NET Standard kitaplığı](/dotnet/articles/standard/library) , .NET API 'lerinin tüm .NET çalışma zamanları üzerinde kullanılabilmesi amaçlanan ve bu sayede .net ekosisteminde daha büyük bir uyumluluk sağlamak amacıyla sunulan biçimsel bir belirtimdir. .NET Standard kitaplığı, iş yüküyle bağımsız olarak uygulanacak tüm .NET platformları için tek bir BCL kümesi (temel sınıf kitaplığı) API 'Lerini tanımlar. Geliştiricilerin tüm .NET çalışma zamanları genelinde kullanılabilir olan kodu üretmesini ve paylaşılan koddaki platforma özgü koşullu derleme yönergelerini ortadan kaldırmaması gerektiğini azaltmasını sağlar.

Bu kılavuzda, .NET Standard kitaplığı 1,4 ' i hedefleyen bir NuGet paketi veya 4,6 .NET Framework hedefleme bir paket oluşturma işlemi adım adım açıklanmaktadır. .NET Standard 1,4 kitaplığı .NET Framework 4.6.1, Evrensel Windows Platformu 10, .NET Core ve mono/Xamarin arasında çalışmaktadır. Ayrıntılar için bkz. [.NET Standard eşleme tablosu](/dotnet/standard/net-standard#net-implementation-support) (.net belgeleri). İsterseniz .NET Standard kitaplığının diğer sürümünü seçebilirsiniz.

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2015 Güncelleştirme 3
1. (Yalnızca .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. NuGet CLı. NuGet. exe ' nin en son sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin ve seçtiğiniz bir konuma kaydederek yükleyin. Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

    > [!Note]
    > NuGet. exe, bir yükleyici değil CLı aracının kendisidir, bu nedenle indirilen dosyayı çalıştırmak yerine tarayıcınızdan kaydettiğinizden emin olun.

## <a name="create-the-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

1. Visual Studio 'da **dosya > yeni > projesi**,  **C# Visual > Windows** düğümünü genişletin, **sınıf kitaplığı (taşınabilir)** öğesini seçin, adı appgünlükçü olarak değiştirin ve **Tamam**' ı seçin.

    ![Yeni sınıf kitaplığı projesi oluştur](media/NetStandard-NewProject.png)

1. Görüntülenen **taşınabilir sınıf kitaplığı Ekle** iletişim kutusunda `.NET Framework 4.6` ve `ASP.NET Core 1.0` seçeneklerini belirleyin. (.NET Framework hedefliyorsanız, uygun seçenekleri belirleyebilirsiniz.)

1. .NET Standard hedefliyorsanız, Çözüm Gezgini `AppLogger (Portable)` ' a sağ tıklayın, **Özellikler**' i seçin, **kitaplık** sekmesini seçin ve **hedefleme** bölümünde **hedef .NET platformu standardı** ' nı seçin. Bu eylem, açılan listeden `.NET Standard 1.4` (veya kullanılabilir başka bir sürüm) seçeneğini belirleyebilirsiniz. onay ister:

    ![Hedef .NET Standard 1,4 olarak ayarlanıyor](media/NetStandard-ChangeTarget.png)

1. **Derleme** sekmesine tıklayın, **yapılandırmayı** `Release` ' ye değiştirin ve **XML belge dosyası**kutusunu işaretleyin.

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

1. Yapılandırmayı serbest olarak ayarlayın, projeyi derleyin ve DLL ve XML dosyalarının `bin\Release` klasöründe üretildiğini denetleyin.

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

1. Bir komut istemi açın, `AppLogger.csproj` klasörü içeren klasöre gidin (`.sln` dosyasının bulunduğu bir düzey aşağıda) ve ilk `AppLogger.nuspec` dosyasını oluşturmak için NuGet `spec` komutunu çalıştırın:

    ```cli
    nuget spec
    ```

1. Düzenleyicide `AppLogger.nuspec` ' ı açın ve aşağıdaki değerle eşleşecek şekilde güncelleştirin, YOUR_NAME değiştirerek uygun bir değer ile değiştirin. @No__t-0 değeri, özellikle nuget.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın. Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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

1. @No__t-0 dosyasına başvuru derlemeleri ekleyin; bu şekilde kitaplığın DLL 'SI ve IntelliSense XML dosyası:

    .NET Standard hedefliyorsanız, girdiler aşağıdakine benzer şekilde görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework hedefliyorsanız, girdiler aşağıdakine benzer şekilde görünür:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Çözüme sağ tıklayın ve paketin tüm dosyalarını oluşturmak için **çözümü oluştur** ' u seçin.

### <a name="declaring-dependencies"></a>Bağımlılıkları bildirme

Diğer NuGet paketlerine yönelik bağımlılıklarınız varsa, bildirimin `<dependencies>` öğesi `<group>` öğeleriyle listeleyin. Örneğin, NewtonSoft. JSON 8.0.3 veya üzeri bir bağımlılık bildirmek için aşağıdakileri ekleyin:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Burada *Sürüm* özniteliğinin sözdizimi, 8.0.3 veya üzeri sürümünün kabul edilebilir olduğunu gösterir. Farklı sürüm aralıkları belirtmek için [paket sürümü oluşturma](../concepts/package-versioning.md)bölümüne bakın.

### <a name="adding-a-readme"></a>Benioku ekleme

@No__t-0 dosyanızı oluşturun, proje kök klasörüne yerleştirin ve `.nuspec` dosyasında bu dosyaya başvurun:

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

Paket bir projeye yüklendiğinde, Visual Studio görüntüleme `readme.txt`. Dosya .NET Core projelerine yüklendiğinde veya bağımlılık olarak yüklenen paketler için gösterilmez.

## <a name="package-the-component"></a>Bileşeni paketleme

Pakette dahil etmeniz gereken tüm dosyalara başvuran tamamlandı `.nuspec` ile `pack` komutunu çalıştırmaya hazırsınız:

```cli
nuget pack AppLogger.nuspec
```

Bu `AppLogger.YOUR_NAME.1.0.0.nupkg` oluşturur. Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek, aşağıdaki içerikleri görürsünüz (.NET Standard için gösterilmektedir):

![Appgünlükçü paketini gösteren NuGet Paket Gezgini](media/NetStandard-PackageExplorer.png)

> [!Tip]
> @No__t-0 dosyası, farklı uzantılı yalnızca bir ZIP dosyasıdır. Ayrıca, paket içeriğini inceleyebilir, sonra `.nupkg` ' ı `.zip` ' i değiştirerek, bir paketi nuget.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

@No__t-0 ' ın Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına unutmayın. Mac 'te, `.nuspec` dosyasındaki Windows yol adlarını UNIX stili yollara da dönüştürmeniz gerekir.

## <a name="related-topics"></a>İlgili konular

- [. nuspec başvurusu](../reference/nuspec.md)
- [Birden çok .NET Framework sürümünü destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [.NET Standard kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Framework .NET Core 'a taşıma](/dotnet/articles/core/porting/index)
