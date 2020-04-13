---
title: Evrensel Windows Platformu için NuGet Paketleri Oluşturun
description: Evrensel Windows Platformu için Bir Windows Runtime Bileşeni kullanarak NuGet paketleri oluşturmanın uçtan uca bir gözden geçirme.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380758"
---
# <a name="create-uwp-packages"></a>UWP paketleri oluşturma

[Evrensel Windows Platformu (UWP),](https://developer.microsoft.com/windows) Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar. Bu modelde, UWP uygulamaları hem tüm cihazlarda ortak olan WinRT API'lerini hem de uygulamanın çalıştırıldığı aygıt ailesine özgü API'leri (Win32 ve .NET dahil) arayabilir.

Bu izlenecek yolda, hem Yönetilen hem de Yerel projelerde kullanılabilecek yerel uwp bileşenine (XAML denetimi dahil) sahip bir NuGet paketi oluşturursunuz.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017 veya Visual Studio 2015. 2017 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/)ücretsiz olarak yükleyin; Profesyonel ve Kurumsal sürümleri de kullanabilirsiniz.

1. NuGet CLI. nuget.org/downloads en son `nuget.exe` [nuget.org/downloads](https://nuget.org/downloads)sürümünü indirin, seçtiğiniz bir konuma kaydedin `.exe` (indirme doğrudan). Daha sonra bu konumu, zaten değilse PATH ortamı değişkenine ekleyin.

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows Runtime bileşeni oluşturma

1. Visual **Studio'da, Yeni > Projesi > Dosya'yı**seçin, **Visual C++ > Windows > Evrensel** düğümünü genişletin, Windows **Runtime Bileşeni (Evrensel Windows)** şablonuna tıklayın, adı ImageEnhancer olarak değiştirin ve Tamam'ı tıklatın. İstendiğinde Hedef Sürüm ve Minimum Sürüm için varsayılan değerleri kabul edin.

    ![Yeni bir UWP Windows Runtime Bileşeni projesi oluşturma](media/UWP-NewProject.png)

1. Solution Explorer'da projeyi sağ tıklatın, **Yeni Öğe> ekle'yi**seçin, **Visual C++ > XAML** düğümünü tıklatın, **Şablon denetim'i**seçin, adını AwesomeImageControl.cpp olarak değiştirin ve **Ekle'yi**tıklatın:

    ![Projeye yeni bir XAML Şablondenetim öğesi ekleme](media/UWP-NewXAMLControl.png)

1. Solution Explorer'da projeyi sağ tıklatın ve **Özellikler'i seçin.** Özellikler sayfasında, **Yapılandırma Özelliklerini C/C++ >** genişletin ve Çıktı **Dosyaları'nı**tıklatın. Sağdaki bölmede, **XML Belge Dosyaları Oluştur** değerini Evet olarak değiştirin:

    ![XML Belge Dosyalarını Evet'e Ayarlama](media/UWP-GenerateXMLDocFiles.png)

1. Şimdi *çözüme* sağ tıklayın, **Toplu Yapı'yı**seçin, iletişim kutusundaki üç Hata Ayıklama kutusunu aşağıda gösterildiği gibi kontrol edin. Bu, bir yapı yaptığınızda, Windows'un desteklediği hedef sistemlerin her biri için tam bir yapı kümesi oluşturmanızı sağlar.

    ![Toplu Yapı](media/UWP-BatchBuild.png)

1. Toplu Yapı iletişim kutusunda ve projeyi doğrulamak ve NuGet paketi için ihtiyacınız olan çıktı dosyalarını oluşturmak için **Oluştur'u** tıklatın.

> [!Note]
> Bu gözden geçirme de paket için Hata Ayıklama yapıtlarını kullanırsınız. Hata ayıklama paketi için, Toplu Yapı iletişim kutusundaki Sürüm seçeneklerini denetleyin ve ardından gelen Sürüm klasörlerine bakın.

## <a name="create-and-update-the-nuspec-file"></a>.nuspec dosyasını oluşturma ve güncelleştirme

İlk `.nuspec` dosyayı oluşturmak için aşağıdaki üç adımı yapın. Ardından gelen bölümler daha sonra diğer gerekli güncelleştirmeler boyunca size rehberlik.

1. Bir komut istemi açın ve `ImageEnhancer.vcxproj` içeren klasöre gidin (bu çözüm dosyasının olduğu yerin altında bir alt klasör olacaktır).
1. Oluşturmak `spec` `ImageEnhancer.nuspec` için NuGet komutunu çalıştırın `.vcxproj` (dosyanın adı dosyanın adından alınır):

    ```cli
    nuget spec
    ```

1. Bir `ImageEnhancer.nuspec` düzenleyicide açın ve YOUR_NAME uygun bir değerle değiştirerek aşağıdakilerle eşleşecek şekilde güncelleştirin. Değer, `<id>` özellikle, nuget.org genelinde benzersiz olmalıdır [(paket oluşturmada](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve açıklama etiketlerini de güncellemeniz gerektiğini veya paketleme adımı sırasında bir hata almanız gerektiğini unutmayın.

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
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Genel tüketim için oluşturulmuş paketler için, `<tags>` bu etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, öğeye özel olarak dikkat edin.

### <a name="adding-windows-metadata-to-the-package"></a>Pakete Windows meta verileri ekleme

Windows Runtime Bileşeni, genel kullanıma açık tüm türlerini açıklayan meta veriler gerektirir ve bu da diğer uygulamaların ve kitaplıkların bileşeni tüketmesini mümkün kılar. Bu meta veriler, projeyi derlediğinizde oluşturulan ve NuGet paketinize eklenmesi gereken bir .winmd dosyasında bulunur. IntelliSense verilerine sahip bir XML dosyası da aynı anda oluşturulur ve eklenmelidir.

`.nuspec` Dosyaya aşağıdaki `<files>` düğümü ekleyin:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>XAML içeriği ekleme

Bileşeninize bir XAML denetimi eklemek için, denetim için varsayılan şablona sahip XAML dosyasını eklemeniz gerekir (proje şablonu tarafından oluşturulan gibi). Bu da `<files>` bölümünde gider:

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

Bileşeniniz içinde, ImageEnhancer türünün temel mantığı, her hedef çalışma `ImageEnhancer.dll` zamanı (ARM, x86 ve x64) için oluşturulan çeşitli derlemelerde bulunan yerel koddadır. Bunları pakete eklemek için, ilişkili `<files>` .pri kaynak dosyalarıyla birlikte bölüme başvurun:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>.targets ekleme

Ardından, NuGet paketinizi tüketebilecek C++ ve JavaScript projeleri, gerekli derleme ve winmd dosyalarını tanımlamak için bir .targets dosyasına ihtiyaç duyar. (C# ve Visual Basic projeleri bunu otomatik olarak yapar.) Aşağıdaki metni kopyalayarak bu dosyayı oluşturun `ImageEnhancer.targets` ve dosyayla `.nuspec` aynı klasöre kaydedin. _Not_: `.targets` Bu dosyanın paket kimliğiyle aynı adla (örn. `<Id>` `.nupspec` dosyadaki öğe) olması gerekir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Ardından dosyanıza `ImageEnhancer.targets` `.nuspec` bakın:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Son .nuspec

Son `.nuspec` dosyanız şimdi aşağıdaki gibi görünmelidir ve yine YOUR_NAME uygun bir değerle değiştirilmelidir:

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
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Bileşeni paketle

Pakete `.nuspec` eklemeniz gereken tüm dosyalara başvuru nun tamamlanmasıyla, komutu `pack` çalıştırmaya hazırsınız:

```cli
nuget pack ImageEnhancer.nuspec
```

Bu oluşturur. `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açmak ve tüm düğümleri genişletmek, aşağıdaki içeriği görürsünüz:

![NuGet Paket Explorer ImageEnhancer paketini gösteriyor](media/UWP-PackageExplorer.png)

> [!Tip]
> Dosya, `.nupkg` farklı uzantılı bir ZIP dosyasıdır. Ayrıca, daha sonra, değiştirerek `.nupkg` paket `.zip`içeriğini inceleyebilirsiniz , ancak nuget.org bir paket yüklemeden önce uzantısı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiricilerin kullanımına açmak [için, paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [.nuspec Başvuru](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Çoklu .NET Framework Sürümlerini Destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [MSBuild sahne ve hedeflerini bir pakete dahil et](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
