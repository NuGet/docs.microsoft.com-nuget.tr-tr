---
title: NuGet 4.6 RTM sürüm notları
description: NuGet 4.6.0 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 3c71d05144aa2b92b916d4ebf319c5a4e321581f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549850"
---
# <a name="nuget-46-rtm-release-notes"></a>NuGet 4.6 RTM sürüm notları

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Özet: Bu Yayındaki Yenilikler

* İçin destek ekledik [imzalama paketleri](../create-packages/sign-a-package.md).
* Visual Studio 2017 nuget.exe artık doğrular ve paket bütünlüğü yüklemeden önce için paketler geri yükleniyor [imzalı paketlerin](../reference/signed-packages-reference.md).
* Art arda gelen geri yüklemeler performansı geliştirildi.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır. [Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde giderilen en önemli sorunlar

**Performans düzeltmeleri**

* Varlık dosyaları - değişiklik olduğunda yazmayın [#6491](https://github.com/NuGet/Home/issues/6491)
* Geri yükleme, alt projeler TFM eşleşmiyor, ana proje ile - ek MSBuild değerlendirme neden [#6311](https://github.com/NuGet/Home/issues/6311)
* Bağımlılık iyileştirerek NoOp geri yükleme perf geliştirmek graph özel oluşturma - [#6252](https://github.com/NuGet/Home/issues/6252)

**Hataları**

* Anında iletme yerel klasöre bırakır kilitli - nupkg [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet eklentisi uygulama: birden çok sorunları - [#6149](https://github.com/NuGet/Home/issues/6149)
* -Sorgu hizmet çağrısı MEF başlatılmasından VSSolutionManager, Remove - UIHang [#6110](https://github.com/NuGet/Home/issues/6110)
* Hata raporlama için özel paket indirme görev - iptal [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe değiştirir '+' ile '% 2B' derleme adı - [#5956](https://github.com/NuGet/Home/issues/5956)
* PM UI ve konsol - fn + F1'e sağ yardım sayfasına almaz [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet mutlak yollar belirli koşullarda - proje dosyalarını Yazar [#5888](https://github.com/NuGet/Home/issues/5888)
* 4.3 regresyon - yer tutucuları $product$ ve dönüştürme - aracılığıyla contentfile yerine değil $AssemblyGuid$ düzeltme [#5880](https://github.com/NuGet/Home/issues/5880)
* DotNet restore ile birden çok kaynaklarını çökme - [#5817](https://github.com/NuGet/Home/issues/5817)
* Paketi git sürüm oluşturma - izin vermek için proje sürümlerini yeniden değerlendir [#4790](https://github.com/NuGet/Home/issues/4790)
* Zorlu hataları - uyumsuz bir paketi yüklediğinizde anlamak için iyileştirmek [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard seçeneği PackageReferences - paketleri yüklemek için gereken [#4549](https://github.com/NuGet/Home/issues/4549)
* Paket teslim özellik dosyaları yoksayıldı dışında bir geliştirici komut istemi - MSBuild.exe çalıştırıldığı zaman [#4530](https://github.com/NuGet/Home/issues/4530)
* Projeye - uygulanamaz .NET Standard kitaplığı başvururken zayıf hata iletisi düzeltildi [#4423](https://github.com/NuGet/Home/issues/4423)
* DotNet ekleme hedefleme taşınabilir profil az Kılavuzu - paket için paket başarısız [#4349](https://github.com/NuGet/Home/issues/4349)
* DotNet pack - Sürüm soneki ProjectReference eksik - [#4337](https://github.com/NuGet/Home/issues/4337)
* Yapı hataları ve .NET Core şablonuyla - VS kilitlenme [#3973](https://github.com/NuGet/Home/issues/3973)
* Hizmet dizini için kaynak https:* - yüklenemedi [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe liste - allversions işe yaramazsa - [#3441](https://github.com/NuGet/Home/issues/3441)
* Yanıltıcı bağımlılık çözümleme hatası iletisini - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe geri yükleme (gerileme) - v3.3.0 3.4.4 yükseltme .msbuildproj .props ve .targets dosyaları üretmek değil [#2921](https://github.com/NuGet/Home/issues/2921)
* Bir NuGet paketi ile XAML güncelleştirirken kullanıcı Arabirimi gecikmesi dosya açık - [#2878](https://github.com/NuGet/Home/issues/2878)
* IIS Web sitesi projesinden başarısız - yolda geçersiz karakterler [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget ekleme askıda CentOS üzerinde - [#2708](https://github.com/NuGet/Home/issues/2708)
* Geri yükleme işlemi packagesavemode - nupkg başarısız için json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Çıkış penceresi için restore komutu - Paket Yöneticisi filtresini vs'de kullanılamıyor [#2704](https://github.com/NuGet/Home/issues/2704)

[Bu sürümde düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
