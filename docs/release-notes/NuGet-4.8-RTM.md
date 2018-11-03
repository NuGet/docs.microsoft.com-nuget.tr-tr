---
title: NuGet 4,8 RTM sürüm notları
description: NuGet 4.8.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 641304059c90e360fae4d0956d7b922e34bc6501
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981125"
---
# <a name="nuget-48-rtm-release-notes"></a>NuGet 4,8 RTM sürüm notları

[Visual Studio 2017 15,8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.8 işlevselliği ile birlikte gelir.


Aynı işlevlere komut satırı sürümleri de mevcuttur:
* 4.8 - NuGet.exe [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK'sı 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>Özet: Bu Yayındaki Yenilikler
* NuGet.exe artık Windows 10'da - LONGFILENAMES destekliyor [#6937](https://github.com/NuGet/Home/issues/6937)
* Kimlik doğrulaması eklentileri artık MsBuild, DotNet.exe, NuGet.exe ve platformlar arası dahil olmak üzere Visual Studio çalışır. Kimlik doğrulaması eklentileri birinci nesil Msbuild'de DotNet.exe desteklenmez. Not: Dahil edilen bir VSTS kimlik doğrulama eklentisi VS 2017 15.9 Önizleme derlemelerini içerir. [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild'ın SDK çözümleyici artık NuGet bir parçası olarak oluşturur ve VS için NuGet araçları yükler. Bu eşitleme alma sürümleri uğraşmasına gerek kalmaz. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference artık destekliyor DevelopmentDependency meta - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Bir CI makinede veya çevrimdışı ortamda imzalı paketlerin yüklenmesi normalden uzun sürüyor

#### <a name="issue"></a>Sorun
Bilgisayarın internet erişimi (örneğin, bir yapı makinesi bir CI/CD senaryosunda) kısıtlanmışsa, yükleme/geri imzalı nuget paketi bir uyarı neden olur ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) iptal sunucuları erişilebilir olmadığından. Bu beklenen bir durumdur. Ancak, bazı durumlarda, bu olabilir paketi gibi istenmeyen concequences yükleme/geri yükleme normalden uzun sürüyor.

#### <a name="workaround"></a>Geçici Çözüm
Visual Studio güncelleştirme 15.8.4 ve NuGet.exe 4.8.1 iptal denetimi moduna geçmek için bir ortam değişkeni burada sunduk.
Ayarı `NUGET_CERT_REVOCATION_MODE` ortam değişkenine `offline` önbelleğe alınan sertifika iptal listesi karşı yalnızca sertifika iptal durumunu denetlemek için NuGet zorlar ve NuGet iptal sunucularına ulaşacak şekilde çalışmayacak. İptal denetimi modu ayarlandığında `offline`, uyarı için bir bilgi alt sürüme.

> [!Warning]
> Normal kural dışı altında çevrimdışı iptal denetimi moduna geçmek için önerilmez. Bunun yapılması, çevrimiçi iptal denetimini atlarsanız ve eski olabilecek önbelleğe alınan sertifika iptal listesi karşı yalnızca bir çevrimdışı iptal denetimi gerçekleştirmek NuGet neden olur. Burada imzalama sertifikasının geçersiz kılınmış olabilir, bu araç paketleri devam eder yüklü ve geri, aksi takdirde, iptal denetimi başarısız ve yüklenmediğini.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Sağ bağlam menüsü seçeneği kullanılamaz

#### <a name="issue"></a>Sorun

Bir projeyi ilk defa açıldığında, NuGet işlemi gerçekleştirilene kadar NuGet başlatılmamış. Bu geçiş seçeneği sağ bağlam menüsü üzerinde görünmesini değil neden `packages.config` veya `References`.

#### <a name="workaround"></a>Geçici Çözüm

Aşağıdaki NuGet eylemlerden birini gerçekleştirin:
* Paket Yöneticisi UI - açık sağ `References` seçin `Manage NuGet Packages...`
* Paket Yöneticisi konsolu - açık `Tools > NuGet Package Manager`seçin `Package Manager Console`
* Çalışma NuGet geri yükleme - Çözüm Gezgini'nde çözüm düğümüne sağ tıklayın ve seçin `Restore NuGet Packages`
* Ayrıca NuGet geri yükleme tetikler projeyi derleyin

Artık geçiş seçeneği görmeye olmalıdır. Bu seçenek desteklenmez ve ASP.NET ve C++ proje türleri için gösterilmez unutmayın.
Not: Bu VS 2017 15.9 Preview 3'te düzeltildi

## <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

### <a name="bugs"></a>Hatalar
#### <a name="signing"></a>imzalama
* İmzalama: Çevrimdışı ortamda Paket imzalı yükleme [#7008](https://github.com/NuGet/Home/issues/7008) --4.8.1 sürümünde düzeltilen
* İmzalama: Yanlış URL onay - [#7174](https://github.com/NuGet/Home/issues/7174)
* İmzalama:, paket deposu imzalanabilir - olduğunda RepositorySignatureVerifier içinde paket bütünlük denetimi [#6926](https://github.com/NuGet/Home/issues/6926)
* "Paket bütünlük denetimi başarısız oldu." ileti (ve hata kodu) - paket kimliği olmalıdır [#6944](https://github.com/NuGet/Home/issues/6944)
* Depo imzalı paket doğrulama sağlayan farklı sertifika tarafından - imzalanmış paketleri [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - imzalama - zaman bilgisi URL'si https:// olmaması? - [#6871](https://github.com/NuGet/Home/issues/6871)
* NuSpec paketleme senaryoda NullRef yoksa, ayrıca seçenekleri - iyileştirin [#6866](https://github.com/NuGet/Home/issues/6866)
* Bellek Geçersiz imzalayan bilgileri güncelleştirilirken zaman damgası için onay imzası - eklerken [#6840](https://github.com/NuGet/Home/issues/6840)
* İmzalama: CTL özel durum - kaldırma [#6794](https://github.com/NuGet/Home/issues/6794)
* İmzalama: contentUrl HTTPS - olmalıdır [#6777](https://github.com/NuGet/Home/issues/6777)
* İmzalama: SignedPackageVerifierSettings.VSClientDefaultPolicy kullanılmayan - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Paketi
* geri yükleme ve yapılandırma gerekmeyen dotnet.exe nuspec - pack kullanırken [#6866](https://github.com/NuGet/Home/issues/6866)
* İçinde NuspecProperties - boş değiştirme belirteçleri izin [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask oluşturur NullReferenceException NuspecProperties belirtildiğinde - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Erişilebilirlik
* [Erişilebilirlik] Dize 'Et' paket düğmesinin altındaki paket açıklamasını PM kullanıcı arabiriminde - kapsamında [#4504](https://github.com/NuGet/Home/issues/4504)
* [Erişilebilirlik] Paket kaynağı açılır ve ayarları düğmesi 'Microsoft Visual Studio çevrimdışı paketleri' PM Kullanıcı Arabiriminde - seçerken kesilmiş [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>PowerShell Yönetim Konsolu (PMC)
* `Update-Package` PackageReference sürüm aralığı - yoksayar [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` Çözüm çapında bir sorun - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` yalnızca adlandırılmış bir - yerine tüm paketleri yeniden yükler [#737](https://github.com/NuGet/Home/issues/737)
* Paket Yöneticisi konsolundan - listelenmemiş NuGet paketine güncelleştirebilir miyim [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Çeşitli
* Düzeltmek için `NuGet update self` NuGet.Commandline nupkg semver2.0 - olmamalıdır [#7116](https://github.com/NuGet/Home/issues/7116)
* NU1107 yükleme hataları - olan deneyimleri iyileştirir [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest serileştirilmesi yanlış - [#6983](https://github.com/NuGet/Home/issues/6983)
* UI iş parçacığından - hazırlarken yüklemek NuGet Visual Studio AsyncPackage başarısız [#6976](https://github.com/NuGet/Home/issues/6976)
* Geri yükleme hataları project.json belirten yanıltıcı gereklidir - raporlama [#6959](https://github.com/NuGet/Home/issues/6959)
* Paket Yöneticisi UI: Tamam düğmesine değil - klavye tarafından otomatik olarak kullanılabilir olan değişiklik önizlemesi [#6893](https://github.com/NuGet/Home/issues/6893)
* -P2p başvuruları olan proje için yoksayıldı RestoreSources [#6776](https://github.com/NuGet/Home/issues/6776)
* .NET Framework kullanarak birim testi projesi oluşturma ile packages.config - şablon eski proje modeli açılır [#6736](https://github.com/NuGet/Home/issues/6736)
* Paket bağımlılığı - geçersiz kılmak proje başvurusu izin [#6536](https://github.com/NuGet/Home/issues/6536)
* MSBuild görevinde - NoDefaultExcludes kullanıma [#6450](https://github.com/NuGet/Home/issues/6450)
* Durum iletisi "Clear tüm NuGet önbellekler" penceresi boyutlandırmada - gizli [#5938](https://github.com/NuGet/Home/issues/5938)


[Bu sürümde düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
