---
title: Evrensel Windows Platformu için NuGet paketleri oluşturma
description: İçindeki C#Evrensel Windows platformu için bir Windows çalışma zamanı bileşeni kullanarak NuGet paketleri oluşturmaya yönelik uçtan uca bir yönerge.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231807"
---
# <a name="create-uwp-packages-c"></a>UWP paketleri oluşturma (C#)

[Evrensel Windows platformu (UWP)](/windows/uwp) , Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar. Bu modelde, UWP uygulamaları tüm cihazlarda ortak olan WinRT API 'Lerini ve ayrıca uygulamanın üzerinde çalıştığı cihaz ailesine özgü API 'Leri (Win32 ve .NET dahil) çağırabilir.

Bu kılavuzda, hem yönetilen hem de yerel projelerde kullanılabilen C# UWP BILEŞENI (XAML denetimi dahil) Ile bir NuGet paketi oluşturacaksınız.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2019. [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz olarak 2019 Community Edition 'ı yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.

1. NuGet CLı. En son `nuget.exe` sürümünü [NuGet.org/downloads](https://nuget.org/downloads)adresinden indirin, bunu istediğiniz konuma kaydederek (indirme işlemi doğrudan `.exe`). Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin. [Daha fazla ayrıntı](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows Çalışma Zamanı bileşeni oluşturma

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, "UWP c#" araması yapın, **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablonunu seçin, ileri ' ye tıklayın, adı ImageEnhancer olarak değiştirin ve Oluştur ' a tıklayın. İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.

    ![Yeni UWP Windows Çalışma Zamanı bileşen projesi oluşturma](media/UWP-NewProject-CS.png)

1. Çözüm Gezgini projeye sağ tıklayın, **> yeni öğe Ekle**' yi seçin, **şablonlu denetim**' i seçin, adı AwesomeImageControl.cs olarak değiştirin ve **Ekle**' ye tıklayın:

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleniyor](media/UWP-NewXAMLControl-CS.png)

1. Çözüm Gezgini ' de projeye sağ tıklayın ve Özellikler ' i seçin **.** Özellikler sayfasında, **derleme** sekmesi ' ni seçin ve **XML belge dosyasını**etkinleştirin:

    ![XML belge dosyalarını oluştur Evet olarak ayarlanıyor](media/UWP-GenerateXMLDocFiles-CS.png)

1. Şimdi *çözüme* sağ tıklayın, **Batch Build**' i seçin, iletişim kutusundaki beş derleme kutusunu aşağıda gösterildiği gibi denetleyin. Bu, bir yapı yaparken, Windows 'un desteklediği her bir hedef sistem için tam bir yapıt kümesi üretmenizi sağlar.

    ![Batch derlemesi](media/UWP-BatchBuild-CS.png)

1. Toplu derleme iletişim kutusunda, projeyi doğrulamak ve NuGet paketi için ihtiyaç duyduğunuz çıkış dosyalarını oluşturmak için **Oluştur** ' a tıklayın.

> [!Note]
> Bu kılavuzda, paket için hata ayıklama yapıtlarını kullanırsınız. Hata ayıklama olmayan paket için, bunun yerine toplu derleme iletişim kutusunda sürüm seçeneklerini işaretleyin ve izleyen adımlarda ortaya çıkan sürüm klasörlerine başvurun.

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

İlk `.nuspec` dosyasını oluşturmak için aşağıdaki üç adımı uygulayın. Aşağıdaki bölümlerde, diğer gerekli güncelleştirmelerde size rehberlik sağlanır.

1. Bir komut istemi açın ve `ImageEnhancer.csproj` içeren klasöre gidin (Bu, çözüm dosyasının bulunduğu alt klasör olacaktır).
1. `ImageEnhancer.nuspec` oluşturmak için [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) komutunu çalıştırın (dosyanın adı `.csroj` dosyanın adından alınır):

    ```cli
    nuget spec
    ```

1. `ImageEnhancer.nuspec` bir düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek, bunları bir düzenleyicide eşleşecek şekilde güncelleştirin. $PropertyName $ değerlerinden hiçbirini bırakmayın. `<id>` değeri özellikle, nuget.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Ortak tüketim için oluşturulmuş paketler için, bu Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olmak üzere `<tags>` öğesine özel bir dikkat edin.

### <a name="adding-windows-metadata-to-the-package"></a>Windows meta verileri pakete ekleniyor

Windows Çalışma Zamanı bileşeni, diğer uygulamaların ve kitaplıkların bileşeni tüketmesini sağlayan, genel olarak kullanılabilir tüm türlerini açıklayan meta veriler gerektirir. Bu meta veriler, projeyi derlerken oluşturulan ve NuGet paketinize dahil etmeniz gereken bir. winmd dosyasında bulunur. IntelliSense verilerine sahip bir XML dosyası aynı anda oluşturulmuştur ve de dahil edilmelidir.

Aşağıdaki `<files>` düğümünü `.nuspec` dosyasına ekleyin:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>XAML içeriği ekleme

Bileşeninizdeki XAML denetimini eklemek için, denetimin varsayılan şablonuna sahip XAML dosyasını (proje şablonu tarafından oluşturulan olarak) eklemeniz gerekir. Bu da `<files>` bölümüne gider:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Yerel uygulama kitaplıklarını ekleme

Bileşeninizin içinde, ImageEnhancer türünün Çekirdek mantığı, her bir hedef çalışma zamanı (ARM, ARM64, x86 ve x64) için oluşturulan çeşitli `ImageEnhancer.winmd` derlemelerindeki yerel kodda bulunur. Bunları pakete eklemek için, `<files>` bölümünde ilişkili. pri kaynak dosyalarıyla birlikte bunlara başvurun:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Final. nuspec

Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada tekrar YOUR_NAME uygun bir değerle değiştirilmelidir:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Bileşeni paketleme

Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlanmış `.nuspec` ile [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) komutunu çalıştırmaya hazırsınız:

```cli
nuget pack ImageEnhancer.nuspec
```

Bu, `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`oluşturur. Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![ImageEnhancer paketini gösteren NuGet Paket Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` dosyası, farklı uzantılı yalnızca bir ZIP dosyasıdır. Ayrıca, paket içeriğini inceleyebilir, sonra `.nupkg` `.zip`olarak değiştirebilir, ancak paketi nuget.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [. nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
