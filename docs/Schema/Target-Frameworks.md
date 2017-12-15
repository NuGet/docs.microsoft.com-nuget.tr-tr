---
title: "Hedef çerçeveler başvurular için NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4343a48e-f6df-4a44-9d66-4616c3caacf5
description: "NuGet hedef framework başvurular tanımlamak ve bir paket framework bağımlı bileşenleri yalıtır."
keywords: "NuGet paketi, .NET framework hedefleri, .NET framework sürümü hedefleme"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d1d2e6850f22306d715b1c2071ee45b0eb050dc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="target-frameworks"></a>Hedef Çerçeve

NuGet hedef framework başvurular yerler çeşitli özellikle tanımlamak ve bir paket framework bağımlı bileşenleri ayırmak için kullanır:

- [.nuspec bildirimi](../schema/nuspec.md): bir paket projenin hedef çerçevesi bağlı olarak bir projeye dahil edilecek ayrı paketleri belirtebilirsiniz.
- [.nupkg klasör adı](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): bir paketin klasörlerde `lib` klasörü adlı DLL'ler ve diğer içeriği o framework uygun her biri içeren hedef framework göre.
- [Packages.config](../Schema/packages-config.md): `targetframework` bir bağımlılık özniteliğinin yüklemek için bir paket türevi belirtir.
- [Project.JSON](../Schema/project-json.md): `frameworks` düğümü karşı proje derlenmiş framework sürümlerini belirtir.

> [!Note]
> Aşağıdaki tablolarda hesaplar NuGet istemci kaynak kodu aşağıdaki konumlardan birinde bulunur:
> -  Desteklenen Framework adları: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> -  Framework önceliği ve eşleme: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Desteklenen çerçeveler

Bir çerçeve, genellikle bir kısa hedef framework ad veya TFM tarafından başvuruluyor. İçinde .NET da budur standart için genelleştirilmiş *TxM* birden çok çerçeveyi tek bir başvuru izin vermek için.

NuGet istemcileri çerçeveleri aşağıdaki tabloda destekler. Eşdeğerleri köşeli ayraç [] içinde gösterilir. Bazı araçlar, gibi Not `dotnet`, kurallı TFMs varyasyonları bazı dosyaları kullanabilirsiniz. Örneğin, `dotnet pack` kullanan `.NETCoreApp2.0` içinde bir `.nuspec` dosya yerine `netcoreapp2.0`. Çeşitli NuGet istemci araçları bu değişimler düzgün bir şekilde işlemek, ancak her zaman kurallı TFMs dosyaları doğrudan düzenlerken kullanmanız gerekir.

