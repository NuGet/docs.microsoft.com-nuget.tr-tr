---
title: Evrensel Windows Platformu için NuGet paketleri oluşturma
description: Evrensel Windows Platformu için bir Windows Çalışma Zamanı bileşeni kullanarak NuGet paketleri oluşturmaya yönelik uçtan uca bir yönerge.
author: JonDouglas
ms.author: jodou
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c077645508cb10e86b3ed1e1f2bf61adcd2013d9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774233"
---
# <a name="create-uwp-packages"></a>UWP paketleri oluşturma

[Evrensel Windows platformu (UWP)](https://developer.microsoft.com/windows) , Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar. Bu modelde, UWP uygulamaları tüm cihazlarda ortak olan WinRT API 'Lerini ve ayrıca uygulamanın üzerinde çalıştığı cihaz ailesine özgü API 'Leri (Win32 ve .NET dahil) çağırabilir.

Bu kılavuzda, hem yönetilen hem de yerel projelerde kullanılabilen yerel UWP bileşeni (XAML denetimi dahil) ile bir NuGet paketi oluşturacaksınız.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017 veya Visual Studio 2015. [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz olarak 2017 Community Edition 'ı yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.

1. NuGet CLı. Nuget.org/downloads adresinden en son sürümünü `nuget.exe` indirin [](https://nuget.org/downloads)ve seçtiğiniz bir konuma kaydederek (indirme işlemi `.exe` doğrudan olur). Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows Çalışma Zamanı bileşeni oluşturma

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, **Visual C++ > Windows > Universal** düğümünü genişletin, **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablonunu seçin, adı ImageEnhancer olarak değiştirin ve Tamam ' a tıklayın. İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.

    ![Yeni UWP Windows Çalışma Zamanı bileşen projesi oluşturma](media/UWP-NewProject.png)

1. Çözüm Gezgini ' de projeye sağ tıklayın, **> yeni öğe Ekle**' yi seçin, **Visual C++ > xaml** düğümüne tıklayın, **şablonlu denetim**' i seçin, adı awesomeımagecontrol. cpp olarak değiştirin ve **Ekle**' ye tıklayın:

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleniyor](media/UWP-NewXAMLControl.png)

1. Çözüm Gezgini ' de projeye sağ tıklayın ve Özellikler ' i seçin **.** Özellikler sayfasında, **C/C++ > yapılandırma özellikleri** ' ni genişletin ve **çıkış dosyaları**' na tıklayın. Sağdaki bölmede, **XML belgesi dosyaları oluştur** değerini Evet olarak değiştirin:

    ![XML belge dosyalarını oluştur Evet olarak ayarlanıyor](media/UWP-GenerateXMLDocFiles.png)

1. Şimdi *çözüme* sağ tıklayın, **Batch Build**' i seçin, Iletişim kutusundaki üç hata ayıklama kutusunu aşağıda gösterildiği gibi denetleyin. Bu, bir yapı yaparken, Windows 'un desteklediği her bir hedef sistem için tam bir yapıt kümesi üretmenizi sağlar.

    ![Batch derlemesi](media/UWP-BatchBuild.png)

1. Toplu derleme iletişim kutusunda, projeyi doğrulamak ve NuGet paketi için ihtiyaç duyduğunuz çıkış dosyalarını oluşturmak için **Oluştur** ' a tıklayın.

> [!Note]
> Bu kılavuzda, paket için hata ayıklama yapıtlarını kullanırsınız. Hata ayıklama olmayan paket için, bunun yerine toplu derleme iletişim kutusunda sürüm seçeneklerini işaretleyin ve izleyen adımlarda ortaya çıkan sürüm klasörlerine başvurun.

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

İlk dosyayı oluşturmak için `.nuspec` aşağıdaki üç adımı uygulayın. Aşağıdaki bölümlerde, diğer gerekli güncelleştirmelerde size rehberlik sağlanır.

1. Bir komut istemi açın ve içeren klasöre gidin `ImageEnhancer.vcxproj` (Bu, çözüm dosyasının bulunduğu alt klasör olacaktır).
1. `spec`Oluşturmak Için NuGet komutunu çalıştırın (dosyanın adı `ImageEnhancer.nuspec` dosyanın adından alınır `.vcxproj` ):

    ```cli
    nuget spec
    ```

1. `ImageEnhancer.nuspec`Bir düzenleyicide açın ve uygun bir değerle YOUR_NAME değiştirerek aşağıdaki ile eşleşecek şekilde güncelleştirin. `<id>`Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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
> Ortak tüketim için oluşturulmuş paketler için, `<tags>` Bu Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olmak üzere öğeye özel bir dikkat edin.

### <a name="adding-windows-metadata-to-the-package"></a>Windows meta verileri pakete ekleniyor

Windows Çalışma Zamanı bileşeni, diğer uygulamaların ve kitaplıkların bileşeni tüketmesini sağlayan, genel olarak kullanılabilir tüm türlerini açıklayan meta veriler gerektirir. Bu meta veriler, projeyi derlerken oluşturulan ve NuGet paketinize dahil etmeniz gereken bir. winmd dosyasında bulunur. IntelliSense verilerine sahip bir XML dosyası aynı anda oluşturulmuştur ve de dahil edilmelidir.

Aşağıdaki `<files>` düğümü `.nuspec` dosyasına ekleyin:

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

Bileşeninizin içinde, ImageEnhancer türünün Çekirdek mantığı, `ImageEnhancer.dll` her bir hedef çalışma zamanı (ARM, x86 ve x64) için oluşturulan çeşitli derlemelerde yer alan yerel koddur. Bunları pakete eklemek için, `<files>` ilgili. pri kaynak dosyalarıyla birlikte bu bölüme başvurun:

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

### <a name="adding-targets"></a>. Targets ekleniyor

Daha sonra, NuGet paketinizi kullanabilen C++ ve JavaScript projelerinin, gerekli derlemeyi ve winmd dosyalarını tanımlamak için bir. targets dosyası olması gerekir. (C# ve Visual Basic projeleri bunu otomatik olarak yapılır.) Aşağıdaki metni içine kopyalayarak bu dosyayı oluşturun `ImageEnhancer.targets` ve dosyayla aynı klasöre kaydedin `.nuspec` . _Note_: Bu `.targets` dosyanın paket kimliğiyle aynı adı olması gerekir (örneğin, `<Id>` `.nupspec` dosyadaki öğesi):

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

Ardından `ImageEnhancer.targets` , `.nuspec` dosyanıza başvurun:

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

### <a name="final-nuspec"></a>Final. nuspec

Son `.nuspec` dosyanız artık aşağıdaki gibi görünmelidir, burada yeniden YOUR_NAME uygun bir değerle değiştirilmelidir:

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

## <a name="package-the-component"></a>Bileşeni paketleme

`.nuspec`Pakete dahil etmeniz gereken tüm dosyalara başvuran tamamlandığında, komutunu çalıştırmaya hazırsınız demektir `pack` :

```cli
nuget pack ImageEnhancer.nuspec
```

Bu oluşturulur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` . Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![ImageEnhancer paketini gösteren NuGet Paket Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg`Dosya, yalnızca farklı bir uzantıya sahip BIR ZIP dosyasıdır. Paket içeriğini de inceleyebilir, ancak öğesini olarak değiştirebilir, `.nupkg` `.zip` ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [. nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
