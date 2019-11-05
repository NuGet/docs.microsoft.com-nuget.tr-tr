---
title: NuGet ile UI denetimlerini paketleme
description: Visual Studio ve Blend tasarımcıları için gerekli meta veriler ve destekleyici dosyalar dahil olmak üzere UWP veya WPF denetimleri içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610624"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet paketleri olarak UI denetimleri oluşturma

Visual Studio 2017 ' den itibaren, NuGet paketlerinde teslim ettiğiniz UWP ve WPF denetimleri için eklenen özelliklerden yararlanabilirsiniz. Bu kılavuzda, [Extensionsdkasnugetpackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)kullanılarak UWP denetimleri bağlamında bu özelliklerde adım adım gösterilmektedir. Aksi belirtilmedikçe WPF denetimleri için de geçerlidir.

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2017
1. [UWP paketleri oluşturmayı](create-uwp-packages.md) anlama

## <a name="generate-library-layout"></a>Kitaplık düzeni oluştur

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

`GenerateLibraryLayout` özelliğinin ayarlanması, proje derleme çıktısının nuspec içindeki bireysel dosya girişlerine gerek olmadan paketlenmesi için hazırlanmaya izin veren bir düzende oluşturulmasını sağlar.

Proje Özellikleri ' nden, derleme sekmesine gidin ve "kitaplık düzeni oluştur" onay kutusunu işaretleyin. Bu, proje dosyasını değiştirecek ve şu anda seçili derleme yapılandırması ve platformunuz için `GenerateLibraryLayout` bayrağını True olarak ayarlayacaktır.

Alternatif olarak, ilk koşulsuz özellik grubuna `<GenerateLibraryLayout>true</GenerateLibraryLayout>` eklemek için proje dosyasını düzenleyin. Bu, yapı yapılandırması ve platformundan bağımsız olarak özelliği uygular.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML denetimleri için araç kutusu/varlık bölmesi desteği ekle

Visual Studio 'da XAML Tasarımcısı araç kutusunda ve Blend 'in varlıklar bölmesinde bir XAML denetiminin görünmesi için, paket projenizin `tools` klasörünün kökünde bir `VisualStudioToolsManifest.xml` dosyası oluşturun. Denetimin araç kutusu veya varlıklar bölmesinde görünmesi gerekmiyorsa bu dosya gerekli değildir.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Dosyanın yapısı aşağıdaki gibidir:

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

- *your_package_file*: denetim dosyanızın adı (örneğin, `ManagedPackage.winmd` ("managedpackage"), bu örnek için kullanılan rastgele bir isimdir ve başka bir anlamı yoktur).
- *vs_category*: denetimin Visual Studio Tasarımcısı araç kutusunda görünmesi gereken grubun etiketi. Denetimin araç kutusunda görünmesi için bir `VSCategory` gereklidir.
- *blend_category*: denetimin Blend Tasarımcısı varlık bölmesinde görünmesi gereken grubun etiketi. Denetimin varlıklarda görünmesi için bir `BlendCategory` gereklidir.
- *type_full_name_n*: `ManagedPackage.MyCustomControl`gibi her bir denetimin tam adı, ad alanı da dahil. Hem yönetilen hem de yerel türler için nokta biçiminin kullanıldığını unutmayın.

Daha Gelişmiş senaryolarda, tek bir paket birden çok denetim derlemesi içerdiğinde `<FileList>` içinde birden çok `<File>` öğesi de ekleyebilirsiniz. Ayrıca, denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız tek bir `<File>` içinde birden fazla `<ToolboxItems>` düğümünüz olabilir.

Aşağıdaki örnekte `ManagedPackage.winmd` ' de uygulanan denetim, Visual Studio 'da görünür ve "yönetilen paket" adlı bir grupta Blend ve bu grupta "MyCustomControl" görüntülenir. Tüm bu adlar rastgele.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio 'da göründüğü haliyle örnek bir denetim](media/UWP-control-vs-toolbox.png)