| Ad           | Kısaltması | TFMs/TxMs |
| -------------  | ------------ | --------- |
|.NET Framework  | NET          | net11     |
|                |              | net20     |
|                |              | Net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Windows Mağazası   | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, olduğu win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | Win          | Win [olduğu win8, netcore45] |
| | | olduğu win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (Windows 10 platformu tarafından desteklenmiyor) |
Silverlight | SL | sl4 |
| | | sl5 |
Windows Phone (SL) | WB | WB [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Evrensel Windows Platformu | uap | uap [uap10.0] |
| | | uap10.0 |
.NET standart | netstandard | netstandard1.0 |
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
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Kullanım dışı çerçeveler
Aşağıdaki çerçevelerini kullanım dışı bırakılmıştır. Bu çerçeveleri hedefleme paketleri için belirtilen değiştirmeler geçirmeniz gerekir.

| Kullanım dışı framework | Değiştirme
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
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

İlgili ve birbiriyle uyumlu, ancak eşdeğer değil mutlaka çerçeveleri sayısı:

| Framework | Kullanabilirsiniz |
| --- | --- |
| uap (Evrensel Windows platformu) | win81 |
| | wpa81 |
| | netcore50 |
| (Microsoft Store) win | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>NET Platform standart

[.NET Platform standardını](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) ikili uyumlu çerçeveleri, diğerleri birleşimi başvurmak bir tek hedef framework izin vererek arasında başvurular basitleştirir. (Arka plan için bkz: [.NET Primer](https://docs.microsoft.com/dotnet/articles/standard/index).)

[NuGet alma yakın Framework aracı](https://aka.ms/s2m3th) NuGet bir framework projenin framework temel alınarak bir paketteki birçok kullanılabilir framework varlıklar arasından seçim yapmak için kullandığı benzetimini yapar.

`dotnet` NuGet 3.3 ve önceki sürümleri; adlar dizi kullanılmalıdır `netstandard` ad sözdizimi v3.4 ve sonraki sürümler kullanılmalıdır.

## <a name="portable-class-libraries"></a>Taşınabilir sınıf kitaplıkları

> [!Warning]
> **PCLs önerilmez**. Paketi yazarları netstandard PCLs desteklenir, ancak bunun yerine desteklemelidir. .NET Platform standardını PCLs bir evrimi olan ve istediğiniz gibi statik olarak bağlı değil tek bir ad kullanarak platformlarda ikili taşınabilirlik temsil *taşınabilir-a + b + c* adlar.

Birden çok alt-hedef-frameworks için başvuruda bulunan bir hedef framework tanımlamak için `portable` başvurulan çerçeveleri listesi öneki için kullanılan anahtar sözcüğü kullanın. Yapay istenmeyen yan etkileri bu çerçeveleri içinde açabilir olduğundan, karşı doğrudan derlenmemiş fazladan çerçeveleri dahil olmak üzere kaçının.

Üçüncü taraflar tarafından tanımlanan ek çerçeveler bu şekilde erişilebilir diğer ortamlar ile uyumluluk sağlar. Ayrıca, bu birleşimleri ilgili çerçeveleri başvurmak kullanılabilir olan toplu Profil numarası vardır `Profile#`, ancak bu klasörleri ve okunabilirliğiniazaltırgibibusayılarıkullanmakiçinönerilenbiryöntemdeğildir`.nuspec`.

| Profil # | çerçeveler | Tam ad | .NET standart |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4.0 | Taşınabilir net40 olduğu win8 + sl4 + wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | . NETFramework 4.0 | Taşınabilir net40 + sl4
 | | Silverlight 4.0 |
 Profile4 | . NETFramework 4.5 | Taşınabilir net45 + sl4 + olduğu win8 + wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | . NETFramework 4.0 | Taşınabilir net40 + olduğu win8
 | | Windows 8.0 |
 Profile6 | . NETFramework 4.0.3 | Taşınabilir net403 + olduğu win8
 | | Windows 8.0 |
 Profile7 | . NETFramework 4.5 | Taşınabilir net45 + olduğu win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | . NETFramework 4.0 | Taşınabilir net40 + sl5
 | | Silverlight 5.0 |
 Profile18 | . NETFramework 4.0.3 | Taşınabilir net403 + sl4
 | | Silverlight 4.0 |
 Profile19 | . NETFramework 4.0.3 | Taşınabilir net403 + sl5
 | | Silverlight 5.0 |
 Profile23 | . NETFramework 4.5 | Taşınabilir net45 + sl4
 | | Silverlight 4.0 |
 Profile24 | . NETFramework 4.5 | Taşınabilir net45 + sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | Taşınabilir win81 + wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | Taşınabilir win81 + wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | . NETFramework 4.0 | Taşınabilir net40 + sl4 + olduğu win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | . NETFramework 4.0 | Taşınabilir net40 + sl5 olduğu win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | . NETFramework 4.0.3 | Taşınabilir net403 + sl4 olduğu win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | . NETFramework 4.0.3 | Taşınabilir net403 + sl5 olduğu win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | . NETFramework 4.5.1 | Taşınabilir net451 + win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4.5 | Taşınabilir net45 + sl4 olduğu win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | . NETFramework 4.5 | Taşınabilir net45 + sl5 olduğu win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | . NETFramework 4.5 | Taşınabilir net45 + wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | . NETFramework 4.5 | Taşınabilir net45 olduğu win8 + wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | Taşınabilir wp81 + wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | . NETFramework 4.0 | Taşınabilir net40 + sl4 + olduğu win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | . NETFramework 4.0 | Taşınabilir net40 olduğu win8 + wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | . NETFramework 4.0.3 | Taşınabilir net403 + sl4 + olduğu win8 + wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | . NETFramework 4.0.3 | Taşınabilir net403 + sl4 + olduğu win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | . NETFramework 4.0.3 | Taşınabilir net403 olduğu win8 + wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | . NETFramework 4.5 | Taşınabilir net45 + sl4 + olduğu win8 + wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | . NETFramework 4.5 | Taşınabilir net45 olduğu win8 + wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | . NETFramework 4.0 | Taşınabilir net40 + sl5 + olduğu win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | . NETFramework 4.0.3 | Taşınabilir net403 + sl4 + olduğu win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | . NETFramework 4.0.3 | Taşınabilir net403 + sl5 + olduğu win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | Taşınabilir net451 + win81 wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | . NETFramework 4.5 | Taşınabilir net45 + sl4 + olduğu win8 + wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | Taşınabilir win81 + wp81 wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | . NETFramework 4.5 | Taşınabilir net45 + sl5 + olduğu win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | . NETFramework 4.0 | Taşınabilir net40 + sl5 + olduğu win8 + wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | . NETFramework 4.0.3 | Taşınabilir net403 + sl5 + olduğu win8 + wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | . NETFramework 4.5 | Taşınabilir net45 + sl5 + olduğu win8 + wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | . NETFramework 4.5 | Taşınabilir net45 olduğu win8 + wpa81 + wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | . NETFramework 4.0 | Taşınabilir net40 + sl5 + olduğu win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | . NETFramework 4.0.3 | Taşınabilir net403 + sl5 + olduğu win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | . NETFramework 4.5 | Taşınabilir net45 + sl5 + olduğu win8 + wpa81 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Ayrıca, Xamarin hedefleme NuGet paketlerini ek Xamarin tanımlı çerçeveleri kullanabilirsiniz. Bkz: [Xamarin oluşturma NuGet paketlerini](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Ad | Açıklama | .NET standart |
| --- | --- | ---
| monoandroid | Mono Android işletim sistemi desteği | netstandard1.4 |
| monotouch | İOS için Mono desteği | netstandard1.4 |
| monomac | Mono OSX desteği | netstandard1.4 |
| xamarinios | İOS için Xamarin desteği | netstandard1.4 |
| xamarinmac | Mac için xamarin destekler | netstandard1.4 |
| xamarinpsthree | Xamarin Playstation 3 üzerinde desteği | netstandard1.4 |
| xamarinpsfour | Xamarin Playstation 4 üzerinde desteği | netstandard1.4 |
| xamarinpsvita | PS Vita üzerinde Xamarin desteği | netstandard1.4 |
| xamarinwatchos | Gözcü işletim sistemi için Xamarin | netstandard1.4 |
| xamarintvos | TV işletim sistemi için Xamarin | netstandard1.4 |
| xamarinxboxthreesixty | XBox 360 için Xamarin | netstandard1.4 |
| xamarinxboxone | XBox biri için Xamarin | netstandard1.4 |

> [!Note]
> Stephen Cleary kendi gönderisini bulabilirsiniz, desteklenen PCLs listeleyen bir araç oluşturdu [.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
