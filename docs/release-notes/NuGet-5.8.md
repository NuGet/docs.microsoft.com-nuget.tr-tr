---
title: NuGet 5,8 sürüm notları
description: yeni özellikler, hata düzeltmeleri ve dtu 'lar dahil NuGet 5,8 sürüm notları.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209936"
---
# <a name="nuget-58-release-notes"></a>NuGet 5,8 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir | .NET SDK 'ları 'nda kullanılabilir |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> .net Core iş yüküne sahip Visual Studio 2019 ile yüklendi
  
> [!NOTE]
> Visual Studio 16,8, MSBuild 16,8 ve .net 5,0 NuGet.exe 5,8 veya üstünü gerektirir.


## <a name="summary-whats-new-in-58"></a>Özet: 5,8 sürümündeki yenilikler
🎉 **.net 5,0 'yi hedefleyen NuGet paketlere yönelik tam yazma ve geri yükleme desteği sunan ilk sürümdür** 🎉

* MMAP/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807) kullanarak nupkg ayıklamayı hızlandırın

* Paket Yöneticisi uı paketi ayrıntıları bölmesinde paket güvenlik açığı ayrıntılarını görüntüle- [#9850](https://github.com/NuGet/Home/issues/9850)

* imzalı NuGet paketlerini yeni [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) komutla doğrulayın- [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples)`--prerelease`, ön sürüm sürümleri de dahil olmak üzere bir paketin en son sürümünü ekleme seçeneğini destekler [#4699](https://github.com/NuGet/Home/issues/4699)

* CLı içindeki paketleri komut ile ara [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) komut, `--verbosity` seçeneği destekler- [#9600](https://github.com/NuGet/Home/issues/9600)

* Visual Studio- [#9565](https://github.com/NuGet/Home/issues/9565) ' de csproj stili, packagereference tabanlı projeler için hızlı No-Op geri yükleme iyileştirmesi etkinleştirin

* çözüm düzeyi Paket Yöneticisi paket yüklemeleri ve güncelleştirmeleri gibi kullanıcı arabirimi işlemleri en fazla 10 x daha hızlıdır [#6010](https://github.com/NuGet/Home/issues/6010)

* Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903) NuGet diğer birçok performans geliştirmesi


### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**DCR**

* .NET 5,0 tfd: çerçeve önceliği kuralları- [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet, targetframework 'ü ayrıştırırken nokta platformu sürümünü çıkarmamalıdır [#9842](https://github.com/NuGet/Home/issues/9842)

* Tek bir TFI, TFV, TPI, TPV özellikleri kullanmak yerine çerçeveleri anlamak için Targetframeworkbilinen & Targetplatformbilinen adını kullanın [#9895](https://github.com/NuGet/Home/issues/9895)

* `GetReferenceNearestTargetFrameworkTask()`Platformlarla hedef çerçeveleri (NET 5.0-Windows) destekleyen güncelleştirme- [#9894](https://github.com/NuGet/Home/issues/9894)

* .net 5,0 Visual Studio apı 'leri- [#9650](https://github.com/NuGet/Home/issues/9650)

* Paket Yöneticisi Kullanıcı arabirimi: birleştirme veya güncelleştirme paketleri işlemleri hatalar nedeniyle engellenmemelidir (paket düşürme, vb.)- [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet özellikler, özelliği olan projeler için hafif olmalıdır; "Packagereferde"- [#9957](https://github.com/NuGet/Home/issues/9957)

* Visual Studio- [#6384](https://github.com/NuGet/Home/issues/6384) No-Op geri yükleme iletilerini gösterme

**Hatalar:**

* OutputWindowTextWriter Oluşturucusu arka plan iş parçacığında çağrılmamalıdır- [#9764](https://github.com/NuGet/Home/issues/9764)

* Büyük endian CPU 'Larda imzalı paketleri geri yükleme- [#9547](https://github.com/NuGet/Home/issues/9547)

* Outputconsolegünlükçü, MEF oluşturucularında önceden başlatma yöntemleri çağırmamalıdır- [#9591](https://github.com/NuGet/Home/issues/9591)

* NuGet hata. CommandLine. Console `PrintJustified()` yöntemi- [#9737](https://github.com/NuGet/Home/issues/9737)

* Paket Yöneticisi Hatalı bağlama nedeniyle paket meta verileri atık olarak toplandığında UI bellek sızıntısı- [#9757](https://github.com/NuGet/Home/issues/9757)

* Açmada Paket Yöneticisi kullanıcı arabiriminde packages.config biçimdeki imzalı bir paket yüklenirken Hata Listesi hiçbir uyarı gösterilmiyor [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat ortak API 'Ler içermemelidir- [#9821](https://github.com/NuGet/Home/issues/9821)

* #9822 iş parçacığı havuzu iş parçacığını engelleyerek çözüm yükleme sırasında kaynak çekişmesini azaltma `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)

* komut satırı geri yükleme ' de, çok hedefli projelerle, NuGet iç derlemeden ilgili hedef framework bilgilerini okuması gerekir [#9869](https://github.com/NuGet/Home/issues/9869)

* Targetframeworkınformation öğesi aracılığıyla çalışma zamanı tanımlayıcı grafiğini oku- [#9874](https://github.com/NuGet/Home/issues/9874)

* statik grafik geri yükleme, Visual Studio ve düzenli MSBuild değerlendirme geri yükleme- [#9881](https://github.com/NuGet/Home/issues/9881) kıyasla çapraz başlangıçlama özelliğine karşılık olarak tutarsız.

* statik grafik geri yükleme ' de, çok hedefli projelerle NuGet, iç derlemeden ilgili hedef framework bilgilerini okumalı. - [#9870](https://github.com/NuGet/Home/issues/9870)

* `net5.0-platform`Visual Studio [#9863](https://github.com/NuGet/Home/issues/9863) projelerin yüklenmesine ve geri yüklenmesine izin ver

* Paket Yöneticisi kullanıcı arabiriminde çözümlenmiş sürümü görüntüleme [#9826](https://github.com/NuGet/Home/issues/9826)

* Paket Yöneticisi uı: Çözüm Gezgini tüm NuGet paketi bağımlılıklarını gösterilmiyor- [#9898](https://github.com/NuGet/Home/issues/9898)

* SPDX lisans listesini güncelleştirme- [#9946](https://github.com/NuGet/Home/issues/9946)

* NuGet paketlerini yönet ' i açtıktan sonra VS 2019 kilitleniyor: simge görüntüde işlenmeyen özel duruma neden olur conversio- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Paketleme. ayıklama, [#9966](https://github.com/NuGet/Home/issues/9966) Newtonsoft.Jshariç tutmak için ılmerge gerektirir

* Bir hata olmadığında devam Packingaftergeneratingnuspec = false ile paketleme başarısız olmamalıdır- [#9786](https://github.com/NuGet/Home/issues/9786)

* Paket Yöneticisi Kullanıcı arabirimi: simgeler renkleri düzgün şekilde tersine çevirme- [#10017](https://github.com/NuGet/Home/issues/10017)

* Geri yükleme sırasında güncel ve No-Op projeler için yanlış proje sayısı- [#10026](https://github.com/NuGet/Home/issues/10026)

* `/p:RestoreUseStaticGraphEvaluation=true`Değer içindeki sonuçların kullanılması null olamaz- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` WPF kitaplığı projeleri için yanlışlıkla diğer ad kullanır- [#10020](https://github.com/NuGet/Home/issues/10020)

* Paket Yöneticisi UI: imza doğrulaması başarısız olduğunda NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: `object` proje meta verileri değerleri için tür kullanmayın- [#10055](https://github.com/NuGet/Home/issues/10055)

* Kod alanları: Araçlar seçeneklerinde paket kaynaklarını kaydetme, kimlik bilgilerinin üzerine yazacak- [#9711](https://github.com/NuGet/Home/issues/9711)


**[Bu yayında düzeltilen tüm sorunların listesi-5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Bu sürümdeki sorunların listesi-5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Topluluk katkıları

bu NuGet yayını harika hale getirmek için size yardımcı olan tüm katkıda bulunanlar için teşekkürler!

|Who|PR 'ler|Sorunlar|
|----|----|----|
[omajıd](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Hata iletisinde typo. "Yönetici" yerine "administator"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Geçersiz Assemblınformationalversion raporlarının bulunduğu paket "Description gereklidir"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` Dal ve tamamlama özelliklerini hesaba eklemez- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Visual Studio Hata Listesi penceresinde NU kodu tıklandığında #9934 'e gitmeniz gerekir [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Visual Studio seçenekleri aracılığıyla yeni paket kaynağı eklerken ' https://' kullanın- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989) performans sorunu
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | SemanticVersion sınıfı için bir TypeConverter ekleyin- [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Özet: 5.8.1 'deki yenilikler

* packages.config package.lock.json 5,8- [#10257](https://github.com/NuGet/Home/issues/10257) içinde yanlış bir hedef Framework kullanır

* 5,8 + 16,8, PackageReference ve packages.config [#10326](https://github.com/NuGet/Home/issues/10326) karıştırdığınızda geçişli Proje bağımlılıklarını çözemez

**[Bu yayında düzeltilen tüm sorunların listesi-5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Bu sürümdeki işlemelerin listesi-5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Geri bildirim hoş geldiniz

Görüşleriniz bizim için önemlidir.  bu sürümle ilgili herhangi bir sorun varsa, mevcut sorunlar için [GitHub sorunlarımızı](https://github.com/NuGet/Home/issues) inceleyin ve [geliştirici Visual Studio Community](https://developercommunity.visualstudio.com/) .  Içindeki yeni sorunlar NuGet lütfen sorunu GitHub [rapor edin.](https://github.com/NuGet/Home/issues/new)
Genel NuGet deneyimi sorunları için, Yardım [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ve Sorun Bildir altında sık kullanılan IDE'niz içinde bulunan **bir sorun > bize bildirebilirsiniz.**