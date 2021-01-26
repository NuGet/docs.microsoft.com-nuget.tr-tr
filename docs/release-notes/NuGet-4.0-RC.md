---
title: NuGet 4,0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,0 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780187"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4,0 RC sürüm notları

[NuGet 3,5 RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)

[Visual Studio 2017 Için NuGet 4,0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0) , .NET Core senaryoları için destek eklemeye, önemli müşteri geri bildirimlerine adresleme ve çeşitli senaryolarda performansı iyileştirmeye odaklanmıştır. Bu sürüm, PackageReference için destek, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yükleme ve daha fazlası gibi çeşitli geliştirmeler sunar.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

- #3838 davranış değişiklikleri `dotnet pack --version-suffix foo`  -  [](https://github.com/NuGet/Home/issues/3838)

- Vs "15" makinesinde geri yükleme nuget.exe başarısız oldu- [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore dosyası yeni proje geri yükleme sırasında derlemeyi engellemelidir- [#3780](https://github.com/NuGet/Home/issues/3780)

- VS2015 öğesinden VS "15" öğesine geçirilen Web uygulaması ASP.NET Core geri yüklenemiyor. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Test hatası] ' JQuery doğrulaması ' paketi PM Kullanıcı arabirimi tarafından kaldırılamaz- [#3755](https://github.com/NuGet/Home/issues/3755)

- UWP 'ye bir paket yüklendiğinde `project.json` , üst projelerin de geri yüklenmesi gerekir [#3731](https://github.com/NuGet/Home/issues/3731)

- NuGet hedeflerini, paket kaynaklarını normal [#3719](https://github.com/NuGet/Home/issues/3719) yerine yüksek düzeyde ayrıntı olarak günlüğe kaydetmek üzere değiştirin

- dotnet
  - dotnetcore Pack3, varsayılan olarak XML belgeleri içermelidir [#3698](https://github.com/NuGet/Home/issues/3698)

- Paket olmadan kaynak ilk kez ve tüm kaynak seçildiğinde, Batch güncelleştirmesi kullanıcı arabiriminden başarısız olur [#3696](https://github.com/NuGet/Home/issues/3696)

- NuGet paketi komutu tüm dosyaları kapsamaz- [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM sorun- [#3661](https://github.com/NuGet/Home/issues/3661)

- Varlıklar dosyasının ProjectFileDependencyGroups bölümü, projeler için kitaplık adları kullanmalıdır- [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" ve yinelenen dizinler- [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 hataları hatalar yerine uyarı olarak günlüğe kaydedilir- [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS sorunu: "[dosya] çalışma alanınızda bulunamadı, ya da ona erişmek için izniniz yok"- [#2805](https://github.com/NuGet/Home/issues/2805)

- <packagename>Vs Hızlı Başlat arama kutusunda "NuGet" yazıldığında "NuGet" öneki- [#2719](https://github.com/NuGet/Home/issues/2719) kalır

- System.Xml.Xmlözel durum: çekirdek Özellikler bölümünde tanınmayan kök öğe. 2. satır, konum 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` kaçışlı &lt; veya &gt; metin alanlarında artık derleme [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe silme, kimlik bilgilerini istemez (etkileşimli olmayan modda) [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe DELETE, yerel kaynaklar için API anahtarı hakkında, hiçbir [#2625](https://github.com/NuGet/Home/issues/2625) anlamlı olmasa da

- EF-Package- [#2566](https://github.com/NuGet/Home/issues/2566) yüklenirken hata deneyimi zayıf

- Paket Yöneticisi 'nde Seçimi değiştirdikten sonra Visual Studio kilitlendi- [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore geri yükleme, kayan sürümler kullanıldığında düz liste yerel depolarında büyük/küçük harfe duyarlı kimlik aramaları gerçekleştirir- [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe DELETE, v2 akışı için bozuk [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe gönderme zaman aşımı, daha iyi bir hata iletisi gerektirir [#2503](https://github.com/NuGet/Home/issues/2503)

- Uygun içeri aktarmalar olmadan araç geri yükleme sessizce başarısız olur. - [#2462](https://github.com/NuGet/Home/issues/2462)

- Nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346) ' den yükleme sırasında bile özel akış olduğunda NuGet kimlik bilgilerini girmesi istenir

- ApplicationInsights 2,0 paketi listeleniyor ancak henüz mevcut değil- [#2317](https://github.com/NuGet/Home/issues/2317)

- Iıdelay, VS "15" Preview 5 dal- [#3500](https://github.com/NuGet/Home/issues/3500)

- UWP- [#3489](https://github.com/NuGet/Home/issues/3489) için derleme sırasında Ilk onbuild olayı geri yükleme için eksik

- PowerShell5, EntityFramework yüklemesi mi? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Kaynakları ayrıntılı günlüğe ekleme (3,5 için göz önünde bulundurun)- [#3294](https://github.com/NuGet/Home/issues/3294)

- NuGet istemci sürümü 3.4 +- [#3074](https://github.com/NuGet/Home/issues/3074) NoCache parametresi kabul edilmez

- Bir kimlik bilgisi sağlayıcısı VS 'de yükleme başarısız olduğunda, NuGet 'yi bozmayın [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Özellikler

- CI 'yi x86- [#3868](https://github.com/NuGet/Home/issues/3868) çalıştırmak için ayarlama

- Otomatik geri yükleme 3/3: engellenmeyen Kullanıcı arabirimi- [#3658](https://github.com/NuGet/Home/issues/3658)

- Otomatik geri yükleme 2/3: aday için arka planda geri yükleme- [#3657](https://github.com/NuGet/Home/issues/3657)

- Proje refs öğesini derleme davranışıyla eşleşecek şekilde geri yükleme (recurse)- [#3615](https://github.com/NuGet/Home/issues/3615)

- VS "15"-Minbar- [#3614](https://github.com/NuGet/Home/issues/3614) ile DPL desteği

- Ayarlar dosyasını program dosyalarına Taşı- [#3613](https://github.com/NuGet/Home/issues/3613)

- Oluşturulan geri yükleme props ve hedefleri için çapraz hedefleme katılım desteği gerekir- [#3496](https://github.com/NuGet/Home/issues/3496)

- PackageTargetFallback için NuGet geri yükleme desteği (f. k. a Imports)- [#3494](https://github.com/NuGet/Home/issues/3494)

- Araçları başvuru uygulama- [#3472](https://github.com/NuGet/Home/issues/3472)

- RID- [#3465](https://github.com/NuGet/Home/issues/3465) için Restore3

- PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457) ekleme/kaldırma/güncelleştirme desteği için NuGet Kullanıcı arabirimi

- Otomatik geri yükleme 1/3: proje geri yükleme bilgilerini önbelleğe alma yoluyla aday API 'nin uygulaması- [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet geri yükleme görevi & hedefleri- [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] MSBuild- [#2993](https://github.com/NuGet/Home/issues/2993) çözüm düzeyinde geri yüklemeyi etkinleştir

- Visual Studio 'da kimlik bilgisi sağlayıcısı genel genişletilebilirliği desteği- [#2909](https://github.com/NuGet/Home/issues/2909)

- Yinelemeli NuGet geri yükleme- [#2533](https://github.com/NuGet/Home/issues/2533)

- Microsoft. TeamFoundation. Client dev15 üzerinde yüklenemiyor, VS "15" Preview- [#2392](https://github.com/NuGet/Home/issues/2392) için Microsoft. TeamFoundation. client sürümünün 15,0 olarak güncelleştirilmesi gerekiyor

- C++ paketi, VS "15" Preview- [#2369](https://github.com/NuGet/Home/issues/2369) ' de c++ UWP projesine yüklenemiyor

- Nupkg 'ın \buildnel stargeting\ Folder 'ı desteklemesi ve `.targets`  /  `.props` "çapraz başlangıç" MSBuild kapsamı için içeri aktarılması gerekir. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Araçları başvuru tasarımı- [#3462](https://github.com/NuGet/Home/issues/3462)

- NuGet Kullanıcı arabirimini, #3455 geri yüklemeyi/packagereferlenimleri destekleyecek şekilde düzeltir `.csproj`  -  [](https://github.com/NuGet/Home/issues/3455)

- VS Paket Yöneticisi ayarlarına önbellek temizle düğmesi ekleme- [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- Otomatik geri yükleme gerçekleşirken çözüm geri yüklemesi engellenmelidir. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NuGet Paket Yöneticisi kullanıcı arabiriminden NetCore yüklemesi, paketin destekleyenler yerine her TFı 'ye yüklenir- [#3721](https://github.com/NuGet/Home/issues/3721)

- Nominator API 'sini geri yükleme, Dotnetclienaraçları 'nın da başvurularını desteklemesi için gereklidir. - [#3702](https://github.com/NuGet/Home/issues/3702)

- VS "15" VSIX 'i bir SystemComponent olarak işaretleyin- [#3700](https://github.com/NuGet/Home/issues/3700)

- Başvuruda bulunan MS 'den geçiş. Anlara. Services. Client-MS. Anlara. Services. Client. Interactive- [#3670](https://github.com/NuGet/Home/issues/3670)

- $ (RestoreLegacyPackagesDirectory), restore- [#3618](https://github.com/NuGet/Home/issues/3618) tarafından bir proje düzeyinde dikkate alınmalıdır

- Tek TargetFramework ile projeye geri yükleme koşul props- [#3588](https://github.com/NuGet/Home/issues/3588) olmamalıdır

- dotnet
  - dotnetcore restore3 foo. csproj, projectref bağımlılıklarını izlemelidir ve bunları geri yükler. Yapı gibi. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "tür": "Platform" bağımlılıkları, kilit dosyasında "tür": "Package" olarak temsil edilir- [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe verbose modu indirme URL 'sini göstermelidir- [#2629](https://github.com/NuGet/Home/issues/2629)

- NuGet xplat 'yi Microsoft. NetCore. App ve netcoreapp 1.0 'a taşıyın- [#2483](https://github.com/NuGet/Home/issues/2483)

- Gönderim- [#2348](https://github.com/NuGet/Home/issues/2348) komut satırından gönderilirken sembol sunucusunu geçersiz kılmak mümkün olmalıdır

- Genel paket yolunu bulmak için kodu birleştirme- [#2296](https://github.com/NuGet/Home/issues/2296)

- SuppressParent- [#2196](https://github.com/NuGet/Home/issues/2196) daha iyi bir ad gerekiyor

- `project.json`MSBuild projeleri için kullanılacak bağımlılık adını belirle- [#1914](https://github.com/NuGet/Home/issues/1914)

- NuGet. Core- [#3383](https://github.com/NuGet/Home/issues/3383) semver 2.0.0 desteği ekleyin

- MSBuild 'de kullanılabilir olan geçişli bağımlılık NuPkgs 'e izin ver `.targets` [#3342](https://github.com/NuGet/Home/issues/3342)

- Komut satırında NuGet geri yükleme, VS- [#3330](https://github.com/NuGet/Home/issues/3330) göre önemli ölçüde yavaştır

- Paket KIMLIĞI ve sürümü karşılaştırma büyük/küçük harfe duyarsız- [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache seçeneği `packages.config` tabanlı geri yükleme/yükleme (GlobalPackagesFolder) için çalışmıyor- [#1406](https://github.com/NuGet/Home/issues/1406)

- Findpackagebyıdresource kaynakları için varsayılan önbellek bağlamı ve günlükçü- [#1357](https://github.com/NuGet/Home/issues/1357) gerekir
