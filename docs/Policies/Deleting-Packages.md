---
title: NuGet paketlerini nuget.org silme | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "Nuget.org unlisting paketlerinden ilkelerini; diğer ilkeler paketleri ihlal silme işlemi geri alınamaz dışında desteklenmez."
keywords: "NuGet paketi silme, NuGet paketini paketlerin unlisting, izin verilmeyen kullanır"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
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
- Bir şeyler galeri girişiminde, açıkça yapmak için tasarlanmamıştır.

İhlal bu öğelerden herhangi birini bir paket bulursanız tıklatın **rapor kötüye** bağlantı paketi ayrıntıları sayfasında ve bir rapor gönderin.

NuGet takım .NET Foundation ayırdığını herhangi bir zamanda Bu ölçütleri değiştirmek için sağ unutmayın.
