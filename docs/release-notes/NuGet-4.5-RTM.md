---
title: NuGet 4.5 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548302"
---
# <a name="nuget-45-rtm-release-notes"></a>NuGet 4.5 RTM sürüm notları

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır. [Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntülenemiyor, eklenemiyor veya Nuget Paket Yöneticisi'ni kullanarak dotnetclıtools'u başlatamadı

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

Bazen, geçersiz imzalı veya paket sürümü 'DateTime' değeriyle ayarlandığında bir derlemeyi içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde çalışmasına geri neden [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM zaman çerçevesinde giderilen sorunlar

4.4 NuGet RTM'de düzeltilen sorunları için lütfen başvurmak [NuGet 4.4 RTM sürüm notları](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Özellikler

- Otomatik-push sembol package - devre dışı [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Hatalar

- [Regresyon] içinde 15.5p1: Portable0.0 atlandı - [#6105](https://github.com/NuGet/Home/issues/6105)
- Paketleri varlıklarından geri yüklemeden sonra - eksik [#5995](https://github.com/NuGet/Home/issues/5995)
- Eklenti kimlik bilgisi sağlayıcıları ile içeren URI'leri alanları - çalışmaz [#5982](https://github.com/NuGet/Home/issues/5982)
- Paket geri yükleme başarısız olursa hata olsa da en az ayrıntı ON - çıkış yazdırılacağı [#5658](https://github.com/NuGet/Home/issues/5658)
- DotNet
  - Çözüm düzeyinde dotnetcore geri yükleme için rastgele oluşturma hataları - ProjectReference false lider, ReferenceOutputAssembly ile izleyin değil [#5490](https://github.com/NuGet/Home/issues/5490)
- Otomatik Tamamlama yanlış nesne yöntemleri ile-PMC'yi geliştirilme [#4800](https://github.com/NuGet/Home/issues/4800)
- nuget.exe geri yükleme başarısız olursa, Visual Studio 2015 araç takımıyla - [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc vs2017'de - örneklemek pahalı [#4205](https://github.com/NuGet/Home/issues/4205)
- Yavaş yavaş bağlantı - bağımlılık bilgi almak [#4089](https://github.com/NuGet/Home/issues/4089)
- birden çok paket ortak bir bağımlılık - paylaşıyorsa - RemoveDependencies çakışabilmektedir kaldırma-package başarısız olur [#4026](https://github.com/NuGet/Home/issues/4026)
- Yayımlama için - NuGet.Core.nupkg Sonlandır [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet paketi csproj + project.json - için - IncludeProjectReferences kullanıldığında, dizin adı bağımlılık Kimliğinden çözümler [#3566](https://github.com/NuGet/Home/issues/3566)
- Bir özel durum oluştu - türü Başlatıcısı 'NuGet.ProxyCache' oluşturdu [#3144](https://github.com/NuGet/Home/issues/3144)
- nuget geri yükleme performansı kudu - sorun [#3087](https://github.com/NuGet/Home/issues/3087)
- UI istemci başarısız araması önceden kayıt BLOB'lar - olduğunda herhangi bir hata veya uyarı gösterilecek [#2149](https://github.com/NuGet/Home/issues/2149)
- -Güncelleştirmeleri, hatalı bir sorgu oluşturur - Get-paketleri [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>GitHub sorunları 4.5 RTM sürümünde sabit bağlantılar

[Konu listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
