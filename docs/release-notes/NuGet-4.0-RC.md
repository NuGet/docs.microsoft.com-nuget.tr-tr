---
title: NuGet 4.0 RC Yayın Notları
description: Bilinen sorunları, hata düzeltmeleri, eklenen özellikler ve DCR'leri içeren NuGet 4.0 RC için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496637"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC Yayın Notları

[NuGet 3.5 RTM Yayın Notları](../release-notes/nuget-3.5-RTM.md)

[Visual Studio 2017 için NuGet 4.0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0) ,NET Core senaryoları için destek eklemeye, önemli müşteri geri bildirimlerini ele almaya ve çeşitli senaryolarda performansı artırmaya odaklanmıştır. Bu sürüm PackageReference desteği, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yükleme ve daha fazlası gibi çeşitli iyileştirmeler getiriyor.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

- `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838) davranış değişiklikleri

- nuget.exe geri yükleme vs "15" makine sadece başarısız olur - [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore dosya yeni proje geri yükleme sırasında yapı engellemelidir - [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET Core web uygulaması, VS2015'ten VS "15"e geçti, geri yüklenememiştir. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Test Hatası] Paket 'jQuery Doğrulama' PM UI tarafından kaldırılamaz - [#3755](https://github.com/NuGet/Home/issues/3755)

- Bir paket UWP'ye `project.json`yüklendiğinde, ana projeler de geri yüklenmelidir - [#3731](https://github.com/NuGet/Home/issues/3731)

- Paket kaynaklarını Normal yerine Yüksek ayrıntılı olarak günlüğe kaydetmek için NuGet hedeflerini [değiştirin](https://github.com/NuGet/Home/issues/3719) - #3719

- dotnet
  - dotnetcore pack3 varsayılan olarak XML belgeleri içermelidir - [#3698](https://github.com/NuGet/Home/issues/3698)

- Paket olmadan kaynak ilk ve Tüm kaynak seçildiğinde Toplu İşlem Kullanıcı Tarafından başarısız olur - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget paketi komutu tüm dosyaları içermez - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM sorunu - [#3661](https://github.com/NuGet/Home/issues/3661)

- Varlıklar dosyasının ProjectFileDependencyGroups bölümü projeler için kitaplık adlarını kullanmalıdır - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet geri yükleme" ve özgünlükleri yineleme - [#3517](https://github.com/NuGet/Home/issues/3517)

- Geri yükleme3 hataları hata yerine uyarı olarak günlüğe kaydedilir - [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS sorunu: "[dosya]çalışma alanınızda bulunmuyor veya erişim izniniz yok" - [#2805](https://github.com/NuGet/Home/issues/2805)

- Vs quicklaunch <packagename>arama kutusunda "nuget" yazmak "nuget" öneki tutar - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Çekirdek Özellikleri bölümünde tanınmayan kök öğesi. Satır 2, pozisyon 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec`kaçan &lt; veya &gt; metin alanlarında artık oluşturur - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe silme kimlik bilgileri için istinamaz (etkileşimli olmayan modda) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe silme hiçbir mantıklı olsa bile, yerel kaynaklar için API Key hakkında uyarır - [#2625](https://github.com/NuGet/Home/issues/2625)

- EF -pre paketi yüklerken hata deneyimi zayıf - [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio Paket Yöneticisi seçimi değiştirdikten sonra çalışırken çöktü - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore geri yükleme kayan sürümleri kullanıldığında düz liste yerel depolarda durumda duyarlı Id aramaları gerçekleştirir - [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe silme V2 beslemesi için bozuldu - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe push zaman aşımı daha iyi bir hata iletisi ihtiyacı - [#2503](https://github.com/NuGet/Home/issues/2503)

- Uygun içeri aktarımlar olmadan araç geri yükleme sessizce başarısız olur. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet, nuget.org yükleme yaparken bile özel bir besleme olduğunda [#2346](https://github.com/NuGet/Home/issues/2346) kimlik bilgilerini girmek için #2346

- ApplicationInsights 2.0 paketi listelenir ancak henüz yok - [#2317](https://github.com/NuGet/Home/issues/2317)

- Vs "15" önizleme 5 şube de UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)

- İlk OnBuild olay UWP için Build sırasında Geri Yükleme için cevapsız - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 EntityFramework yüklemek tatili? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Ayrıntılı günlüğe kaynak ekleyin (3,5 için düşünün) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Nuget istemci sürümünde onurlandırılmayan NoCache parametresi 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)

- Bir kimlik bilgisi sağlayıcısı VS yüklemek için başarısız olduğunda, NuGet kırmak yok - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Özellikler

- X86 çalıştırmak için CI ayarlayın - [#3868](https://github.com/NuGet/Home/issues/3868)

- Otomatik Geri Yükleme 3/3: non engelleme Kullanıcı BiruAr - [#3658](https://github.com/NuGet/Home/issues/3658)

- Otomatik Geri Yükleme 2/3: adaylık arka plan geri yükleme - [#3657](https://github.com/NuGet/Home/issues/3657)

- Yapı davranışıyla eşleşecek şekilde proje hakemlerini geri yükleme (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15" DPL desteği - minber - [#3614](https://github.com/NuGet/Home/issues/3614)

- Ayarlar dosyasını Program Dosyaları'na taşıma - [#3613](https://github.com/NuGet/Home/issues/3613)

- Oluşturulan geri yükleme sahne ve hedefleri çapraz hedefleme katılım desteği gerekir - [#3496](https://github.com/NuGet/Home/issues/3496)

- NuGet Geri Destek PackageTargetFallback (f.k.a İthalat) için - [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef uygulaması - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID için Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet UI Paketi'nin Ekle/Kaldır/Güncellenisini destekleyecek - [#3457](https://github.com/NuGet/Home/issues/3457)

- Otomatik Geri Yükleme 1/3: Önbelleğe Alma Projesi Geri Yükleme Bilgileri ile Adaylık API Implemenation - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet Geri Yükleme Görev & Hedefleri - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] MSBuild'te Çözüm düzeyi geri yüklemesini etkinleştir - [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio'da kamu genişletilebilirliğini destekle - [#2909](https://github.com/NuGet/Home/issues/2909)

- Özyinelemeli nuget geri yükleme - [#2533](https://github.com/NuGet/Home/issues/2533)

- Microsoft.TeamFoundation.Client'ı dev15'e yükleyemiyorum, Microsoft.TeamFoundation.Client sürümünü VS "15" Önizlemeiçin 15.0 olarak güncelleştirmeli - [#2392](https://github.com/NuGet/Home/issues/2392)

- VS "15" Preview'da C++ UWP projesine C++ paketi yükleneme - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg \buildCrossTargeting\ klasörünü desteklemesi `.targets`  /  `.props` ve MSBuild kapsamını "çapraz hedefleme" için içe aktarması gerekir. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)

- `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455) w/ PackageReferences geri yüklemek için NuGet UI düzeltin

- VS paket yöneticisi ayarlarına net önbellek düğmesi ekleme - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCRs

- Otomatik geri yükleme olurken Çözüm Geri Yükleme engellenmelidir. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet Paket Yöneticisi UI netcore yüklemek her TFM yükler , yerine paket destekler olanlar - [#3721](https://github.com/NuGet/Home/issues/3721)

- Geri nominator API dotNetCliToolsReferences çok desteklemesi gerekir. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Vs "15" vsix'imizi bir sistem bileşeni olarak [işaretleyin](https://github.com/NuGet/Home/issues/3700) - #3700

- MS'e başvurudan geçirin. Vs. Services.Client - MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) geri yükleyerek bir proje düzeyinde saygı gösterilmelidir - [#3618](https://github.com/NuGet/Home/issues/3618)

- Tek bir TargetFramework ile projeye geri yükleme, sahne koşullandırmamalıdır - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj projectref bağımlılıkları takip etmeli ve bu da geri yükleyin. İnşa etmek gibi. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": Kilit dosyasında "type":"package" olarak temsil edilen "platform" [Bağımlılıkları](https://github.com/NuGet/Home/issues/2695) - #2695

- nuget.exe Verbose modu indirme url göstermelidir - [#2629](https://github.com/NuGet/Home/issues/2629)

- Move NuGet xplat Microsoft.NetCore.App ve netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- İtme - Komut satırından iterken sembol sunucusugeçersiz kılmak mümkün olmalıdır - [#2348](https://github.com/NuGet/Home/issues/2348)

- Küresel paketler yolunu bulmak için kodu birleştirin - [#2296](https://github.com/NuGet/Home/issues/2296)

- SuppressParent daha iyi bir ada ihtiyacınız var - [#2196](https://github.com/NuGet/Home/issues/2196)

- MSBuild projeleri için kullanılacak bağımlılık adını belirleme `project.json` - [#1914](https://github.com/NuGet/Home/issues/1914)

- NuGet.Core'a SemVer 2.0.0 desteği ekle - [#3383](https://github.com/NuGet/Home/issues/3383)

- MSBuild'te kullanılabilir geçişli bağımlılık `.targets` NuPkg'larına izin verin - [#3342](https://github.com/NuGet/Home/issues/3342)

- NuGet komut satırından geri yükleme VS'den önemli ölçüde daha yavaştır - [#3330](https://github.com/NuGet/Home/issues/3330)

- Paket kimliği ve sürüm karşılaştırma örneği duyarsız olun - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache seçeneği tabanlı `packages.config` geri yükleme/yükleme (GlobalPackagesFolder) için çalışmıyor - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource kaynakları varsayılan önbellek bağlamı ve logger gerekir - [#1357](https://github.com/NuGet/Home/issues/1357)
