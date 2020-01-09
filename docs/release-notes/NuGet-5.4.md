---
title: NuGet 5,4 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,4 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384117"
---
# <a name="nuget-54-release-notes"></a>NuGet 5,4 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi

## <a name="summary-whats-new-in-54"></a>Özet: 5,4 sürümündeki yenilikler

* Daha hızlı çözüm yükleme süresi-ilk çözüm yükü sırasında NuGet kodu çalıştıran ek yük, JıT maliyetini azaltmak için kısmi Ngen aracılığıyla azaltılmıştır [#6007](https://github.com/NuGet/Home/issues/6007)

* Yeni yardımcı işlev-paket kimliklerinin ve sürümlerinin bir listesi verildiğinde, olası en üst düzey paketleri alın. - [#8316](https://github.com/NuGet/Home/issues/8316)

* [GitHub eylemleri](https://github.com/features/actions)üzerinde NuGet. exe ' yi yükleme ve yapılandırma için yeni [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) eylem. - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hata**

* Eklenti: Linux/Mac 'te günlüğe kaydetme süresi doğruluğu kapalı [#8747](https://github.com/NuGet/Home/issues/8747)

* Bir eklentiyi elden atmak bazen tüm işlemi oluşturabilir ve başarısız olabilir. - [#8732](https://github.com/NuGet/Home/issues/8732)

* PMUI- [#8679](https://github.com/NuGet/Home/issues/8679) izin verilen ve engellenen sürümler listesinde sürüm yinelemelerini görüntülemeyi durdur

* Kilit dosyası düzgün oluşturulmamış-çerçeve sıralaması geri yüklemeyi lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645) ile etkilememelidir

* SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639) <RuntimeIdentifiers> ayarlanan projelerde LockFile doğrulaması başarısız oluyor

* İmzalama doğrulaması artık aynı OID altında 2 değere sahip olan zaman damgalarıyla imzaları doğru şekilde reddedecek [#8629](https://github.com/NuGet/Home/issues/8629)

* Lisans listesini güncelleştirme- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535) tanılama dosyalarını ekleme

**[Bu yayında düzeltilen tüm sorunların listesi-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
