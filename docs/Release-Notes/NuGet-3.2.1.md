---
title: "NuGet 3.2.1 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.2.1 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.2.1 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 sürüm notları

[NuGet 3.2 sürüm notları](../release-notes/nuget-3.2.md) | [NuGet 3.3 sürüm notları](../release-notes/nuget-3.3.md)

Komut satırı için NuGet 3.2.1 12 Ekim 2015 en iyi duruma getirme ve düzeltmeleri 3.2 sürümü sayıda ile serbest bırakıldı ve kullanılabilir [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Geliştirmeleri

* NuGet özgün büyük küçük harf kullanımını ile artık yapılandırma dosyasını kullanır `NuGet.Config`.  Bu büyük küçük harfe duyarlı işletim sistemlerinde önemlidir [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet restore şimdi dnx projelerini yoksay (`*.xproj`) ile işlenmelidir `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* En iyi duruma getirilmiş ağ kullanımı ile çalışırken `index.json` ve paket kayıt verileri [1426](https://github.com/NuGet/Home/issues/1426)
* Geliştirilmiş kaynak indirme v2 Hizmetleri ile daha sağlam olması için işleme [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Düzeltmeler

* NuGet güncelleştirme doğru güncelleştirmeleri `.csproj` / `.vcxproj` başvuruları [1483 te](https://github.com/NuGet/Home/issues/1483)
* Şimdi bir SpecialFolders.UserProfile bulunamıyor zaman oluşturulan bir yerel .nuget klasörü önleme [1531](https://github.com/NuGet/Home/issues/1531)
* Yükleme sırasında bozuk paketler yerel önbellekteki işlenmesini geliştirilmiş [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Komut satırı ve Visual Studio uzantısı NuGet Github'da bulunabilir ele sorunların tam listesi [3.2.1 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Bilinen Sorunlar

Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)