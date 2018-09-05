---
title: NuGet için hedef Framework başvurusu
description: NuGet hedef framework başvuruları belirleyin ve bir paket framework bağımlı bileşenlerden ayırmak.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 047ede14c7935844cb4f6d0315772c2a1190e5b8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547265"
---
# <a name="target-frameworks"></a>Hedef Çerçeve

NuGet, özel olarak belirlemek ve bir paket framework bağımlı bileşenlerden ayırmak için çeşitli yerlerde hedef framework başvurularını kullanır:

- [.nuspec bildirimi](../reference/nuspec.md): bir paket bir proje projenin hedef çerçevesi bağlı olarak dahil edilecek ayrı paketleri belirtebilirsiniz.
- [.nupkg klasör adı](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): bir paketin klasörlerde `lib` klasörü adı göre her biri içeren dll ve diğer içerikleri bu çerçeve için uygun hedef çerçeve.
- [Packages.config](../reference/packages-config.md): `targetframework` bağımlılık özniteliği yüklemek için bir paket türevi belirtir.

> [!Note]
> Aşağıdaki tablolarda hesaplar NuGet istemci kaynak kodu, aşağıdaki konumlarda bulunur:
> - Desteklenen Framework adları: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Framework öncelik ve eşleme: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Desteklenen çerçeveler

Bir çerçeve, genellikle bir kısa hedef çerçeve adı veya TFM tarafından başvuruluyor. İçinde .NET ayrıca bu, standart için genelleştirilmiş olduğundan *TxM* birden çok çerçeveyi tek bir başvuruya izin vermek için.

NuGet istemcileri, aşağıdaki tabloda çerçeveleri destekler. Eşdeğerleri köşeli ayraçlar [] içinde gösterilir. Bazı araçlar, gibi Not `dotnet`, kurallı Tfm'ler çeşitleri klasördeki bazı dosyaları kullanabilirsiniz. Örneğin, `dotnet pack` kullanan `.NETCoreApp2.0` içinde bir `.nuspec` dosya yerine `netcoreapp2.0`. Çeşitli NuGet istemci araçları bu farklılıkların düzgün bir şekilde işlemek, ancak kurallı Tfm'ler dosyaları doğrudan düzenlerken her zaman kullanmalısınız.

