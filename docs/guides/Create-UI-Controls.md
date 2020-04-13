---
title: NuGet ile UI denetimleri nasıl paketilir?
description: Visual Studio ve Blend tasarımcıları için gerekli meta veriler ve destekleyici dosyalar da dahil olmak üzere UWP veya WPF denetimleri içeren NuGet paketleri nasıl oluşturulur?
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610624"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet paketleri olarak UI denetimleri oluşturma

Visual Studio 2017'den itibaren NuGet paketlerinde sağladığınız UWP ve WPF denetimleri için ek özelliklerden yararlanabilirsiniz. Bu [kılavuz, ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)kullanarak UWP kontrolleri bağlamında bu yetenekleri size yol. Aynı durum, aksi belirtilmedikçe WPF denetimleri için de geçerlidir.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017
1. [UWP Paketlerinin](create-uwp-packages.md) Nasıl Oluşturulabildiğini Anlama

## <a name="generate-library-layout"></a>Kitaplık Düzeni Oluşturma

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

Özelliğin `GenerateLibraryLayout` ayarlanması, proje oluşturma çıktısının nuspec'te tek tek dosya girişlerine gerek kalmadan paketlenmeye hazır bir düzende oluşturulmasını sağlar.

Proje özelliklerinden yapı sekmesine gidin ve "Kitaplık Düzeni Oluştur" onay kutusunu işaretleyin. Bu, proje dosyasını değiştirir `GenerateLibraryLayout` ve bayrağı şu anda seçili yapı yapılandırmanız ve platformunuz için doğru olarak ayarlar.

Alternatif olarak, ilk koşulsuz özellik `<GenerateLibraryLayout>true</GenerateLibraryLayout>` grubuna eklemek için proje dosyasını edin. Bu, yapı yapılandırması ve platformune bakılmaksızın özelliği uygular.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML denetimleri için araç kutusu/varlık bölmedesteği ekleme

Visual Studio'daki XAML tasarımcısının araç kutusunda ve Karışım'ın Varlıklar bölmesinde bir XAML denetiminin `tools` görünmesi için, paket projenizin klasörünün kökünde bir `VisualStudioToolsManifest.xml` dosya oluşturun. Araç kutusunda veya Varlıklar bölmesinde görünmesi için denetime ihtiyacınız yoksa, bu dosya gerekli değildir.

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

- *your_package_file*: ("Yönetilen Paket" `ManagedPackage.winmd` bu örnek için kullanılan rasgele bir adlandırılmış ve başka bir anlamı yoktur) gibi kontrol dosyanızın adı.
- *vs_category*: Visual Studio tasarımcısının araç kutusunda kontrolün görünmesi gereken grubun etiketi. Denetimin araç kutusunda görünmesi için A `VSCategory` gereklidir.
- *blend_category*: Karma tasarımcısının Varlıklar bölmesinde denetimin görünmesi gereken grubun etiketi. Denetimin Varlıklar'da görünmesi için A `BlendCategory` gereklidir.
- *type_full_name_n*: Ad alanı da `ManagedPackage.MyCustomControl`dahil olmak üzere her denetim için tam nitelikli ad. Nokta biçiminin hem yönetilen hem de yerel türler için kullanıldığını unutmayın.

Daha gelişmiş senaryolarda, tek bir `<File>` paket `<FileList>` birden çok denetim derlemesi içerdiğinde, birden çok öğe de ekleyebilirsiniz. Denetimlerinizi ayrı `<ToolboxItems>` kategorilerhalinde düzenlemek istiyorsanız, tek `<File>` bir düğüm içinde birden çok düğüm de olabilir.

Aşağıdaki örnekte, uygulanan `ManagedPackage.winmd` denetim Visual Studio ve Blend'te "Yönetilen Paket" adlı bir grupta görünür ve bu grupta "MyCustomControl" görünür. Tüm bu isimler rasgele.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio'da göründüğü gibi bir örnek denetim](media/UWP-control-vs-toolbox.png)

