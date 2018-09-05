---
title: NuGet 4.0 RC sürüm notları
description: NuGet 4.0 RC bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549252"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC sürüm notları

[NuGet 3.5 RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)

[Visual Studio 2017 için NuGet 4.0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0) .NET Core senaryolarına destek ekleme, başlıca müşteri geri adresleme ve çeşitli senaryoları performans iyileştirme odaklanmıştır. Bu sürüm, NuGet MSBuild hedefleri, arka planda paket geri yükleme ve diğer komutları PackageReference, desteği gibi çeşitli iyileştirmeler getirir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

- Davranış değişiklikleri `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- nuget.exe vs "15" makine yalnızca geri yükleme başarısız - [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore dosya yeni proje derleme sırasında geri yükleme - block [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET Core web uygulaması, geçirilen VS2015 ' VS "15", geri yükleyemedi. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Test hatası] Paket 'jQuery doğrulaması' PM UI tarafından - kaldırılamıyor [#3755](https://github.com/NuGet/Home/issues/3755)

- Bir paket için UWP yüklü olduğunda `project.json`, üst projeleri aynı zamanda geri yüklenmelidir - [#3731](https://github.com/NuGet/Home/issues/3731)

- NuGet hedefleri olarak yüksek ayrıntı yerine Normal - paket kaynaklarını oturum değiştirme [#3719](https://github.com/NuGet/Home/issues/3719)

- DotNet
  - Varsayılan olarak - dotnetcore pack3 XML belgeleri içermelidir [#3698](https://github.com/NuGet/Home/issues/3698)

- Toplu güncelleştirme başarısız kullanıcı Arabiriminden kaynak paketi olmadan ilk ve tüm kaynak seçildiğinde - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget Paketi komutu tüm dosyaları - içermez [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM sorunu - [#3661](https://github.com/NuGet/Home/issues/3661)

- Varlıklar dosyasının ProjectFileDependencyGroups bölümü, kitaplık adlarını projeler - kullanmalıdır [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" ve dizinleri - recursing [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 hataları hatası - uyarı olarak kaydedilir [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS sorunu: "[file] çalışma alanınızda bulunan olmaması ya da ona erişmek için izniniz yok"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Yazarak "nuget <packagename>" vs'de hızlı arama kutusuna "nuget" ön eki - tutar [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Çekirdek özellikleri bölümünde tanınmayan kök öğe. 2 satır, 2 konum. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` ile kaçış &lt; veya &gt; metin alanları artık derlenmiyor - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete (etkileşimli olmayan modda olduğundan) kimlik bilgileri - istemi olmayacaktır [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete uyarır yerel kaynakları için API anahtarı hakkında hiçbir - mantıklıdır olsa bile [#2625](https://github.com/NuGet/Home/issues/2625)

- EF pre - package - yüklerken hata deneyimi düşük [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio kilitlendi seçimi değiştirdikten sonra çalışan Paket Yöneticisi'nde - [#2551](https://github.com/NuGet/Home/issues/2551)

- DotNet
  - dotnetcore geri yükleme kayan sürümleri kullanıldığında - bu kimliği büyük küçük harfe duyarlı aramalar düz liste yerel depolarda gerçekleştirir [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe delete V2 akışı için - bozulur [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe gönderme zaman aşımı gerekiyor daha iyi hata iletisi - [#2503](https://github.com/NuGet/Home/issues/2503)

- Aracı geri uygun olmadan sessizce başarısız içeri aktarır. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet olduğunda özel bir akış nuget.org adresinden - yüklerken bile kimlik bilgilerini girmek için istemleri [#2346](https://github.com/NuGet/Home/issues/2346)

- Applicationınsights 2.0 paket listelenir, ancak henüz - mevcut olmayan [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay VS "15" preview 5 dal - [#3500](https://github.com/NuGet/Home/issues/3500)

- İlk Onbuıld olay UWP için-derleme sırasında geri yüklemek için eksik [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 sonları EntityFramework yüklensin mi? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Ayrıntılı günlük kaydı için kaynak ekleme (düşünün. 3.5 için) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Nuget istemci sürümünde 3.4 + - kabul değil NoCache parametre [#3074](https://github.com/NuGet/Home/issues/3074)

- VS'de yüklemek bir kimlik bilgisi sağlayıcı başarısız olduğunda, NuGet - bölme [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Özellikler

- CI'yi kurma x86-çalıştırmak için ayarlanmış [#3868](https://github.com/NuGet/Home/issues/3868)

- Otomatik geri 3/3: kullanıcı Arabirimi olmayan engelleme - [#3658](https://github.com/NuGet/Home/issues/3658)

- Otomatik geri 2/3: arka plan ADAYLIK - geri yükleme [#3657](https://github.com/NuGet/Home/issues/3657)

- Proje başvuruları derleme davranışı (recurse) - eşleşecek şekilde geri [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15" - minbar - DPL Destek [#3614](https://github.com/NuGet/Home/issues/3614)

- Program dosyaları için - ayarları dosya taşıma [#3613](https://github.com/NuGet/Home/issues/3613)

- Oluşturulan geri yükleme özellikler ve hedefler gereksinim katılım desteği - çapraz hedefleme [#3496](https://github.com/NuGet/Home/issues/3496)

- Csproj'daki (f.k.a Imports) - NuGet geri yükleme desteği [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef uygulama - [#3472](https://github.com/NuGet/Home/issues/3472)

- Bir RID için-Restore3 [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet ekleme/kaldırma/güncelleştirmeye PackageRefs - desteklemek için kullanıcı Arabirimi [#3457](https://github.com/NuGet/Home/issues/3457)

- : Otomatik 1/3 proje önbelleğe alma ile API ADAYLIK, Implemenation geri bilgisi - [#3456](https://github.com/NuGet/Home/issues/3456)

- Görev & hedeflerini - [0] NuGet geri yükleme [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] etkin çözüm düzeyinde geri yükleme - msbuild'de [#2993](https://github.com/NuGet/Home/issues/2993)

- Visual Studio'da - kimlik bilgisi sağlayıcısı genel genişletilebilirlik desteği [#2909](https://github.com/NuGet/Home/issues/2909)

- Özyinelemeli nuget geri yükleme - [#2533](https://github.com/NuGet/Home/issues/2533)

- Gönderilemiyor Microsoft.TeamFoundation.Client dev15 üzerinde yük, Microsoft.TeamFoundation.Client sürüm 15.0 için VS "15" için güncelleştirmeniz gerekiyor Önizleme - [#2392](https://github.com/NuGet/Home/issues/2392)

- Yüklenemiyor C++ paketi C++ UWP projesi VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg \buildCrossTargeting\ klasörü - desteklemek ve içeri aktarma için gereksinim duyduğu `.targets`  /  `.props` "crosstargeting" MSBuild kapsam için. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference tasarım - [#3462](https://github.com/NuGet/Home/issues/3462)

- NuGet PackageReferences içinde ile geri yüklemeyi desteklemek için kullanıcı Arabirimi düzeltme `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- VS Paket Yöneticisi ayarları - ekleyerek Önbelleği Temizle düğmesine [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Dcr

- Çözüm geri yükleme, otomatik yükleme gerçekleşirken engellenmelidir. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet Paket Yöneticisi UI NetCore yükle yükler için paket destekleyen - olanları yerine her TFM [#3721](https://github.com/NuGet/Home/issues/3721)

- Geri yükleme aday API DotNetCliToolsReferences çok desteklemesi gerekir. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Bizim VS "15" işaretlemek bir systemcomponent - olarak VSIX [#3700](https://github.com/NuGet/Home/issues/3700)

- MS başvuran dan geçirin. VS. Services.Client ile MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) dikkate tarafından geri yükleme - proje düzeyinde [#3618](https://github.com/NuGet/Home/issues/3618)

- Geri yükleme ile tek TargetFramework Project özellikler - değil koşul gerekir [#3588](https://github.com/NuGet/Home/issues/3588)

- DotNet
  - dotnetcore restore3 foo.csproj projectref bağımlılıkları izleyin ve bunlar çok geri gerekir. Derleme gibi. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platformu" bağımlılıklar "türü olarak" gösterilen: kilit dosyası - "paketi" [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe ayrıntılı modu indirme göstermelidir adresa url – [#2629](https://github.com/NuGet/Home/issues/2629)

- NuGet xplat taşıyın Microsoft.NetCore.App ve netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - olmalıdır komut satırından - gönderirken sembol sunucusu geçersiz kılmak olası [#2348](https://github.com/NuGet/Home/issues/2348)

- Genel bulmak için kod birleştirme paketleri yol - [#2296](https://github.com/NuGet/Home/issues/2296)

- SuppressParent - daha iyi bir ada ihtiyacınız [#2196](https://github.com/NuGet/Home/issues/2196)

- Belirlemek `project.json` MSBuild projeleri için - kullanılacak bağımlılık adı [#1914](https://github.com/NuGet/Home/issues/1914)

- NuGet.Core için - SemVer 2.0.0 desteği ekleme [#3383](https://github.com/NuGet/Home/issues/3383)

- Geçişli bağımlılık NuPkgs izin ile `.targets` Msbuild'de - kullanılabilir olmasını [#3342](https://github.com/NuGet/Home/issues/3342)

- Komut satırı NuGet geri yükleme - VS önemli ölçüde yavaş [#3330](https://github.com/NuGet/Home/issues/3330)

- Paket kimliği ve sürüm karşılaştırma büyük/küçük harfe duyarsız - olun [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache seçeneği için çalışmaz `packages.config` geri yükleme/yükleme (GlobalPackagesFolder) - temel [#1406](https://github.com/NuGet/Home/issues/1406)

- Varsayılan önbellek içeriği ve Günlükçü - ihtiyacı FindPackageByIdResource kaynakları [#1357](https://github.com/NuGet/Home/issues/1357)
