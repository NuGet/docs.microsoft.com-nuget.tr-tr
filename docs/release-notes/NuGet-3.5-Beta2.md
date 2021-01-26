---
title: 3,5 beta2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 Beta 2 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776388"
---
# <a name="nuget-35-beta2-release-notes"></a>NuGet 3,5 beta2 sürüm notları

[NuGet 3,5-Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)  |  [NuGet 3,5-RC sürüm notları](../release-notes/nuget-3.5-RC.md)

NuGet 3,5 Beta 2 RTM, Visual Studio 2013 ve nuget.exe için 27 Haziran 2016 ' de yayımlandı

[Tam changelog](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Sorun listesi](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Kimlik doğrulamalı akışlar için .NET Core 'da parola azaltma desteği nedeniyle hata iletisi güncelleştirildi- [#2942](https://github.com/NuGet/Home/issues/2942)

* .NET Core projesi açık ise, Paket Yöneticisi konsolu Get-Package başarısız olur [#2932](https://github.com/NuGet/Home/issues/2932)

* NuGet Push komutu [#2910](https://github.com/NuGet/Home/issues/2910) 403 yanlış işlemesini düzeltir

* Disablesourcecontrolintefinto değeri true olarak ayarlandığında TFS kaynak denetimine yönelik bir çözümde paket kaldırma sorunlarını giderin. [#2739](https://github.com/NuGet/Home/issues/2739)

* Paket güncelleştirmesini, hedef olmayan paketleri hesaba alacak şekilde onarma- [#2724](https://github.com/NuGet/Home/issues/2724)

* NuGet Paket Yöneticisi Kullanıcı Arabirimi eylemleri için günlükçü düzeyini ayarlamak için MSBuild ayrıntı düzeyi 'ni kullanın- [#2705](https://github.com/NuGet/Home/issues/2705)

* NuGet yapılandırmasını onarma Web sitesi projelerinde geçersiz hata-VS 2015 VSıX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* `.csproj`İçerik dosyaları dahil edildiğinde paket sorunlarını giderin- [#2658](https://github.com/NuGet/Home/issues/2658)

* () İçindeki DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` çalışmıyor- [#2653](https://github.com/NuGet/Home/issues/2653)

* NuGet 3.4.3 sürümündeki sorunu giderme-değer paket oluşturma sırasında null olamaz- [#2648](https://github.com/NuGet/Home/issues/2648)

* Restore, VSTS akışları için Nuget.Config depolanan kimlik bilgilerini kullanır- [#2647](https://github.com/NuGet/Home/issues/2647)

* Performans-sürüm karşılaştırmalarının çok fazla ayırmasını düzeltir- [#2632](https://github.com/NuGet/Home/issues/2632)

* Birden çok nuget.exe örneği paralel [#2628](https://github.com/NuGet/Home/issues/2628) aynı paketi yüklemeye çalıştığında oluşan sorunları giderin

* Çok projeli işlemler için performans önbelleği bağımlılık bilgileri- [#2619](https://github.com/NuGet/Home/issues/2619)

* Kaynak listesi boş olduğunda paket kaynaklarının ayarlardan eklenebileceği sorunu çözme- [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cephe 'e bağlı paketi yüklemeye çalışırken yanıltıcı hatası giderme- [#2594](https://github.com/NuGet/Home/issues/2594)

* PackageManager konsolundan paket yükleme "All" ayarı yalnızca ilk kaynak- [#2557](https://github.com/NuGet/Home/issues/2557) çalışır

* Gelecekte yazma süreleriyle dosyaları olan paketlerle ilgili sorunları giderin (mono) [#2518](https://github.com/NuGet/Home/issues/2518)

* Güncelleştirme komutunda projeleri bulmada hata olduğunda özel durum görüntüle- [#2418](https://github.com/NuGet/Home/issues/2418)

* Paket dosyaları içerdiğinde-NoCache bağımsız değişkenine sahip bir NuGet v 3.3 + akışından bir paket yüklenirken paket içeriği doğru şekilde geri yüklenmedi `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)

* Paket, 1 kaynak üzerinde eksik olduğunda paket yüklemesi (tüm kaynaklar) ile ilgili sorunu giderme [#2322](https://github.com/NuGet/Home/issues/2322)

* Tek bir kaynak yetkilendirme başarısız olursa blokları yükler- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` sürüm aralığı geçersiz kılınmalıdır-ınclukıd proje sürümü- [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe güncelleştirme, bütünleştirilmiş kod tanımlayıcı adı ve Private özniteliği bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" için göreli dosya yoluyla sorunları giderin- [#1746](https://github.com/NuGet/Home/issues/1746)

* Güncelleştirme Çözümleyicisi hata iletilerini geliştirme- [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Özellikler ve davranış değişiklikleri

* nuget.exe Push-timeout parametresi çalışmıyor- [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe geri yükleme `.props` , `.targets` projeler için dosya oluşturmaz ve dosyalar `.nuproj` (v 3.4.3.855 'de gerileme)- [#2711](https://github.com/NuGet/Home/issues/2711)

* Çerçeveleri içeri aktarmaları ile karşılaştırmak için genişletilebilirlik API 'SI gerekir- [#2633](https://github.com/NuGet/Home/issues/2633)

* #2486 kullanırken bağımlılık seçeneklerini gizle `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* Ayrıntılı çıkışta nuget.exe sürüm üst bilgisini Yazdır- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet/Runtimes/{lar}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782) için destek eklemesi gerekir