![Karışım'da görünen bir örnek denetim](media/UWP-control-blend-assets.png)

> [!Note]
> Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetimi açıkça belirtmeniz gerekir. Biçimde `Namespace.ControlName`belirttiğinizi emin olun.

## <a name="add-custom-icons-to-your-controls"></a>Denetimlerinize özel simgeler ekleme

Araç kutusu/varlıklar bölmesinde özel bir simge görüntülemek için, projenize `design.dll` veya ilgili projeye "Namespace.ControlName.extension" adıyla bir resim ekleyin ve yapı eylemini "Gömülü Kaynak" olarak ayarlayın. Ayrıca, ilişkili `AssemblyInfo.cs` nin ProvideMetadata özniteliğini belirttiğinden `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`de emin olmalısınız . Bu [örneğe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)bakın.

Desteklenen biçimler `.png`, `.jpg` `.jpeg`, `.gif`, `.bmp`, ve . Önerilen format 16 piksele 16 pikselbMP24'dür.

![Araç kutusu simgesi örneği](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Pembe arka plan çalışma zamanında değiştirilir. Visual Studio teması değiştirildiğinde ve arka plan rengi beklendiğinde simgeler yeniden renklendirilir. Daha fazla bilgi için, [Visual Studio için Lütfen Resim ve Simgelere](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)başvurun.

Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir resim dosyası içerir.

![Projede özel simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> Yerel denetimler için simgeyi `design.dll` projeye kaynak olarak koymanız gerekir.

## <a name="support-specific-windows-platform-versions"></a>Belirli Windows platform sürümlerini destekleyin

UWP paketleri, uygulamanın yüklenebileceği işletim sistemi sürümünün üst ve alt sınırlarını tanımlayan targetplatformversion (TPV) ve TargetPlatformMinVersion (TPMinV) içerir. TPV ayrıca, uygulamanın oluşturuladığı SDK sürümünü de belirtir. Bir UWP paketi yazarken bu özelliklere dikkat edin: Uygulamada tanımlanan platform sürümlerinin sınırları dışında API'ler kullanmak, yapının çalışma zamanında başarısız olmasıveya uygulamanın başarısız olması durumunda neden olur.

Örneğin, denetim paketiniz için TPMinV'i Windows 10 Anniversary Edition (10.0; 14393) oluşturun, böylece paketin yalnızca alt sınırla eşleşen UWP projeleri tarafından tüketilmesini sağlamak istiyorsunuz. Paketinizin UWP projeleri tarafından tüketilmesine izin vermek için, denetimlerinizi aşağıdaki klasör adlarıyla paketlemeniz gerekir:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet, tüketen projenin TPMinV'ini otomatik olarak denetler ve Windows 10 Anniversary Edition'dan daha düşükse yüklemeyi başarısız olur (10.0; Yapı 14393)

WPF durumunda, WPF kontrol paketinizin .NET Framework v4.6.1 veya daha yüksek hedefleyen projeler tarafından tüketilmesini istediğinizi varsayalım. Bunu uygulamak için denetimlerinizi aşağıdaki klasör adlarıyla paketlemeniz gerekir:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Tasarım zamanı desteği ekleme

Denetim özelliklerinin özellik denetçisinde nerede görünacağını yapılandırmak, özel süsleyiciler `design.dll` vb. `lib\uap10.0.14393\Design` eklemek için dosyanızı hedef platforma uygun şekilde klasörün içine yerleştirin. Ayrıca, **[Şablonu Edit > Kopyala](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özelliğinin çalıştığından emin `Generic.xaml` olmak için, `<your_assembly_name>\Themes` klasörde birleştirdiği kaynak sözlüklerini (yine, gerçek derleme adınızı kullanarak) eklemeniz gerekir. (Bu dosyanın denetimin çalışma zamanı davranışı üzerinde hiçbir etkisi yoktur.) Klasör yapısı böylece aşağıdaki gibi görünür:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


WPF için, WPF denetim paketinizin .NET Framework v4.6.1 veya daha yüksek hedefleyen projeler tarafından tüketilmesini istediğiniz örnekle devam edin:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Varsayılan olarak, denetim özellikleri özellik denetçisindeki Çeşitli kategori altında gösterilecek.

## <a name="use-strings-and-resources"></a>Dizeleri ve kaynakları kullanma

Paketinize, denetiminiz`.resw`veya tüketen UWP projeniz tarafından kullanılabilecek dize kaynaklarını ( ) katıştırabilir, dosyanın **Yapı Eylemi** özelliğini `.resw` **PRIResource**olarak ayarlayabilirsiniz.

Örneğin, ExtensionSDKasNuGetPackage örneğindeki [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) bakın.

> [!Note]
> Bu yalnızca UWP denetimleri için geçerlidir.

## <a name="see-also"></a>Ayrıca bkz.

- [UWP Paketleri Oluşturma](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
