---
title: NuGet 5,1 RTM sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699859"
---
# <a name="nuget-51-release-notes"></a>NuGet 5,1 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi 

<sup>2</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile isteğe bağlı bir install olarak kullanılabilir

## <a name="summary-whats-new-in-51"></a>Özet: 5,1 sürümündeki yenilikler

* CI/CD iş akışlarıyla daha iyi tümleştirme sağlamak için zaten mevcutsa bir paket gönderimi atlama desteği- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio artık paketin nuget.org Galeri sayfasına uygun bir bağlantı sağlamaktadır [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* [Hedefleme paketleri](https://github.com/dotnet/cli/issues/10006) ve [çalışma zamanı paketleri](https://github.com/dotnet/cli/issues/10007) gibi yeni .NET Core 3,0 varlıkları için destek
  * Hedef ve çalışma zamanı paket başvurularını etkinleştirmek üzere FrameworkReferences için NuGet paketi ve geri yükleme desteği- [#7342](https://github.com/NuGet/Home/issues/7342)
  * PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339) ile "yalnızca indir" paket senaryosunu destekleme
  * Çalışma zamanı ve hedefleme paketlerini, PackageType- [#7337](https://github.com/NuGet/Home/issues/7337) kullanarak & geri yükleme graflarından çıkar

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hata**

* Eklentiler: eklenti oluşturma sırasında özel durum ayrıntıları kayboldu- [#8057](https://github.com/NuGet/Home/issues/8057)

* , Kaynaklardan birinde alt sınır varsa, özel alt sınırı olan PackageReference aralığı çalışmaz. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Ispackabsolalseerror iletisini geliştirme- [#8021](https://github.com/NuGet/Home/issues/8021)

* Paketler kilit dosyası-proje grafiği değiştiğinde kilit dosyasını yeniden oluştur- [#8019](https://github.com/NuGet/Home/issues/8019)

* ProjectSystem hatası: NuGet paketleri otomatik olarak kaldırılıyor- [#8017](https://github.com/NuGet/Home/issues/8017)

* CollectPackageDownloads ve Collectpackagerefersin- [#8005](https://github.com/NuGet/Home/issues/8005) benzer bir frameworkreference döndürmek için bir hedef ekleyin

* HTTP önbelleği: Depokaynak kaynağı, sürümlü bir şekilde önbelleğe alınmaz- [#7997](https://github.com/NuGet/Home/issues/7997)

* Günlüğe kaydetme: özel durum callyığınları ayrıntılı ayrıntı düzeyi ile bildirilmedi [#7955](https://github.com/NuGet/Home/issues/7955)

* Tüm NuGet belgeleri URL 'Lerini HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950) kullanacak şekilde değiştir

* NU3024 uyarı iletisini geliştirme- [#7933](https://github.com/NuGet/Home/issues/7933)

* packagereference kaldırıldığında kilit dosyası güncelleştirilmiyor- [#7930](https://github.com/NuGet/Home/issues/7930)

* Nuspec- [#7915](https://github.com/NuGet/Home/issues/7915) içinde licenseurl ve lisans öğesi doğrulanırken hata durum işlemeyi geliştir

* PM Kullanıcı arabirimi-sekme başlığına sağ tıklayıp "dosya konumunu aç" seçeneğine tıkladığınızda hata [#7913](https://github.com/NuGet/Home/issues/7913)

* Eklentiler: eklenti işlemi çıktığında günlüğe kaydet- [#7907](https://github.com/NuGet/Home/issues/7907)

* Eklentiler: günlük tarih değerlerini günlüğe kaydetme sırasında yüksek çakışma oranı- [#7899](https://github.com/NuGet/Home/issues/7899)

* LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894) ile herhangi bir nuspec üzerinde manifest. ReadFrom başarısız

* RestoreLockedMode: ProjectReference özel AssemblyName içeren bir projeye başvurduğunda, beklenmeyen NU1004- [#7889](https://github.com/NuGet/Home/issues/7889)

* Eklenti başlatması bir özel durumla başarısız olduğunda daha iyi hata iletisi [#7857](https://github.com/NuGet/Home/issues/7857)

* Bir NoOp geri yükleme işlemi yaparken, obj dizininde yazma sırasında * .dgspec.jsönleyin- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true, büyük/küçük harf uyuşmazlığı üzerinde özellik üretemiyor- [#7843](https://github.com/NuGet/Home/issues/7843)

* Ayarlar: paket kaynak yolunda geçersiz karakter kilitlenebilir VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* Kilit dosyası silinirse, geri yükleme işlemi NoOp 'de kilit dosyası oluşturmaz [#7807](https://github.com/NuGet/Home/issues/7807)

* Lisans URL 'SI ve lisans, meta verilerle okuma hatasına neden olur- [#7547](https://github.com/NuGet/Home/issues/7547)

* V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523) işlenmemiş özel durumlar

* nuget.exe geçersiz bağımsız değişkenler için sıfır çıkış kodu döndürüyor- [#7178](https://github.com/NuGet/Home/issues/7178)

* İmzalama ilgili senaryolarını yansıtmak için hataları ve uyarı belgelerini güncelleştirin- [#6498](https://github.com/NuGet/Home/issues/6498)

* Varlıklar dosyası, projeleri taşımayı daha kolay bir şekilde etkinleştirmek için göreli yollar kullanmalıdır [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* Eklentiler: Tanılama günlüğünü etkinleştirme- [#7859](https://github.com/NuGet/Home/issues/7859)

* Tizen 6 eşlemesini NetStandard 2,1 ile yapın [#7773](https://github.com/NuGet/Home/issues/7773)

**[Bu yayında düzeltilen tüm sorunların listesi-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
