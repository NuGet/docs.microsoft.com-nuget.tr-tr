---
title: NuGet 3.0 sürüm notları
description: NuGet 3.0.0 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551869"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 sürüm notları

[NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 sürüm notları](../release-notes/nuget-3.1.md)

NuGet 3.0, Visual Studio 2015 için bir paket uzantısı olarak 20 Temmuz 2015 tarihinde yayınlanmıştır. Bu sürüm Visual Studio ile böylece eksiksiz güncelleştirilmiş NuGet 3.0 deneyimi yeni Visual Studio kullanıcıların kullanımına sunmak için gönderildi. Bu NuGet uzantısı sürüm, yalnızca Visual Studio 2015 için kullanılabilir.

Biz güncelleştirilmiş Windows 10 için geliştirme desteği içeren Visual Studio 2015'in kısa süre sonra yayımlama gibi kullanılabilir en son sürümü için Visual Studio Galerisi Update'e erişecek bu geliştiriciler öneririz.

Toplam 240 sorunları 3.0 sürümündeki biz kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Bilinen Sorunlar

Bu sürümle birlikte sunulan bilinen sorunlara ilişkin birkaç vardı ve bu öğelerin tümünü Windows 10'ın yayınlanmasıyla birlikte 29 Temmuz tarihinde başlayacak şekilde zamanlanmış 3.1 sürümümüzü giderilen.  Bu bilinen sorunları düzeltmek için bu tarihte veya daha sonra Galerisi, Visual Studio uzantısı güncelleştiremezsiniz.

*  Önizleme penceresini "bunu bir daha gösterme" etiketi ve Paket açıklaması penceresinde "Yazar" etiketi için çeviri sağlanmadı.
*  TFS kullanarak bir proje üzerinde çalışan, kaynak denetimi, Nuget.Config dosyası salt okunur olarak işaretlenmişse NuGet Paket Yöneticisi kullanıcı arabirimi var olamaz.
   * **Geçici çözüm** TFS dosyasından göz atın.
*  Visual Studio koyu tema kullandığınızda, "yeniden başlatma çubuğu" NuGet Powershell penceresinde sarı metinde görünür değil.
   * **Geçici çözüm** Visual Studio açık tema kullanın.


## <a name="summary-of-top-issues-resolved"></a>Çözümlenen üst sorunların özeti

* [Paket Yöneticisi penceresini yenilediğinde ağ sık sık güncelleştirme çağırır.](https://github.com/NuGet/Home/issues/515)
* [Kaydırma değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde Gecikmeli](https://github.com/NuGet/Home/issues/519)
* [Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır](https://github.com/NuGet/Home/issues/516)
* [Eklenen 'Önizleme penceresini gösterme' onay kutusu](https://github.com/NuGet/Home/issues/566)
* [Ek işlem işlemci kullanımını azaltmak için azaltma](https://github.com/NuGet/Home/issues/356)
* Geliştirilmiş işleme taşınabilir sınıf kitaplığı başvurusu
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Otomatik Tamamlama hizmeti büyük küçük harfe duyarlı](https://github.com/NuGet/Home/issues/198)
* [Temel kimlik doğrulama kimlik bilgileri güçlendirebilir güncelleştirme](https://github.com/NuGet/Home/issues/456)
* [Geliştirilmiş hata günlüğü](https://github.com/NuGet/Home/issues/407)
* [Update-Package çağırırken powershell geliştirilmiş hata iletileri](https://github.com/NuGet/Home/issues/5)
* [Windows 10'da kilitlenen önlemek için 'Seçenekleri hakkında bilgi edinin' bağlantıyı düzeltildi](https://github.com/NuGet/Home/issues/822)
* [Yayın öncesi onay kutusunu ayarını unutmayın](https://github.com/NuGet/Home/issues/732)
* [Bir Çözümdeki projeler arasında sonuçları önbelleğe alma geliştirilmiş toplama performansı](https://github.com/NuGet/Home/issues/721)
* [Paralel olarak birden çok paket toplanabilir](https://github.com/NuGet/Home/issues/713)
* [Install-package kaldırıldı-komut zorla](https://github.com/NuGet/Home/issues/697)

Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve duyuruları biz Windows 10 için geliştirme için destek sunmaya hazır olarak.