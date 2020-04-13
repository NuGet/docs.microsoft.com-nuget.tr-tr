---
title: NuGet Paketlerini nuget.org Silme
description: nuget.org gelen paketleri listedışı bırakma ilkeleri; paketlerin diğer ilkeleri ihlal ettiği durumlar dışında kalıcı silme desteklenmez.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581274"
---
# <a name="deleting-packages"></a>Paketleri silme

nuget.org paketlerin kalıcı olarak silinmesini desteklemez. Bunu yapmak, özellikle paket geri yüklemeiçeren yapı iş akışları ile, paketin kullanılabilirliğine bağlı olarak her projeyi bozar.

nuget.org, web sitesindeki paket yönetim sayfasında yapılabilecek [bir paketin listedışı kalınmasına](#unlisting-a-package)destek veriyor. Listelenmemiş paketler nuget.org veya Visual Studio UI'de görünmez ve arama sonuçlarında görünmez. Ancak listelenmemiş paketler, paket geri yüklemeyi destekleyen tam bir sürüm numarası kullanılarak indirilebilir ve yüklenebilir. Buna ek olarak, listelenmemiş paketler hala aşağıdaki özel senaryolarda keşfedilebilir:

- Sürüm veya bağımlılık kısıtlamalarıyla eşleşen `1.0.0-*`en son kullanılabilir paket listelenmemiş bir paketse, kayan sürümleri (örneğin, ) kullanarak paket geri yükleme.
- Katalog aracılığıyla paketlerin çoğaltılması (katalog da listelenmemiş paketleri içerdiğinden).

## <a name="exceptions"></a>Özel durumlar

Telif hakkı ihlali ve zararlı olabilecek içerik gibi istisnai durumlarda paketler NuGet ekibi tarafından el ile silinebilir. NuGet.org paket ayrıntıları sayfasındaki "Kötüye kullanımı bildir" düğmesini kullanarak paketi bildirebilirsiniz. Paket sahibiyseniz, NuGet.org paket ayrıntıları sayfasındaki "Destekle İletişim" düğmesini kullanarak NuGet desteğine ulaşmak için NuGet.org hesabınıza giriş yapın.

## <a name="prohibited-use"></a>Yasak kullanım

Aşağıdaki ölçütlerden herhangi birini karşılayan paketlerin genel NuGet galerisinde girmesine izin verilmez ve tartışmadan hemen kaldırılır. Ancak paket sahipleri kaldırma hakkında bilgilendirilecek.

- Kötü amaçlı yazılımlar, adware veya her türlü casus yazılım içerir.
- Bir geliştiricinin iş istasyonuna veya kuruluşuna zarar vermek üzere tasarlanmıştır.
- Telif haklarını ihlal eder veya lisansları ihlal eder.
- Yasa dışı içerik içerir.
- Sıfır üretken içeriğe sahip paketler de dahil olmak üzere paket tanımlayıcıları üzerinde çömelmek için kullanılıyor. Paketler kod içermelidir veya sahipleri aslında sevk için bir ürün olan birine tanımlayıcı kabul etmelidir.
- Galeriye açıkça tasarlanmadığı bir şeyi yapmaya çalış.

Bu öğelerden herhangi birini ihlal eden bir paket bulursanız, paket ayrıntıları sayfasındaki **Kötüye Kullanımı Bildir** bağlantısını tıklayın ve bir rapor gönderin.

NuGet ekibinin ve .NET Vakfı'nın bu kriterleri istediği zaman değiştirme hakkını saklı tutar.

## <a name="unlisting-a-package"></a>Paketi listeleme
Paket sürümünün listelenmesi, paketi aramadan ve paket ayrıntıları sayfasından nuget.org gizler. Bu, paketin mevcut kullanıcılarının paketi kullanmaya devam etmesine izin verir, ancak paket aramada görünmediğinden yeni benimsenmesini azaltır.

Paketin listesini çıkarmak için adımlar:

1. Seçin `Your account name` (sağ üst köşede) >`Manage packages` > `Published packages`
1. "Paketi yönet" simgesini seçin
1. "Listeleme" bölümünü genişletin ve paket sürümünü seçin
1. "Arama sonuçlarında listele" seçeneğini kaldırın ve "Kaydet"i seçin

Belirli paket sürümü artık listedışı bırakıldı. Bunu doğrulamak için, hesabınızın oturumuna geçin ve paket sayfasına (sürüm bölümü olmadan) gidin: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/. Bu paketin listelenmemiş tüm sürümlerini görürsünüz. **not** Ancak, paket sahibi oturum açtığınızda tüm sürümleri ve giriş durumlarını görebilir.

Bir paket sürümünü amortismana kullanabilirsiniz (paket sürümünü silemezseniz). Paket sürümlerini küçümseme hakkında daha fazla bilgi için [bkz.](../deprecate-packages.md)
