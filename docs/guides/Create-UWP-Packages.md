---
title: Evrensel Windows platformu için NuGet paketleri oluşturma
description: Evrensel Windows platformu için bir Windows çalışma zamanı bileşeni kullanarak NuGet paketleri oluşturmanın bir uçtan uca kılavuz.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 16e19be0356bc1d2734ade5cd593ca3ef05bbe5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546427"
---
# <a name="create-uwp-packages"></a>UWP paketleri oluşturma

[Evrensel Windows Platformu (UWP)](https://developer.microsoft.com/windows) ortak bir uygulama platformu, Windows 10 çalıştıran her cihazda sağlar. Bu model içinde UWP uygulamaları tüm cihazlar için ortak bir WinRT API'leri hem de (Win32 ve .NET dahil) ve uygulamanın üzerinde çalıştığı cihaz ailesine özgü API'leri çağırabilirsiniz.

Bu izlenecek yolda, hem yönetilen hem de yerel projeleri için kullanılabilir (bir XAML denetimi dahil) yerel UWP bileşeni ile bir NuGet paketi oluşturun.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017 veya Visual Studio 2015. 2017 Community edition ücretsiz yamasını [visualstudio.com](https://www.visualstudio.com/); Professional ve Enterprise sürümleri de kullanabilirsiniz.

1. NuGet CLI. En son sürümünü indirin `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads), seçtiğiniz bir konuma kaydetme (indirme `.exe` doğrudan). Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

## <a name="create-a-uwp-windows-runtime-component"></a>Bir UWP Windows çalışma zamanı bileşeni oluşturma

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C++ > Windows > Evrensel** düğümünü **Windows çalışma zamanı bileşeni (Evrensel Windows)** şablon ImageEnhancer için adı değiştirin ve Tamam'a tıklayın. Hedef sürümü ve en düşük istendiğinde sürümü için varsayılan değerleri kabul.

    ![Yeni bir UWP Windows çalışma zamanı bileşeni projesi oluşturma](media/UWP-NewProject.png)

1. Seçin Çözüm Gezgini'nde projeye sağ tıklayın **Ekle > Yeni öğe**, tıklayın **Visual C++ > XAML** düğümünü **şablonlu denetim**, adla değiştirin AwesomeImageControl.cpp seçeneğine tıklayıp **Ekle**:

    ![Projeye yeni bir XAML şablonlu denetim öğe ekleme](media/UWP-NewXAMLControl.png)

1. Çözüm Gezgini'nde projeye sağ tıklayıp **özellikleri.** Özellikler sayfasında genişletin **yapılandırma özellikleri > C/C++** tıklatıp **Çıkış dosyalarını**. Sağ taraftaki bölmede değerini değiştirin **XML belge dosyaları oluştur** Evet:

    ![Ayarı Evet olarak XML belge dosyaları oluştur](media/UWP-GenerateXMLDocFiles.png)

1. Sağ tıklayın *çözüm* şimdi seçin **Toplu derleme**, aşağıda gösterildiği gibi iletişim kutusundaki üç hata ayıklama kutuları işaretleyin. Bu, bir derleme yaptığınızda, yapıtlar tam bir dizi her Windows destekleyen hedef sistemleri için oluşturduğunuz emin emin olur.

    ![Toplu derleme](media/UWP-BatchBuild.png)

1. Toplu derleme iletişim ve tıklayın **derleme** proje doğrulamak ve NuGet paketi için gereksinim duyduğunuz çıktı dosyaları oluşturmak için.

> [!Note]
> Bu izlenecek yolda paket için hata ayıklama yapıları kullanın. Hata ayıklama olmayan paketi için Toplu derleme iletişim kutusunda yayın seçenekleri yerine denetleyin ve sonuçta elde edilen sürüm klasörler, aşağıdaki adımları başvurun.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturma ve güncelleştirme .nuspec dosyası

İlk oluşturmak için `.nuspec` dosya, aşağıdaki üç adımı yapın. Ardından aşağıdaki bölümlerde, diğer gerekli güncelleştirmeleri size rehberlik eder.

1. Bir komut istemi açın ve klasör içeren dizine gidin `ImageEnhancer.vcxproj` (Bu çözüm dosyasının bulunduğu bir alt aşağıdaki olacaktır).
1. NuGet komutunu çalıştırarak `spec` oluşturmak için komutu `ImageEnhancer.nuspec` (adından dosyasının adı alınmış `.vcxproj` dosyası):

    ```cli
    nuget spec
    ```

1. Açık `ImageEnhancer.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirmeniz YOUR_NAME uygun bir değerle değiştirin. `<id>` Değeri, özellikle benzersiz olmalıdır nuget.org arasında (açıklanan adlandırma kuralları bakın [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Ayrıca, yazar ve açıklama etiketleri de güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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
> Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi olarak, bu etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.

### <a name="adding-windows-metadata-to-the-package"></a>Windows meta veri paketi ekleme

Bir Windows çalışma zamanı bileşeni tüm diğer uygulamaları ve kitaplıkları bileşeni kullanma için mümkün kılar, genel kullanıma açık türleri açıklayan meta verileri gerektirir. Bu meta veriler, projeyi derleyin ve NuGet paketle birlikte oluşturulduğu bir .winmd dosyası içinde yer alır. IntelliSense verilerini içeren bir XML dosyası da aynı anda yerleşik olarak bulunur ve de eklenmelidir.

Aşağıdaki `<files>` düğüme `.nuspec` dosyası:

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

### <a name="adding-xaml-content"></a>XAML İçerik ekleme

Bir XAML bileşeniniz Generic.XAML'yi eklemeniz (proje şablonu tarafından oluşturulan gibi) bir denetim için varsayılan şablonu olan bir XAML dosyası eklemeniz gerekir. Bu ayrıca gider `<files>` bölümü:

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

### <a name="adding-the-native-implementation-libraries"></a>Yerel uygulama kitaplıkları ekleme

Bileşeniniz çeşitli yer alan yerel kod ImageEnhancer türü çekirdek mantığını bulunduğu `ImageEnhancer.dll` her hedef çalışma zamanı (x 86 ve x64, ARM) için oluşturulan derlemeler. Bu paketi eklemek için bunları başvuru `<files>` ilişkili .pri kaynak dosyalarla birlikte bölümü:

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

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>.Targets ekleme

Ardından, NuGet paketinizi tüketebilir C++ ve JavaScript projeleri, gerekli bütünleştirilmiş kod ve winmd dosyaları belirlemek için bir .targets dosyasında gerekir. (C# ve Visual Basic projeleri otomatik olarak bunu.) Aşağıdaki metni içine kopyalayarak bu dosyayı oluşturmak `ImageEnhancer.targets` ve aynı klasöre kaydedin `.nuspec` dosya. _Not_: Bu `.targets` dosya paket kimliği adıyla aynı olması gerekir (örneğin `<Id>` öğesinde `.nupspec` dosyası):

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

Daha sonra başvurmak `ImageEnhancer.targets` içinde `.nuspec` dosyası:

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

Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden YOUR_NAME uygun bir değer ile değiştirilmelidir:

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
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Paket bileşeni

Tamamlanan ile `.nuspec` paket içerisine dâhil için ihtiyacınız olan tüm dosyaları başvuran, çalıştırmaya hazır olduğunuz `pack` komutu:

```cli
nuget pack ImageEnhancer.nuspec
```

Bu oluşturur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Gibi bir aracı bu dosyayı açmayı [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:

![NuGet paket Gezgini ImageEnhancer paket gösteriliyor](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` bir ZIP dosyası yalnızca farklı uzantılı bir dosyadır. Ayrıca paket içeriğini, ardından değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri unutmayın.

Paketiniz diğer geliştiriciler için kullanılabilir yapmak için yönergeleri takip edin [paket yayımlama](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>İlgili konular

- [.nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok .NET Framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellikler ve hedefler](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
