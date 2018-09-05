---
title: NuGet 3.0 RC sürüm notları
description: NuGet 3.0 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551725"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC sürüm notları

[NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC ile Visual Studio 2015 RC sürüm 29 Nisan 2015 tarihinde yayınlanmıştır. Bu sürüm, birkaç önemli hata düzeltmeleri ve performans iyileştirmeleri yeni çerçeveleri desteklemek için güncelleştirmeleri sahiptir.  Yalnızca, Visual Studio 2015 için de kullanılabilir.

### <a name="continued-focus-on-performance"></a>Devam eden performansa odaklanan

Kararlılık ve NuGet sorguların performansını üzerinde odaklanıyorsunuz rastladığımız devam etmektedir.  Bu sürümle birlikte, çok hızlı arama işlemleri NuGet UI ve Web sitesi görmeye başlamanız gerekir.  Hizmet ve biz bu işlemleri ayarlamaya devam edebilmesi için hizmet kullanımını izleme yapıyorsanız.

## <a name="significant-issues-resolved"></a>Çözümlenen önemli sorunlar

NuGet istemcileri Sabitle için bu yayının bir parçası çok sayıda sorunu biz çözüldü.  Çözümlenen daha önemli sorunlar bazılarının yalnızca kısa bir listesi aşağıda verilmiştir:

* ASP.NET 5 K framework'ün yeniden adlandırma işleminin bir parçası olarak framework adlar dnx ve dnxcore işlemeye güncelleştirildi [bağlantı](https://github.com/NuGet/Home/issues/215)
* Visual Studio kullanıcı arabiriminde bağlantılardan Yardım belgeleri eklenen [bağlantı](https://github.com/NuGet/Home/issues/232)
* Karmaşık bir başvuru daha iyi işleme `.nuspec` virgülle ayrılmış framework başvurularıyla [bağlantı](https://github.com/NuGet/Home/issues/276)
* Sabit kültür Japonca desteği [bağlantı](https://github.com/NuGet/Home/issues/253)
* ASP.NET 5 projelerine yeni v3 uç noktalarını kullanacak şekilde izin vermek için güncelleştirilmiş istemci [bağlantı](https://github.com/NuGet/Home/issues/219)
* Kaynak denetimi ile daha iyi güncelleştirilmiş tanıtıcı paketler klasörü [bağlantı](https://github.com/NuGet/Home/issues/56)
* Uydu paketleri için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/17)
* Çerçeveye özgü içerik dosyaları için desteği düzeltildi [bağlantı](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub varlığı bir revizyona imza attı

Bazı değişiklikler yaptık bizim [kaynak kod deposu github'da](http://github.com/nuget/home).  NuGet Visual Studio istemcisinde, Powershell komutlarını veya komut satırı ile herhangi bir sorun varsa yürütülebilir bu sorunların oturum açıp üzerinde ilerlemelerini izlemeye bizim [GitHub giriş depo sorunlar listesini](http://github.com/nuget/home/issues).  Galeride sorunlarda takip ettiğimiz bizim [GitHub NuGetGallery depo](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve NuGet 3.0 duyuruları!