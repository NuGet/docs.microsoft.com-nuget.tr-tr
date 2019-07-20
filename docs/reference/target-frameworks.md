---
title: NuGet için hedef çerçeveler başvurusu
description: NuGet hedef çerçevesi, bir paketin çerçeveye bağlı bileşenlerini belirler ve yalıtır.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ea9f699b202d7f32648f0ccfeac3ceb1ca325b7e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342433"
---
# <a name="target-frameworks"></a>Hedef çerçeveler

NuGet, bir paketin çerçeveye bağlı bileşenlerini özellikle tanımlamak ve yalıtmak için çeşitli yerlerde hedef çerçeve başvurularını kullanır:

- [Proje dosyası](../create-packages/multiple-target-frameworks-project-file.md): SDK stilindeki projeler için *. csproj* , hedef Framework başvurularını içerir.
- [. nuspec bildirimi](../reference/nuspec.md): Bir paket, projenin hedef çerçevesine bağlı olarak bir projeye dahil edilecek ayrı paketleri belirtebilir.
- [. nupkg klasör adı](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): Bir paket `lib` klasörünün içindeki klasörler, her biri dll 'leri ve söz konusu çerçeveye uygun olan diğer içerikleri içeren hedef Framework 'e göre adlandırılmış olabilir.
- [Packages. config](../reference/packages-config.md): Bir `targetframework` bağımlılığın özniteliği, yüklenecek bir paketin türevini belirtir.

> [!Note]
> Aşağıdaki tabloları hesaplayan NuGet istemci kaynak kodu aşağıdaki konumlarda bulunur:
> - Desteklenen çerçeve adları: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Çerçeve önceliği ve eşleme: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Desteklenen çerçeveler

Bir çerçeveye genellikle kısa bir hedef Framework bilinen adı veya tfd tarafından başvurulur. .NET Standard Bu, birden çok çerçeve için tek bir başvuruya izin vermek üzere *TXD* için de genelleştirilir.

NuGet istemcileri aşağıdaki tablodaki çerçeveleri destekler. Eşdeğerleri köşeli ayraç [] içinde gösterilir. Gibi bazı araçların `dotnet`bazı dosyalardaki kurallı tfms 'lerin çeşitlemelerini kullanabileceğini unutmayın. Örneğin, `dotnet pack` yerine bir `.NETCoreApp2.0` `.nuspec` dosyasında kullanır.`netcoreapp2.0` Çeşitli NuGet istemci araçları bu çeşitlemeleri düzgün şekilde işler, ancak dosyaları doğrudan düzenlenirken her zaman kurallı TFMs 'Leri kullanmanız gerekir.

