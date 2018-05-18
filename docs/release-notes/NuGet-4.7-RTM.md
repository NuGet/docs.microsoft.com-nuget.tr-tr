---
title: NuGet 4.7 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 4.7.0 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f23cc2973fa6370d9b7513d415fd8151b822c104
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/17/2018
---
# <a name="nuget-47-rtm-release-notes"></a>NuGet 4.7 RTM sürüm notları

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Özet: Bu Yayındaki Yenilikler

* Etkinleştirmek imzalama augemented paket sahibiz [depo imzalanan paketleri](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Visual Studio sürümü 15.7 ile yeteneği gösterdiğimizi [packages.config biçimi PackageReference kullanmayı mevcut projeleri geçirmek](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) yerine.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Seçeneği sağ bağlam menüsünde kullanılabilir değil

#### <a name="issue"></a>Sorun

Bir proje ilk kez açıldığında bir NuGet işlemi gerçekleştirilene kadar NuGet başlatılmamış. Bu geçiş seçeneği sağ bağlam menüsü üzerinde gösterme neden `packages.config` veya `References`.

#### <a name="workaround"></a>Geçici Çözüm

SPN'i aşağıdaki NuGet eylemlerden herhangi birini:
* Paket Yöneticisi kullanıcı Arabirimi - açık sağ `References` ve seçin `Manage NuGet Packages...`
* Gelen Paket Yöneticisi konsolu - açmak `Tools > NuGet Package Manager`seçin `Package Manager Console`
* Çalışma NuGet geri yükleme - Çözüm Gezgini'nde çözüm düğümüne sağ tıklayın ve seçin `Restore NuGet Packages`
* Ayrıca NuGet restore tetikler projeyi derleme

Şimdi geçiş seçeneği görüyor olmalısınız. Bu seçenek desteklenmiyor ve ASP.NET ve C++ proje türleri için gösterilmez unutmayın.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları

.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır. [Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde sabit üst sorunları

### <a name="bugs"></a>Hatalar

* NuGet bir kilitlenme çekirdek proje sistemini (yeni regresyon) .net içinde çalışır. - [#6733](https://github.com/NuGet/Home/issues/6733)
* Paketi: TfmSpecificPackageFile genelleme yollarını ile - kullandıysanız ise PackagePath hatalı oluşturulmuş [#6726](https://github.com/NuGet/Home/issues/6726)
* Paketi: ispackable açıkça ayarlanmazsa web API projesi paket oluşturulamaz. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS kullanıcı Arabirimi ve PMC ele yeni paket görmek için 30 dakika (nuget.exe görür, hemen) - [#6657](https://github.com/NuGet/Home/issues/6657)
* İmzalama: SignatureUtility.GetCertificateChain(...) tüm zinciri durumların - denetlemez [#6565](https://github.com/NuGet/Home/issues/6565)
* İmzalama: DER GeneralizedTime işleme - artırmak [#6564](https://github.com/NuGet/Home/issues/6564)
* İmzalama: VS göstermiyor NU3002 hata - üzerinde oynanmış bir paket yüklerken [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary büyük küçük harf duyarlı - [#6500](https://github.com/NuGet/Home/issues/6500)
* Geri yükleme/kodunun ve geri yükleme kod yolları tutarlı değil - [#3471](https://github.com/NuGet/Home/issues/3471)
* Çözüm PackageManager sürüm ComboBox ayırıcı - klavyeden seçebilirsiniz [#2606](https://github.com/NuGet/Home/issues/2606)
* Kaynak hizmet dizini yüklenemiyor `https://www.myget.org/F/<id>` System.Net.Http.HttpRequestException--->: yanıt durum kodu, başarı belirtmez: 403 (Yasak) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Dcr

* [Özellik teklifi] - isteklerinde ilişkilendirmek için emit X-NuGet-oturum-ID üstbilgi [#5330](https://github.com/NuGet/Home/issues/5330)
* Visual Studio'da çalışan Iv'ler API'leri geri yükleme işlemi üzerinde çalışan bekleyin bir şekilde kullanıma sunma. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint hizmeti URL'si sonuna ekleme engel olacak soneki - [#6586](https://github.com/NuGet/Home/issues/6586)
* bilgilendirme sürüme - yürütme karmasını eklemek [#6492](https://github.com/NuGet/Home/issues/6492)
* İmzalama: depo imza/onay imzası - kaldırılmasını etkinleştirmek [#6646](https://github.com/NuGet/Home/issues/6646)
* İmzalama: depo imza/onay imzası çıkarma için API- [#6589](https://github.com/NuGet/Home/issues/6589)
* Kaynak bilgileri VS - oturum [#6527](https://github.com/NuGet/Home/issues/6527)
* Ayarları XML /tools klasöründe - yerleştirilebileceği /tools yalnızca TFM ve RID, filtre [#6197](https://github.com/NuGet/Home/issues/6197)
* Ne zaman uyar Paketi komutu ile başlayan bir dosya dışlar.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Bu sürümde giderilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
