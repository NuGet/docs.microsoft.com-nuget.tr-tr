---
title: NuGet paketi UI denetimleriyle nasıl
description: UWP ya da WPF içeren NuGet paketleri oluşturmak nasıl destek dosyaları için Visual Studio ve harmanlama tasarımcıları ve gerekli meta veriler dahil olmak üzere denetler.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: fc6ab9e45d18807a6d69bb50ad5bac94b662a638
ms.sourcegitcommit: 80c1a37d8794e9219e310a21a6a6885a65d24e53
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/23/2018
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet paketleri UI denetimleri oluşturma

Visual Studio 2017 ile NuGet paketlerini teslim UWP ve WPF denetimleri eklenen özelliklerinin avantajından yararlanabilirsiniz. Bu kılavuzda, bu özellikleri kullanarak UWP denetimleri bağlamında anlatılmaktadır [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Aksi belirtilmediği sürece aynı WPF denetimleri için geçerlidir.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017
1. Nasıl yapılır anlayış [UWP paketleri oluşturma](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Kitaplık düzenine oluştur

> [!Note]
> Bu, yalnızca UWP denetimleri için geçerlidir.

Ayar `GenerateLibraryLayout` özelliği sağlar proje derleme çıktısı nuspec tek tek dosya girişlerinde gerek kalmadan paketlenmesi hazır bir düzende oluşturulur.

Proje Özellikleri yapı sekmesine gidin ve "Kitaplığı düzeni oluştur" onay kutusunu işaretleyin. Bu proje dosyasını değiştirmek ve ayarlama `GenerateLibraryLayout` bayrağı şu anda seçili yapı yapılandırması ve platformu için true.

Alternatif olarak, düzenleme eklemek için proje dosyası `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özelliği gruba. Bu özellik yapı yapılandırması ve platformu yedeklemiş geçerli.

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

Örneğin, Windows 10 Anniversary Edition (10.0; denetimleri paketinize TPMinV ayarladınız düşünelim Yapı 14393), böylece paket yalnızca UWP tarafından tüketilen emin olmak istiyorsanız, bağlı alt eşleşen projeleri. UWP projeleri tarafından tüketilmesi paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet otomatik olarak alabilir proje TPMinV denetleyin ve Windows 10 Anniversary Edition (10.0; düşükse yükleme başarısız Yapı 14393)

WPF durumunda, .NET Framework v4.6.1 hedefleyen projeler tarafından tüketilen veya daha yüksek olması, WPF denetimleri paket istediğiniz varsayalım. Zorlamak için aşağıdaki klasör adları denetimleriyle paketi gerekir:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Tasarım zamanı desteği ekleme

Burada Özellik denetçisi'nde denetim özelliklerini göster yapılandırmak için özel donatıcıların, vb. yerleştirin ekleyin, `design.dll` içinde dosya `lib\uap10.0.14393\Design` klasörü hedef platformu için uygun olarak. Ayrıca, emin olmak için **[Şablonu Düzenle > bir kopyasını düzenlemek](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özelliği works içermelidir `Generic.xaml` ve içinde birleştirir tüm kaynak sözlükleri `<your_assembly_name>\Themes` klasörü (yeniden kullanma Gerçek derleme adınız). (Bu dosyayı bir denetimin çalışma zamanı davranışını etkisi yoktur.) Bu nedenle, klasör yapısı şu şekilde görünür:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


WPF için WPF oluşturulacağı yeri örnekle devam edersek, .NET Framework v4.6.1 hedefleyen projeler tarafından tüketilen veya daha yüksek olması paketi denetler:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisinde altında gösterilir.

## <a name="use-strings-and-resources"></a>Kullanım dizeler ve kaynakları

Dize kaynakları katıştırma (`.resw`) denetiminizi veya kaybı UWP projesi tarafından kullanılan, pakette ayarlanan **yapı eylemi** özelliği `.resw` dosya **PRIResource**.

Bir örnek için bkz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.

> [!Note]
> Bu, yalnızca UWP denetimleri için geçerlidir.

## <a name="see-also"></a>Ayrıca bkz.

- [UWP Paketleri oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
