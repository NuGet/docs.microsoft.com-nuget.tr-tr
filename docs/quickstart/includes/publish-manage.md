---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496058"
---
nuget.org'daki profilinizden, yeni yayınladığınız profili görmek için **Paketleri Yönet'i** seçin. Ayrıca bir onay e-postası alırsınız. Paketinizin dizine eklenmenin ve başkalarının bulabileceği arama sonuçlarında görünmesinin biraz zaman alacağını unutmayın. Bu süre zarfında paket sayfanız aşağıdaki iletiyi gösterir:

![Bu paket henüz dizine eklenmedi. Arama sonuçlarında görünür ve dizin oluşturma tamamlandıktan sonra yüklemek/geri yükleme için kullanılabilir olacaktır.](../media/QS_Create-03-NotIndexed.png)

Hepsi bu! Diğer geliştiricilerin kendi projelerinde kullanabilecekleri nuget.org için ilk NuGet paketinizi yayınladınız.

Bu gözden geçirme de gerçekten yararlı olmayan bir paket oluşturduysanız (boş bir sınıf kitaplığıyla oluşturulmuş bir paket gibi), paketi arama sonuçlarından gizlemek için *listeyi boşaltmanız* gerekir:

1. nuget.org kullanıcı adınızı (sayfanın sağ üst tarafında) seçin ve **ardından Paketleri Yönet'i**seçin.

1. **Yayımlanmış** altında listeyi boşaltmak istediğiniz paketi bulun ve sağdaki çöp kutusu simgesini seçin:

    ![nuget.org'da bir paket listesi için gösterilen çöp kutusu simgesi](../media/qs_create-vs-03-trash-can.png)

1. Sonraki sayfada, **arama sonuçlarında Liste (paket adı)** etiketli kutuyu temizleyin ve **Kaydet'i**seçin:

    ![nuget.org'da bir paket için Liste onay kutusunu temizleme](../media/qs_create-vs-04-unlist.png)