---
title: NuGet 4.7 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.7.0 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813799"
---
# <a name="nuget-47-release-notes"></a>NuGet 4.7 Yayın Notları

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)ile geliyor.

## <a name="summary-whats-new-in-470"></a>Özeti: 4.7.0 Yenilikler

* [Depo İmzalı paketleri](https://github.com/NuGet/Home/wiki/Repository-Signatures) etkinleştirmek için artırılmış paket imzalama

* Visual Studio Sürüm 15.7 ile [packagereference biçimini kullanan mevcut projeleri geçirebilme](../consume-packages/migrate-packages-config-to-package-reference.md) özelliğini kullanıma sunduk.

## <a name="summary-whats-new-in-472"></a>Özet: 4.7.2'de Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır

## <a name="summary-whats-new-in-473"></a>Özeti: Yenilikler 4.7.3

* Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906

## <a name="known-issues"></a>Bilinen sorunlar

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

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar

.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır. [Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde düzeltilen en önemli sorunlar

### <a name="bugs"></a>Hatalar

* NuGet .Net Core proje sisteminde (yeni regresyon) bir çıkmaza girer. - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: PackagePath, TfmSpecificPackageFile globbing yolları ile [kullanılırsa](https://github.com/NuGet/Home/issues/6726) yanlış oluşturulur - #6726
* Pack: web api projesi, ispackable açıkça ayarlanmadığı sürece paket oluşturamaz. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI ve PMC yeni paketi görmek için 30min almak (nuget.exe hemen görür) - [#6657](https://github.com/NuGet/Home/issues/6657)
* İmzalama: SignatureUtility.GetCertificateChain(...) tüm zincir durumlarını kontrol etmez - [#6565](https://github.com/NuGet/Home/issues/6565)
* İmzalama: DER GeneralizedTime işleme geliştirmek - [#6564](https://github.com/NuGet/Home/issues/6564)
* İmzalama: VS, değiştirilmiş bir paket yüklerken NU3002 hatası göstermez - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary büyük/küçük harf duyarlıdır - [#6500](https://github.com/NuGet/Home/issues/6500)
* Yükleme/güncelleştirme geri yükleme kodu ve Geri Yükleme kodu yolları tutarlı değildir - [#3471](https://github.com/NuGet/Home/issues/3471)
* Çözüm PackageManager Version ComboBox klavye üzerinden ayırıcı seçebilirsiniz - [#2606](https://github.com/NuGet/Home/issues/2606)
* Kaynak `https://www.myget.org/F/<id>` --- için hizmet dizinini yükleyemeyen> system.Net.Http.HttpRequestException: Yanıt durum kodu başarıyı göstermez: 403 (Yasak) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCRs

* İstekler arasında ilişkilendirmek için X-NuGet-Session-Id üstbilgisini yayan [özellik önerisi] - [#5330](https://github.com/NuGet/Home/issues/5330)
* IVs apis üzerinden Visual Studio'da çalışan geri yükleme işlemini beklemenin bir yolunu ortaya çıkar. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint ek hizmet url soneki kaçınacaktır - [#6586](https://github.com/NuGet/Home/issues/6586)
* bilgilendirme sürümüne karma ekleme - [#6492](https://github.com/NuGet/Home/issues/6492)
* İmzalama: depo imza/karşı imza kaldırma etkinleştirme - [#6646](https://github.com/NuGet/Home/issues/6646)
* İmzalama: Depo imza/karşı imza sıyırma için API - [#6589](https://github.com/NuGet/Home/issues/6589)
* Kaynak bilgilerini VS'de günlüğe kaydedin - [#6527](https://github.com/NuGet/Home/issues/6527)
* Yalnızca TFM ve RID'deki araçlara filtre uygulayın, böylece XML ayarları /tools klasörüne konabilir - [#6197](https://github.com/NuGet/Home/issues/6197)
* Pack komutu ile başlayan bir dosyayı dışladığında uyar  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Bu sürümde düzeltilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
