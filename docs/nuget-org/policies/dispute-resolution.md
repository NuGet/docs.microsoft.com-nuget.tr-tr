---
title: NuGet paket adı Itiraz çözümlemesi
description: Marka, ticari markalar ve diğer çakışma durumlarında ilgili NuGet paket yayımcıları arasında anlaşmazlıkların çözümlenme işlemi.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775663"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet paket adları üzerinden anlaşmazlıklar çözümleniyor

Bu makalede, topluluk üyelerinin diğer NuGet yayımcılarla anlaşmazlıkların çözülmesi için önerilen bir çözüm süreci sunulmaktadır.

Örneğin, Northwind Traders 'ın, Web sitelerinden indirilebilir bir MSI olarak istemci sürücüleri sundukları bir CRM sistemi oluşturduğunu varsayalım. Bağımsız bir geliştirici olan Gamze, Northwind 'nin istemci kitaplığını kullanmayı kolaylaştırmak istiyor ve adlı bir NuGet paketine dönüştürür `NorthwindTraders.Client` . Daha sonra, Northwind kendi istemci kitaplıkları için kendi kendine ait resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adının sahipliğinin itirazlarını sağlamak istiyor.

Bu senaryoda, Gamze kötü amaçları ile hareket ediyor gibi görünüyor, ancak kendi zaman ve koduna katkıda bulunan Northwind 'nin araç ve müşterilerini desteklerken. Aynı zamanda Northwind, Northwind adının meşru sahibidir.

Aşağıdaki işlemi uygulayarak, her ikisi de geliştirici topluluğu 'na hizmet etmek ilgilendiği için Northwind ve Gamze uygun bir çözünürlükte birlikte çalışabilir. Genellikle NuGet ekibinin dahil olması gerekmez; işbirliği genellikle en iyi şekilde çalışmaktadır.

## <a name="process"></a>İşleme

1. Paket ayrıntıları sayfasındaki **Ilgili sahipler** bağlantısını kullanarak itiraz ettiğiniz paketin sahiplerine başvurun. Sorununuzu bir tür ve doğrudan şekilde açıklayın.
2. NuGet ve .NET Foundation 'ın, anlaşmazlarınızın farkında olması için iletinizin bir kopyasını gönderin [support@nuget.org](mailto:support@nuget.org) .
3. Bir çözüm için en fazla 30 gün bekleyip [support@nuget.org](mailto:support@nuget.org) yeniden uyarın. Nuget.org destek ekibi dahil edilir ve her iki taraf ile itiraz aracılığıyla çalışmayı dener.
