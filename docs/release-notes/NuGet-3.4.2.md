---
title: 3.4.2 NuGet sürüm notları
description: NuGet 3.4.2 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549157"
---
# <a name="nuget-342-release-notes"></a>3.4.2 NuGet sürüm notları

[3.4.1 NuGet sürüm notları](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 8 Nisan 3.4 ve 3.4.1 içinde tanımlanan çeşitli sorunları ele almak için 2016 bırakıldığını bırakın.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC kullanıma sunuldu

Nuget.exe 3.4.2 Sürüm Adayı indirebileceğiniz [burada](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve iyileştirmeler

* Kapsamlı bağımlılık grafikleri paketlerle güncelleştirmeleri nerede gerçekten uzun sürdü ve Visual Studio askıda belirli bir senaryoda, güncelleştirmeleri performansını önemli ölçüde geliştirildi.
* nuget geri yükleme ağ trafiğini olmadan 2,5 x – 3 Visual Studio'da daha hızlı olur.
* Bu değişiklik ek olarak, bir sorun iki kez güncelleştirme getirilirken sayarken VS Arabiriminde nerede biz ağ ulaşmaktan düzelttik. Bu, kısmen 3.4/3.4.1 deneyimli bazı zaman aşımı sorunları müşteriler için sorumluydu.
* No_proxy ayarı desteği eklendi

## <a name="fixes"></a>Düzeltmeleri

* Nuget.org kaynak için 3.4.1 güncelleştirdikten sonra NuGet ayarları veya yapılandırma eksik olduğu bir sorun düzeltildi.
* Burada 3.4.1 FindPackagesById için büyük/küçük harf değişikliği Artifactory keser bir sorun düzeltildi.
* Nuget.exe ile NuGet geri yükleme ile hatalarına neden olan FIPS ile ilgili bir sorun düzeltildi.
* Geçersiz simge URL'si kaynaklarıyla göz atılırken bir kilitlenme düzeltildi.
* Sürümleri ve Girişleri 'Tüm kaynakları' ndan birleştirme ile sorunlar düzeltildi.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Bilinen sorunlar 3.4.2 içinde x86 Windows komut satırı (RC)

Bu sorunları erken sonraki biz RTM isabet önce hafta düzeltilecektir.

*  Çözüm dosyası proje dosyalarını daha düşük bir klasör hiyerarşisi yerleştirilen bir çözüm üzerinde çalışan nuget geri yükleme başarısız olur.
*  V2 akışı kullanarak bir pakete nuget delete komutu çalıştırma başarısız olur. V3 akışı kullanın.


Düzeltmeleri ve geliştirmeleri bu sürümde tam listesi için sorunların listeye bir göz atın [burada](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).