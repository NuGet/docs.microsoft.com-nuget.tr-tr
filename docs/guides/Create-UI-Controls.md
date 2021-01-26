---
title: NuGet ile UI denetimlerini paketleme
description: Visual Studio ve Blend tasarımcıları için gerekli meta veriler ve destekleyici dosyalar dahil olmak üzere UWP veya WPF denetimleri içeren NuGet paketleri oluşturma.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 317937b4d9d773d74384b8ebfcd2146062236ac1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774323"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet paketleri olarak UI denetimleri oluşturma

Visual Studio 2017 ' den itibaren, NuGet paketlerinde teslim ettiğiniz UWP ve WPF denetimleri için eklenen özelliklerden yararlanabilirsiniz. Bu kılavuzda, [Extensionsdkasnugetpackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)kullanılarak UWP denetimleri bağlamında bu özelliklerde adım adım gösterilmektedir. Aksi belirtilmedikçe WPF denetimleri için de geçerlidir.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017
1. [UWP paketleri oluşturmayı](create-uwp-packages.md) anlama

## <a name="generate-library-layout"></a>Kitaplık düzeni oluştur

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

Özelliği ayarlamak, `GenerateLibraryLayout` proje yapı çıkışının nuspec içindeki bireysel dosya girişlerine gerek olmadan paketlenebilecek şekilde hazırlanmaya izin veren bir düzende oluşturulmasını sağlar.

Proje Özellikleri ' nden, derleme sekmesine gidin ve "kitaplık düzeni oluştur" onay kutusunu işaretleyin. Bu işlem, proje dosyasını değiştirecek ve `GenerateLibraryLayout` geçerli olarak seçili derleme yapılandırması ve platformunuz için bayrağı true olarak ayarlar.

Alternatif olarak, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özellik grubuna eklemek için proje dosyasını düzenleyin. Bu, yapı yapılandırması ve platformundan bağımsız olarak özelliği uygular.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML denetimleri için araç kutusu/varlık bölmesi desteği ekle

Xaml tasarımcısının Visual Studio 'daki araç kutusunda ve Blend 'nin varlıklar bölmesinde görünmesi için, `VisualStudioToolsManifest.xml` paket projenizin klasörünün kökünde bir dosya oluşturun `tools` . Denetimin araç kutusu veya varlıklar bölmesinde görünmesi gerekmiyorsa bu dosya gerekli değildir.

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

Dosyanın yapısı aşağıdaki gibidir:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

burada:

- *your_package_file*: `ManagedPackage.winmd` ("managedpackage" gibi) denetim dosyanızın adı bu örnek için kullanılan rastgele bir adlandırılmış addır ve başka bir anlamı yoktur).
- *vs_category*: denetimin Visual Studio Tasarımcısı araç kutusunda görünmesi gereken grubun etiketi. `VSCategory`Denetim, denetimin araç kutusunda görünmesi için gereklidir.
*ui_framework*: çerçeve adı (örneğin, ' WPF '), `UIFramework` denetimin araç kutusunda görünmesi için Visual Studio 16,7 Preview 3 veya üzeri sürümlerde ToolBoxItems düğümlerinde bu özniteliğin gerekli olduğunu unutmayın.
- *blend_category*: denetimin Blend Tasarımcısı varlık bölmesinde görünmesi gereken grubun etiketi. , `BlendCategory` Denetimin varlıklarda görünmesi için gereklidir.
- *type_full_name_n*: ad alanı da dahil olmak üzere her denetim için tam olarak nitelenmiş addır `ManagedPackage.MyCustomControl` . Hem yönetilen hem de yerel türler için nokta biçiminin kullanıldığını unutmayın.

