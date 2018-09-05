---
title: NuGet 4.7 RTM sürüm notları
description: NuGet 4.7.0 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 4ecbdc5475837b1aa1e723a94c2c6c3e8460f9ef
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549434"
---
# <a name="nuget-47-rtm-release-notes"></a>NuGet 4.7 RTM sürüm notları

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Özet: Bu Yayındaki Yenilikler

* Biz paketi etkinleştirmek imzalama Genişletilmiş [depo imzalanmış paketleri](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Visual Studio sürüm 15.7 ile yeteneği ekledik [PackageReference kullanılacak Packages.config dosyasının biçimini kullanan mevcut projeleri](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) yerine.

## <a name="known-issues"></a>Bilinen sorunlar

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar

.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır. [Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde giderilen en önemli sorunlar

### <a name="bugs"></a>Hatalar

* NuGet bir kilitlenme.Net Core proje sistemi (yeni gerileyiş) çalıştırır. - [#6733](https://github.com/NuGet/Home/issues/6733)
* Paketi: TfmSpecificPackageFile ile Glob yolları - kullanılıyorsa PackagePath hatalı oluşturulmuş [#6726](https://github.com/NuGet/Home/issues/6726)
* Paketi: web API projesi ispackable açıkça ayarlamadığınız sürece paket oluşturulamıyor. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS kullanıcı Arabirimi ve PMC ele yeni paket görmek için 30 dakika (nuget.exe görür, hemen) - [#6657](https://github.com/NuGet/Home/issues/6657)
* İmzalama: Tüm zincir durumları - SignatureUtility.GetCertificateChain(...) denetlemez [#6565](https://github.com/NuGet/Home/issues/6565)
* İmzalama: DER GeneralizedTime işleme - geliştirmek [#6564](https://github.com/NuGet/Home/issues/6564)
* İmzalama: VS göstermiyor NU3002 hata üzerinde oynanmış bir paket - yüklerken [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary küçük harfe duyarlıdır - [#6500](https://github.com/NuGet/Home/issues/6500)
* Yükleme/güncelleştirme geri yükleme kod ve geri yükleme kod yollarını tutarlı değil - [#3471](https://github.com/NuGet/Home/issues/3471)
* Çözüm PackageManager sürüm ComboBox - klavyeden ayırıcı seçebilirsiniz [#2606](https://github.com/NuGet/Home/issues/2606)
* Hizmet dizini için kaynak yüklenemedi `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: yanıt durum kodu, başarı belirtmez: 403 (Yasak) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Dcr

* [Özellik teklifi] - istekler arasında bağıntı kurmak için emit X-NuGet-oturum-Id üst bilgisi [#5330](https://github.com/NuGet/Home/issues/5330)
* Visual Studio'da Iv'ler API'leri üzerinden çalışan geri yükleme işlemi üzerinde çalışan beklenecek bir yol ortaya çıkarır. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint hizmet URL'si ekleme engel olacak soneki - [#6586](https://github.com/NuGet/Home/issues/6586)
* Bilgilendirme sürümü için - yürütme karmasını ekleme [#6492](https://github.com/NuGet/Home/issues/6492)
* İmzalama: depo imza/onay imzası - kaldırılmasını etkinleştirme [#6646](https://github.com/NuGet/Home/issues/6646)
* İmzalama: depo imza/onay imzası şeridi oluşturma için API- [#6589](https://github.com/NuGet/Home/issues/6589)
* VS - kaynak bilgilerini günlüğe kaydetme [#6527](https://github.com/NuGet/Home/issues/6527)
* Ayarları XML /tools klasöründe - koyabilirsiniz /tools yalnızca TFM ve RID, filtre [#6197](https://github.com/NuGet/Home/issues/6197)
* Uyar paketi komut ile başlayan bir dosya dahil değildir.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Bu sürümde düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
