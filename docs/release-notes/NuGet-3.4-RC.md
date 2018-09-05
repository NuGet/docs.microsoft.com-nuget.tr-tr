---
title: NuGet 3.4 RC sürüm notları
description: NuGet 3.4 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546760"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC sürüm notları

[NuGet 3.3 Sürüm Notları](../release-notes/nuget-3.3.md) | [NuGet 3.4 sürüm notları](../release-notes/nuget-3.4.md)

NuGet 3.4-RC, 3 Mart 2016'dan Visual Studio 2015 güncelleştirme 2 RC ile birlikte yayımlanan ve aklını içinde birkaç sacayakları derlendiği:

* Platformlar arası destek
* Performans iyileştirmeleri
* Küçük bir kullanıcı Arabirimi geliştirmeleri

Aşağıdaki özellikler daha 3.4 son sürümlerde sunulması planlanmaktadır bu RC sürümünde mevcuttur.

## <a name="new-features"></a>Yeni Özellikler

* NuGet istemcileri artık gzip içerik kodlamasını depolarından destekler
* Xproj projelerindeki paketlerden PDB'leri için destek
* Derleme eylemleri contentFiles öğesinde iOS ve Android desteği
* Netstandard ve netstandardapp framework bilinen adlar için destek

## <a name="new-user-interface-features"></a>Yeni kullanıcı arabirimi özellikleri

* Yüklü, güncelleştirmeleri ve birleştirme sekmelerinde özellikle önemli performans geliştirmeleri
* Yüklü ve güncelleştirmeleri sekmeleri artık alfabetik olarak sıralanır.
* Sağlayan bir arama yenilenmesi yenile düğmesine eklendi

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve iyileştirmeler

* Başvurulan paketleri `project.json` sahip kayan sürüm her derleme üzerinde güncelleştirmez. Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecek `project.json`.
* NuGet Yapılandırması kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırması zorlanır.
* NuGet artık paylaşılan projelerde paketleri geri yükler veya bir kilit dosyası yazar.
* Biz, ağ hatası geliştirdik ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.
* Klavye ve fare davranışlar Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.
* En son artık desteklenmektedir `project.json` DNX şemasında.

## <a name="known-issues"></a>Bilinen Sorunlar

Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)