---
title: NuGet 4,7 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4.7.0 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 143781cf0a95c6a156d4afcd83ad277f3e227711
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780167"
---
# <a name="nuget-47-release-notes"></a>NuGet 4,7 sürüm notları

[Visual Studio 2017 15,7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)ile birlikte gelir.

## <a name="summary-whats-new-in-470"></a>Özet: 4.7.0 'deki yenilikler

* [Depodaki imzalı paketleri](https://github.com/NuGet/Home/wiki/Repository-Signatures) etkinleştirmek için genişlettik paket imzalama

* Visual Studio sürüm 15,7 ile, [packages.config biçimini kullanan mevcut projeleri, bunun yerine PackageReference kullanmak için geçirme](../consume-packages/migrate-packages-config-to-package-reference.md) özelliğini sunuyoruz.

## <a name="summary-whats-new-in-472"></a>Özet: 4.7.2 'deki yenilikler

* Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Özet: 4.7.3 'deki yenilikler

* Güvenlik onarımı: NUPKGs içindeki dosyaların, NUPKG dizininin üzerinde göreli bir yolu olabilir [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...`Seçenek, sağ tıklama bağlam menüsünde kullanılamaz

#### <a name="issue"></a>Sorun

Bir proje ilk açıldığında NuGet bir NuGet işlemi gerçekleştirilene kadar başlatılmamış olabilir. Bu, veya üzerindeki sağ tıklama bağlam menüsünde geçiş seçeneğinin gösterilmamasını sağlar `packages.config` `References` .

#### <a name="workaround"></a>Geçici çözüm

Aşağıdaki NuGet eylemlerinden birini gerçekleştirin:
* Paket Yöneticisi Kullanıcı arabirimini açın-sağ tıklayıp `References` seçin `Manage NuGet Packages...`
* Paket Yöneticisi konsolunu açın-Kimden `Tools > NuGet Package Manager` ' i seçin `Package Manager Console`
* NuGet geri yükleme Çalıştır-Çözüm Gezgini çözüm düğümüne sağ tıklayın ve şu seçeneği belirleyin `Restore NuGet Packages`
* Ayrıca NuGet geri yüklemeyi tetikleyen projeyi oluştur

Şimdi geçiş seçeneğini görebilmeniz gerekir. Bu seçeneğin desteklenmediğini ve ASP.NET ve C++ proje türleri için gösterilmediğini unutmayın.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2,0 ile ilgili sorunlar

.NET Standard & aracı .NET Framework, .NET Standard 2,0 veya önceki sürümleri hedefleyen projeler & NuGet paketlerini tüketebileceği şekilde tasarlanmıştır. [Bu belgede, bu](https://github.com/dotnet/standard/issues/481) senaryonun etrafındaki sorunlar, bunları ele almak için plan ve BT 'nin araç durumuyla birlikte dağıtabileceğiniz geçici çözümler özetlenmektedir.

## <a name="top-issues-fixed-in-this-release"></a>Bu yayında düzeltilen en önemli sorunlar

### <a name="bugs"></a>Hatalar

* NuGet .Net Core proje sisteminde bir kilitlenme halinde çalışır (yeni regresyon). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: TfmSpecificPackageFile, glob Paths ile kullanılırsa, PackagePath yanlış oluşturulur- [#6726](https://github.com/NuGet/Home/issues/6726)
* Paket: ıpackable açık olarak ayarlanmadığı takdirde Web API projesi paket oluşturamaz. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS Kullanıcı arabirimi ve PMC, yeni paketi (nuget.exe hemen görür) görmek için 30 dakika sürer [#6657](https://github.com/NuGet/Home/issues/6657)
* İmzalama: SignatureUtility. Getcertificatezincirine (...) tüm zincir durumlarını denetlemez- [#6565](https://github.com/NuGet/Home/issues/6565)
* İmzalama: DER GeneralizedTime işlemeyi geliştirme- [#6564](https://github.com/NuGet/Home/issues/6564)
* İmzalama: VS paketi yüklenirken bir NU3002 hatası göstermez- [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile. GetLibrary büyük/küçük harfe duyarlıdır- [#6500](https://github.com/NuGet/Home/issues/6500)
* Yükleme/güncelleştirme geri yükleme kodu ve geri yükleme kodu yolları tutarlı değil [#3471](https://github.com/NuGet/Home/issues/3471)
* Çözüm PackageManager sürümü açılan kutusu, klavye ile ayırıcı seçebilir [#2606](https://github.com/NuGet/Home/issues/2606)
* Kaynak `https://www.myget.org/F/<id>` ---> sistemi .NET için hizmet dizini yüklenemiyor. http. HttpRequestException: yanıt durum kodu başarıyı göstermiyor: 403 (yasak)- [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* İstekler arasında ilişkilendirmek için X-NuGet-Session-ID üst bilgisini yay [özellik teklifi]- [#5330](https://github.com/NuGet/Home/issues/5330)
* Visual Studio 'da IVS API 'leri aracılığıyla çalışan geri yükleme işlemini beklemek için bir yol sunun. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe-NoServiceEndpoint, hizmet URL sonekini eklemeyi önler- [#6586](https://github.com/NuGet/Home/issues/6586)
* bilgilendirici sürüme COMMIT Hash ekleme- [#6492](https://github.com/NuGet/Home/issues/6492)
* İmzalama: depo imzasını/onay imzasını kaldırmayı etkinleştir- [#6646](https://github.com/NuGet/Home/issues/6646)
* İmzalama: performans deposu imzası/onay imzası için API- [#6589](https://github.com/NuGet/Home/issues/6589)
* VS [#6527](https://github.com/NuGet/Home/issues/6527) 'de günlük kaynağı bilgileri
* /Tools 'u yalnızca tfd ve RID üzerinde filtreleyin. bu nedenle, ayarlar XML 'i/Tools klasörüne koyabilirsiniz- [#6197](https://github.com/NuGet/Home/issues/6197)
* Paket komutu ile başlayan bir dosyayı dışladığı zaman uyar.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Bu yayında düzeltilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
