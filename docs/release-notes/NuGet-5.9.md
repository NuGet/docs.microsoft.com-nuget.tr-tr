---
title: NuGet 5.9 Sürüm Notları
description: Yeni özellikler, hata düzeltmeleri ve DCR'ler de dahil olmak üzere NuGet 5.9 sürüm notları.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323888"
---
# <a name="nuget-59-release-notes"></a>NuGet 5.9 Sürüm Notları

NuGet dağıtım araçları:

| NuGet sürümü | Yeni sürümde Visual Studio kullanılabilir | .NET SDK'larında kullanılabilir |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküyle Visual Studio 2019 ile yükleme
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 ve .NET 5.0.200+ için 5.9 veya NuGet.exe gerekir.

## <a name="summary-whats-new-in-59"></a>Özet: 5.9'daki YeniLer

* Güncelleştirilen önceden seçilmiş paketlerle Paket Yöneticisi kullanıcı arabirimini başlatan paket bağımlılıkları için "Güncelleştir" bağlam menü öğesini [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Paket "Güncelleştirme" deneyimine sağ tıklayın](media/releasenotes-59-update.png)

* İstenen sürümü (kayan sürüm veya sürüm aralığı isteği dahil) çözüm düzeyindeki proje listesinin "Sürüm" sütununda Paket Yöneticisi ui - [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Kullanıcı arabiriminde çözüm düzeyinde istenen Paket Yöneticisi](media/releasenotes-59-requested-version.png)

