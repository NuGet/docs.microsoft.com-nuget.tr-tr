---
title: NuGet 4.6 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 4.6.0 dahil etmek için sürüm notları.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 11e604ad9a28ac2b22880a13ef9d8b41d8c09507
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
---
# <a name="nuget-46-rtm-release-notes"></a>NuGet 4.6 RTM sürüm notları

[Visual Studio 2017 15,6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Özet: Bu Yayındaki Yenilikler

* İçin destek ekledik [paketleri imzalama](../create-packages/sign-a-package.md).
* Visual Studio 2017 nuget.exe şimdi doğrular ve paket bütünlüğü yüklemeden önce paketleri geri yükleniyor [paketleri imzalı](../reference/signed-packages-reference.md).
* Biz art arda geri yüklemeler performansı geliştirilmiştir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları 

.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır. [Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde sabit üst sorunları

**Performans düzeltmeleri**

* Herhangi bir değişiklik - olduğunda varlık dosyaları yazmayın [#6491](https://github.com/NuGet/Home/issues/6491)
* Geri yükleme neden olan ek MSBuild değerlendirmeleri alt projeleri TFM eşleşmiyor, üst projenin ile - [#6311](https://github.com/NuGet/Home/issues/6311)
* Bağımlılık iyileştirerek sekmeyi geri yükleme perf artırmak grafik belirtim oluşturma - [#6252](https://github.com/NuGet/Home/issues/6252)

**Hataları**

* Yerel klasöre itme bırakır kilitli - nupkg [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet eklentisi uygulama: birden çok sorunları - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - Kaldır sorgu hizmet çağrısından VSSolutionManager MEF başlatma - [#6110](https://github.com/NuGet/Home/issues/6110)
* Hata özel durum için raporlama iptal paket yükleme görev - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe değiştirir '+' derleme adı - '% 2B' ile [#5956](https://github.com/NuGet/Home/issues/5956)
* PM Kullanıcı Arabirimi ve konsolu - için fn + F1'e sağ yardım sayfasına olmaz [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet proje dosyalarına belirli koşullarda - mutlak yollar Yazar [#5888](https://github.com/NuGet/Home/issues/5888)
* 4.3 regresyon - yer tutucuları $product$ ve dönüşüm - aracılığıyla contentfile yerini değil $AssemblyGuid$ düzeltme [#5880](https://github.com/NuGet/Home/issues/5880)
* birden çok kaynakları kilitlenme ile-dotnet geri yükleme [#5817](https://github.com/NuGet/Home/issues/5817)
* Paketi git sürüm oluşturma - izin vermek için proje sürümlerini yeniden değerlendirmeniz [#4790](https://github.com/NuGet/Home/issues/4790)
* Uyumsuz bir paket - yüklediğinizde hatalarını anlamak için sabit artırmak [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard seçeneği PackageReferences - paketleri yüklemek için gereken [#4549](https://github.com/NuGet/Home/issues/4549)
* Özellik paketi teslim dosyaları göz ardı Geliştirici komut istemi dışında - MSBuild.exe çalıştırıldığı zaman [#4530](https://github.com/NuGet/Home/issues/4530)
* Zayıf hata iletisi projeye - uygulanamaz .NET standart kitaplığı başvururken düzeltme [#4423](https://github.com/NuGet/Home/issues/4423)
* DotNet eklemek hedefleme taşınabilir profil az Kılavuzu - paket için paket başarısız [#4349](https://github.com/NuGet/Home/issues/4349)
* DotNet pack - Sürüm soneki ProjectReference eksik - [#4337](https://github.com/NuGet/Home/issues/4337)
* Derleme hataları ve .NET Core şablonuyla - VS kilitlenme [#3973](https://github.com/NuGet/Home/issues/3973)
* Kaynak https:* - hizmet dizini yüklenemiyor [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe listesi - allversions çalışmıyor - [#3441](https://github.com/NuGet/Home/issues/3441)
* Yanıltıcı bağımlılık çözümleme hata iletisini - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe geri yükleme .msbuildproj (v3.3.0 3.4.4 yükseltme gerileme) - .props ve .targets dosyaları üretmek değil [#2921](https://github.com/NuGet/Home/issues/2921)
* Bir NuGet paketi XAML ile güncelleştirirken UI gecikmesi dosyası Aç - [#2878](https://github.com/NuGet/Home/issues/2878)
* IIS Web sitesi projeden başarısız - yolundaki geçersiz karakterler içeren [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget ekleme askıda CentOS üzerinde - [#2708](https://github.com/NuGet/Home/issues/2708)
* Packagesavemode - nupkg ile geri yükleme başarısız için json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Paket Yöneticisi filtresi vs üzerinde kullanılamaz çıktı penceresi için restore komutu - [#2704](https://github.com/NuGet/Home/issues/2704)

[Bu sürümde giderilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
