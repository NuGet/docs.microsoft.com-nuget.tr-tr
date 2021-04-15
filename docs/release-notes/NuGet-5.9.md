---
title: NuGet 5,9 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,9 sürüm notları.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 50fd277a4f1f39b4a68a89cd07af4e21f0d3d831
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508819"
---
# <a name="nuget-59-release-notes"></a>NuGet 5,9 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir | .NET SDK 'ları 'nda kullanılabilir |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi
  
> [!NOTE]
> Visual Studio 16,9, MSBuild 16,9 ve .NET 5.0.200 + NuGet.exe 5,9 veya üzeri bir sürüm gerektirir.

## <a name="summary-whats-new-in-59"></a>Özet: 5,9 sürümündeki yenilikler

* Güncelleştirme- [#10378](https://github.com/NuGet/Home/issues/10378) için önceden seçilmiş paketlerle Paket Yöneticisi Kullanıcı arabirimini başlatan paket bağımlılıkları Için "Güncelleştir" bağlam menü öğesi Ekle

    ![Paket "Güncelleştir" deneyimine sağ tıklayın](media/releasenotes-59-update.png)

* Çözüm düzeyi Paket Yöneticisi Kullanıcı arabirimindeki proje listesinin "sürüm" sütununda istenen sürümü (kayan sürüm veya sürüm aralığı isteği dahil) göster [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Çözüm düzeyinde Paket Yöneticisi Kullanıcı arabirimindeki istenen sürüm](media/releasenotes-59-requested-version.png)

* Paket Yöneticisi Kullanıcı arabirimi tarama sekmesinde A/B testi- [#10053](https://github.com/NuGet/Home/issues/10053) olarak yayınlanan ıntellicode paket önerileri

* `.nupkg.metadata`Dosyayı yükleme kaynağını içerecek şekilde genişletin- [#10354](https://github.com/NuGet/Home/issues/10354)

* Paket görevi sırasında belirli TFMs 'Ler için derleme çıkışını hariç tutmak üzere yeni bir MSBuild özelliği ortaya çıkar [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**DTU 'lar (tasarım değişiklik Isteği):**

* En son paket sürümü yüklü olduğunda aşağı simge simgesi sezgisel değildir. Eski yeşil değer kusursuz [#9789](https://github.com/NuGet/Home/issues/9789)

* NuGet hata ayıklama ayrıntı düzeyi, bir paketin nereden geldiğini ( [#3055](https://github.com/NuGet/Home/issues/3055) ) bilmelidir

* NuGet paketi, sürüm numaraları içindeki noktanın yanlış bir şekilde atlanması yakalamalı [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Merkezi geçişli bağımlılıkların sabitlenmesini devre dışı bırakma- [#10132](https://github.com/NuGet/Home/issues/10132)

* Net5 TFG: eksik TPV [#9441](https://github.com/NuGet/Home/issues/9441) hata üret

* Geri yükleme günlüğü sırasında günlük paketi contenthash (ayıklama sırasında)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Restore- [#9986](https://github.com/NuGet/Home/issues/9986) eklentisini ÇAĞıRAN eski PR projeleri için bir ön kayıt mekanizması uygulayın

* Paket Yöneticisi 'nde birden fazla kaynak seçildiğinde NuGet paketi öneren çalışmalıdır [#10433](https://github.com/NuGet/Home/issues/10433)

* Normal ayrıntı düzeyinde geri yükleme yaparken, bir paketin hangi kaynak olarak geri yüklendiğini günlüğe kaydet- [#10461](https://github.com/NuGet/Home/issues/10461)

**Hatalar:**

* Inugetpackagefileservice-Codespaces ile bağlantılı ve tek başına [#10151](https://github.com/NuGet/Home/issues/10151) için görüntüleri ve ekli lisansları getirme

* VS OE: ıprojectmetadatacontextınfo eksik biçimlendirici- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-perf] Tek merkezde geçişli Tivedependencygroups- [#10002](https://github.com/NuGet/Home/issues/10002) yazılan bilgileri azaltma

* Yüklenemeyen bir proje nedeniyle oluşturulan geri yükleme işlemleri `NoOp` telemetri [#9985](https://github.com/NuGet/Home/issues/9985) olarak raporlanır

* Belirli renk paletlerine sahip simgeler PM Kullanıcı arabirimine KARŞı çökme ve- [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-perf] CPVM bilgilerini eklerken PackageSpec klonu azaltma- [#10003](https://github.com/NuGet/Home/issues/10003)

* PM Kullanıcı arabirimi-asyncbelirt simge yükleme- [#10009](https://github.com/NuGet/Home/issues/10009)

* PM Kullanıcı arabirimine simge URL 'Leri yüklenirken UI gecikmesi- [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource ve WPF Kullanıcı arabirimi iş parçacıklarında iş parçacığı benzeşimi- [#9161](https://github.com/NuGet/Home/issues/9161)

* TargetFramework diğer adı ile packastool olduğunda uyarı NU5128 için Uyarı- [#10097](https://github.com/NuGet/Home/issues/10097)

* Özelleştirilmiş bir derlemede paket hedeflerinde OutputPath mantığı düzgün çalışmıyor- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: istemcideki ıservicebroker örneğini önbelleğe alma- [#10141](https://github.com/NuGet/Home/issues/10141)

* PM kullanıcı arabiriminden kaldırma için NuGetProjectActions oluşturma bir paralel işlem- [#9956](https://github.com/NuGet/Home/issues/9956)

* Performans: eski projeler ve çekme isteği olmayan projeler için GetPackageSpecsAsync içindeki Uıdeyerleştirleri azaltma- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` birden fazla dosya göndermiyor- [#4393](https://github.com/NuGet/Home/issues/4393)

* Çıkış, yeniden yönlendirildiğinde macOS üzerinde 80 karaktere kaydırılır [#10198](https://github.com/NuGet/Home/issues/10198)

* Geri yükleme, kaynak <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406) ile başarısız oluyor

* netcoreapp 5.0-Windows, yolculuğa yuvarlamaz ve platform bilgilerini ayrıştırmaz- [#10177](https://github.com/NuGet/Home/issues/10177)

* Özel CPS projeleri geri yüklemek için AssemblyReferences proje özelliği gerektirir. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Lisans ve simge dosyası varlık denetimi her zaman büyük/küçük harfe duyarlı karşılaştırma kullanmalıdır [#9817](https://github.com/NuGet/Home/issues/9817)

* Dotnetclientoolreference geri yüklemeleri, Hayır-op projesi sayısı/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038) neden olmasını zorlaştırır

* "NuGet Paket Yöneticisi biçimini Seç" iletişim kutusunda, koyu Temada "bir sekmeye gidilirken, paket biçiminin kesik çizgi satırı kutusunu görmek zordur [#9729](https://github.com/NuGet/Home/issues/9729)

* #10314 geçişli çerçeve başvurularını hariç tut `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* Karşılaştırıcı statik özellikleri ıdempotent- [#10339](https://github.com/NuGet/Home/issues/10339) olmalıdır

* iç sözleşmeleri çözümleyin derleme yükleme (RPS 'yi çözün veya özel durum Al)- [#9919](https://github.com/NuGet/Home/issues/9919)

* GetServiceAsync ile GetService 'i NuGet. clients, 1. bölüm- [#10362](https://github.com/NuGet/Home/issues/10362) değiştirme

* CLı yüklemeleri listelenmemiş paketleri yüklememelidir- [#7466](https://github.com/NuGet/Home/issues/7466)

* Statik MSBuild Graf geri yükleme-gerekli MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335) günlüğü

* Privatevarlıklar olarak işaretlenen ProjectReferences 'ın Proje bağımlılıkları, kilit dosyasına en güncel Denetim- [#8565](https://github.com/NuGet/Home/issues/8565) dahil edilmemelidir.

* VS [#10406](https://github.com/NuGet/Home/issues/10406) 'de geri yükleme hatalarını göstermeyen hatalı VERILERI olan SDK projeleri

* LockedMode- [#9623](https://github.com/NuGet/Home/issues/9623) ile cmd satırından karışık eski ve netstandard2 projelerine sahip bir çözümü GERI yüklerken NU1004

* Paket, bağımlılık paketleri aracılığıyla geçerli projenin paketine getirilen içeriği içerir (yalnızca SDK tabanlı projeler)- [#8867](https://github.com/NuGet/Home/issues/8867)

* NuGet 'in VS genişletilebilirlik API hataları için telemetri ekleme- [#10062](https://github.com/NuGet/Home/issues/10062)

* Hata ayıklama performansını artırmak için statik grafik geri yüklemeye GenerateRestoreGraphFile ekleyin.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* NuGet Paket Yöneticisi açılamıyor- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/ekran okuyucusu "Apache-2,0" bağlantısı için "Lisans" etiketini okumuyor [#10425](https://github.com/NuGet/Home/issues/10425)

* Güncel durum çubuğu iletisi VS- [#9402](https://github.com/NuGet/Home/issues/9402) için mükemmel değildir

* packages.config package.lock.js, yanlış bir hedef Framework kullanır- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: #10439 telemetri çözme https://github.com/NuGet/NuGet.Client/pull/3786  -  [](https://github.com/NuGet/Home/issues/10439)

* "RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973) etkinleştirildikten sonra çözüm OLUŞTURULURKEN hata NU1004 kayboluyor

* Ters içindeki PMUı aracılığıyla sekme, ileri yönü yansıtmalıdır- [#10234](https://github.com/NuGet/Home/issues/10234)

* Deneysel örnekte PMUI hata ayıklaması bazen SolutionView 'dan ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416) 'e InvalidCastException oluşturur

* Varsayılan sürüm, uygun olmayan bir pakete tıklandıktan sonra, gözden geçirme sekmesinde- [#10380](https://github.com/NuGet/Home/issues/10380)

* Odak [#4176](https://github.com/NuGet/Home/issues/4176) , Visual Studio 'daki NuGet Yöneticisi yeniden yükler

* IPackageSourceProvider2 ve ilgili türleri kaldırma- [#10098](https://github.com/NuGet/Home/issues/10098)

* ' NameOfPackage ' paketi, projedeki ' All ' çerçeveleri ile uyumlu değil [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync gereksiz Ngetversion karşılaştırmaları- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. Client, Knowntakma adlarıyla Managedımagetakma adların kullanımı ile değiştirilmelidir [#9977](https://github.com/NuGet/Home/issues/9977)

* Kullanım dışı simgesi, gezinme sekmesindeki kullanım dışı bırakılan paketin sürümüyle örtüşüyor [#10452](https://github.com/NuGet/Home/issues/10452)

* PackageReference NU1604 hata işleme VS ve komut satırında (geri yükleme & Paket Yöneticisi Kullanıcı arabirimi) farklıdır. [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: gerekli biçimlendiricileri kayıtlı değil- [#10467](https://github.com/NuGet/Home/issues/10467)

* Net45 as 'yi NuGet. çerçeveler 'den hedef çerçeve olarak kaldırın- [#10470](https://github.com/NuGet/Home/issues/10470)

* Uygulama-PMC ve PowerShell kullanımıyla ilgili olayları izlemek için yeni Telemetriler ekleyin. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Paket Yöneticisi Kullanıcı arabiriminde güncelleştirilecek birden fazla paket varsa, yalnızca bir pakette önizleme değişiklikleri penceresinde gösterilir. [#10483](https://github.com/NuGet/Home/issues/10483)

* Çoklu hedefli projeler paketlendiğinde boş frameworkReferences grupları oluşturulmalıdır- [#10218](https://github.com/NuGet/Home/issues/10218)

* ' Güncelleştirmeler ' sekmesinde paketin onay kutusu, mavi/mavi (ekstra kontrast)/açık Temalar- [#8963](https://github.com/NuGet/Home/issues/8963) sekme ile gezinilirken kesik çizgi satırı kutusuyla odaklanır.

* Güncelleştirmeler sekmesi onay kutuları ekran okuyucular ile iyi çalışmaz [#10449](https://github.com/NuGet/Home/issues/10449)

* PMUI 'de güncelleştirme, nesne başvurusunun bir nesne örneğine ayarlanmamasını sağlar- [#9882](https://github.com/NuGet/Home/issues/9882)

* Uygulama-PMC ve PowerShell kullanımıyla ilgili olayları izlemek için yeni Telemetriler ekleyin. - [#10478](https://github.com/NuGet/Home/issues/10478)

* V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480) Kopyala-Yapıştır hatası

* NuGetPackageFileService onarımı- [#10503](https://github.com/NuGet/Home/issues/10503) atılabilir MemoryStream için using kullanın

**[Bu yayında düzeltilen tüm sorunların listesi-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Bu sürümdeki işlemelerin listesi-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Topluluk katkıları

Bu NuGet yayınını harika hale getirmek için size yardımcı olan tüm katkıda bulunanlar için teşekkürler!

|Sağlayan|PR 'ler|Sorunlar|
|----|----|----|
[omajıd](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480) Kopyala-Yapıştır hatası
[Marcin-kronyıstianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Privatevarlıklardır = "All" özniteliği- [#10397](https://github.com/NuGet/Home/issues/10397) için paketlere başvurulduğu durumlar için testler eksik
[Marcin-kronyıstianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Birden çok paket dağıtmaya yönelik destek ekleme- [#4393](https://github.com/NuGet/Home/issues/4393)
[Marcin-kronyıstianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Derleme imzalama devre dışı bırakıldığında NuGet kitaplıklarının derlemesi bozulur- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Katkıda bulunan belgeleri Temizleme- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Lisans ve simge dosyası varlık denetimi her zaman büyük/küçük harfe duyarlı karşılaştırma kullanmalıdır [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037) kullanırken, GEÇICI çözüm WPF sorunu Için BitmapCreateOptions. IgnoreColorProfile kullanın
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | NuGet 'de Windows SDK 10 bağlantısı kopuk. Istemci katkı Kılavuzu- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Göreli bağlantılar NuGet 'de kopuk. Istemci hata ayıklama Kılavuzu- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Test armatürleri ve ilgili kod [#9996](https://github.com/NuGet/Home/issues/9996) geliştirme
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Çıkış, yeniden yönlendirildiğinde macOS üzerinde 80 karaktere kaydırılır [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | NuGet. PackageManagement 'ı .NET Standard paket olarak kullanılabilir hale getirin- [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Paket görevi sırasında belirli tfms 'ler için derleme çıkışını hariç tutmak üzere yeni bir MSBuild özelliği ortaya çıkar [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Özet: 5.9.1 'deki yenilikler

* "DotNet NuGet Remove Source nuget.org" ilk [#10745](https://github.com/NuGet/Home/issues/10745) çalışmaz
* Varsayılan doğrulamayı Linux üzerinde devre dışı bırak, ancak varsayılan olarak Windows- [#10713](https://github.com/NuGet/Home/issues/10713) 'de etkin yap

**[Bu yayında düzeltilen tüm sorunların listesi-5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Bu sürümdeki işlemelerin listesi-5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="feedback-welcome"></a>Geri bildirim hoş geldiniz

Görüşleriniz bizim için önemlidir.  Bu sürümle ilgili herhangi bir sorun varsa, mevcut sorunlar için [GitHub sorunlarımızı](https://github.com/NuGet/Home/issues) ve [Visual Studio Geliştirici topluluğu](https://developercommunity.visualstudio.com/) ' na bakın.  NuGet içindeki yeni sorunlar için lütfen bir [GitHub sorunu](https://github.com/NuGet/Home/issues/new)bildirin.
Genel NuGet deneyimi sorunları için, **yardım > bir sorun bildirmek** üzere en sevdiğiniz IDE 'de bulunan [sorun bildir](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) seçeneğini kullanarak bize bilgi verin.