* A/B testi olarak yayımlanan Paket Yöneticisi Kullanıcı Arabirimi Gözat sekmesinde IntelliCode paket önerileri - [#10053](https://github.com/NuGet/Home/issues/10053)

* Dosyayı `.nupkg.metadata` yükleme kaynağını içerecek şekilde genişletme - [#10354](https://github.com/NuGet/Home/issues/10354)

* Paket görevi sırasında belirli TFM'ler için derleme çıkışını dışlamak için yeni bir msbuild [özelliği](https://github.com/NuGet/Home/issues/10396) #10396

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**DCR'ler (Tasarım Değişikliği İsteği):**

* En son paket sürümü yüklüyken aşağı simge simgesi sezgisel değildir. Eski yeşil onay işareti mükemmeldi - [#9789](https://github.com/NuGet/Home/issues/9789)

* Nuget Hata Ayıklama ayrıntılılığı paketin nereden geldiğini [](https://github.com/NuGet/Home/issues/3055) #3055

* NuGet paketi, noktanın sürüm numaralarıyla yanlış şekilde eksik olduğunu yakalamalı - [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Merkezi geçişli bağımlılıkların sabitlemesini devre dışı bırakma - [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: TPV eksik olduğunda hata üret - [#9441](https://github.com/NuGet/Home/issues/9441)

* Geri yükleme günlüğü (ayıklama sırasında) sırasında paket içeriğini günlüğe kaydetme - [#10384](https://github.com/NuGet/Home/issues/10384)

* Çözüm açıkken geri yükleme çağıran eski PR projeleri için bir ön kayıt mekanizması uygulama - [#9986](https://github.com/NuGet/Home/issues/9986)

* Paket yöneticisinde birden fazla kaynak seçildiğinde NuGet paket [](https://github.com/NuGet/Home/issues/10433) önericisi #10433

* Normal ayrıntılı olarak geri yüklenirken, paketin hangi kaynaktan geri [](https://github.com/NuGet/Home/issues/10461) yükleniyor olduğunu günlüğe #10461

**Hatalar:**

* INuGetPackageFileService - Codespaces'a bağlı ve tek başına için görüntüleri ve katıştırılmış lisansları getirme - [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo eksik biçimlendiren - [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] centralTransitiveDependencyGroups [-](https://github.com/NuGet/Home/issues/10002) #10002

* Projenin yüklenmemiş olması nedeniyle meydana gelen geri yükleme işlemleri `NoOp` telemetrisinde olarak [raporlandı](https://github.com/NuGet/Home/issues/9985) - #9985

* Belirli renk paletleri olan simgeler PM kullanıcı arabiriminin VS [-](https://github.com/NuGet/Home/issues/10037) #10037

* [CPVM-Perf] CPVM bilgilerini eklerken PackageSpec kopyasını azaltma - [#10003](https://github.com/NuGet/Home/issues/10003)

* PM kullanıcı arabirimi - zaman uyumsuzlaştırma simgesi yükleme - [#10009](https://github.com/NuGet/Home/issues/10009)

* PM kullanıcı arabiriminde simge URL'leri yüklenirken kullanıcı arabirimi gecikmesi - [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource ve WPF UI iş parçacıklarında iş parçacığı benzeşmi - [#9161](https://github.com/NuGet/Home/issues/9161)

* Targetframework diğer adı ile packastool olduğunda nu5128 uyarısı - [#10097](https://github.com/NuGet/Home/issues/10097)

* Özelleştirilmiş bir derlemede Pack hedeflerine yönelik OutputPath mantığı düzgün çalışmıyor - [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: İstemcide IServiceBroker [](https://github.com/NuGet/Home/issues/10141) örneğini önbelleğe #10141

* PM kullanıcı arabiriminden kaldırmak için NuGetProjectActions oluşturmayı paralel bir işlem yapma - [#9956](https://github.com/NuGet/Home/issues/9956)

* Performans: Eski projeler ve PR olmayan projeler için GetPackageSpecsAsync içinde UIDelays azaltma - [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` birden fazla dosya itmez - [#4393](https://github.com/NuGet/Home/issues/4393)

* Çıkış, yeniden yönlendirilmesiyle macOS üzerinde 80 karakter olarak sarmalanmış - [#10198](https://github.com/NuGet/Home/issues/10198)

* -Source #9406 ile geri <Relative Path>  -  [yükleme başarısız oluyor](https://github.com/NuGet/Home/issues/9406)

* netcoreapp5.0-windows gidiş dönüş değil ve platform bilgilerini ayrıştırmaz - [#10177](https://github.com/NuGet/Home/issues/10177)

* Özel CPS projeleri geri yüklemek için AssemblyReferences proje özelliği gerektirir. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Lisans ve simge dosya varlığı denetimi her zaman büyük/küçük harfe duyarlı bir karşılaştırma kullan [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference geri yüklemeleri, hiçbir op proje sayısı/uptodateprojectscount [-](https://github.com/NuGet/Home/issues/10038) #10038

* Koyu tema - #9729'daki "NuGet Paket Yöneticisi Biçimi Seç" iletişim kutusunda sekmeyle gezinirken paket biçiminin çizgi çizgi kutusunu [görmek #9729](https://github.com/NuGet/Home/issues/9729)

* Geçişli çerçeve başvurularını #10314 `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* Karşılaştırıldığında statik özellikleri birmpotent olmalıdır - [#10339](https://github.com/NuGet/Home/issues/10339)

* iç anlaşma derleme yüklemesini çözümleme (RPS'yi düzeltme veya özel durum #9919 [](https://github.com/NuGet/Home/issues/9919)

* GetService'i NuGet.Clients'da GetServiceAsync ile değiştirin, Bölüm 1 - [#10362](https://github.com/NuGet/Home/issues/10362)

* CLI yüklemeleri listelenmemiş paketleri yüklemez - [#7466](https://github.com/NuGet/Home/issues/7466)

* Statik msbuild graf geri yükleme - MSBuildStartupDirectory hakkında yeni günlük kaydı - [#10335](https://github.com/NuGet/Home/issues/10335)

* PrivateAssets olarak işaretlenmiş ProjectReferences Proje Bağımlılıkları, kilit dosyasına güncel denetime dahil edilme #8565 [](https://github.com/NuGet/Home/issues/8565)

* VS'de geri yükleme hatalarını göstermeyen hatalı verilere sahip SDK projeleri - [#10406](https://github.com/NuGet/Home/issues/10406)

* LockedMode ile cmd hattından Eski ve netstandard2 projeleri karışık olan bir çözümü geri yüklemede NU1004 - [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack, bağımlılık paketleri aracılığıyla geçerli projenin paketine getirilen içeriği içerir (yalnızca SDK tabanlı projeler) - [#8867](https://github.com/NuGet/Home/issues/8867)

* NuGet'in VS genişletilebilirlik API'si hataları için telemetri ekleme - [#10062](https://github.com/NuGet/Home/issues/10062)

* Hata ayıklamayı geliştirmek için statik graf geri yüklemesinde GenerateRestoreGraphFile ekleyin.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* NuGet Paket yöneticisi aç değil - [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Ekran Okuyucusu "Apache-2.0" bağlantısı için "Lisans" etiketini okuymister - [#10425](https://github.com/NuGet/Home/issues/10425)

* VS'de güncel durum çubuğu iletisi harika değil [-](https://github.com/NuGet/Home/issues/9402) #9402

* packages.config package.lock.jsyanlış bir hedef çerçeve kullanıyor - [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: veri kaynaklarından https://github.com/NuGet/NuGet.Client/pull/3786  -  [telemetri #10439](https://github.com/NuGet/Home/issues/10439)

* "RestoreLockedMode" - #8973 etkinleştirdikten sonra çözüm 1004 [hatası görüntüden #8973](https://github.com/NuGet/Home/issues/8973)

* Ters yönde PMUI üzerinden sekmeyle ilerlemenin ileri yönde yansıtılmış olması gerekir - [#10234](https://github.com/NuGet/Home/issues/10234)

* Deneysel Örnekte PMUI hata ayıklaması bazen SolutionView'dan ProjectView'a InvalidCastException hatası [#10416](https://github.com/NuGet/Home/issues/10416)

* Gözat sekmesinde kullanım dışı bir pakete tıklandıktan sonra varsayılan sürüm null olur - [#10380](https://github.com/NuGet/Home/issues/10380)

* Odak yeniden Visual Studio nuGet yöneticisi yeniden yük biner - [#4176](https://github.com/NuGet/Home/issues/4176)

* IPackageSourceProvider2 ve ilgili türleri kaldırma - [#10098](https://github.com/NuGet/Home/issues/10098)

* 'NameOfPackage' paketi projesinde 'all' çerçeveleriyle uyumsuz - [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync gereksiz NuGetVersion Karşılaştırmaları yapar - [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client, ManagedImageMonikers yerine KnownMonikers - [#9977](https://github.com/NuGet/Home/issues/9977)

* Kullanım dışı simgesi, Gözat sekmesindeki kullanım dışı paketin sürümüyle çakışıyor [-](https://github.com/NuGet/Home/issues/10452) #10452

* PackageReference NU1604 hata işleme VS ve komut satırı (Kullanıcı Arabirimini geri & Paket Yöneticisi) arasında [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: gerekli biçimlendirenler kayıtlı değil - [#10467](https://github.com/NuGet/Home/issues/10467)

* NuGet.Frameworks'te net45'i hedef çerçeve olarak kaldırma - [#10470](https://github.com/NuGet/Home/issues/10470)

* Uygulama - PMC ve PowerShell kullanımıyla ilgili olayları izlemek için yeni telemetriler ekleyin. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Paket Yöneticisi Kullanıcı Arabiriminde güncelleştirilebilir birden çok paket olduğunda Önizleme Değişiklikleri penceresinde yalnızca Paket Yöneticisi paket [#10483](https://github.com/NuGet/Home/issues/10483)

* Çok hedefli projeleri paketlerken boş frameworkReferences grupları oluşturulacak - [#10218](https://github.com/NuGet/Home/issues/10218)

* 'Güncelleştirmeler' Sekmesinde paketin onay kutusunu görmek, Mavi/Mavi (Ek Karşıtlık)/Açık temalarda Sekme'de gezinirken [](https://github.com/NuGet/Home/issues/8963) çizgi çizgi kutuyla #8963

* Güncelleştirmeler Sekmesi onay kutuları ekran okuyucularla iyi çalışmıyor - [#10449](https://github.com/NuGet/Home/issues/10449)

* PMUI'de güncelleştirme Nesne başvurusu bir nesnenin örneğine ayarlanmazken neden oluyor - [#9882](https://github.com/NuGet/Home/issues/9882)

* Uygulama - PMC ve PowerShell kullanımı izlemesi ile ilgili olayları izlemek için yeni telemetriler ekleyin. - [#10478](https://github.com/NuGet/Home/issues/10478)

* V2FeedPackageInfo içinde kopyala-yapıştır hatası - [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService düzeltmesi - atılabilir bellek akışı için kullanma - [#10503](https://github.com/NuGet/Home/issues/10503)

**[Bu sürümde düzeltilecek tüm sorunların listesi - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Bu sürümde işlemelerin listesi - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Topluluk katkıları

Bu NuGet yayına harika bir şekilde katkıda bulunan tüm katılımcılara teşekkür ederiz!

|Kim|Prs|Sorunlar|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo içinde kopyala-yapıştır hatası - [#10480](https://github.com/NuGet/Home/issues/10480)
[janin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Paketlerin PrivateAssets="All" özniteliğiyle başvurul olduğu durum için eksik testler - [#10397](https://github.com/NuGet/Home/issues/10397)
[janin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Birden çok paket itme desteği ekleme - [#4393](https://github.com/NuGet/Home/issues/4393)
[janin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Derleme imzalama devre dışı bırakılırken NuGet kitaplıklarının derlemesi bozuk - [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Katkıda bulunan belgeleri temizleme - [#10399](https://github.com/NuGet/Home/issues/10399)
[OlarakLavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Lisans ve simge dosya varlığı denetimi her zaman büyük/küçük harfe duyarlı bir karşılaştırma kullan [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | DecodePixelWidth - #10037 kullanırken WPF sorununa geçici çözüm olarak BitmapCreateOptions.IgnoreColorProfile [kullanın](https://github.com/NuGet/Home/issues/10037)
[gökyamcıkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10 bağlantı NuGet.Client Katkı kılavuzunda bozuk - [#10099](https://github.com/NuGet/Home/issues/10099)
[gökyamcıkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | NuGet.Client hata ayıklama kılavuzunda göreli bağlantılar bozuk - [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Test testlerini ve ilgili kodu geliştirme - [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbarakne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Çıkış, yeniden yönlendirilmesiyle macOS üzerinde 80 karakter olarak sarmalanmış - [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | NuGet.PackageManagement'ı bir .NET Standard olarak kullanılabilir [hale](https://github.com/NuGet/Home/issues/6150) #6150
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Paket görevi sırasında belirli tfm'ler için derleme çıkışını dışlamak için yeni bir msbuild [özelliği](https://github.com/NuGet/Home/issues/10396) #10396

## <a name="summary-whats-new-in-591"></a>Özet: 5.9.1'de YapılanLar

* "dotnet nuget remove source nuget.org" ilk kez çalışmıyor - [#10745](https://github.com/NuGet/Home/issues/10745)
* Linux'ta varsayılan doğrulamayı devre dışı bırak ama Windows'da varsayılan olarak etkinleştir - [#10713](https://github.com/NuGet/Home/issues/10713)

**[Bu sürümde düzeltilecek tüm sorunların listesi - 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Bu sürümde işlemelerin listesi - 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>nuget 5.9 paketi özel durum `Null Reference` oluşturur. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Sorun
Bir dosyayı kullanmaya devam etmek, açıkça derleme başvuruları hedeflenen projeler için herhangi bir eklemeden belirtilirse sürüm `pack` `.nuspec` bir özel durum `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` `multiple frameworks` oluşturur.

#### <a name="workaround"></a>Geçici çözüm
`nuget.exe` [5.8.1 veya](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe) dışında en son sürümü `5.9.1` kullanın.

## <a name="feedback-welcome"></a>Geri bildirim hoş geldiniz

Geri bildiriminiz bizim için önemlidir.  Bu sürümle ilgili herhangi bir sorun varsa GitHub Sorunları [sayfamızı ve mevcut Visual Studio Geliştirici Topluluğu](https://github.com/NuGet/Home/issues) bakın. [](https://developercommunity.visualstudio.com/)  NuGet içindeki yeni sorunlar için lütfen bir [GitHub Sorunu rapor edin.](https://github.com/NuGet/Home/issues/new)
Genel NuGet deneyimi sorunları için Yardım [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ve Sorun Bildir altında sık kullanılan IDE'niz içinde bulunan **bir sorun > bize bildirebilirsiniz.**