| Ad | Kısaltması | Tfm'ler/TxMs |
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
|Microsoft Store (Windows Store) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | Win | Win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (Windows 10 platformu tarafından desteklenmez) |
Silverlight | SL | sl4 |
| | | sl5 |
Windows Phone (yükleme SL) | WP | WP [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Evrensel Windows Platformu | uap | uap [uap10.0] |
| | | uap10.0 |
.NET standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET core uygulaması | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
Tizen | Tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Kullanım dışı çerçeveleri

Aşağıdaki çerçeveleri kullanım dışı bırakılmıştır. Bu çerçeveler hedefleme paketleri için belirtilen değişiklik geçirmeniz gerekir.

| Kullanım dışı framework | Değiştirme
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 olarak |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| DotNet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | Win |

## <a name="precedence"></a>Önceliği

Çerçeve sayısı, ilgili ve birbiriyle uyumlu, ancak eşdeğer değil gerekmeyen şunlardır:

| Framework | Kullanabilirsiniz |
| -- | --- |
| uap (Evrensel Windows platformu) | win81 |
| | wpa81 |
| | netcore50 |
| (Microsoft Store) kazanın | winrt |
| | |

## <a name="net-platform-standard"></a>NET Platform standart

[.NET Platform standardını](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) arasında ikili ile uyumlu çerçeveleri, diğerleri birleşimi başvurmak bir tek hedef Framework'ü izin vererek başvurular basitleştirir. (Arka plan bilgileri için bkz. [.NET öncü](/dotnet/articles/standard/index).)

[NuGet alma yakın Framework aracı](https://aka.ms/s2m3th) NuGet bir çerçeve proje framework tabanlı bir paket içinde çoğu kullanılabilir framework varlık seçmek için kullandığı benzetimini yapar.

`dotnet` Takma adlar bir dizi kullanılmalıdır, NuGet 3.3 ve daha önce; `netstandard` v3.4 ve daha sonra ad sözdizimi kullanılmalıdır.

## <a name="portable-class-libraries"></a>Taşınabilir sınıf kitaplıkları

> [!Warning]
> **PCLs önerilmez**. Paket yazarlarının netstandard PCLs desteklenir ancak bunun yerine desteklemelidir. .NET Platform standardını PCLs'ın Gelişmiş hali olan ve bir statik kitaplığa gibi bağlı değil tek bir ad kullanarak platformlar arası ikili taşınabilirlik temsil *taşınabilir-a + b + c* takma adlar.

Birden çok alt-target-çerçeveleri için başvuruda bulunan bir hedef çerçeve tanımlamak için `portable` başvurulan çerçeveleri listesini önek olarak eklemek için kullanılan anahtar sözcüğünü kullanın. İçin bu çerçeveleri, istenmeyen yan etkilere neden olabileceği için doğrudan karşı derlenmemiş ek çerçeveler sınırlarına eklemekten kaçınır.

Ek çerçeveler üçüncü taraflar tarafından tanımlanan bu şekilde erişilebilir olan diğer ortamlara ile uyumluluk sağlar. Ayrıca, bu ilgili çerçeveleri birleşimlerini başvurmak kullanılabilen toplu profili numaraları vardır `Profile#`, ancak bu bu numaraları okunabilirliğini veklasörleridüşürürolarakkullanılmaküzereönerilenbiryöntemdeğildir`.nuspec`.

| Profil # | Çerçeveler | Tam adı | .NET standard |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4.0 | Taşınabilir net40 + win8 + sl4 + wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | . NETFramework 4.0 | Taşınabilir net40 + sl4
 | | Silverlight 4.0 |
 Profile4 | . NETFramework 4.5 | Portable-net45 + sl4 + win8 + wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | . NETFramework 4.0 | Taşınabilir net40 + win8
 | | Windows 8.0 |
 Profile6 | . 4.0.3 NETFramework | Taşınabilir net403 + win8
 | | Windows 8.0 |
 Profile7 | . NETFramework 4.5 | Portable-net45 + win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | . NETFramework 4.0 | Taşınabilir net40 + sl5
 | | Silverlight 5.0 |
 Profile18 | . 4.0.3 NETFramework | Taşınabilir net403 + sl4
 | | Silverlight 4.0 |
 Profile19 | . 4.0.3 NETFramework | Taşınabilir net403 + sl5
 | | Silverlight 5.0 |
 Profile23 | . NETFramework 4.5 | Portable-net45 + sl4
 | | Silverlight 4.0 |
 Profile24 | . NETFramework 4.5 | Portable-net45 + sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | Taşınabilir win81 + wp81 | netstandard1.0
 | | WindowsPhone 8.1 (yükleme SL) |
 Profile32 | Windows 8.1 | Taşınabilir win81 + wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | . NETFramework 4.0 | Taşınabilir net40 sl4 + win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | . NETFramework 4.0 | Taşınabilir net40 sl5 + win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | . 4.0.3 NETFramework | Taşınabilir net403 sl4 + win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | . 4.0.3 NETFramework | Taşınabilir net403 sl5 + win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | . 4.5.1 NETFramework | Taşınabilir net451 + win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4.5 | Portable-net45 + sl4 + win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | . NETFramework 4.5 | Portable-net45 + sl5 + win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | . NETFramework 4.5 | Portable-net45 + wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | . NETFramework 4.5 | Portable-net45 + win8 wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | Taşınabilir wp81 + wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | . NETFramework 4.0 | Taşınabilir net40 sl4 + win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | . NETFramework 4.0 | Taşınabilir net40 + win8 wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | . 4.0.3 NETFramework | Taşınabilir net403 sl4 + win8 + wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | . 4.0.3 NETFramework | Taşınabilir net403 sl4 + win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | . 4.0.3 NETFramework | Taşınabilir net403 + win8 wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | . NETFramework 4.5 | Portable-net45 + sl4 + win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | . NETFramework 4.5 | Portable-net45 + win8 wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | . NETFramework 4.0 | Taşınabilir net40 sl5 + win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | . 4.0.3 NETFramework | Taşınabilir net403 sl4 + win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | . 4.0.3 NETFramework | Taşınabilir net403 sl5 + win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | 4.5.1 NETFramework | Taşınabilir net451 + win81 wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | . NETFramework 4.5 | Portable-net45 + sl4 + win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | Taşınabilir win81 + wp81 wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (yükleme SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | . NETFramework 4.5 | Portable-net45 + sl5 + win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | . NETFramework 4.0 | Taşınabilir net40 sl5 + win8 + wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | . 4.0.3 NETFramework | Taşınabilir net403 sl5 + win8 + wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | . NETFramework 4.5 | Portable-net45 + sl5 + win8 + wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | . NETFramework 4.5 | Portable-net45 + win8 + wpa81 + wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | . NETFramework 4.0 | Taşınabilir net40 sl5 + win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | . 4.0.3 NETFramework | Taşınabilir net403 sl5 + win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | . NETFramework 4.5 | Portable-net45 + sl5 + win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Ayrıca, Xamarin hedefleyen NuGet paketlerini ek Xamarin tanımlı çerçeveleri kullanabilirsiniz. Bkz: [Xamarin için oluşturma NuGet paketlerini](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Ad | Açıklama | .NET standard |
| --- | --- | ---
| monoandroid | Mono Android işletim sistemi desteği | netstandard1.4 |
| monotouch | İOS için Mono desteği | netstandard1.4 |
| monomac | OSX Mono desteği | netstandard1.4 |
| xamarinios | İOS için Xamarin desteği | netstandard1.4 |
| xamarinmac | Mac için Xamarin için destekler | netstandard1.4 |
| xamarinpsthree | Playstation 3 üzerinde Xamarin desteği | netstandard1.4 |
| xamarinpsfour | Xamarin 4 Playstation üzerinde desteği | netstandard1.4 |
| xamarinpsvita | PS Vita şirket Xamarin desteği | netstandard1.4 |
| xamarinwatchos | Watch işletim sistemi için Xamarin | netstandard1.4 |
| xamarintvos | TV OS için Xamarin | netstandard1.4 |
| xamarinxboxthreesixty | XBox 360 için Xamarin | netstandard1.4 |
| xamarinxboxone | XBox One için Xamarin | netstandard1.4 |

> [!Note]
> Stephen Cleary kendi gönderi bulabilirsiniz, desteklenen PCLs listeleyen bir araç oluşturmuştur [.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
