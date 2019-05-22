---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975852"
---
# <a name="nuget-51-release-notes"></a>NuGet 5.1 sürüm notları

NuGet dağıtım araçları:

| NuGet sürüm | Visual Studio sürümü içinde kullanılabilir| .NET SDK'sı sürümünü kullanılabilir|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.1 sürümü](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core iş yüküyle Visual Studio 2019 ile yüklü 

<sup>2</sup>.NET Core iş yüküyle Visual Studio 2019 ile isteğe bağlı bir yükleme olarak kullanılabilir

## <a name="summary-whats-new-in-51"></a>Özet: 5.1 yenilikler nelerdir?

* Daha iyi iş akışlarıyla tümleştirme CI/CD - izin vermek için zaten bir paket anında iletme atlayın için destek [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio artık uygun bir bağlantı sağlar paketin nuget.org galeri sayfası - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Yeni .NET Core 3.0 varlıklarını gibi destekleyen [Targeting Pack](https://github.com/dotnet/cli/issues/10006) ve [çalışma zamanı paketleri](https://github.com/dotnet/cli/issues/10007)
  * NuGet paketi ve geri yükleme desteği ve çalışma zamanı paket başvuruları - etkinleştirmek FrameworkReferences için destek [#7342](https://github.com/NuGet/Home/issues/7342)
  * Destek "yalnızca indirin" PackageDownload - paket senaryosuyla [#7339](https://github.com/NuGet/Home/issues/7339)
  * Exlcude çalışma zamanı ve arama sonuçları & geri yükleme paketlerinden hedefleyen grafiğini kullanarak PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hataları**

* Eklentiler: özel durum ayrıntıları kayıp eklentisi oluşturma sırasında - [#8057](https://github.com/NuGet/Home/issues/8057)

* Alt sınır kaynaklardan biri mevcutsa PackageReference aralığı özel alt sınırı ile çalışmaz. - [#8054](https://github.com/NuGet/Home/issues/8054)

* IsPackableFalseError iletisi - geliştirmek [#8021](https://github.com/NuGet/Home/issues/8021)

* Paketler kilidi dosyası - proje graf değiştiğinde yeniden oluşturma kilit - [#8019](https://github.com/NuGet/Home/issues/8019)

* Proje sistemi hatası: Nuget paketlerini otomatik alma kaldırıldı - [#8017](https://github.com/NuGet/Home/issues/8017)

* FrameworkReference döndürmek için bir hedef ekleyin CollectPackageDownloads ve CollectPackageReferences - benzer [#8005](https://github.com/NuGet/Home/issues/8005)

* HTTP önbellek:  Tutulan bir biçimde - RepositoryResources kaynak önbelleğe alınmamış [#7997](https://github.com/NuGet/Home/issues/7997)

* Günlüğe kaydetme: özel durum çağrı yığınını ayrıntılı ayrıntı ile - bildirilmez [#7955](https://github.com/NuGet/Home/issues/7955)

* Tüm NuGet belgeleri - HTTPS kullanacak şekilde URL'leri değiştirmeyi [#7950](https://github.com/NuGet/Home/issues/7950)

* Uyarı iletisi NU3024 - geliştirmek [#7933](https://github.com/NuGet/Home/issues/7933)

* ne zaman güncelleştirilmiyor kilit dosyası kaldırıldı - packagereference [#7930](https://github.com/NuGet/Home/issues/7930)

* Hata örneği işleme nuspec - licenseurl ve lisans öğesindeki doğrularken geliştirmek [#7915](https://github.com/NuGet/Home/issues/7915)

* PM UI - sağ tıklayın sekmesini üstbilgi ve sonuçları hata - tıklatarak "dosya konumunu Aç" [#7913](https://github.com/NuGet/Home/issues/7913)

* Eklentiler: oturum eklentisi işlem çıktığında - [#7907](https://github.com/NuGet/Home/issues/7907)

* Eklentiler: yüksek çakışma oranı günlük datetime değerleri - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom başarısız LicenseExpression ile-herhangi bir nuspec üzerinde [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Bir projeye özel AssemblyName ile-ProjectReference başvurduğunda beklenmeyen NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)

* Bir özel durumla - eklentisi başlatma başarısız olduğunda daha iyi hata iletisi [#7857](https://github.com/NuGet/Home/issues/7857)

* NoOp geri yükleme yaparken önlemek *. obj dizinindeki - dgspec.json yazma [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty büyük/küçük harf uyuşmazlığı - özelliği oluşturmak için true başarısız = [#7843](https://github.com/NuGet/Home/issues/7843)

* Ayarları: VS - paket kaynağı yolu geçersiz karakter çökebilir [#7820](https://github.com/NuGet/Home/issues/7820)

* Kilit dosya silinirse, geri yükleme - NoOp üzerinde kilit dosyası oluşturmaz [#7807](https://github.com/NuGet/Home/issues/7807)

* Lisans URL'si ve lisans nedenleri okuma hatası - meta verilerle [#7547](https://github.com/NuGet/Home/issues/7547)

* İşlenmeyen özel durumları V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe - geçersiz bağımsız değişkenler için çıkış kodu sıfır döndürür [#7178](https://github.com/NuGet/Home/issues/7178)

* Hata ve uyarı docs imzalama ilgili senaryoları - yansıtacak şekilde güncelleştirmek [#6498](https://github.com/NuGet/Home/issues/6498)

* Varlıklar dosya taşıma projeleri daha bir kolayca - etkinleştirmek için göreli yolların kullanmalıdır [#4582](https://github.com/NuGet/Home/issues/4582)

**Dcr**

* Eklentiler: Tanılama günlüğüne kaydetme - etkinleştirme [#7859](https://github.com/NuGet/Home/issues/7859)

* NetStandard 2.1 - yapma Tizen 6 eşlemesine [#7773](https://github.com/NuGet/Home/issues/7773)

**[Bu sürümde - 5.1 RTM düzeltilen tüm sorunlara listesi](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
