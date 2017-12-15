---
title: "NuGet 3.0 RC2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20f9b360-2d78-4676-a803-e86996eb2f10
description: "NuGet 3.0 RC2 için bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0 RC2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2a708babf200a650a0faffc704235d3c142f510f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 sürüm notları

[NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 yayımlanan 3 Haziran 2015 tarihinde Visual Studio 2015 uzantısı galerisinden kullanılabilir sürüm bir geçici olarak ve [Codeplex](https://nuget.codeplex.com/releases/view/615507). Önemli hata düzeltmeleri sayısı bu sürümde var ve biz Keçeli performans iyileştirmeleri tamamlanmış Visual Studio 2015 yayımlanmadan önce serbest bırakmak önemli. Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.

Toplam, biz bu sürümde 158 sorunları kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

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

Bu karşıdan [güncelleştirmek için NuGet uzantısı](https://nuget.codeplex.com/releases/view/615507) Codeplex ve Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!