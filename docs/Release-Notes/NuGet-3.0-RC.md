---
title: "NuGet 3.0 RC sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.0 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0 RC sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC sürüm notları

[NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC 29 Nisan 2015 tarihinde Visual Studio 2015 RC sürüm ile serbest bırakıldı. Bu sürüm çeşitli önemli hata düzeltmeleri, performans iyileştirmeleri ve yeni çerçeveleri desteklemek için güncelleştirmeleri vardır.  Yalnızca, Visual Studio 2015 için de kullanılabilir.

### <a name="continued-focus-on-performance"></a>Devam eden odak performansı

Kararlılık ve performans NuGet sorguların biz üzerine odaklanan bir konudur devam etmektedir.  Bu sürümle birlikte, NuGet kullanıcı Arabirimi ve Web sitesi çok hızlı arama işlemlerinin görmeye başlamanız gerekir.  Hizmet ve biz bu işlemlerin ayarlamaya devam edebilmesi için bu hizmetin kullanımı izleme.

## <a name="significant-issues-resolved"></a>Önemli sorunlar çözüldüğünde

NuGet istemcileri Sabitle için bu sürümde bir parçası olarak çoğu sorunu biz çözümlendi.  Aşağıda, daha önemli sorunlar çözüldüğünde bazılarının yalnızca kısa bir listesi verilmiştir:

* ASP.NET 5 K framework'ün yeniden adlandırma işleminin bir parçası olarak, framework adlar dnx ve dnxcore işlemek için güncelleştirilmiş [bağlantı](https://github.com/NuGet/Home/issues/215)
* Visual Studio kullanıcı arabiriminde bağlantılardan Yardım belgelerine eklenen [bağlantı](https://github.com/NuGet/Home/issues/232)
* Karmaşık başvurularında, daha iyi işleme `.nuspec` virgülle ayrılmış framework başvurularıyla [bağlantı](https://github.com/NuGet/Home/issues/276)
* Japonca kültürler için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/253)
* Yeni v3 uç nokta kullanmak ASP.NET 5 projeleri izin vermek için güncelleştirilmiş istemci [bağlantı](https://github.com/NuGet/Home/issues/219)
* Kaynak denetimi ile daha iyi güncelleştirilmiş tanıtıcı paketler klasörü [bağlantı](https://github.com/NuGet/Home/issues/56)
* Uydu paketleri için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/17)
* Çerçeveye özel içerik dosyaları için destek düzeltildi [bağlantı](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub varlığı onarımı

Bazı değişiklikler yaptık bizim [kaynak kodu depolarına github'da](http://github.com/nuget/home).  NuGet Visual Studio istemcisi, Powershell komutlarını veya komut satırı ile ilgili sorununuz olursa yürütülebilir, bu sorunları oturum ve üzerinde kendi ilerleme durumunu izlemek bizim [GitHub giriş depo sorunlar listesine](http://github.com/nuget/home/issues).  Galeride sorunlarda takip ettiğimiz bizim [GitHub NuGetGallery depo](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!