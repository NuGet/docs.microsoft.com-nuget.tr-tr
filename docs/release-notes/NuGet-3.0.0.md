---
title: NuGet 3,0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.0.0 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776550"
---
# <a name="nuget-30-release-notes"></a>NuGet 3,0 sürüm notları

[NuGet 3,0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)  |  [NuGet 3,1 sürüm notları](../release-notes/nuget-3.1.md)

NuGet 3,0, Visual Studio 2015 için bir paket uzantısı olarak 20 Temmuz 2015 tarihinde yayınlanmıştır. Bu sürümü Visual Studio ile sunmaya itiyoruz, böylece tüm güncelleştirilmiş NuGet 3,0 deneyimi yeni Visual Studio kullanıcıları için kullanılabilir olacaktır. Bu NuGet uzantısı sürümü yalnızca Visual Studio 2015 için kullanılabilir.

Windows 10 geliştirme desteği içeren Visual Studio 2015 yayımlandıktan hemen sonra bir güncelleştirme yayımladığımızda, Visual Studio Galerisi güncelleştirmesine erişimi olan geliştiricilerin, mevcut en son sürüme, bir güncelleştirmeyi yayımladığımız için, bu geliştiricilerin kullanılabilir en son sürüme erişimi önerilir.

Total, 3,0 sürümündeki 240 sorunu kapattık ve [GitHub 'daki sorunların tam listesini](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)inceleyebilirsiniz.

## <a name="known-issues"></a>Bilinen Sorunlar

Bu sürümle birlikte sunulan bazı bilinen sorunlar vardı ve bu öğelerin tümü, 29 Temmuz 'da Windows 10 ' un yayınlanmasıyla çakıştığı için zamanlanmış 3,1 sürümümüzde düzeltildi.  Bu bilinen sorunları çözmek için Visual Studio uzantınızı bu tarihten sonra veya sonra Galeriden güncelleştirebilirsiniz.

*  "Bunu bir daha gösterme" etiketini önizleme penceresinde ve paket açıklaması penceresinde "yazarlar" etiketi için çeviri sağlanmaz.
*  TFS kaynak denetimini kullanarak bir proje üzerinde çalışırken, Nuget.Config dosyası salt okunurdur olarak işaretlenmişse, NuGet Paket Yöneticisi Kullanıcı arabirimini sunamaz.
   * **Geçici çözüm** TFS 'den dosyaya göz atın.
*  NuGet PowerShell penceresindeki sarı "yeniden başlatma çubuğunda" metin, Visual Studio koyu temasını kullandığınızda görünür değildir.
   * **Geçici çözüm** Visual Studio Light temasını kullanın.


## <a name="summary-of-top-issues-resolved"></a>Çözümlenen başlıca sorunların Özeti

* [Paket Yöneticisi penceresi yenilendiğinde sık kullanılan ağ güncelleştirme çağrıları](https://github.com/NuGet/Home/issues/515)
* [Paket Yöneticisi 'nde yüklü görünüme geçiş yaparken gecikmeli kaydırma](https://github.com/NuGet/Home/issues/519)
* [Ağ çağrıları bir arka plan iş parçacığında çalıştırılmalıdır](https://github.com/NuGet/Home/issues/516)
* [' Önizleme penceresini gösterme ' onay kutusu eklendi](https://github.com/NuGet/Home/issues/566)
* [İşlemci kullanımını azaltmak için işlem azaltma eklendi](https://github.com/NuGet/Home/issues/356)
* İyileştirilmiş taşınabilir sınıf kitaplığı başvuru işleme
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Otomatik tamamlama hizmeti büyük/küçük harfe duyarlıdır](https://github.com/NuGet/Home/issues/198)
* [Temel kimlik doğrulama kimlik bilgilerini yeniden tanıtmak için Güncelleştir](https://github.com/NuGet/Home/issues/456)
* [İyileştirilmiş hata günlüğü](https://github.com/NuGet/Home/issues/407)
* [Update-Package çağrılırken geliştirilmiş PowerShell hata iletileri](https://github.com/NuGet/Home/issues/5)
* [Windows 10 ' da kilitlenme oluşmasını engellemek için ' Seçenekler hakkında bilgi edinin ' bağlantısı düzeltildi](https://github.com/NuGet/Home/issues/822)
* [Yayın öncesi onay kutusu ayarı](https://github.com/NuGet/Home/issues/732)
* [Bir çözümdeki projeler arasında sonuçları önbelleğe alarak geliştirilmiş toplama performansı](https://github.com/NuGet/Home/issues/721)
* [Paralel olarak birden çok paket toplaneklenebilir](https://github.com/NuGet/Home/issues/713)
* [Install-Package-zorlama komutu kaldırıldı](https://github.com/NuGet/Home/issues/697)

Windows 10 geliştirme desteği sunmaya hazırlanma konusunda daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun.