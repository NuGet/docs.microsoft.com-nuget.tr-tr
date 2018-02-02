---
title: "NuGet 3.4.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.2 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 sürüm notları

[NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 yayımlanan 8 Nisan 3.4 ve 3.4.1 belirlendi birkaç sorunlarını gidermek üzere 2016 üzerinde bırakın.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC artık kullanılabilir

Nuget.exe 3.4.2 Sürüm Adayı'na indirebilirsiniz [burada](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Güncelleştirmeleri ve geliştirmeleri

* Biz, burada derin bağımlılık grafikleri paketlerle güncelleştirmeleri gerçekten uzun sürdü ve Visual Studio askıda belirli bir senaryoda, güncelleştirmelerinin performansını önemli ölçüde iyileştirilmiştir.
* nuget restore ağ trafiğini olmadan 2,5 x – 3 Visual Studio içinde daha hızlı olur.
* Bu değişiklik ek olarak, size iki kez güncelleştirme getirme sayısı, VS Arabiriminde nerede biz ağ basarsa bir sorunu düzelttikten. Bazı zaman aşımı sorunları müşteriler 3.4/3.4.1 deneyimli kısmen sorumlu.
* No_proxy ayarı desteği eklendi

## <a name="fixes"></a>Düzeltmeler

* Nuget.org kaynak için 3.4.1 güncelleştirdikten sonra NuGet ayarları veya yapılandırma eksik olduğu bir sorun düzeltilmiştir.
* Bir sorun nerede 3.4.1 FindPackagesById için büyük/küçük harf değişikliği Artifactory keser sabit.
* Nuget.exe ile NuGet geri yükleme ile hataları nedeniyle FIPS ile ilgili bir sorunu düzeltildi.
* Bir kilitlenme geçersiz simge URL'si kaynaklarıyla göz atarken sabit.
* Birleştirme sürümleri ve 'Tüm kaynakları' girişleri ile giderilen sorunlar.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Bilinen sorunlar 3.4.2 içinde Windows x86 Commandline (RC)

Bu sorunları erken sonraki biz RTM isabet önce hafta düzeltilecektir.

*  Çözüm dosyası proje dosyalarını daha düşük bir klasör hiyerarşisi yerleştirilen bir çözüm üzerinde çalışan nuget geri yükleme başarısız olur.
*  V2 akış kullanarak bir pakete nuget silme komutunu çalıştırarak başarısız olur. V3 akışı kullanın.


Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).