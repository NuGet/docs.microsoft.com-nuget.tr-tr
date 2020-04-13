---
title: NuGet 4.8 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.8.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813773"
---
# <a name="nuget-48-release-notes"></a>NuGet 4.8 Sürüm Notları

[Visual Studio 2017 15.8 RTW,](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.8 işlevselliğiyle birlikte geliyor.


Aynı işlevselliğin komut satırı sürümleri de mevcuttur:
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Çekirdek SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Özeti: 4.8.0 Yenilikler
* NuGet.exe artık Windows 10'da uzun dosya adlarını destekliyor - [#6937](https://github.com/NuGet/Home/issues/6937)
* Kimlik doğrulama eklentileri artık msbuild, DotNet.exe, NuGet.exe ve Visual Studio genelinde çapraz platform da dahil olmak üzere çalışır. Kimlik doğrulama eklentilerinin ilk nesli MsBuild, DotNet.exe'de desteklenmedi. Not: VS 2017 15.9 Önizleme yapılarında VSTS kimlik doğrulama eklentisi bulunmaktadır. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild'in SDK Çözümleyicisi artık NuGet'in bir parçası olarak inşa edildi ve VS için NuGet araçlarıyla yüklüyor. Bu, sürümlerin eşitlemeyi önler. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference şimdi DevelopmentDependency meta verilerini destekler - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Özet: 4.8.2'de Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>İmzalı paketleri bir CI makinesine veya çevrimdışı bir ortama yüklemek normalden daha uzun sürer

#### <a name="issue"></a>Sorun
Makine internet erişimini kısıtlamışsa (CI/CD senaryosundaki bir yapı makinesi gibi), imzalı bir nuget paketinin yüklenmesi/geri yüklenmesi, iptal sunucuları erişilemediğinden bir uyarıya[(NU3028)](../reference/errors-and-warnings/nu3028.md)neden olur. Bu beklenen bir durumdur. Ancak, bazı durumlarda, bu paket yüklemek / normalden daha uzun sürme geri yükleme gibi istenmeyen gebelik olabilir.

#### <a name="workaround"></a>Geçici çözüm
Visual Studio 15.8.4 ve NuGet.exe 4.8.1'e güncelleyin ve iptal kontrol modunu değiştirmek için bir ortam değişkeni tanıttık.
Ortam `NUGET_CERT_REVOCATION_MODE` değişkenini, `offline` NuGet'i yalnızca önbelleğe alınmış sertifika iptal listesiyle karşılayın, iptal durumunu denetlemeye zorlar ve NuGet iptal sunucularına ulaşmaya çalışmaz. İptal denetim modu `offline`ayarlandığında, uyarı bir bilgilere indirgenecektir.

> [!Warning]
> İptal denetimi modunu normal srumstances altında çevrimdışı olarak değiştirmek önerilmez. Bunu yapmak, NuGet'in çevrimiçi iptal denetimini atlamasına ve önbelleğe alınmış sertifika iptal listesine karşı yalnızca çevrimdışı iptal denetimi gerçekleştirmesine neden olur. Bu, imzalama sertifikasının iptal edilmiş olabileceği, yüklenmeye/geri yüklenmeye devam edeceği, aksi takdirde iptal denetiminin başarısız olacağı ve yüklenmediği paketler anlamına gelir.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Seçenek `Migrate packages.config to PackageReference...` sağ tıklama bağlam menüsünde kullanılamıyor

#### <a name="issue"></a>Sorun

Bir proje ilk açıldığında, NuGet işlemi gerçekleştirilene kadar önbaşlatma olmayabilir. Bu, geçiş seçeneğinin sağ tıklatma bağlam menüsünde `packages.config` `References`veya .

#### <a name="workaround"></a>Geçici çözüm

Aşağıdaki NuGet eylemlerinden herhangi birini gerçekleştirin:
* Paket Yöneticisi UI'yi açın `References` - Sağ tıklayın ve seçin`Manage NuGet Packages...`
* Paket Yöneticisi Konsolu'nu açın - From `Tools > NuGet Package Manager`, seçin`Package Manager Console`
* NuGet geri yükleme çalıştırın - Çözüm Gezgini'ndeki çözüm düğümüne sağ tıklayın ve`Restore NuGet Packages`
* NuGet geri yüklemesini de tetikleyen projeyi oluşturun

Artık geçiş seçeneğini görebilmelisin. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmeyeceğini unutmayın.
Not: Bu vs 2017 15,9 Önizleme 3 sabit olmuştur

## <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

### <a name="bugs"></a>Hatalar
#### <a name="signing"></a>İmzalama
* İmzalama: İmzalı paketi çevrimdışı [ortama](https://github.com/NuGet/Home/issues/7008) yükleme #7008 -- 4.8.1'de düzeltildi
* İmzalama: yanlış URL denetimi - [#7174](https://github.com/NuGet/Home/issues/7174)
* İmzalama: Paket depo karşı imzalandığında DepoSignatureVerifier'de paket bütünlüğünü kontrol [edin](https://github.com/NuGet/Home/issues/6926) - #6926
* "Paket Bütünlüğü denetimi başarısız oldu." iletide paket kimliği (ve hata kodu) olmalıdır - [#6944](https://github.com/NuGet/Home/issues/6944)
* Depo imzalı paket doğrulama, farklı sertifika ile imzalanan [paketlere](https://github.com/NuGet/Home/issues/6884) izin verir - #6884
* NuGet - İmzalama - Timestamp URL https:// olamaz? - [#6871](https://github.com/NuGet/Home/issues/6871)
* NuSpec ambalaj senaryosunda NullRef etmeyin, aynı zamanda seçenekleri geliştirmek - [#6866](https://github.com/NuGet/Home/issues/6866)
* Karşı imzaya zaman damgası eklerken imzalayan bilgileri güncellerken bellek geçersizdir - [#6840](https://github.com/NuGet/Home/issues/6840)
* İmzalama: CTL özel durumlarını kaldırın - [#6794](https://github.com/NuGet/Home/issues/6794)
* İmzalama: contentUrl HTTPS olmalı - [#6777](https://github.com/NuGet/Home/issues/6777)
* İmzalama: İmzalıPackageVerifierSettings.VSClientDefaultPolicy kullanılmaz - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Paketi
* nuspec paketi dotnet.exe kullanırken geri yükleme ve inşa gerekli olmamalıdır - [#6866](https://github.com/NuGet/Home/issues/6866)
* NuspecProperties'de boş değiştirme belirteçlerine izin ver - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask NuspecProperties belirtildiğinde NullReferenceException atar - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Erişilebilirlik
* [Erişilebilirlik] Paket düğmesinin altındaki string 'Prerelease' PM UI 'paket açıklaması kapsamındadır - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Erişilebilirlik] PM UI'de 'Microsoft Visual Studio Çevrimdışı Paketler' seçilirken paket kaynağı açılır ve ayarlar düğmesi kesilir - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Powershell Yönetim Konsolu (PMC)
* `Update-Package`PackageReference sürüm aralığını yok sayar - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall`çözüm geniş sorun - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall`yerine sadece bir adlandırılmış tüm paketleri yeniden yükler - [#737](https://github.com/NuGet/Home/issues/737)
* Paket Yöneticisi Konsolundan listelenmemiş NuGet paketine güncellenebilir - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Çeşitli
* NuGet.Commandline nupkg düzeltmek `NuGet update self` için semver2.0 olmamalıdır - [#7116](https://github.com/NuGet/Home/issues/7116)
* NU1107 yükleme hataları ile ilgili deneyimleri [geliştirin](https://github.com/NuGet/Home/issues/7107) - #7107
* GetAuthenticationCredentialRequest serileştirme yanlıştır - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage, UI iş parçacığının başlatılmasıyla yüklenmez - [#6976](https://github.com/NuGet/Home/issues/6976)
* Geri yükleme project.json gerekli olduğunu belirten yanıltıcı hatalar bildiriyor - [#6959](https://github.com/NuGet/Home/issues/6959)
* Paket yöneticisi UI : önizleme değişiklikleri, tamam düğmesi klavye tarafından otomatik olarak kullanılabilir değil - [#6893](https://github.com/NuGet/Home/issues/6893)
* Geri Yükleme Kaynakları p2p referansları ile proje için yoksayılır - [#6776](https://github.com/NuGet/Home/issues/6776)
* .NET Framework şablonu kullanarak birim test projesi oluşturma paketleri.config ile eski proje modeli açılacaktır - [#6736](https://github.com/NuGet/Home/issues/6736)
* proje başvurusu paket bağımlılığını geçersiz kılmak için izin - [#6536](https://github.com/NuGet/Home/issues/6536)
* MSBuild görevinde NoDefaultExclude'leri açığa çıkar - [#6450](https://github.com/NuGet/Home/issues/6450)
* "Clear All NuGet Önbelleği(ler)" için durum iletisi pencere yeniden boyutlandırmada gizlenebilir - [#5938](https://github.com/NuGet/Home/issues/5938)


[Bu sürümde düzeltilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
