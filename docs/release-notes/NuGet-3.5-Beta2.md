---
title: 3.5 Beta2 sürüm notları
description: NuGet 3.5 Beta 2 bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551997"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3.5 Beta2 sürüm notları

[NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM'ye 27 Haziran 2016'dan Visual Studio 2013 ve nuget.exe için yayımlanan

[Tam bir Changelog](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Sorun listesi](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Güncelleştirilmiş hata iletisi için kimliği doğrulanmış akışları için-parola decrpytion .NET core'da desteğinin [#2942](https://github.com/NuGet/Home/issues/2942)

* Paket Yöneticisi konsolu Get-Package, .NET Core projesi açıksa - başarısız [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet anında iletme komutu yanlış işlenmesini 403 düzeltme [#2910](https://github.com/NuGet/Home/issues/2910)

* DisableSourceControlIntegration ayarlandığında TFS kaynak denetimine bağımlı bir çözümdeki paketler kaldırma sorunlarını gidermek true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Paket güncelleştirme hesabı olmayan hedef paketlere - gerçekleştirilecek düzeltme [#2724](https://github.com/NuGet/Home/issues/2724)

* MSBuild ayrıntı düzeyi UI eylemlerini - Nuget Paket Yöneticisi Günlükçü düzeyini ayarlamak için kullanın [#2705](https://github.com/NuGet/Home/issues/2705)

* Düzeltme NuGet yapılandırmadır geçersiz hata - VS 2015 VSIX (v3.4.3) - Web sitesi projelerinde [#2667](https://github.com/NuGet/Home/issues/2667)

* Paketi sorunları düzeltmek `.csproj` içerik dosyalarını eklendiğinde - [#2658](https://github.com/NuGet/Home/issues/2658)

* İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) işe yaramazsa - [#2653](https://github.com/NuGet/Home/issues/2653)

* -Değer üzerinde paket oluşturma null olamaz - Nuget 3.4.3 sürümde sorunu [#2648](https://github.com/NuGet/Home/issues/2648)

* Geri yükleme için VSTS akışlarındaki - Nuget.Config depolanan kimlik bilgilerini kullanan [#2647](https://github.com/NuGet/Home/issues/2647)

* Performans - sürüm karşılaştırma kodu düzeltme aşırı ayırmaları - [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe birden çok örneğini çalıştığında paralel olarak - aynı paketini yüklemek sorunları giderin [#2628](https://github.com/NuGet/Home/issues/2628)

* Performans - birden çok proje işlemleri için önbellek bağımlılık bilgileri - [#2619](https://github.com/NuGet/Home/issues/2619)

* Sorunu kaynak listesi boşken - paket kaynaklarını bürünülemiyor ayarlarından eklenmesi burada [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cepheleri üzerinde - bağlıdır paket yüklemeye çalışırken Misleading hatayı düzeltmek [#2594](https://github.com/NuGet/Home/issues/2594)

* "Tüm" ayarı ile PackageManager konsolundan bir paket yükleme, yalnızca ilk kaynak - çalışır [#2557](https://github.com/NuGet/Home/issues/2557)

* (Tekli) - dosya yazma süresi, gelecekte olan paketleri ile sorunları giderin [#2518](https://github.com/NuGet/Home/issues/2518)

* Güncelleştirme komutunda - bulma projeleri bir hata olduğunda özel durum görüntüleme [#2418](https://github.com/NuGet/Home/issues/2418)

* Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 + yükleme bağımsız değişkeniyle akışı güncelleştirildiğinde - NoCache paketi içeriyorsa `.nupkg` dosyalar - [#2354](https://github.com/NuGet/Home/issues/2354)

* Düzeltme paketi sorun yükleyin (tüm kaynakları) 1 kaynağından - paket eksik olduğunda [#2322](https://github.com/NuGet/Home/issues/2322)

* Tek bir kaynak yetkilendirme - başarısız olursa blokları yükleme [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Sürüm - IncludeReferencedProjects sürüm - aralık geçersiz kılmalıdır [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 güncelleştirmesi başarısız ' bir ek kısıtlama... tanımlanan packages.config bu işlemi engeller.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource için" - göreli dosya yolu ile sorunları giderin [#1746](https://github.com/NuGet/Home/issues/1746)

* Güncelleştirme çözümleyici hata iletileri - geliştirmek [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Özellikler ve davranışı değişiklikleri

* nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe geri yükleme değil üretmek `.props` ve `.targets` dosyaları `.nuproj` projeleri (gerileme v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Genişletilebilirlik çerçeveleri içeri aktarmalar ile-karşılaştırmak için API gereken [#2633](https://github.com/NuGet/Home/issues/2633)

* Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Nuget.exe sürüm üst bilgisi içinde ayrıntılı çıkış - out yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet {RID} /runtimes/ /nativeassets/ {txm} için destek ekleme / - [#2782](https://github.com/NuGet/Home/issues/2782)