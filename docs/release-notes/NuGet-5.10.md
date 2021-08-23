---
title: NuGet 5,10 sürüm notları
description: yeni özellikler, hata düzeltmeleri ve dtu 'lar dahil NuGet 5,10 sürüm notları.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726957"
---
# <a name="nuget-510-release-notes"></a>NuGet 5,10 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir | .NET SDK 'ları 'nda kullanılabilir |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .net Core iş yüküne sahip Visual Studio 2019 ile yüklendi
  
> [!NOTE]
> Visual Studio 16,10, MSBuild 16,10 ve .net 5.0.300 + NuGet.exe 5,10 veya sonraki bir sürümü gerektirir.

## <a name="summary-whats-new-in-510"></a>Özet: 5,10 sürümündeki yenilikler

* İmzalama: DotNet güvenilir-signers komutunu uygulama- [#8053](https://github.com/NuGet/Home/issues/8053)

* varsayılan doğrulamayı Linux üzerinde devre dışı bırak, ancak varsayılan olarak Windows- [#10713](https://github.com/NuGet/Home/issues/10713) etkinleştirildi

* .NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742) 'de paket imzalama doğrulaması IÇIN bir env değişkeni ekleyin

* Büyük çözümler için yeni paket performansını yüklemeyi geliştirme- [#10166](https://github.com/NuGet/Home/issues/10166)

* `nfproj`NUGET CLI Için Supportedprojec_1 listesine proje türünü ekleyin. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* `<requireLicenseAcceptance>`Proje paketleme sırasında öğeyi bastır- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] Önizleme uyarısı DotNet CLI- [#10226](https://github.com/NuGet/Home/issues/10226) gösterilmelidir

* PMUı 'nin arka plan ve ön plan rengi belirteçlerini, CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608) güncelleştirme

* [Hata Bash] "İşlem Kullanıcı tarafından iptal edildi" hatası, PM Kullanıcı arabiriminde hızla sekmeler arasında geçiş yaparken Hata Listesi penceresinde göster [#10671](https://github.com/NuGet/Home/issues/10671)

* PM Kullanıcı arabirimi: çözüm düzeyinde paket yükleme performansını Iyileştirme- [#10210](https://github.com/NuGet/Home/issues/10210)

* GetService 'i NuGet her yerde GetServiceAsync değiştirin. İstemciler- [#3784](https://github.com/NuGet/Home/issues/3784)

* `..`Göreli yol ile [#5016](https://github.com/NuGet/Home/issues/5016) paketi performans sorunu NuGet.exe

* "NuGet Pack" performansı, kaynak yollarında artan düzeyler ile düşüyor- [#5706](https://github.com/NuGet/Home/issues/5706)

* yinelenen dosyalarla nuspec paketleme sırasında hata NuGet. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet pack "belirtilen DateTimeOffset bir Zip dosyası zaman damgasına dönüştürülemez"- [#7001](https://github.com/NuGet/Home/issues/7001)

* Paketlenmiş paketin dosyasının zaman damgaları, saat dilimi tarafından kaydırılacağı [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 daha fazla işlem yapılabilir bilgi içermelidir [#7696](https://github.com/NuGet/Home/issues/7696)

* [Hata Bash] [Test hatası] Boş/hatalı biçimlendirilmiş kilit dosyası ' dotnet restore--Use-Lock-File--kilitli-Mode '- [#8640](https://github.com/NuGet/Home/issues/8640) çalıştırılırken güncelleştirilmeyecek

* NuGetVersionRange, mantıksal olarak yanlış aralıkların ayrıştırılmasını sağlar- [#9145](https://github.com/NuGet/Home/issues/9145)

* PM Kullanıcı arabirimi, seçili ve vurgulanan paket kaynakları arasında ayırt edilemeyen bir arka plan rengi gösteremez- [#9538](https://github.com/NuGet/Home/issues/9538)

* Yüklenecek projeleri, ekran okuyucu tarafından okunmayacak şekilde seçme onay kutusu- [#9578](https://github.com/NuGet/Home/issues/9578)

* Ayrıntılar bölmesi sürümler açılan menüsü varsayılan seçimi, yüklü/güncelleştirmeler sekmelerinde yüklü/yerinde olmalıdır- [#9887](https://github.com/NuGet/Home/issues/9887)

* Bazı .NET 5 SDK 'ları için geçici çözüm hesabını kaldırma #9913 targetplatformbilinen adı ` ,Version= `  -  [](https://github.com/NuGet/Home/issues/9913)

* DotNet NuGet doğrulaması çok sessiz- [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange tek basamaklı aralıkları ayrıştıramıyor- [#10342](https://github.com/NuGet/Home/issues/10342)

* VS Solution Manager, hata ayıklama sırasında için null özel durumu oluşturur- [#10352](https://github.com/NuGet/Home/issues/10352)

* CLı özel durum iletilerini dize kaynak dosyalarına taşıma- [#10392](https://github.com/NuGet/Home/issues/10392)

* Ölü kodu Kaldır (TabItemButtonAutomationPeer)- [#10435](https://github.com/NuGet/Home/issues/10435)

* Bağlam menüsünü Güncelleştir- [#10498](https://github.com/NuGet/Home/issues/10498) ilk seçili öğeye kaydırılmalıdır

* Çözüm PMUI ayrıntıları çakışan yatay çubuğa sahip [#10533](https://github.com/NuGet/Home/issues/10533)

* İmzalama: sertifikanın süre dolduğunda ve zaman damgası güvenilir değil olduğunda birincil imza ayrıntıları gösterilmez. [#10535](https://github.com/NuGet/Home/issues/10535)

* Etkin olmayan hiçbir kaynak olması, PM Kullanıcı arabiriminin şunu göstermesini önler [#10541](https://github.com/NuGet/Home/issues/10541)

* Paket meta verileri (Ayrıntılar, kullanımdan kaldırma) bazen CodeSpaces 'daki nuget.org 'tan çekilmemelidir [#10549](https://github.com/NuGet/Home/issues/10549)

* Hata ayıklama oturumu sırasında PMUI başlatması özel durumla başarısız oluyor- [#10559](https://github.com/NuGet/Home/issues/10559)

* big endian sistem [#10567](https://github.com/NuGet/Home/issues/10567) üzerinde bir paket bütünlük denetimi hatasına yönelik NuGet geri yükleme sonuçları

* PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595) yerine FormatException oluşturuldu

* CPVM-grafik yürüme algoritmasındaki eşzamanlılık sorunları- [#10598](https://github.com/NuGet/Home/issues/10598)

* PMC PowerShell sürüm telemetrisi ekleme- [#10609](https://github.com/NuGet/Home/issues/10609)

* NuGetVersion sıralama performansını iyileştirme- [#10611](https://github.com/NuGet/Home/issues/10611)

* Güvenilir-sonuçcılar ekleme işlemi tutarsız bağımsız değişkenlere sahip- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0: NuGet Paket Yöneticisi "Updates" ile "yüklü" arasındaki sekmelerin değiştirilmesi çerçeveyi güncelleştirmez. - [#10654](https://github.com/NuGet/Home/issues/10654)

* "V" öğesini PMUI- [#10677](https://github.com/NuGet/Home/issues/10677) sürüm numarasından kaldır

* Inugetprojectservice. Getınstalınstaltesync, CPS proje sistemi aday [#10681](https://github.com/NuGet/Home/issues/10681) almadan önce oluşturur

* katıştırılmış simgeler, "Microsoft Visual Studio çevrimdışı paketler" kaynağından, gezinme sekmesinde erişim engellendi- [#10687](https://github.com/NuGet/Home/issues/10687)

* Msbuildprojectsınspath ayarlandığında ınugetprojectservice. Getınstallationpackagesasync oluşturulur [#10739](https://github.com/NuGet/Home/issues/10739)

* "DotNet NuGet Remove Source nuget.org" ilk [#10745](https://github.com/NuGet/Home/issues/10745) çalışmaz

* NuGet zaman uyumsuz bir yöntemde işlem parçacığı iş parçacığını engeller- [#10775](https://github.com/NuGet/Home/issues/10775) zaman uyumlu bir çağrı yapar

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` etkin olmayan kod ve performans için [#10790](https://github.com/NuGet/Home/issues/10790)

* NuGet SDK paketlerinde embedded simgesini kullanın- [#10795](https://github.com/NuGet/Home/issues/10795)

* SPDX lisans listesini güncelleştirme- [#10806](https://github.com/NuGet/Home/issues/10806)

**[Bu yayında düzeltilen tüm sorunların listesi-5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Bu sürümdeki işlemelerin listesi-5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Topluluk katkıları

bu NuGet yayını harika hale getirmek için size yardımcı olan tüm katkıda bulunanlar için teşekkürler!

|Who|PR 'ler|Sorunlar|
|----|----|----|
[louo-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange tek basamaklı aralıkları ayrıştıramıyor- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajıd](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. İstemci build.sh bozuk [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. İstemci build.sh bozuk [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackICE](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | "NuGet Pack" performansı, kaynak yollarında artan düzeyler ile düşüyor- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackICE](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | İle NuGet.exe paketi performans sorunu.. göreli yol- [#5016](https://github.com/NuGet/Home/issues/5016)
[Marcin-kronyıstianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-grafik yürüme algoritmasındaki eşzamanlılık sorunları- [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Nfproj proje türünü NuGet CLı için Supportedprojec_1 listesine ekleyin. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Geri bildirim hoş geldiniz

Görüşleriniz bizim için önemlidir.  bu sürümle ilgili herhangi bir sorun varsa, mevcut sorunlar için [GitHub sorunlarımızı](https://github.com/NuGet/Home/issues) inceleyin ve [geliştirici Visual Studio Community](https://developercommunity.visualstudio.com/) .  NuGet içindeki yeni sorunlar için lütfen bir [GitHub sorunu](https://github.com/NuGet/Home/issues/new)bildirin.
genel NuGet deneyimi sorunları için, **yardım > bir sorun bildirmek** üzere en sevdiğiniz ıde 'de bulunan [sorun bildir](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) seçeneğini kullanarak bize bildirin.
