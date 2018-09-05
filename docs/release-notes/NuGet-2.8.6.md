---
title: 2.8.6 NuGet sürüm notları
description: NuGet 2.8.6 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546497"
---
# <a name="nuget-286-release-notes"></a>2.8.6 NuGet sürüm notları

[2.8.5 NuGet sürüm notları](../release-notes/nuget-2.8.5.md) | [2.8.7 NuGet sürüm notları](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 bırakıldığını 20 Temmuz 2015 bizim 2.8.5 küçük bir güncelleştirme olarak bazı VSIX hedeflenen düzeltmeler ve teslim edilebilir paketleri Windows 10 UWP geliştirme modeli desteği ile desteklemeye yönelik geliştirmeleri.

NuGet Paket Yöneticisi uzantısı'nın bu sürümü, yalnızca Visual Studio 2013 için destek sağlar.

Bu sürümde, NuGet Paket Yöneticisi iletişim için eklenen destek sahipti:

* Windows 10 için uygulama geliştirme desteği için UAP hedef çerçeve adı kullanıma sunuldu.
* NuGet Protokolü sürüm 3 uç noktaları
* Destek [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) depo kaynakları protocolVersion özniteliği. Varsayılan değer: "2"
* Gerekli Paket sürümü yerel önbellek üzerinde kullanılabilir değilse, uzak depoya geri dönülüyor