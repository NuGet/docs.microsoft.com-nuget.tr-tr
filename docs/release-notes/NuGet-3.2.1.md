---
title: NuGet 3.2.1 sürüm notları
description: NuGet 3.2.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548196"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 sürüm notları

[3.2 NuGet sürüm notları](../release-notes/nuget-3.2.md) | [NuGet 3.3 sürüm notları](../release-notes/nuget-3.3.md)

Komut satırı için NuGet 3.2.1 12 Ekim 2015 bir küçük iyileştirmeler ve düzeltmeler 3.2 sürümü için yayımlanmıştır ve kullanılabilir [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Geliştirmeleri

* NuGet artık yapılandırma dosyası ile özgün harflendirmeyi kullanan `NuGet.Config`.  Bu büyük/küçük harfe işletim sistemlerinde önemlidir [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet geri yükleme artık dnx projelerinin yoksay (`*.xproj`) ile işlenmelidir `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* En iyi duruma getirilmiş ağ kullanımı ile çalışırken `index.json` ve paket kayıt verisi [1426](https://github.com/NuGet/Home/issues/1426)
* Geliştirilmiş kaynak indirme v2 hizmetleriyle daha sağlam olması için işleme [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Düzeltmeleri

* NuGet güncelleştirme doğru güncelleştirmeleri `.csproj` / `.vcxproj` başvuruları [1483 te](https://github.com/NuGet/Home/issues/1483)
* Artık bir SpecialFolders.UserProfile bulunamıyor, oluşturulan bir yerel .nuget klasör önleme [1531](https://github.com/NuGet/Home/issues/1531)
* Geliştirilmiş indirme sırasında bozuk paketler yerel önbellekte işleme [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Komut satırı ve Visual Studio uzantısı NuGet Github'da bulunabilir giderilen sorunların tam bir listesi [3.2.1 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Bilinen Sorunlar

Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)