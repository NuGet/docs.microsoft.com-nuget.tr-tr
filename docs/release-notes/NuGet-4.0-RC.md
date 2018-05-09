---
title: NuGet 4.0 RC sürüm notları
description: NuGet 4.0 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC sürüm notları

[NuGet 3.5 RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC için Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) .NET Core senaryolar için destek ekleyerek, başlıca müşteri geri bildirimlerine adresleme ve çeşitli senaryolarda performansı iyileştirme odaklanmıştır. Bu sürüm, NuGet MSBuild hedefleri, arka plan paket geri yükleme ve daha fazlasını komutları PackageReference, desteği gibi çeşitli iyileştirmeler getirir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

- Davranış değişiklikleri `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- makine "15" yalnızca vs nuget.exe geri yükleme başarısız - [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore dosya yeni proje geri yükleme sırasında - yapı engelleme [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET Core web uygulaması, VS "15", geri yükleyemedi VS2015 geçirildi. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Test hatası] Paket 'jQuery doğrulama' PM UI tarafından - kaldırılamıyor [#3755](https://github.com/NuGet/Home/issues/3755)

- Bir paket UWP'ye yüklü olduğunda `project.json`, üst projeleri de geri yüklenmelidir - [#3731](https://github.com/NuGet/Home/issues/3731)

- Normal - yerine yüksek ayrıntı olarak paket kaynaklarını oturum NuGet hedefleri değiştirme [#3719](https://github.com/NuGet/Home/issues/3719)

- DotNet
  - Varsayılan olarak - dotnetcore pack3 XML belgeleri içermelidir [#3698](https://github.com/NuGet/Home/issues/3698)

- Toplu güncelleştirme paketi olmadan kaynağıdır ilk ve tüm kaynak seçildiğinde - kullanıcı Arabiriminden başarısız [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget Paketi komutu tüm dosyaları - içermez [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM sorunu - [#3661](https://github.com/NuGet/Home/issues/3661)

- Varlıklar dosyasının ProjectFileDependencyGroups bölümü, kitaplık adları - projelerde kullanmalıdır [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet geri yükleme" ve dizinleri - recursing [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 hataları, uyarıları hataları - yerine olarak kaydedilir [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS sorun: "[dosya] çalışma alanında bulunan olmaması veya erişmek için izniniz yok"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Yazarak "nuget <packagename>" vs üzerinde Hızlı Başlat Arama kutusuna "nuget" öneki - tutar [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Çekirdek özellikler bölümü tanınmayan kök öğe. 2 satır, 2 konum. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` ile kaçışlı &lt; veya &gt; metin alanları artık oluşturur - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe Sil (etkileşimli olmayan modda olduğundan) kimlik bilgilerini - isteyebilir olmaz [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete uyarır yerel kaynakları için API anahtarı hakkında hiçbir - mantıklıdır olsa bile [#2625](https://github.com/NuGet/Home/issues/2625)

- EF - öncesi paket - yüklerken hata deneyimi düşük [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio kilitlendi seçimi değiştirdikten sonra çalışırken Paket Yöneticisi'nde - [#2551](https://github.com/NuGet/Home/issues/2551)

- DotNet
  - dotnetcore geri yükleme kayan sürümleri kullanıldığında - bu büyük küçük harfe duyarlı kimliği aramaları düz liste yerel depoları üzerinde gerçekleştirir [#2516](https://github.com/NuGet/Home/issues/2516)

- V2 akış için - nuget.exe delete bozulur [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe gönderme zaman aşımı gerekiyor daha iyi bir hata iletisi - [#2503](https://github.com/NuGet/Home/issues/2503)

- Aracı geri yükleme uygun olmadan sessizce başarısız alır. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet ister olduğunda özel bir akış bile nuget.org - yüklerken kimlik bilgilerini girmek için [#2346](https://github.com/NuGet/Home/issues/2346)

- Applicationınsights 2.0 Paketi listelenir, ancak henüz - yok [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay vs'de "15" preview 5 dal - [#3500](https://github.com/NuGet/Home/issues/3500)

- UWP için-derleme sırasında geri yükleme için ilk OnBuild olay eksik [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 sonları EntityFramework yüklensin mi? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Kaynağı için ayrıntılı günlük kaydı Ekle (düşünün. 3.5 için) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Nuget istemci sürümünün 3.4 + - dikkate alınır değil NoCache parametresi [#3074](https://github.com/NuGet/Home/issues/3074)

- VS üzerinde yüklemek bir kimlik bilgisi sağlayıcısı başarısız olduğunda, NuGet - kesmeyin [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Özellikler

- CI x86-çalışacak şekilde ayarlanmış [#3868](https://github.com/NuGet/Home/issues/3868)

- Otomatik geri yükleme 3/3: olmayan engelleme UI - [#3658](https://github.com/NuGet/Home/issues/3658)

- Otomatik geri yükleme 2/3: arka plan Adaylığı - geri yükleme [#3657](https://github.com/NuGet/Home/issues/3657)

- Proje başvuruları yapı davranışını (recurse) - eşleşecek şekilde geri [#3615](https://github.com/NuGet/Home/issues/3615)

- DPL destek VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Program dosyaları için - ayarları dosya taşıma [#3613](https://github.com/NuGet/Home/issues/3613)

- Oluşturulan geri yükleme özellik ve hedefleri gereksinim katılım desteği - arası hedefleme [#3496](https://github.com/NuGet/Home/issues/3496)

- PackageTargetFallback (f.k.a içeri aktarmalar) - NuGet geri yükleme desteği [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef uygulama - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID - Restore3 [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet Ekle/Kaldır/güncelleştirme PackageRefs - desteklemek için kullanıcı Arabirimi [#3457](https://github.com/NuGet/Home/issues/3457)

- : Otomatik 1/3 proje önbelleğe alma yoluyla API Adaylığı Implemenation geri bilgisi - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet geri görev & hedefleri - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] etkinleştir çözüm düzeyinde geri yükleme MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio'da - kimlik bilgisi sağlayıcısı ortak genişletilebilirlik desteği [#2909](https://github.com/NuGet/Home/issues/2909)

- Özyinelemeli nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- Gönderilemiyor Microsoft.TeamFoundation.Client dev15 yük, VS "15" için 15.0 Microsoft.TeamFoundation.Client sürüm güncellemeniz gerekiyor Önizleme - [#2392](https://github.com/NuGet/Home/issues/2392)

- Yüklenemiyor C++ pakete C++ UWP projesi VS üzerinde "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg \buildCrossTargeting\ klasör - destekler ve içeri aktarmak için gereksinim duyduğu `.targets`  /  `.props` "crosstargeting" MSBuild kapsam için. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference tasarım - [#3462](https://github.com/NuGet/Home/issues/3462)

- NuGet içinde PackageReferences ve geri yükleme desteği için kullanıcı Arabirimi düzeltme `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- VS Paket Yöneticisi ayarları - ekleme Önbelleği Temizle düğmesine [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Dcr

- Otomatik geri yükleme sürerken çözüm geri yükleme engellenmelidir. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet Paket Yöneticisi kullanıcı Arabirimi NetCore yükle yükler için paket destekleyen - olanları yerine her TFM [#3721](https://github.com/NuGet/Home/issues/3721)

- API DotNetCliToolsReferences çok desteklemesi gerekir nominator geri yükleyin. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Bizim VS "15" işaretlemek systemcomponent - olarak VSIX [#3700](https://github.com/NuGet/Home/issues/3700)

- MS başvuran geçirin. VS. MS Services.Client. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) dikkate geri yükleme ile - proje düzeyinde [#3618](https://github.com/NuGet/Home/issues/3618)

- Tek TargetFramework projeyle geri özellik - değil koşul gerekir [#3588](https://github.com/NuGet/Home/issues/3588)

- DotNet
  - dotnetcore restore3 foo.csproj projectref bağımlılıkları izleyin ve bu çok geri gerekir. Yapı gibi. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platform" bağımlılıkları temsil "türünde": kilit dosyası - "paketi" [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe ayrıntılı mod indirme Göster url - [#2629](https://github.com/NuGet/Home/issues/2629)

- NuGet xplat taşıyın Microsoft.NetCore.App ve netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - olmalıdır simge sunucusunu komut satırından - itme olduğunda geçersiz kılmanıza olanak [#2348](https://github.com/NuGet/Home/issues/2348)

- Genel bulmak için kod birleştirmek paketleri yol - [#2296](https://github.com/NuGet/Home/issues/2296)

- SuppressParent - daha iyi bir ada ihtiyacınız [#2196](https://github.com/NuGet/Home/issues/2196)

- Belirlemek `project.json` MSBuild projelerine - kullanılacak bağımlılık adı [#1914](https://github.com/NuGet/Home/issues/1914)

- SemVer 2.0.0 desteği eklemek için NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Geçişli bağımlılık NuPkgs izin ile `.targets` Msbuild'de - kullanılabilir olması için [#3342](https://github.com/NuGet/Home/issues/3342)

- Komut satırı NuGet geri VS - önemli ölçüde daha yavaş [#3330](https://github.com/NuGet/Home/issues/3330)

- Paket Kimliğini ve sürümünü karşılaştırmayı büyük küçük harfe duyarlı - yapmak [#2522](https://github.com/NuGet/Home/issues/2522)

- İçin NoCache seçeneği çalışmıyor `packages.config` tabanlı geri yükleme/yüklemeye (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource kaynakları gereken bir varsayılan önbellek içeriği ve Günlükçü - [#1357](https://github.com/NuGet/Home/issues/1357)
