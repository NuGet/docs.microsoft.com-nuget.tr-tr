---
title: Evrensel Windows Platformu için NuGet paketleri oluşturma
description: Evrensel Windows Platformu için bir Windows Çalışma Zamanı bileşeni kullanarak NuGet paketleri oluşturmaya yönelik uçtan uca bir yönerge.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 1683349faacdf5ad47baafeef3457bbb3bb1baa9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488987"
---
# <a name="create-uwp-packages"></a>UWP paketleri oluşturma

[Evrensel Windows platformu (UWP)](https://developer.microsoft.com/windows) , Windows 10 çalıştıran her cihaz için ortak bir uygulama platformu sağlar. Bu modelde, UWP uygulamaları tüm cihazlarda ortak olan WinRT API 'Lerini ve ayrıca uygulamanın üzerinde çalıştığı cihaz ailesine özgü API 'Leri (Win32 ve .NET dahil) çağırabilir.

Bu kılavuzda, hem yönetilen hem de yerel projelerde kullanılabilen yerel UWP bileşeni (XAML denetimi dahil) ile bir NuGet paketi oluşturacaksınız.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017 veya Visual Studio 2015. [VisualStudio.com](https://www.visualstudio.com/)'ten ücretsiz olarak 2017 Community Edition 'ı yükleyin; Profesyonel ve kurumsal sürümlerini de kullanabilirsiniz.

1. NuGet CLı. `nuget.exe` [NuGet.org/downloads](https://nuget.org/downloads)adresinden en son sürümünü indirin ve seçtiğiniz bir konuma kaydederek (indirme işlemi `.exe` doğrudan olur). Daha sonra bu konumu yol ortam değişkeninizin zaten olmaması durumunda ekleyin.

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows Çalışma Zamanı bileşeni oluşturma

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, **visual C++ > Windows > Universal** düğümünü genişletin, **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablonunu seçin, adı ImageEnhancer olarak değiştirin ve Tamam ' a tıklayın. İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.

    ![Yeni UWP Windows Çalışma Zamanı bileşen projesi oluşturma](media/UWP-NewProject.png)

1. Çözüm Gezgini ' de projeye sağ tıklayın, **> yeni öğe Ekle**' yi seçin, **Visual C++ > xaml** düğümüne tıklayın, **şablonlu denetim**' i seçin, adı awesomeımagecontrol. cpp olarak değiştirin ve **Ekle**' ye tıklayın:

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleniyor](media/UWP-NewXAMLControl.png)

1. Çözüm Gezgini ' de projeye sağ tıklayın ve Özellikler ' i seçin **.** Özellikler sayfasında, **yapılandırma özellikleri > CC++ /** öğesini genişletin ve **çıkış dosyaları**' na tıklayın. Sağdaki bölmede, **XML belgesi dosyaları oluştur** değerini Evet olarak değiştirin:

    ![XML belge dosyalarını oluştur Evet olarak ayarlanıyor](media/UWP-GenerateXMLDocFiles.png)

1. Şimdi *çözüme* sağ tıklayın, **Batch Build**' i seçin, Iletişim kutusundaki üç hata ayıklama kutusunu aşağıda gösterildiği gibi denetleyin. Bu, bir yapı yaparken, Windows 'un desteklediği her bir hedef sistem için tam bir yapıt kümesi üretmenizi sağlar.

    ![Batch derlemesi](media/UWP-BatchBuild.png)

1. Toplu derleme iletişim kutusunda, projeyi doğrulamak ve NuGet paketi için ihtiyaç duyduğunuz çıkış dosyalarını oluşturmak için **Oluştur** ' a tıklayın.

> [!Note]
> Bu kılavuzda, paket için hata ayıklama yapıtlarını kullanırsınız. Hata ayıklama olmayan paket için, bunun yerine toplu derleme iletişim kutusunda sürüm seçeneklerini işaretleyin ve izleyen adımlarda ortaya çıkan sürüm klasörlerine başvurun.

## <a name="create-and-update-the-nuspec-file"></a>. Nuspec dosyasını oluşturun ve güncelleştirin

İlk `.nuspec` dosyayı oluşturmak için aşağıdaki üç adımı uygulayın. Aşağıdaki bölümlerde, diğer gerekli güncelleştirmelerde size rehberlik sağlanır.

1. Bir komut istemi açın ve içeren `ImageEnhancer.vcxproj` klasöre gidin (Bu, çözüm dosyasının bulunduğu alt klasör olacaktır).
1. `.vcxproj` Oluşturmak `spec` içinNuGetkomutunuçalıştırın(dosyanınadıdosyanın`ImageEnhancer.nuspec` adından alınır):

    ```cli
    nuget spec
    ```

1. Bir `ImageEnhancer.nuspec` düzenleyicide açın ve YOUR_NAME ile eşleşecek şekilde güncelleştirin ve uygun bir değerle değiştirin. Değer, özellikle NuGet.org genelinde benzersiz olmalıdır ( [paket oluşturma](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)bölümünde açıklanan adlandırma kurallarına bakın). `<id>` Ayrıca, yazar ve Açıklama etiketlerini de güncelleştirmeniz gerektiğini veya paketleme adımı sırasında bir hata almanızı unutmayın.

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
> Ortak tüketim için oluşturulmuş paketler için, bu Etiketler başkalarının paketinizi bulmasına `<tags>` ve ne yaptığını anlamasına yardımcı olmak üzere öğeye özel bir dikkat edin.

### <a name="adding-windows-metadata-to-the-package"></a>Windows meta verileri pakete ekleniyor

Windows Çalışma Zamanı bileşeni, diğer uygulamaların ve kitaplıkların bileşeni tüketmesini sağlayan, genel olarak kullanılabilir tüm türlerini açıklayan meta veriler gerektirir. Bu meta veriler, projeyi derlerken oluşturulan ve NuGet paketinize dahil etmeniz gereken bir. winmd dosyasında bulunur. IntelliSense verilerine sahip bir XML dosyası aynı anda oluşturulmuştur ve de dahil edilmelidir.

Aşağıdaki `<files>` düğümü`.nuspec` dosyasına ekleyin:

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

Bileşeninizin içinde, ImageEnhancer türünün Çekirdek mantığı, her bir hedef çalışma zamanı (ARM, x86 ve x64) için `ImageEnhancer.dll` oluşturulan çeşitli derlemelerde yer alan yerel koddur. Bunları pakete eklemek için, ilgili. pri kaynak dosyalarıyla birlikte `<files>` bu bölüme başvurun:

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

Daha sonra C++ , NuGet paketinizi kullanabilen JavaScript projelerinin, gerekli derlemeyi ve winmd dosyalarını tanımlamak için bir. targets dosyası olması gerekir. (C# ve Visual Basic projeler bu otomatik olarak yapılır.) Aşağıdaki metni içine `ImageEnhancer.targets` kopyalayarak bu dosyayı oluşturun ve `.nuspec` dosyayla aynı klasöre kaydedin. _Not_: Bu `.targets` dosyanın paket kimliğiyle aynı ada sahip olması gerekir (örneğin, `<Id>` `.nupspec` dosyadaki öğesi):

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

`ImageEnhancer.targets` Ardından`.nuspec` , dosyanıza başvurun:

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

Pakete dahil etmeniz `.nuspec` gereken tüm dosyalara başvuran tamamlandığında, `pack` komutunu çalıştırmaya hazırsınız demektir:

```cli
nuget pack ImageEnhancer.nuspec
```

Bu oluşturulur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Bu dosyayı [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) gibi bir araçta açıp tüm düğümleri genişleterek aşağıdaki içerikleri görürsünüz:

![ImageEnhancer paketini gösteren NuGet Paket Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` Dosya, yalnızca farklı bir uzantıya sahip bir ZIP dosyasıdır. Paket içeriğini `.nupkg` de inceleyebilir, ancak öğesini olarak `.zip`değiştirebilir, ancak paketi NuGet.org 'e yüklemeden önce uzantıyı geri yüklemeyi unutmayın.

Paketinizi diğer geliştiriciler için kullanılabilir hale getirmek için, [paket yayımlama](../nuget-org/publish-a-package.md)yönergelerini izleyin.

## <a name="related-topics"></a>İlgili konular

- [. nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Çoklu .NET Framework sürümlerini destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild props ve hedefleri dahil etme](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
