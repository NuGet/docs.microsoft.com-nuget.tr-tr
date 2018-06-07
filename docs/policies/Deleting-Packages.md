---
title: Nuget.org silme NuGet paketleri
description: Nuget.org unlisting paketlerinden ilkelerini; diğer ilkeler paketleri ihlal silme işlemi geri alınamaz dışında desteklenmez.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 84a27c16968fa55ff1929db1adf98b8242a64fcf
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817001"
---
# <a name="deleting-packages"></a>Paketlerin silinmesi

nuget.org paketleri kalıcı silinmesini desteklemez. Bunun yapılması her proje paket geri yükleme ile ilgili özellikle yapı iş akışlarıyla paketinin kullanılabilirliği bağlı olarak çalışmamasına neden.

nuget.org destekliyor mu *unlisting* web sitesinde paket Yönetimi sayfasındaki yapılabilir bir paket. Listede bulunmayan paketleri nuget.org veya Visual Studio kullanıcı arabiriminde görünmez ve arama sonuçlarında görünmez. Listede bulunmayan paketleri, ancak hala indirilebilen ve paket geri yüklemesi destekleyen bir tam sürüm numarası kullanarak yüklü. Ayrıca, listede bulunmayan paketleri hala aşağıdaki belirli senaryolarda bulunan:

- Paket geri yükleme kayan sürümlerini kullanan (örneğin, `1.0.0-*`), sürüm veya bağımlılık kısıtlamaları eşleşen en son kullanılabilir paket listelenmemiş paketidir.
- Çoğaltma Kataloğu yoluyla paketlerin (katalog de listelenmemiş paketlerini içeren gibi).

## <a name="exceptions"></a>Özel Durumlar

Telif hakkı ihlali ve zararlı içeriği gibi olağanüstü durumlarda, paketleri el ile NuGet ekibi tarafından silinebilir. Bir destek isteği üzerinden göndermek [NuGet galerisinde](http://www.nuget.org) işlemini başlatmak için.

## <a name="prohibited-use"></a>Yasaklanan kullanın

Herhangi bir aşağıdaki ölçütleri karşılayan paketleri ortak NuGet galerisinde izin verilmiyor ve tartışma hemen kaldırılacak. Sahipleri olacaktır, ancak paket, kaldırılmasını bildirilmesi.

- Kötü amaçlı yazılım, reklam veya casus yazılım her türlü içerir.
- Bir geliştiricinin iş istasyonu veya kuruluşu zarar vermek için tasarlanmıştır.
- Telif Hakkı ihlal eden veya lisansları ihlal ediyor.
- Geçersiz içerik var.
- Kullanılmakta olan sıfır üretken içeriğe sahip paketleri de dahil olmak üzere paket tanımlayıcıları üzerinde squat için. Paketleri kodu içermelidir veya sahipleri tanımlayıcı aktarmak üzere bir ürün olan başka birine bırakma gerekir.
- Açıkça yapmak için tasarlanmış bir şeyler galeri yapmaya çalışır.

İhlal bu öğelerden herhangi birini bir paket bulursanız tıklatın **rapor kötüye** bağlantı paketi ayrıntıları sayfasında ve bir rapor gönderin.

NuGet takım .NET Foundation ayırdığını herhangi bir zamanda Bu ölçütleri değiştirmek için sağ unutmayın.
