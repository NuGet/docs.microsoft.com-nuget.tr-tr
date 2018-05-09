---
title: NuGet 4.5 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-45-rtm-release-notes"></a>NuGet 4.5 RTM sürüm notları

[Visual Studio 2017 15,5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları 

.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır. [Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntüleme, ekleme ya da DotNetCLITools, Nuget Paket Yöneticisi'ni kullanarak güncelleştirme

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici Çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici Çözüm

El ile geri yükleme yapın.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun

Bazen, bir derlemeyi imzası geçersiz olan veya paket sürümü ile 'DateTime' borsa takip ayarlandığında içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde çalıştırılacak geri yükleme neden [dotnet/project-sistem #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM zaman çerçevesinde giderilen sorunlar

4.4 NuGet RTM ile giderilen sorunlar için lütfen [NuGet 4.4 RTM sürüm notları](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Özellikler

- Otomatik-itme simgeleri paketinin - devre dışı [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Hatalar

- [Regresyon] 15.5p1 içinde: Portable0.0 atlandı - [#6105](https://github.com/NuGet/Home/issues/6105)
- Paketleri varlıklarından geri yüklendikten sonra - eksik [#5995](https://github.com/NuGet/Home/issues/5995)
- Eklentisi kimlik bilgisi sağlayıcıları URI'ler içeren alanları ile - çalışmıyor [#5982](https://github.com/NuGet/Home/issues/5982)
- Paket geri yükleme işlemi başarısız olursa hata en az ayrıntı ON - çıkışıyla bile yazdırılacağı [#5658](https://github.com/NuGet/Home/issues/5658)
- DotNet
  - Çözüm düzeyinde dotnetcore geri yükleme için rastgele derleme hataları - false başında ReferenceOutputAssembly ile ProjectReference izleyin değil [#5490](https://github.com/NuGet/Home/issues/5490)
- Otomatik Tamamlama PMC işe yanlış yöntemleriyle nesnesi - [#4800](https://github.com/NuGet/Home/issues/4800)
- nuget.exe geri yükleme başarısız ile Visual Studio 2015 araç takımı - [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc vs2017 içinde - örneği pahalı [#4205](https://github.com/NuGet/Home/issues/4205)
- Yavaş yavaş bağlantı - bağımlılık bilgi almak [#4089](https://github.com/NuGet/Home/issues/4089)
- birden çok paket ortak bir bağımlılık - paylaşıyorsanız - RemoveDependencies içeren kaldırma-package başarısız olur [#4026](https://github.com/NuGet/Home/issues/4026)
- Yayımlama için - NuGet.Core.nupkg Sonlandır [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet paketi çözümler dizin adı bağımlılık Kimliğinden - IncludeProjectReferences kullanıldığında csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Bir özel durum oluştu - 'NuGet.ProxyCache' tür başlatıcısı belirtti [#3144](https://github.com/NuGet/Home/issues/3144)
- nuget restore performans sorunu kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- UI istemci başarısız arama kayıt BLOB'lar öncesinde - olduğunda herhangi bir hata veya uyarı göstermek [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-paketler - güncelleştirmeleri, hatalı bir sorgu oluşturur - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>GitHub sorunları 4.5 RTM sabit bağlantılar

[Konu listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)