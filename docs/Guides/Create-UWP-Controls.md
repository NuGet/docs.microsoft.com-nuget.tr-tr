---
title: "UWP için nasıl NuGet ile denetimleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "UWP içeren NuGet paketleri oluşturmak nasıl gerekli meta veriler ve Visual Studio ve harmanlama tasarımcıları için destek dosyaları dahil olmak üzere denetler."
keywords: "NuGet UWP denetimleri, Visual Studio XAML Tasarımcısı, harmanlama Tasarımcısı, özel denetimler"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3af17121f73b878decd5f0c933696fc1b0c786d7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>NuGet paketleri olarak UWP denetimler oluşturma

Visual Studio 2017 ile NuGet paketlerini teslim UWP denetimleri eklenen özelliklerinin avantajından yararlanabilirsiniz. Bu kılavuzda kullanarak şu olanakları anlatılmaktadır [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="pre-requisites"></a>Ön koşullar

1. Visual Studio 2017
1. Nasıl yapılır anlayış [UWP paketleri oluşturma](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML denetimler için araç kutusu/varlıklar bölmesinde desteği ekleme

XAML Tasarımcısı araç Visual Studio ve harmanlama varlıklar bölmesinde görünür bir XAML denetime sahip olmasını oluşturma bir `VisualStudioToolsManifest.xml` kökündeki dosyasında `tools` paket projenizin klasör. Araç kutusu veya varlıklar bölmesinde görünmesi denetimi gerekmiyorsa, bu dosyayı gerekli değildir.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Dosya yapısı aşağıdaki gibidir:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

burada:

- *your_package_file*: denetiminizin dosya adı, gibi `ManagedPackage.winmd` ("ManagedPackage" olan bir rastgele adlı bu örnek için kullanılan ve diğer bir anlamı yoktur).
- *vs_category*: denetim Visual Studio tasarımcının araç kutusunda görünmelidir grubun etiketi. A `VSCategory` araç kutusunda görünmesi denetimi için gereklidir.
- *blend_category*: denetim karışım tasarımcının varlıklar bölmesinde görünmelidir grubun etiketi. A `BlendCategory` varlıkları görünmesi denetimi için gereklidir.
- *type_full_name_n*: ad alanı gibi dahil her denetim için tam ad `ManagedPackage.MyCustomControl`. Nokta biçimi hem yönetilen hem de yerel türleri için kullanılır.

Daha gelişmiş senaryolarda, birden çok da içerebilir `<File>` içinde öğelerin `<FileList>` zaman tek bir paket birden çok denetim derlemelerini içerir. Ayrıca birden çok olabilir `<ToolboxItems>` tek bir düğüm `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız.

Aşağıdaki örnekte, Denetim uygulanan `ManagedPackage.winmd` Visual Studio'da görünür ve "Yönetilen paketi" adlı bir grup Blend ve "MyCustomControl", o grupta görüntülenir. Tüm bu rasgele adlardır.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio'da bir örnek denetimi olarak görünür](media/UWP-control-vs-toolbox.png)

![Bir örnek denetimi olarak grubunda görünür](media/UWP-control-blend-assets.png)

> [!Note]
> Araç kutusu/varlıklar Bölmesi'nde görmek istediğiniz her denetim açıkça belirtmeniz gerekir. Belirttiğiniz bunları biçiminde olun `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Özel simge, denetimleri ekleme

Araç kutusu/varlıklar Bölmesi'nde özel bir simge görüntülemek için görüntüyü projenizi veya karşılık gelen ekleme `design.dll` proje adında "Namespace.ControlName.extension" ve "Katıştırılmış kaynağa" yapı eylemi ayarlayın. Desteklenen biçimler: `.png`, `.jpg`, `.jpeg`, `.gif`, ve `.bmp`. Önerilen görüntü boyutu 64 x 64 piksel ' dir.

Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyası içeriyor.

![Bir proje ile özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> Yerel denetimler için bir kaynak olarak simge konulmalıdır `design.dll` projesi.

## <a name="support-specific-windows-platform-versions"></a>Belirli Windows platform sürümleri desteği

UWP paketleri, uygulamanın yüklendiği bir işletim sistemi sürümü üst ve alt sınırları tanımlamak TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) sahiptir. Daha fazla TPV karşı uygulama derlendiği SDK sürümünü belirtir. Bir UWP paketi yazarken bu özellikleri oluşturduğunu unutmayın: uygulamada tanımlı platform sürümlerinin sınırları dışındaki API'lerini kullanarak neden olacak yapılandırmanın başarısız olmasına veya uygulamanın çalışma zamanında başarısız.

Örneğin, Windows 10 Anniversary Edition (10.0; TPMinV, denetimleri paketi için ayarladığınız düşünelim Yapı 14393), böylece paket yalnızca UWP tarafından tüketilen emin olmak istiyorsanız, bağlı alt eşleşen projeleri. UWP projeleri tarafından tüketilmesi paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:

    \lib\uap10.0\*
    \ref\uap10.0\*

Uygun TPMinV onay zorlamak için oluşturma bir [MSBuild hedefleri dosya](/visualstudio/msbuild/msbuild-targets) ve ("your_assembly_name" belirli derlemenizi adıyla değiştirerek) yapı klasörü altındaki paket:

    \build
      \uap10.0
        your_assembly_name.targets
    \lib
    \tools

Hedef dosyanın aşağıdaki gibi görünmelidir örneği şöyledir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Tasarım zamanı desteği ekleme

Burada Özellik denetçisi'nde denetim özelliklerini göster yapılandırmak için özel donatıcıların, vb. yerleştirin ekleyin, `design.dll` içinde dosya `lib\<platform>\Design` klasörü hedef platformu için uygun olarak. Ayrıca, emin olmak için  **[Şablonu Düzenle > bir kopyasını düzenlemek](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**  özelliği works içermelidir `Generic.xaml` ve içinde birleştirir tüm kaynak sözlükleri `<AssemblyName>\Themes` klasör. (Bu dosyayı bir denetimin çalışma zamanı davranışını etkisi yoktur.)

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml
    \tools

> [!Note]
> Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisinde altında gösterilir.

## <a name="use-strings-and-resources"></a>Kullanım dizeler ve kaynakları

Dize kaynakları katıştırma (`.resw`) denetiminizi veya kaybı UWP projesi tarafından kullanılan, pakette ayarlanan **yapı eylemi** özelliği `.resw` dosya **PRIResource**.

Bir örnek için bkz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.

## <a name="package-content-such-as-images"></a>Paket içeriğini görüntüleri gibi

Denetim veya kaybı UWP projesi tarafından kullanılan görüntüleri gibi paket içeriğini. Bu dosyaları ekleme `lib\uap10.0.14393.0` ("your_assembly_name" belirli denetiminizi yeniden de eşleşmelidir) şekilde klasörü:

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \your_assembly_name
    \contosoSampleImage.jpg
    \tools

Ayrıca Yaz bir[MSBuild hedefleri dosya](/visualstudio/msbuild/msbuild-targets) varlık Süren projenin çıkış klasörüne kopyalanır emin olmak için:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Ayrıca bkz.

- [UWP Paketleri oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
