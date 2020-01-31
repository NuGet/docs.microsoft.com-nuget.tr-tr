---
title: NuGet 4,8 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4.8.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813773"
---
# <a name="nuget-48-release-notes"></a>NuGet 4,8 sürüm notları

[Visual Studio 2017 15,8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , NuGet 4,8 işlevselliğiyle birlikte gelir.


Aynı işlevselliğin komut satırı sürümleri de kullanılabilir:
* NuGet. exe 4,8- [NuGet.org/downloads](https://nuget.org/downloads)
* DotNet. exe- [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Özet: 4.8.0 'deki yenilikler
* NuGet. exe artık Windows 10 ' da LongDosya adlarını destekliyor- [#6937](https://github.com/NuGet/Home/issues/6937)
* Kimlik doğrulama eklentileri artık MsBuild, DotNet. exe, NuGet. exe ve platformlar arası dahil olmak üzere Visual Studio arasında çalışır. İlk nesil kimlik doğrulama eklentileri MsBuild, DotNet. exe ' de desteklenmez. Note: VS 2017 15,9 Önizleme derlemeleri bir VSTS kimlik doğrulama eklentisi içerir. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild 'in SDK 'Sı çözümleyici, artık NuGet 'in bir parçası olarak ve VS için NuGet araçları ile yüklenmektedir. Bu, sürümlerin eşitlemeyi önlemenize engel olur. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference artık DevelopmentDependency meta verilerini destekliyor- [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Özet: 4.8.2 'deki yenilikler

* Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>İmzalı paketleri bir CI makinesine veya çevrimdışı bir ortama yüklemek normalden daha uzun sürer

#### <a name="issue"></a>Sorun
Makinede internet erişimi kısıtlamalı (bir CI/CD senaryosunda derleme makinesi gibi), imzalı bir NuGet paketinin yüklenmesi/geri yüklenmesi, iptal sunucuları ulaşılamaz olduğundan bir uyarı ([NU3028](../reference/errors-and-warnings/nu3028.md)) sonucunu vermez. Bu beklenen bir durumdur. Ancak, bazı durumlarda bu, paket yükleme/geri yükleme normalden daha uzun sürüyor gibi istenmeyen bir gizleme olabilir.

#### <a name="workaround"></a>Geçici Çözüm
Visual Studio 15.8.4 ve NuGet. exe ' ye güncelleştirin; burada, iptal denetimi modunu değiştirmek için bir ortam değişkeni sunuyoruz.
`NUGET_CERT_REVOCATION_MODE` ortam değişkeninin `offline` olarak ayarlanması, NuGet 'in sertifikanın iptal durumunu yalnızca önbelleğe alınmış sertifika iptal listesine karşı denetlemesini zorlayacaktır ve NuGet, iptal sunucularına ulaşmaya çalışmaz. İptal denetimi modu `offline`olarak ayarlandığında, uyarı bir bilgiyle indirgenir.

> [!Warning]
> Normal engelleri altında, iptal denetimi modunun çevrimdışına geçmeniz önerilmez. Bunun yapılması, NuGet 'in çevrimiçi iptal denetimini atlamasına ve yalnızca önbelleğe alınmış sertifika iptal listesine karşı yalnızca çevrimdışı bir iptal denetimi gerçekleştirmesine neden olur. Bu, imzalama sertifikasının iptal edilmiş olabileceği, aksi takdirde iptal denetimi olmayan ve yüklenmemiş olan paketleri yükleme/geri yükleme olmaya devam edecektir.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` seçeneği sağ tıklama bağlam menüsünde kullanılamaz

#### <a name="issue"></a>Sorun

Bir proje ilk açıldığında NuGet bir NuGet işlemi gerçekleştirilene kadar başlatılmamış olabilir. Bu, geçiş seçeneğinin `packages.config` veya `References`sağ tıklama kısayol menüsünde gösterilmamasını sağlar.

#### <a name="workaround"></a>Geçici Çözüm

Aşağıdaki NuGet eylemlerinden birini gerçekleştirin:
* Paket Yöneticisi Kullanıcı arabirimini açın-`References` ' a sağ tıklayıp `Manage NuGet Packages...` ' ı seçin.
* Paket Yöneticisi konsolunu açın-`Tools > NuGet Package Manager`' den `Package Manager Console` ' ı seçin.
* NuGet geri yükleme Çalıştır-Çözüm Gezgini çözüm düğümüne sağ tıklayın ve `Restore NuGet Packages` ' ı seçin.
* Ayrıca NuGet geri yüklemeyi tetikleyen projeyi oluştur

Şimdi geçiş seçeneğini görebilmeniz gerekir. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmediğini unutmayın.
Note: Bu, VS 2017 15,9 Preview 3 ' te düzeltildi

## <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

### <a name="bugs"></a>Hatalar
#### <a name="signing"></a>Açmada
* İmzalama: imzalı paketi, çevrimdışı ortamda yükleme [#7008](https://github.com/NuGet/Home/issues/7008) --4.8.1 içinde düzeltildi
* İmzalama: Hatalı URL denetimi- [#7174](https://github.com/NuGet/Home/issues/7174)
* İmzalama: paket depo onayını imzalayan- [#6926](https://github.com/NuGet/Home/issues/6926) olduğunda, havuz doğrulama içindeki paket bütünlüğünü denetleyin
* "Paket bütünlük denetimi başarısız oldu." ileti içinde paket KIMLIĞI (ve hata kodu) olmalıdır- [#6944](https://github.com/NuGet/Home/issues/6944)
* Depo imzalı paket doğrulaması, farklı sertifika tarafından imzalanmış paketlere izin verir- [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet-Signing-timestamp URL 'SI https://olamaz. - [#6871](https://github.com/NuGet/Home/issues/6871)
* NuSpec paketleme senaryosunda NullRef yapmayın, Ayrıca seçenekleri de geliştirebilirsiniz- [#6866](https://github.com/NuGet/Home/issues/6866)
* Onay imzasına zaman damgası eklenirken imza bilgileri güncelleştirilirken bellek geçersiz- [#6840](https://github.com/NuGet/Home/issues/6840)
* İmzalama: CTL özel durumlarını kaldırma- [#6794](https://github.com/NuGet/Home/issues/6794)
* İmzalama: contentUrl, HTTPS- [#6777](https://github.com/NuGet/Home/issues/6777) olmalıdır
* İmzalama: SignedPackageVerifierSettings. VSClientDefaultPolicy kullanılmıyor- [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Paket
* nuspec- [#6866](https://github.com/NuGet/Home/issues/6866) Pack için DotNet. exe dosyası kullanılırken restore ve Build gerekmez
* Nusguproperties 'de boş değiştirme belirteçlerine izin ver- [#6722](https://github.com/NuGet/Home/issues/6722)
* Nusbir Properties belirtildiğinde Pacatask, NullReferenceException öğesini oluşturur- [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Erişilebilirlik
* Larınızdaki Paket düğmesi altında ' ön sürüm ' dizesinin, PM Kullanıcı arabirimi- [#4504](https://github.com/NuGet/Home/issues/4504) içindeki paket açıklaması kapsamında
* Larınızdaki PM Kullanıcı arabiriminde ' Microsoft Visual Studio çevrimdışı paketler ' seçilirken paket kaynak açılan ve Ayarlar düğmesi kesildi- [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>PowerShell Yönetim Konsolu (PMC)
* `Update-Package`, PackageReference sürüm aralığını yok sayıyor- [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` çözüm genelinde sorun- [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` yalnızca adlandırılmış tek [#737](https://github.com/NuGet/Home/issues/737) yerine tüm paketleri yeniden yükler
* , Paket yöneticisi konsolundan listelenmemiş NuGet paketine güncelleştirebilir- [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Çeşitli
* `NuGet update self` NuGet 'i onarmak için. CommandLine nupkg, semver 2.0 olamaz- [#7116](https://github.com/NuGet/Home/issues/7116)
* NU1107 yüklemesi hatalarıyla ilgili deneyimleri geliştirme- [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest 'in serileştirilmesi yanlış- [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage, Kullanıcı arabirimi iş parçacığından başlatıldığında yüklenemiyor- [#6976](https://github.com/NuGet/Home/issues/6976)
* Restore, Project 'i belirten yanıltıcı hataları bildiriyor. JSON gereklidir- [#6959](https://github.com/NuGet/Home/issues/6959)
* Paket Yöneticisi Kullanıcı arabirimi: önizleme değişiklikleri, Tamam düğmesi klavye tarafından otomatik olarak kullanılamaz [#6893](https://github.com/NuGet/Home/issues/6893)
* P2P başvuruları olan proje için RestoreSources yoksayıldı- [#6776](https://github.com/NuGet/Home/issues/6776)
* .NET Framework şablonu kullanarak birim testi projesi oluşturma, Packages. config ile eski Proje modelini açar [#6736](https://github.com/NuGet/Home/issues/6736)
* Proje başvurusunun paket bağımlılığını geçersiz kılmasına izin ver- [#6536](https://github.com/NuGet/Home/issues/6536)
* MSBuild görevinde NoDefaultExcludes 'i kullanıma sunma- [#6450](https://github.com/NuGet/Home/issues/6450)
* "Tüm NuGet önbelleklerini temizle" için durum iletisi, pencere yeniden boyutlandırma- [#5938](https://github.com/NuGet/Home/issues/5938) gizlenebilir


[Bu yayında düzeltilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
