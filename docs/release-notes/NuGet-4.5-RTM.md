---
title: NuGet 4.5 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496576"
---
# <a name="nuget-45-release-notes"></a>NuGet 4.5 Yayın Notları

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)ile birlikte geliyor.

## <a name="summary-whats-new-in-450"></a>Özeti: 4.5.0 Yenilikler

## <a name="summary-whats-new-in-452"></a>Özeti: 4.5.2 Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır

## <a name="summary-whats-new-in-453"></a>Özeti: 4.5.3 Yenilikler

* Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır. [Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici çözüm

El ile geri yükleme yapın.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzaiçeren bir derleme içeren bir paket kullandığınızda veya paket sürümü 'DateTime' işaretleyicisi ile ayarlandığında, paket otomatik geri yüklemesinin sonsuz bir döngü [dotnet/proje sistemi#1457'de](https://github.com/dotnet/project-system/issues/1457)çalışmasına neden olur.

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM zaman diliminde düzeltilen sorunlar

NuGet 4.4 RTM'de düzeltilen sorunlar için lütfen [NuGet 4.4 RTM Yayın Notları'na](../release-notes/nuget-4.4-RTM.md) bakın 

### <a name="features"></a>Özellikler

- Semboller paketinin otomatik itme devre dışı - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Hatalar

- [Regresyon] içinde 15.5p1: Portable0.0 atlanır - [#6105](https://github.com/NuGet/Home/issues/6105)
- Paketlerden elde edilen varlıklar geri yüklendikten sonra eksik - [#5995](https://github.com/NuGet/Home/issues/5995)
- Plugin kimlik bilgileri sağlayıcıları boşluk içeren URI'lerle çalışmaz - [#5982](https://github.com/NuGet/Home/issues/5982)
- Paket geri yüklenemediyse, hata en az ayrıntılı on ile bile çıktıya yazdırılmalıdır - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - çözüm düzeyinde dotnetcore geri yükleme rasgele yapı hataları na yol açan falseOutputAssembly ile ProjectReference takip etmez - [#5490](https://github.com/NuGet/Home/issues/5490)
- PMC'de otomatik tamamlama nesne yöntemleriyle yanlış çalışır - [#4800](https://github.com/NuGet/Home/issues/4800)
- nuget.exe geri yükleme Visual Studio 2015 araç seti ile başarısız olur - [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc vs2017 yılında anlık pahalı - [#4205](https://github.com/NuGet/Home/issues/4205)
- Yavaş bağlantı da bağımlılık bilgisi almak için yavaş - [#4089](https://github.com/NuGet/Home/issues/4089)
- paketi kaldırma w/ -RemoveDependencies birden fazla paket ortak bir bağımlılık paylaşırsa başarısız olur - [#4026](https://github.com/NuGet/Home/issues/4026)
- NuGet.Core.nupkg yayıncılık için Finalize - [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet paketi dizin adından bağımlılık kimliğini giderir -IncludeProjectReferences csproj + project.json için kullanıldığında - [#3566](https://github.com/NuGet/Home/issues/3566)
- 'NuGet.ProxyÖnbellek' için tür baş harfbir özel durum attı - [#3144](https://github.com/NuGet/Home/issues/3144)
- kudu ile nuget geri yükleme performans sorunu - [#3087](https://github.com/NuGet/Home/issues/3087)
- UI İstemci, arama kayıt lekeleri öncesinde olduğunda herhangi bir hata veya uyarı göstermek için başarısız - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Güncelleştirmeler yanlış bir sorgu oluşturur - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>4,5 RTM'de düzeltilen GitHub sorunlarına bağlantılar

[Sorunlar listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