![Blend 'de göründüğü şekliyle örnek bir denetim](media/UWP-control-blend-assets.png)

> [!Note]
> Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetimi açıkça belirtmeniz gerekir. `Namespace.ControlName`biçimde belirttiğinizden emin olun.

## <a name="add-custom-icons-to-your-controls"></a>Denetimleriniz için özel simgeler ekleme

Araç kutusu/varlıklar bölmesinde özel bir simge göstermek için projenize veya "namespace. ControlName. Extension" adlı karşılık gelen `design.dll` projesine bir görüntü ekleyin ve derleme eylemini "katıştırılmış kaynak" olarak ayarlayın. Ayrıca, ilişkili `AssemblyInfo.cs` ProvideMetadata özniteliğini `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`belirttiğinden emin olmanız gerekir. Bu [örneğe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)bakın.

Desteklenen biçimler `.png`, `.jpg`, `.jpeg`, `.gif`ve `.bmp`. Önerilen biçim 16 piksel ile 16 piksel BMP24.

![Araç kutusu simgesi örneği](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Pembe arka plan, çalışma zamanında değiştirilmiştir. Visual Studio teması değiştirildiğinde ve arka plan rengi beklendiğinde simgeler yeniden renklendirilmez. Daha fazla bilgi için lütfen [Visual Studio görüntüleri ve simgelerine](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)başvurun.

Aşağıdaki örnekte, proje "ManagedPackage. MyCustomControl. png" adlı bir görüntü dosyası içerir.

![Bir projede özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> Yerel denetimler için, simgeyi `design.dll` projesine kaynak olarak koymanız gerekir.

## <a name="support-specific-windows-platform-versions"></a>Belirli Windows platformu sürümlerini destekleme

UWP paketlerinde, uygulamanın yüklenebildiği işletim sistemi sürümünün üst ve alt sınırlarını tanımlayan bir TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) vardır. TPV daha fazla uygulamanın oluşturulduğu SDK sürümünü belirtir. UWP paketi yazarken bu özelliklerden en az birine sahip olun: uygulamada tanımlanan platform sürümlerinin sınırları dışında API 'Lerin kullanılması, derleme başarısız olur ya da uygulamanın çalışma zamanında başarısız olmasına neden olur.

Örneğin, denetimler paketiniz için TPMinV 'i Windows 10 yıldönümü sürümüne (10,0;) ayarlayadığınızı varsayalım. Derleme 14393), bu nedenle paketin yalnızca alt sınır ile eşleşen UWP projeleri tarafından tüketildiğinden emin olmak istiyorsunuz. Paketinizin UWP projeleri tarafından tüketilebilmesi için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet, tüketen projenin TPMinV otomatik olarak kontrol eder ve Windows 10 yıldönümü Edition 'dan düşükse yükleme başarısız olur (10,0; Derleme 14393)

WPF söz konusu olduğunda, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini varsayalım. Bunu zorlamak için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Tasarım zamanı desteği ekle

Denetim özelliklerinin, Özellik denetçisinde nerede olduğunu yapılandırmak için, özel Donatıcılar ekleyin, vb., `design.dll` dosyanızı hedef platforma uygun `lib\uap10.0.14393\Design` klasöre yerleştirin. Ayrıca, **[şablonu düzenle > kopyalama özelliğini Düzenle](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** ' nin çalıştığından emin olmak için, `Generic.xaml` ve `<your_assembly_name>\Themes` klasöre (gerçek derleme adınızı kullanarak) Birleşmiş tüm kaynak sözlüklerini dahil etmeniz gerekir. (Bu dosya, bir denetimin çalışma zamanı davranışını etkilemez.) Bu nedenle, klasör yapısı şu şekilde görünür:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


WPF için, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini istediğiniz örneğe devam edin:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Varsayılan olarak, denetim özellikleri, Özellik denetçisindeki çeşitli Kategoriler altında görünür.

## <a name="use-strings-and-resources"></a>Dizeleri ve kaynakları kullanma

Paketinize veya tüketen UWP projesi tarafından kullanılabilen, paketinizdeki dize kaynaklarını (`.resw`) ekleyebilir ve `.resw` dosyasının **Yapı eylemi** özelliğini **priresource**olarak ayarlayabilirsiniz.

Bir örnek için, ExtensionSDKasNuGetPackage örneğindeki [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) adresine bakın.

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

## <a name="see-also"></a>Ayrıca bkz.

- [UWP Paketleri oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
