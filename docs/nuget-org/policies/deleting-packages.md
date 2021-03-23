---
title: NuGet paketlerini nuget.org 'dan silme
description: Nuget.org konumundan paketlerin listesini kaldırma ilkeleri paketlerin diğer ilkeleri ihlal ettiği durumlar dışında kalıcı silme desteklenmez.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 574ee874e2d6555a2e3e0a0643962e33b7ec1b09
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859453"
---
# <a name="deleting-packages"></a>Paketleri silme

nuget.org, paketlerin kalıcı olarak silinmesini desteklemez. Bunun yapılması, özellikle paket geri yüklemeyi içeren derleme iş akışlarıyla, paketin kullanılabilirliğine bağlı olarak her projeyi keser.

nuget.org, Web sitesindeki paket yönetimi sayfasında yapılabilecek [bir paketin listesini kaldırma](#unlisting-a-package)desteği. Listelenmemiş paketler nuget.org veya Visual Studio Kullanıcı arabiriminde görünmez ve arama sonuçlarında görünmez. Ancak, listelenmemiş paketler, paket geri yüklemeyi destekleyen tam bir sürüm numarası kullanılarak indirilip yüklenebilirler. Ayrıca, listelenmemiş paketler yine de aşağıdaki belirli senaryolarda bulunabilir:

- Kayan sürümler (örneğin,) kullanarak paket geri yükleme `1.0.0-*` , sürüm veya bağımlılık kısıtlamalarıyla eşleşen en son paket listelenmemiş bir pakettir.
- Katalog aracılığıyla paketlerin çoğaltılması (Katalog Ayrıca listelenmemiş paketleri de içerir).

## <a name="exceptions"></a>Özel durumlar

Telif hakkı ihlali ve potansiyel olarak zararlı içerik gibi olağanüstü durumlarda, paketler NuGet ekibi tarafından el ile silinebilir. NuGet.org paket ayrıntıları sayfasındaki "kötüye kullanımı raporla" düğmesini kullanarak bir paket bildirebilirsiniz. Paket sahibiyseniz, NuGet.org paket ayrıntıları sayfasındaki "desteğe başvur" düğmesini kullanarak NuGet desteğine ulaşmak için NuGet.org hesabınızda oturum açın.

## <a name="prohibited-use"></a>Yasaklanmış Kullanım

Ortak NuGet galerisinde aşağıdaki ölçütlerden birine uyan paketlere izin verilmez ve hiçbir tartışma yapılmadan hemen kaldırılır. Bununla birlikte, paket sahipleri, kaldırma işleminin bilgilendirilmesine sahip olur.

- Kötü amaçlı yazılım, reklam yazılımı veya herhangi bir tür casus yazılım içerir.
- , Bir geliştiricinin iş istasyonuna veya kuruluşuna zarar verecek şekilde tasarlanmıştır.
- Kuruluşa ait telif hakları veya ihlal ediyor.
- Geçersiz içerik içeriyor.
- , Sıfır üretken içeriğe sahip paketler dahil paket tanımlayıcılarında squon 'ta kullanılıyor. Paketler kod içermeli veya sahipler, gerçekten bir ürüne sahip olan bir kişiye tanımlayıcıyı bir biçimde gizleme olmalıdır.
- Galeri 'yi açıkça yapmak üzere tasarlanmadığı bir şeyi yapmayı deneyin.

Bu öğelerden herhangi birini ihlal eden bir paket bulursanız, paket ayrıntıları sayfasında **kötüye kullanımı bildir** bağlantısına tıklayın ve bir rapor gönderebilirsiniz.

NuGet ekibi ve .NET Foundation 'ın, bu ölçütleri istediğiniz zaman değiştirme hakkını ayırdığını unutmayın.

## <a name="unlisting-a-package"></a>Bir paketin listesini kaldırma
Bir paket sürümünün listesinin kaldırılması, onu arama ve nuget.org paket ayrıntıları sayfasından gizler. Bu, paketin var olan kullanıcılarının bu uygulamayı kullanmaya devam etmesine izin verir, ancak paket aramada görülemediğinden yeni benimsemeyi azaltır.

Paket listesini kaldırma adımları:

1. Seç `Your account name` (sağ üst köşede) >`Manage packages` > `Published packages`
1. "Paketi Yönet" simgesini seçin
1. "Listeleme" bölümünü genişletin ve paket sürümünü seçin
1. "Arama sonuçlarında Listele" seçeneğinin işaretini kaldırın ve "Kaydet" i seçin

Belirli paket sürümü artık listelenmemiş. Bunu doğrulamak için, hesabınızın oturumunu kapatın ve paket sayfasına (sürüm bölümü olmadan) gidin, örneğin: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Bu paketin listede listelenmemiş tüm sürümlerini görürsünüz.  Ancak, oturum açıldığında paket sahibi, tüm sürümleri ve bunların listeleme durumlarını görebilir.

Paket sürümünü kullanımdan kaldırmak da mümkündür (bir paket sürümünü silemmeniz durumunda). Paket sürümlerini kullanımdan kaldırma hakkında daha fazla bilgi için bkz. [paketleri kullanımdan](../deprecate-packages.md)kaldırma.
