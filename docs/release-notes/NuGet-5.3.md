---
title: NuGet 5,3 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 683ee7d1bef30d0a7414ec1694a9735d79b2ab45
ms.sourcegitcommit: c529f5944868a0692ca8550b716a73e05df0ccbf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71687882"
---
# <a name="nuget-53-release-notes"></a>NuGet 5,3 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi

## <a name="summary-whats-new-in-53"></a>Özetleme 5,3 sürümündeki yenilikler

* Paket simgesi, harici bir URL [olması yerine pakete gömülebilir](../reference/msbuild-targets.md#packing-an-icon-image-file). - [#352](https://github.com/NuGet/Home/issues/352)

* SHA izleme ve paketler için zorlama ile geliştirilmiş güvenlik. config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Eski/eski NuGet paketlerinin kullanımdan kaldırılması için [#2867](https://github.com/NuGet/Home/issues/2867) | [blog gönderisi](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hata**

* 3\.0.100-preview9 SDK ile oluşturulan NuGet paketleri 2,2 SDK kullanıcıları tarafından kullanılamaz... Saat dilimlerinize bağlı olarak [#8603](https://github.com/NuGet/Home/issues/8603)

* QUOTE "yoldaki karakterler" yolda geçersiz karakterler "hata oluşmasına neden olur" `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168) hatası

* VS: derlemeler tamamen NGen tarafından, kısmen Ngen-Ed değil [#8513](https://github.com/NuGet/Home/issues/8513)

* Bellek kullanımını azaltma (etkinliklerden abonelik kaldırma)- [#8471](https://github.com/NuGet/Home/issues/8471)

* "Error_UnableToFindProjectInfo" iletisi dilsiz doğru değil [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 geliştirmeleri-tüm paketleri doğrula, beklenen/fiili SHA değerlerini dahil et- [#8424](https://github.com/NuGet/Home/issues/8424)

* [#8401](https://github.com/NuGet/Home/issues/8401) birden çok `NuGetPackageManager.PreviewUpdatePackagesAsync`sabit listesi  - 

* PluginProcess 'de "Public-> Internal" değişikliğini " [#8390](https://github.com/NuGet/Home/issues/8390)

* Ispackagesourceprovider. GetSources (...) hatalı tanımlanmış özel durum davranışına sahip- [#8383](https://github.com/NuGet/Home/issues/8383)

* PluginManager oluşturucusunu bir daha genel yapın- [#8379](https://github.com/NuGet/Home/issues/8379)

* PM Kullanıcı arabiriminin yenileme oranını izlemek için ölçümler- [#8369](https://github.com/NuGet/Home/issues/8369)

* Paket Yöneticisi Kullanıcı arabirimi aracılığıyla yüklenirken UI yenilemelerinin sayısını azaltın- [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetri: DateTime değerleri kültüre özgü biçimler kullanır- [#8351](https://github.com/NuGet/Home/issues/8351)

* Paket Yöneticisi Kullanıcı arabirimindeki #6570- [#8339](https://github.com/NuGet/Home/issues/8339) Kullanıcı arabirimi yenilemelerinin azaltın

* [Test hatası] "Yapılandırma dosyası ayrıştırılamıyor", iki kez [#8320](https://github.com/NuGet/Home/issues/8320) isteyecek

* Müşteri düzeltmelerini (pakette gerekli nuspec dosyası eksik) açıklayan iyi belge sayfasıyla NU5037 hatası oluştur- [#8291](https://github.com/NuGet/Home/issues/8291)

* Bir projenin Runtimeıdentifier değiştirildiğinde kilitli modda geri yükleme başarısız olur- [#8260](https://github.com/NuGet/Home/issues/8260)

* VS yavaş [#8156](https://github.com/NuGet/Home/issues/8156) ayarları okuma

* "': ' Karakteri, onaltılık değeri 0x3a," Errors-#7948 bir ada eklenemez. [](https://github.com/NuGet/Home/issues/7948) `Nuget sources add`

* NuGet eklentisi kimlik bilgileri sağlayıcıları-işlem penceresini gizleyin- [#7511](https://github.com/NuGet/Home/issues/7511)

* PackagePathResolver 'ı zorlama mutlak bir yoldur- [#7349](https://github.com/NuGet/Home/issues/7349)

* Paket Yöneticisi Kullanıcı arabirimine yönelik Install ve Update sekmelerinde UI yenilemelerini azaltma- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR**

* Xamarin çerçevelerini NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368) eşlenecek şekilde güncelleştirme

* Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324) Paket Yöneticisi "Önizleme penceresi" içeriğinin kopyalanmasını etkinleştir

* . Proj dosyalarında geri yüklemeyi etkinleştir- [#8212](https://github.com/NuGet/Home/issues/8212)

* Her `NUGET_NETFX_PLUGIN_PATHS` ikisinin `NUGET_NETCORE_PLUGIN_PATHS` de aynı anda yapılandırmasını tanıtın ve bu yapılandırmayı destekler [#8151](https://github.com/NuGet/Home/issues/8151)

* Sürüm özniteliği aracılığıyla PackageDownload için birden çok sürümü etkinleştirme- [#8074](https://github.com/NuGet/Home/issues/8074)

* NuGet. exe paketine-SolutionDirectory ve-PackageDirectory seçeneklerini ekleyin- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Bu yayında düzeltilen tüm sorunların listesi-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
