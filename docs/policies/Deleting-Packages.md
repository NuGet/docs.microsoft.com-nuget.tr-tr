---
title: NuGet paketleri nuget.org adresinden silme
description: Nuget.org unlisting paketleri için ilkeleri; paketleri diğer ilkelerini ihlal olduğunda dışında kalıcı silme desteklenmiyor.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196193"
---
# <a name="deleting-packages"></a>Paketleri silme

nuget.org paketleri kalıcı olarak silinmesini desteklemez. Bunun yapılması özellikle paket geri yükleme içeren derleme iş akışlarıyla paket kullanılabilirliğini bağlı olarak her proje bölün.

nuget.org destekliyor mu *unlisting* bir paketi paket Yönetim sayfasında web sitesinde yapılabilir. Listelenmemiş paketleri nuget.org üzerinde veya Visual Studio kullanıcı arabiriminde görünmez ve arama sonuçlarında görünmez. Listelenmemiş paketleri, ancak yine de indirilebilen ve paket geri yükleme destekleyen bir tam sürüm numarası kullanarak yüklü. Ayrıca, listede bulunmayan paketler hala aşağıdaki belirli senaryolarda bulunan:

- Kayan sürümleri kullanılarak geri yükleme paketini (örneğin, `1.0.0-*`), sürüm veya bağımlılık kısıtlamalarıyla eşleşen en son kullanılabilir paket listelenmemiş bir pakettir.
- Paket Kataloğu aracılığıyla çoğaltma (Kataloğu ayrıca listelenmemiş paketleri içerdiği için).

## <a name="exceptions"></a>Özel Durumlar

Telif hakkı ihlali ve potansiyel olarak zararlı içeriği gibi olağanüstü durumlarda, paketleri el ile NuGet ekibi tarafından silinebilir. NuGet.org Paket Ayrıntıları sayfasındaki "Uygunsuz" düğmesini kullanarak bir paket bildirebilirsiniz. NuGet.org Paket Ayrıntıları sayfasındaki "desteğe başvurun" düğmesini kullanarak NuGet desteği ulaşmaya NuGet.org hesabınızda oturum açın paket sahibinden varsa.

## <a name="prohibited-use"></a>Yasaklanmış kullanımı

Aşağıdaki ölçütleri karşılayan paketleri genel NuGet galerisinde izin verilmez ve tartışma hemen kaldırılacak. Sahipleri olacaktır, ancak paket, kaldırılmasını bildirim.

- Kötü amaçlı yazılım, reklam yazılımlarından ve her türlü bir casus yazılım içerir.
- Geliştirici iş istasyonu veya kuruluş zarar vermek için tasarlanmıştır.
- Telif Hakkı herhangi bir mülkiyet veya lisans ihlal ediyor.
- Geçersiz içerik içerir.
- Kullanılmakta olan sıfır üretken içerik paketleri de dahil olmak üzere paket tanımlayıcılarla ilgili squat için. Kod paketleri içermelidir veya sahipleri tanımlayıcısını oluşturmak için bir ürün olan birisi bırakma gerekir.
- Açıkça yapmak için tasarlanmış bir şey yapın galerisini çıkarmaya çalışın.

İhlal bu öğelerden herhangi birinin bir paketi bulursanız, tıklayın **uygunsuz** Paket Ayrıntıları sayfasına bağlantı ve bir rapor gönderin.

NuGet takım ve .NET Foundation herhangi bir zamanda bu ölçütlerini değiştirmek için sağ ayırdığını unutmayın.
