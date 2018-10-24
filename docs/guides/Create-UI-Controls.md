---
title: NuGet ile paket kullanıcı Arabirimi denetimleri hakkında
description: UWP ya da WPF içeren NuGet paketleri oluşturmak nasıl destek dosyaları Visual Studio'da ve Blend'de tasarımcılarına ve gerekli meta veriler dahil olmak üzere denetler.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dd36987e020c2daa02bb875aa9dbd69c85bba4d3
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951752"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet paketleri olarak kullanıcı Arabirimi denetimleri oluşturma

Visual Studio 2017 ile NuGet paketlerinde teslim UWP ve WPF denetimleri için eklenen özelliklerin yararlanabilirsiniz. Bu kılavuzu kullanarak UWP denetimleri bağlamında bu özellikler size [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Aksi belirtilmediği sürece aynı WPF denetimleri için geçerlidir.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017
1. Olma [UWP paketleri oluşturma](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Kitaplık düzeni oluştur

> [!Note]
> Bu, yalnızca UWP denetimleri için geçerlidir.

Ayarı `GenerateLibraryLayout` özelliği sağlar projesi yapı çıkış nuspec tek tek dosya girişleri gerek kalmadan paketlenmesi hazır bir düzende oluşturulur.

Proje Özellikleri derleme sekmesine gidin ve "Kitaplık düzeni oluştur" onay kutusunu işaretleyin. Bu proje dosyasını değiştirmek ve ayarlama `GenerateLibraryLayout` bayrağı şu anda seçilen derleme yapılandırması ve platformu için true.

Alternatif olarak, Düzen eklemek için proje dosyasını `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özellik grubuna. Bu özellik derleme yapılandırması ve platform fark etmeksizin geçerli.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML denetimleri için araç kutusu/varlıklar bölmesinde desteği ekleme

Visual Studio ve varlıklar bölmesinde Blend, XAML Tasarımcısı araç çubuğunda görünen bir XAML denetimi sağlamak için oluşturun bir `VisualStudioToolsManifest.xml` köküne dosya `tools` paket projenizin klasör. Araç kutusu veya varlıklar bölmesinde görüntülenmesinin denetimini gerekmiyorsa, bu dosya gerekli değildir.

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

- *your_package_file*: gibi bir denetimin adını dosya `ManagedPackage.winmd` ("ManagedPackage" olan bir rastgele adlı bu örnek için kullanılan ve diğer bir anlamı yoktur).
- *vs_category*: denetimin Visual Studio Tasarımcısı araç kutusunda görünmelidir grubun etiketi. A `VSCategory` denetimi araç kutusunda görünmesi için gereklidir.
- *blend_category*: denetimin Blend tasarımcının varlıklar bölmesinde görünmelidir grubun etiketi. A `BlendCategory` varlıkları görüntülenmesini denetim için gereklidir.
- *type_full_name_n*: tam adı ad alanı, aşağıdaki gibi her denetim için `ManagedPackage.MyCustomControl`. Nokta biçimi hem yönetilen hem de yerel türleri için kullanıldığını unutmayın.

Daha gelişmiş senaryolarda, birden çok de içerebilir `<File>` öğeleri içinde `<FileList>` tek bir paket birden çok denetim derleme içerdiğinde. Birden çok bulundurabilirsiniz `<ToolboxItems>` tek bir düğüm `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız.

Aşağıdaki örnekte, denetime uygulanan `ManagedPackage.winmd` Visual Studio'da görünür ve "Yönetilen paket" adlı bir grupta Blend ve "MyCustomControl", o grupta görünür. Bu adların hepsinin rastgele.

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

![Blend'de bir örnek denetimi olarak görünür](media/UWP-control-blend-assets.png)

> [!Note]
> Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetim açıkça belirtmeniz gerekir. Belirttiğiniz bunları biçiminde olun `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Özel simgeleri denetimlerinizi ekleyin

Araç kutusu/varlıklar Bölmesi'nde özel bir simge görüntülemek için bir görüntü projenizi veya ilgili ekleme `design.dll` proje adıyla "Namespace.ControlName.extension" ve "Gömülü kaynak" derleme eylemi ayarlayın. Ayrıca ilişkili emin olmanız gerekir `AssemblyInfo.cs` ProvideMetadata özniteliği - belirtir `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Bkz. Bu [örnek](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Desteklenen biçimler `.png`, `.jpg`, `.jpeg`, `.gif`, ve `.bmp`. Önerilen görüntü boyutu 64 x 64 piksel ' dir.

Aşağıdaki örnekte, "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyasının proje içerir.

![Bir projeye özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> Yerel denetimler için bir kaynak olarak simgesi yerleştirmelidir `design.dll` proje.

## <a name="support-specific-windows-platform-versions"></a>Belirli Windows platform sürümleri desteği

UWP paketleri, uygulamanın yüklendiği bir işletim sistemi sürümünün alt ve üst sınırlarını tanımlayın TargetPlatformVersion (TPV) ve targetplatformminversion'ından (TPMinV) sahip. Daha fazla TPV karşı yerleşik uygulama SDK'sı sürümünü belirtir. Bir UWP paket yazarken bu özellikleri dikkatli olmanızı: uygulamada tanımlanan platform sürümleri sınırları dışında API'lerini kullanarak neden olacak başarısız için yapı ya da uygulama çalışma zamanında başarısız.

Örneğin, Windows 10 Anniversary Edition (10.0; denetimleri paketinize için TPMinV ayarladığınızdan varsayalım Derleme 14393), paket yalnızca UWP tarafından tüketilmesi sağlamak istediğiniz şekilde karşılayan bağlı alt projeleri. UWP projeleri tarafından kullanılacak paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet otomatik olarak kullanan projenin TPMinV denetleyin ve Windows 10 Anniversary Edition (10.0; düşükse, yükleme başarısız Derleme 14393)

WPF olması durumunda, WPF denetimleri paketinizi v4.6.1 .NET Framework'ü hedefleyen projeleri tarafından tüketilen veya daha yüksek olmasını istediğiniz varsayalım. Zorlamak için aşağıdaki klasör adları, denetimleriyle paketi gerekir:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Tasarım zamanı desteği eklendi

Burada özelliği denetçi'deki denetim özelliklerini göster yapılandırmak için özel donatıcıları, vs. yerleştirin ekleyin, `design.dll` içinde dosya `lib\uap10.0.14393\Design` klasörü olarak hedef platform için uygun. Ayrıca, emin olmak için **[Şablonu Düzenle > Kopya Düzenle](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özellik works içermelidir `Generic.xaml` ve içinde birleştirir herhangi bir kaynak sözlükleri `<your_assembly_name>\Themes` klasörü (yeniden kullanma Gerçek derleme adı). (Bu dosya, bir denetimin çalışma zamanı davranışı üzerinde herhangi bir etkisi yoktur.) Bu nedenle, klasör yapısı aşağıdaki gibi görünür:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Paket, .NET Framework v4.6.1 hedefleyen projeleri tarafından tüketilen veya daha yüksek olmasını denetimleri, WPF istediğiniz örneğiyle devam WPF için:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisi altında görünür.

## <a name="use-strings-and-resources"></a>Kullanım dizeleri ve kaynakları

Dize kaynakları ekleyebilir (`.resw`) denetiminiz veya alıcı UWP projesi tarafından kullanılan, pakette ayarlanan **derleme eylemi** özelliği `.resw` dosyasını **PRIResource**.

Örneğin, başvurmak [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.

> [!Note]
> Bu, yalnızca UWP denetimleri için geçerlidir.

## <a name="see-also"></a>Ayrıca bkz.

- [UWP Paketleri oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
