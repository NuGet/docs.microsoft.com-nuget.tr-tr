---
title: NuGet Paket Adı Uyuşmazlık Çözümü
description: NuGet paket yayıncıları arasındaki markalama, ticari markalar ve diğer çakışma durumlarla ilgili anlaşmazlıkları çözme süreci.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427499"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet paket adları ile ilgili anlaşmazlıkları çözme

Bu makalede, topluluk üyelerinin diğer NuGet yayıncılarıyla olan anlaşmazlıkları çözmeleri için önerilen bir çözüm süreci sağlanmaktadır.

Örneğin, Northwind Traders'ın istemci sürücülerini web sitelerinden indirilebilir bir MSI olarak sağladıkları bir CRM sistemi ürettiklerini varsayalım. Nancy, bağımsız bir geliştirici, daha kolay Northwind istemci kitaplığı kullanmak yapmak istiyor, ve `NorthwindTraders.Client`bir NuGet paketi olarak adlandırılan dönüşür. Daha sonra, Northwind kendi müşteri kütüphanesi için kendi resmi bir NuGet paketi üretmek istiyor, ve böylece paket adı Nancy sahipliğini tartışmak istiyorum.

Bu senaryoda, Nancy kötü niyetleri ile hareket gibi görünmüyor, ama oldukça northwind araçları ve müşterilerine kendi zaman ve kod katkıda bulunarak destekliyor. Aynı zamanda, Northwind Northwind adının meşru sahibidir.

Aşağıdaki süreci izleyerek, Northwind ve Nancy birlikte uygun bir çözüm için çalışabilir, her ikisi de geliştirici topluluk hizmet ilgilenen çünkü. Genellikle NuGet ekibinin katılması na gerek yoktur; işbirliği genellikle en iyi şekilde çalışır. Aslında, bugüne kadar NuGet ekibinin dikkatine getirilen her anlaşmazlık, takım karar vermek gerek kalmadan halledilmiştir.

## <a name="process"></a>İşleme

1. Paket detayları **sayfasındaKi İletişim Sahipleri** bağlantısını kullanarak sorun yaşadığın paketin sahipleriyle iletişim kurun. Sorununuzu nazik ve doğrudan bir şekilde açıklayın.
2. NuGet ve .NET [support@nuget.org](mailto:support@nuget.org) Vakfı'nın anlaşmazlığınızdan haberdar olması için mesajınızın bir kopyasını gönderin.
3. Bir çözüm için en fazla 30 [support@nuget.org](mailto:support@nuget.org) gün bekleyin ve sonra tekrar bildirin. nuget.org destek ekibi olaya dahil olacak ve her iki tarafla da anlaşmazlığı çözmeye çalışacaktır.
