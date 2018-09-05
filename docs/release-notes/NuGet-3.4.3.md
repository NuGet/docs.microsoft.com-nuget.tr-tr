---
title: NuGet 3.4.3 sürüm notları
description: NuGet 3.4.3 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549171"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 sürüm notları

[3.4.2 NuGet sürüm notları](../release-notes/nuget-3.4.2.md) | [3.4.4 NuGet sürüm notları](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 22 Nisan 3.4 ve sonraki sürümlerde tanımlanmış olan çeşitli sorunları ele almak için 2016 yayınlanmıştır.

VSIX ve nuget.exe indirebileceğiniz [burada](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve iyileştirmeler

* Visual Studio güvenilirlik düzeyi artırıldı. Visual Studio'da kilitlenmelere neden nuget'te bazı sorunları düzelttik.

## <a name="fixes"></a>Düzeltmeleri

* Bazı yetkilendirme sorunları ile parola korumalı özel nuget akışları düzeltildi.
* PCL'ın gelen geri erişememe geçici bir sorun düzeltildi `project.json` belirtilen çalışma zamanları ile.
* Bazı müşteriler, paketleri yüklerken aralıklı hatalar çalışıyordu. Bu, bu sürümde artık düzeltildi.
* Geri yükleme hatalarının C + kaynaklanan bir sorun düzeltildi +/ CLI projeleri ile `project.json`.
* Burada değil olan doğru mono'da nuget kullanırken sıkıştırması açılan bazı paketler (ör. ModernHttpClient). Bu, bu sürümde artık düzeltildi.

Düzeltmeleri ve geliştirmeleri bu sürümde tam listesi için sorunların listeye bir göz atın [burada](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).