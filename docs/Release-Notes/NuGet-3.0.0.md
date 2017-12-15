---
title: "NuGet 3.0 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.0.0 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0.0 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 sürüm notları

[NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 sürüm notları](../release-notes/nuget-3.1.md)

NuGet 3.0 20 Temmuz 2015 tarihinde Visual Studio 2015 için bir paket uzantısı olarak yayımlanmıştır. Eksiksiz güncelleştirilmiş NuGet 3.0 deneyimi yeni Visual Studio kullanıcılar için kullanılabilir olması için bu sürüm Visual Studio ile sağlamak için gönderilir. Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.

Visual Studio Galerisi güncelleştirme biz bir güncelleştirme, Windows 10 geliştirme desteği içeren Visual Studio 2015 kısa süre sonra yayımlama olarak kullanılabilir olan, en son sürüme erişimi bu geliştiriciler öneririz.

Toplam 240 sorunları 3.0 sürümünde biz kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Bilinen Sorunlar

Bu sürüm ile birlikte sunulan bilinen sorunlar sayısı yoktu ve bu öğelerin tümünü sürümünde Windows 10 sürümünü 29 Temmuz çakıştığı bizim zamanlanmış 3.1 düzeltilen.  Visual Studio uzantınızın ya da bu bilinen sorunları gidermek için bu tarihten sonra galerisinden güncelleştirmek.

*  Çeviri önizleme penceresi "bunu tekrar gösterme" etiketi ve Paket açıklaması penceresinde "Yazar" etiketi için sağlanmaz.
*  TFS kullanarak bir proje üzerinde çalışan denetim kaynağı, Nuget.Config dosya salt okunur olarak işaretlenmiş NuGet Paket Yöneticisi kullanıcı arabirimi varsa olamaz.
   * **Geçici çözüm** TFS dosyasından göz atın.
*  Visual Studio koyu tema kullandığınızda metni NuGet Powershell penceresinde "yeniden başlatma çubuğu" sarı görünür değil.
   * **Geçici çözüm** Visual Studio açık tema kullanın.


## <a name="summary-of-top-issues-resolved"></a>Üst Sorunlar çözüldüğünde özeti

* [Paket Yöneticisi penceresi yenilendiğinde sık ağ güncelleştirme çağırır](https://github.com/NuGet/Home/issues/515)
* [Değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde kaydırma ertelendi](https://github.com/NuGet/Home/issues/519)
* [Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır](https://github.com/NuGet/Home/issues/516)
* [Eklenen 'önizleme penceresi gösterme' onay kutusu](https://github.com/NuGet/Home/issues/566)
* [Eklenen işlemi işlemci kullanımını azaltmak için azaltma](https://github.com/NuGet/Home/issues/356)
* Geliştirilmiş taşınabilir sınıf kitaplığı başvurusu işleme
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Otomatik Tamamlama hizmet büyük küçük harfe duyarlı](https://github.com/NuGet/Home/issues/198)
* [Temel kimlik doğrulama kimlik bilgilerini yeniden etkilenmesine neden güncelleştirme](https://github.com/NuGet/Home/issues/456)
* [Geliştirilmiş hata günlüğü](https://github.com/NuGet/Home/issues/407)
* [Güncelleştirme paketi çağrılırken geliştirilmiş powershell hata iletileri](https://github.com/NuGet/Home/issues/5)
* [Windows 10 kilitlenen önlemek için 'Seçenekleri hakkında bilgi edinin' bağlantı sabit](https://github.com/NuGet/Home/issues/822)
* [Yayın öncesi onay kutusunu ayarını unutmayın](https://github.com/NuGet/Home/issues/732)
* [Sonuçları bir Çözümdeki projeler arasında önbelleğe alma geliştirilmiş toplama performansı](https://github.com/NuGet/Home/issues/721)
* [Paralel olarak birden çok paket toplanabilir](https://github.com/NuGet/Home/issues/713)
* [Install-package kaldırıldı-komutu zorla](https://github.com/NuGet/Home/issues/697)

Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları biz Windows 10 geliştirme desteği sunmaya hazır olarak.