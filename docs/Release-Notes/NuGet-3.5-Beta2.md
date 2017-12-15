---
title: "3.5 Beta2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "NuGet 3.5 Beta 2 bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.5 Beta 2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a>3.5 Beta2 sürüm notları

[NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM, 27 Haziran 2016 Visual Studio 2013 ve nuget.exe için yayımlanan

[Tam bir değişim günlüğü](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Konu listesi](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a>Önemli değişiklikleri

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Güncelleştirilmiş hata iletisi için kimliği doğrulanmış akışları - parola decrpytion .NET Core içinde desteğinin [#2942](https://github.com/NuGet/Home/issues/2942)

* Paket Yöneticisi konsolu Get-Package başarısız .NET Core proje açıksa - [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet itme komutta 403 hatalı işlenmesi düzeltme [#2910](https://github.com/NuGet/Home/issues/2910)

* Paketleri disableSourceControlIntegration ayarlandığında TFS kaynak denetimine bağlı bir çözümde kaldırma sorunlarını gidermek true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Paket güncelleştirme hesabı hedef olmayan paketlere - gerçekleştirilecek düzeltme [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild ayrıntı düzeyi UI eylemlerini - Nuget Paket Yöneticisi Günlükçü düzeyini ayarlamak için kullanma [#2705](https://github.com/NuGet/Home/issues/2705)

* Düzeltme NuGet yapılandırmadır Web sitesi projelerine - VS 2015 VSIX (v3.4.3) - geçersiz hata [#2667](https://github.com/NuGet/Home/issues/2667)

* Paketi sorunlarını düzeltmek `.csproj` içerik dosyaları dahil - olduğunda [#2658](https://github.com/NuGet/Home/issues/2658)

* İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) çalışmıyor - [#2653](https://github.com/NuGet/Home/issues/2653)

* -Değer üzerinde paket oluşturma null olamaz - Nuget 3.4.3 sürümdeki sorunu düzeltin [#2648](https://github.com/NuGet/Home/issues/2648)

* Geri yükleme için VSTS akışları - Nuget.Config depolanan kimlik bilgilerini kullanır [#2647](https://github.com/NuGet/Home/issues/2647)

* Performans - sürüm karşılaştırma kodu düzeltme aşırı ayırmaları - [#2632](https://github.com/NuGet/Home/issues/2632)

* Birden çok örneğini nuget.exe çalıştığında paralel olarak - aynı paketini yüklemek ilgili sorunları giderme [#2628](https://github.com/NuGet/Home/issues/2628)

* Performans - birden çok proje işlemleri için önbellek bağımlılık bilgi - [#2619](https://github.com/NuGet/Home/issues/2619)

* Sorunu düzeltmek kaynak listesi boşken - paket kaynaklarını adlı ayarlarından eklenmesi burada [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cepheleri üzerinde - bağlıdır paketini yüklemeye çalışırken Misleading hatayı düzeltmek [#2594](https://github.com/NuGet/Home/issues/2594)

* Bir paketi "Tümü" ayar PackageManager konsolundan yükleme çalışır yalnızca ilk kaynak - [#2557](https://github.com/NuGet/Home/issues/2557)

* Gelecekte yazma sürelerine sahip (Mono) - dosyalarınız paketlerle ilgili sorunları giderme [#2518](https://github.com/NuGet/Home/issues/2518)

* Güncelleştirme komutunda - bulma projeleri bir hata olduğunda özel durumu görüntülemek [#2418](https://github.com/NuGet/Home/issues/2418)

* Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 +'dan yükleme bağımsız değişkeniyle akış zaman - NoCache paketi içeriyorsa `.nupkg` dosyaları - [#2354](https://github.com/NuGet/Home/issues/2354)

* Düzeltme sorunu paketini yükleyin (tüm kaynakları) paket 1 kaynağından - eksik olduğunda [#2322](https://github.com/NuGet/Home/issues/2322)

* Tek bir kaynak yetkilendirme - blokları yükleyin [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`Aralık - IncludeReferencedProjects sürümü - geçersiz kıl sürüm [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource için" - göreli dosya yolu ile ilgili sorunları giderme [#1746](https://github.com/NuGet/Home/issues/1746)

* Güncelleştirme çözümleyici hata iletileri - artırmak [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Özellikler ve davranış değişiklikleri

* nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)

* değil nuget.exe geri yükleme üretmek `.props` ve `.targets` dosyalarını `.nuproj` projeleri (v3.4.3.855 gerileme) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Genişletilebilirlik API içeri aktarmalar - çerçeveleri karşılaştırmak için gereken [#2633](https://github.com/NuGet/Home/issues/2633)

* Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Ayrıntılı bir çıkış - nuget.exe sürüm üstbilgisinde çıkışı yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet {RID} /runtimes/ /nativeassets/ {txm} için destek eklemek / - [#2782](https://github.com/NuGet/Home/issues/2782)