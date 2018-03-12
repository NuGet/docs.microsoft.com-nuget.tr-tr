---
title: "Evrensel Windows platformu için NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Windows çalışma zamanı bileşeni için evrensel Windows platformu kullanarak NuGet paketleri oluşturma bir uçtan uca kılavuz."
keywords: "paketler UWP, Windows çalışma zamanı bileşenleri için bir paket oluşturun"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: af650b6cd67855a67d0f49cdbd9f510bf90a60f6
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="create-uwp-packages"></a>UWP paketleri oluşturma

[Evrensel Windows Platformu (UWP)](https://developer.microsoft.com/windows) Windows 10 çalıştıran her aygıt için ortak bir uygulama platformu sağlar. Bu model tüm aygıtlar için ortak olan WinRT API'leri hem de uygulama çalışırken cihaz ailesi belirli (Win32 ve .NET dahil) API'leri UWP uygulamaları çağırabilirsiniz.

Bu kılavuzda hem yönetilen hem de yerel projeleri kullanılabilecek (XAML denetim dahil) bir yerel UWP bileşeni ile bir NuGet paketi oluşturun.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017 veya Visual Studio 2015. 2017 Community edition ücretsiz yükleyin [visualstudio.com](https://www.visualstudio.com/); Professional ve Enterprise sürümleri de kullanabilirsiniz.

1. NuGet CLI. En son sürümünü indirme `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads), tercih ettiğiniz bir konuma kaydetme (karşıdan yüklemenin `.exe` doğrudan). Zaten yoksa bu konum, PATH ortam değişkenine ekleyin.

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows çalışma zamanı bileşeni oluşturma

1. Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C++ > Windows > Evrensel** düğümü, select **Windows çalışma zamanı bileşeni (Evrensel Windows)**şablonu adı için ImageEnhancer değiştirin ve Tamam'ı tıklatın. Hedef sürüm ve Minimum istendiğinde sürüm için varsayılan değerleri kabul.

    ![Yeni bir UWP Windows çalışma zamanı bileşeni projesi oluşturma](media/UWP-NewProject.png)

1. Seçin Çözüm Gezgini'nde projeye sağ tıklayın **Ekle > Yeni öğe**, tıklatın **Visual C++ > XAML** düğümü, select **şablonlu denetim**, adla değiştirin AwesomeImageControl.cpp ve tıklatın **Ekle**:

    ![Projeye yeni bir XAML şablonlu denetim öğesi ekleme](media/UWP-NewXAMLControl.png)

1. Çözüm Gezgini'nde projeye sağ tıklayıp **özellikleri.** Özellikler sayfasında genişletin **yapılandırma özellikleri > C/C++** tıklatıp **çıktı dosyaları**. Sağ bölmede, değerini değiştirin **XML belge dosyalarını oluşturmak** Evet:

    ![Ayar Evet olarak XML belge dosyalarını oluştur](media/UWP-GenerateXMLDocFiles.png)

1. Sağ tıklayın *çözüm* şimdi seçin **Toplu derleme**, aşağıda gösterildiği gibi iletişim kutusundaki üç hata ayıklama kutuları işaretleyin. Bu derleme yaptığınızda, yapıları tam bir dizi Windows destekler hedef sistemlerinin her biri için oluşturacağı emin olur.

    ![Toplu iş derleme](media/UWP-BatchBuild.png)

1. Toplu derleme iletişim ve tıklayın **yapı** proje doğrulayın ve NuGet paketi için gereksinim duyduğunuz çıktı dosyaları oluşturmak için.

> [!Note]
> Bu kılavuzda paket için hata ayıklama yapıları kullanın. Hata ayıklama olmayan paketi için Toplu derleme iletişim yayın seçeneklerinde bunun yerine denetleyin ve adımları ortaya çıkan sürüm klasörlerde bakın.

## <a name="create-and-update-the-nuspec-file"></a>Oluşturun ve .nuspec dosyası güncelleştirin

İlk oluşturmak için `.nuspec` dosya, aşağıdaki üç adımda yapın. Ardından bölümlerde diğer gerekli güncelleştirmeleri aracılığıyla yol.

1. Bir komut istemi açın ve içeren klasöre gidin `ImageEnhancer.vcxproj` (Bu çözüm dosyasını olduğu alt aşağıdaki olacaktır).
1. NuGet Çalıştır `spec` oluşturmak için komutu `ImageEnhancer.nuspec` (dosya adı adından alınır `.vcxproj` dosyası):

    ```cli
    nuget spec
    ```

1. Açık `ImageEnhancer.nuspec` bir düzenleyicide ve aşağıdaki ile eşleşecek şekilde güncelleştirebilirsiniz adiniz uygun bir değerle değiştirin. `<id>` Değeri, özellikle, benzersiz olmalıdır nuget.org (açıklanan adlandırma kuralları Bkz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Ayrıca yazar ve açıklama etiketleri güncelleştirmeniz gerekir veya paket adımı sırasında bir hata alıyorsunuz unutmayın.

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
> Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi, bu etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olmak gibi.

### <a name="adding-windows-metadata-to-the-package"></a>Paketi Windows meta verileri ekleme

Windows çalışma zamanı bileşeni tüm diğer uygulamaları ve bileşen tüketmeye kitaplıkları için mümkün hale getirir, genel kullanıma açık türlerini açıklayan meta veriler gerektirir. Projeyi derlemek ve, NuGet paketine dahil oluşturmuş .winmd dosyasında bu meta veriler içeriyor. IntelliSense verilerini içeren bir XML dosyası da aynı anda yerleşik olarak bulunur ve de eklenmelidir.

Aşağıdakileri ekleyin `<files>` düğüme `.nuspec` dosyası:

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

Bileşeniniz XAML denetimiyle eklemek için denetim (proje şablonu tarafından oluşturulan gibi) için varsayılan şablon XAML dosyaları eklemeniz gerekir. Bu ayrıca gider `<files>` bölümü:

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

Çeşitli bulunan yerel kodda ImageEnhancer türü çekirdek mantığını bileşeniniz içinde olduğu `ImageEnhancer.dll` her hedef çalışma zamanı (x 86 ve x64, ARM) için oluşturulan derlemeler. Bu pakete dahil etmek için bunları başvuru `<files>` bölüm ilişkili .pri kaynak dosyalarına yanı sıra:

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

Ardından, NuGet paketi tüketebilir C++ ve JavaScript projeleri gerekli derleme ve winmd dosyaları belirlemek üzere bir .targets dosyasında gerekir. (C# ve Visual Basic projeleri otomatik olarak bunu.) Aşağıda metne kopyalayarak bu dosyayı oluşturmak `ImageEnhancer.targets` ve aynı klasöre kaydedin `.nuspec` dosya. _Not_: Bu `.targets` dosya paket Kimliğini adıyla aynı olması gerekir (örneğin `<Id>` öğesinde `.nupspec` dosyası):

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

Ardından `ImageEnhancer.targets` içinde `.nuspec` dosyası:

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

Son `.nuspec` dosya artık görünmelidir aşağıdaki gibi burada yeniden adiniz uygun bir değerle değiştirilmelidir:

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

Tamamlanan ile `.nuspec` pakete eklemek için gereken tüm dosyaları başvuran, çalıştırmak hazırsınız `pack` komutu:

```cli
nuget pack ImageEnhancer.nuspec
```

Bu oluşturur `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriğe bakın:

![NuGet paket ImageEnhancer paket gösteren Gezgini](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır. Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.

Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>İlgili konular

- [.nuspec başvurusu](../reference/nuspec.md)
- [Sembol paketleri](../create-packages/symbol-packages.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok .NET Framework sürümleri destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Bir pakete MSBuild özellik ve hedefler](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Yerelleştirilmiş Paketler Oluşturma](../create-packages/creating-localized-packages.md)