Daha Gelişmiş senaryolarda, `<File>` `<FileList>` tek bir paket birden çok denetim derlemesi içerdiğinde içinde birden çok öğe de ekleyebilirsiniz. Ayrıca, `<ToolboxItems>` `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız tek bir içinde birden fazla düğüme sahip olabilirsiniz.

Aşağıdaki örnekte, içinde uygulanan denetim `ManagedPackage.winmd` Visual Studio 'da görünür ve "yönetilen paket" adlı bir grupta Blend ve bu grupta "MyCustomControl" görüntülenir. Tüm bu adlar rastgele.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio 'da göründüğü haliyle örnek bir denetim](media/UWP-control-vs-toolbox.png)

![Blend 'de göründüğü şekliyle örnek bir denetim](media/UWP-control-blend-assets.png)

> [!Note]
> Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetimi açıkça belirtmeniz gerekir. Bunları biçimde belirttiğinizden emin olun `Namespace.ControlName` .

## <a name="add-custom-icons-to-your-controls"></a>Denetimleriniz için özel simgeler ekleme

Araç kutusu/varlıklar bölmesinde özel bir simge göstermek için projenize veya `design.dll` "namespace. ControlName. Extension" adlı ilgili projeye bir resim ekleyin ve derleme eylemini "katıştırılmış kaynak" olarak ayarlayın. Ayrıca, ilişkili öğesinin `AssemblyInfo.cs` ProvideMetadata özniteliğini belirttiğinden emin olmanız gerekir `[assembly: ProvideMetadata(typeof(RegisterMetadata))]` . Bu [örneğe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)bakın.

Desteklenen biçimler şunlardır,,, `.png` `.jpg` `.jpeg` `.gif` ve `.bmp` . Önerilen biçim 16 piksel ile 16 piksel BMP24.

![Araç kutusu simgesi örneği](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Pembe arka plan, çalışma zamanında değiştirilmiştir. Visual Studio teması değiştirildiğinde ve arka plan rengi beklendiğinde simgeler yeniden renklendirilmez. Daha fazla bilgi için lütfen [Visual Studio görüntüleri ve simgelerine](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)başvurun.

Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyası içerir.

![Bir projede özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> Yerel denetimler için, simgeyi projeye bir kaynak olarak koymanız gerekir `design.dll` .

## <a name="support-specific-windows-platform-versions"></a>Belirli Windows platformu sürümlerini destekleme

UWP paketlerinde, uygulamanın yüklenebildiği işletim sistemi sürümünün üst ve alt sınırlarını tanımlayan bir TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) vardır. TPV daha fazla uygulamanın oluşturulduğu SDK sürümünü belirtir. UWP paketi yazarken bu özelliklerden en az birine sahip olun: uygulamada tanımlanan platform sürümlerinin sınırları dışında API 'Lerin kullanılması, derleme başarısız olur ya da uygulamanın çalışma zamanında başarısız olmasına neden olur.

Örneğin, denetimler paketiniz için TPMinV 'i Windows 10 yıldönümü sürümüne (10,0;) ayarlayadığınızı varsayalım. Derleme 14393), bu nedenle paketin yalnızca alt sınır ile eşleşen UWP projeleri tarafından tüketildiğinden emin olmak istiyorsunuz. Paketinizin UWP projeleri tarafından tüketilebilmesi için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

NuGet, tüketen projenin TPMinV otomatik olarak kontrol eder ve Windows 10 yıldönümü Edition 'dan düşükse yükleme başarısız olur (10,0; Derleme 14393)

WPF söz konusu olduğunda, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini varsayalım. Bunu zorlamak için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a>Tasarım zamanı desteği ekle

Denetim özelliklerinin, Özellik denetçisinde nerede olduğunu yapılandırmak için özel Donatıcılar ekleyin, vb., `design.dll` `lib\uap10.0.14393\Design` hedef platforma uygun şekilde dosyanızı klasöre yerleştirin. Ayrıca, **[şablonu düzenle > kopyalama özelliğini Düzenle](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** ' nin çalıştığından emin olmak için, `Generic.xaml` `<your_assembly_name>\Themes` klasöre (gerçek derleme adınızı kullanarak) Birleşmiş olan ve tüm kaynak sözlüklerini dahil etmeniz gerekir. (Bu dosya, bir denetimin çalışma zamanı davranışını etkilemez.) Bu nedenle, klasör yapısı şu şekilde görünür:

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

WPF için, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini istediğiniz örneğe devam edin:

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> Varsayılan olarak, denetim özellikleri, Özellik denetçisindeki çeşitli Kategoriler altında görünür.

## <a name="use-strings-and-resources"></a>Dizeleri ve kaynakları kullanma

`.resw`Paketinize veya tüketen UWP projesi tarafından kullanılabilecek dize kaynaklarını (),, dosyanın **derleme eylemi** özelliğini `.resw` **priresource** olarak ayarlayabilirsiniz.

Bir örnek için, ExtensionSDKasNuGetPackage örneğindeki [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) adresine bakın.

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

## <a name="see-also"></a>Ayrıca bkz.

- [UWP paketleri oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)