| Ad | Grubunun | TFMs/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | NET | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Windows Mağazası) | netcore | netcore [netcore45] |
| | | netcore45 [Win, Win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET mikro Framework | netmf | netmf |
|Windows | kazanırsınız | Win [Win8, netcore45] |
| | | Win8 [netcore45, Win] |
| | | win81 [netcore451] |
| | | Win10 (Windows 10 platformunda desteklenmez) |
Silverlight | SL | sl4 |
| | | sl5 |
Windows Phone (SL) | WB | WP [WP7] |
| | | wp7 |
| | | wp75 |
| | | WP8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Evrensel Windows Platformu | UAP | UAP [UAP 10.0] |
| | | UAP 10.0 |
| | | uıap 10.0. xxxxx (burada 10.0. xxxxx, tüketen uygulamanın en düşük hedef platform sürümüdür) |
.NET Standard | Netstandard | Netstandard 1.0 |
| | | Netstandard 1.1 |
| | | Netstandard 1.2 |
| | | Netstandard 1.3 |
| | | Netstandard 1.4 |
| | | Netstandard 1.5 |
| | | Netstandard 1.6 |
| | | Netstandard 2.0 |
.NET Core uygulaması | netcoreapp | netcoreapp 1.0 |
| | | netcoreapp 1.1 |
| | | netcoreapp 2.0 |
| | | netcoreapp 2.1 |
| | | netcoreapp 2.2 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Kullanım dışı çerçeveler

Aşağıdaki çerçeveler kullanım dışıdır. Bu çerçeveleri hedefleyen paketlerin belirtilen değişikliklere geçirilmesi gerekir.

| Kullanım dışı çerçeve | Başka
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| adlar |
| DNX |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | Netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| wınrt | kazanırsınız |

## <a name="precedence"></a>Önceliği

Bir dizi çerçeve birbirleriyle ve birbirleriyle uyumludur, ancak eşdeğer değildir:

| Framework | Kullanabilir |
| -- | --- |
| UAP (Evrensel Windows Platformu) | win81 |
| | wpa81 |
| | netcore50 |
| Win (Microsoft Store) | wınrt |
| | |

## <a name="net-standard"></a>NET standart

[.NET Standard](/dotnet/standard/net-standard) , ikili uyumlu Çerçeveler arasındaki başvuruları basitleştirir ve tek bir hedef çerçevenin diğerlerinin birleşimine başvurmasına olanak tanır. (Arka plan için bkz. [.net öncü](/dotnet/articles/standard/index).)

[NuGet en yakın çerçeve aracı](https://aka.ms/s2m3th) , NuGet 'in, projenin çerçevesini temel alan bir pakette bulunan çok sayıda çerçeve varlıklarından bir çerçeve seçmek için hangi şekilde kullanacağını taklit eder.

Takma ad `netstandard` serisi NuGet 3,3 ve önceki sürümlerde kullanılmalıdır; bilinen ad sözdizimi v 3.4 ve sonrasında kullanılmalıdır. `dotnet`

## <a name="portable-class-libraries"></a>Taşınabilir sınıf kitaplıkları

> [!Warning]
> **PCLS önerilmez**. PCLs destekleniyor olsa da, paket yazarları bunun yerine Netstandard 'ı desteklemelidir. .NET Platform standardı, PCLs 'in bir gelişmidir ve *Taşınabilir-a + b + c* takma adları gibi bir statik kitaplığa bağlı olmayan tek bir bilinen ad kullanarak platformlar arasında ikili taşınabilirliği temsil eder.

Birden çok alt hedef çerçevesine başvuran bir hedef çerçeve tanımlamak için, `portable` başvurulan çerçeveler listesine önek olarak kullanılan anahtar sözcüğü kullanılır. Doğrudan derlenmeyen ekstra çerçeveler de dahil olmak üzere yapay kullanmaktan kaçının ve bu çerçeveler içinde istenmeyen yan etkilere neden olabilir.

Üçüncü taraflar tarafından tanımlanan ek çerçeveler, bu şekilde erişilebilen diğer ortamlarla uyumluluk sağlar. Ayrıca, bu ilgili çerçevelerin kombinasyonlarıyla aynı `Profile#`şekilde başvuruda bulunmak için kullanılabilen bir Özet profil numarası vardır, ancak klasörlerin okunabilirliğini azalttığı için bu numaraları kullanmak önerilen bir uygulama değildir ve `.nuspec`.

| Profilinizi # | Çerçeveler | Tam ad | .NET Standard |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4,0 | Taşınabilir-net40 + Win8 + SL4 + WP7 |
 | | Windows 8,0 | |
 | | Silverlight 4,0 |
 | | WindowsPhone 7,0|
 Profile3 | . NETFramework 4,0 | Taşınabilir-net40 + SL4
 | | Silverlight 4,0 |
 Profile4 | . NETFramework 4,5 | Taşınabilir-net45 + SL4 + Win8 + WP7
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 7,0 |
 Profile5 | . NETFramework 4,0 | Taşınabilir-net40 + Win8
 | | Windows 8,0 |
 Profile6 | . NETFramework 4.0.3 | Taşınabilir-net403 + Win8
 | | Windows 8,0 |
 Profile7 | . NETFramework 4,5 | Taşınabilir-net45 + Win8 | Netstandard 1.1
 | | Windows 8,0 |
 Profile14 | . NETFramework 4,0 | Taşınabilir-net40 + SL5
 | | Silverlight 5,0 |
 Profile18 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL4
 | | Silverlight 4,0 |
 Profile19 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL5
 | | Silverlight 5,0 |
 Profile23 | . NETFramework 4,5 | Taşınabilir-net45 + SL4
 | | Silverlight 4,0 |
 Profile24 | . NETFramework 4,5 | Taşınabilir-net45 + SL5
 | | Silverlight 5,0 |
 Profile31 | Windows 8.1 | Taşınabilir-win81 + wp81 | Netstandard 1.0
 | | WindowsPhone 8,1 (SL) |
 Profile32 | Windows 8.1 | Taşınabilir-win81 + wpa81 | Netstandard 1.2
 | | WindowsPhone 8,1 (UWP) |
 Profile36 | . NETFramework 4,0 | Taşınabilir-net40 + SL4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile37 | . NETFramework 4,0 | Taşınabilir-net40 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 Profile41 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL4 + Win8
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 Profile42 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 Profile44 | . NETFramework 4.5.1 | Taşınabilir-net451 + win81 | Netstandard 1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4,5 | Taşınabilir-net45 + SL4 + Win8
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 Profile47 | . NETFramework 4,5 | Taşınabilir-net45 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 Profile49 | . NETFramework 4,5 | Taşınabilir-net45 + WP8 | Netstandard 1.0
 | | WindowsPhone 8,0 (SL) |
 Profile78 | . NETFramework 4,5 | Taşınabilir-net45 + Win8 + WP8 | Netstandard 1.0
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile84 | WindowsPhone 8.1 | Taşınabilir-wp81 + wpa81 | Netstandard 1.0
 | | WindowsPhone 8,1 (UWP) |
 Profile88 | . NETFramework 4,0 | Taşınabilir-net40 + SL4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile92 | . NETFramework 4,0 | Taşınabilir-net40 + Win8 + wpa81
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile95 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL4 + Win8 + WP7
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 7,0 |
 Profile96 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile102 | . NETFramework 4.0.3 | Taşınabilir-net403 + Win8 + wpa81
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile104 | . NETFramework 4,5 | Taşınabilir-net45 + SL4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile111 | . NETFramework 4,5 | Taşınabilir-net45 + Win8 + wpa81 | Netstandard 1.1
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile136 | . NETFramework 4,0 | Taşınabilir-net40 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile143 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile147 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile151 | NETFramework 4.5.1 | Taşınabilir-net451 + win81 + wpa81 | Netstandard 1.2
 | | Windows 8.1 |
 | | WindowsPhone 8,1 (UWP) |
 Profile154 | . NETFramework 4,5 | Taşınabilir-net45 + SL4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile157 | Windows 8.1 | Taşınabilir-win81 + wp81 + wpa81 | Netstandard 1.0
 | | WindowsPhone 8,1 (SL) |
 | | WindowsPhone 8,1 (UWP) |
 Profile158 | . NETFramework 4,5 | Taşınabilir-net45 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile225 | . NETFramework 4,0 | Taşınabilir-net40 + SL5 + Win8 + wpa81
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile240 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL5 + Win8 + wpa8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile255 | . NETFramework 4,5 | Taşınabilir-net45 + SL5 + Win8 + wpa81
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile259 | . NETFramework 4,5 | Taşınabilir-net45 + Win8 + wpa81 + WP8 | Netstandard 1.0
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile328 | . NETFramework 4,0 | Taşınabilir-net40 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile336 | . NETFramework 4.0.3 | Taşınabilir-net403 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile344 | . NETFramework 4,5 | Taşınabilir-net45 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8,0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |

Ayrıca, Xamarin 'i hedefleyen NuGet paketleri ek Xamarin tanımlı çerçeveler kullanabilir. Bkz. [Xamarin Için NuGet paketleri oluşturma](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Ad | Açıklama | .NET Standard |
| --- | --- | ---
| monoandroid | Android işletim sistemi için mono desteği | Netstandard 1.4 |
| MonoTouch | İOS için mono desteği | Netstandard 1.4 |
| monomac | OSX için mono desteği | Netstandard 1.4 |
| xamarinios | İOS için Xamarin desteği | Netstandard 1.4 |
| xamarinmac | Mac için Xamarin 'i destekler | Netstandard 1.4 |
| xamarinpsthree | PlayStation 3 üzerinde Xamarin desteği | Netstandard 1.4 |
| xamarinpsfour | PlayStation 4 üzerinde Xamarin desteği | Netstandard 1.4 |
| xamarinpsvita | PS Vita 'da Xamarin desteği | Netstandard 1.4 |
| xamarinwatchos | Izleme işletim sistemi için Xamarin | Netstandard 1.4 |
| xamarintvos | TV OS için Xamarin | Netstandard 1.4 |
| xamarinxboxthreesixty | XBox 360 için Xamarin | Netstandard 1.4 |
| xamarinxboxone | XBox One için Xamarin | Netstandard 1.4 |

> [!Note]
> Stephen Cleary, [.net 'teki, çerçeve profilleri içinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)bulabileceğiniz desteklenen PCLS 'yi listeleyen bir araç oluşturdu.
