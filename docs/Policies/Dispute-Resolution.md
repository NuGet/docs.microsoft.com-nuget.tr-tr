---
title: "\"NuGet paketi ad itiraz çözümleme | Microsoft Docs\""
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: "NuGet paket yayımcılar markası, ticari markaları ve diğer çakışma durumlarında ilgili arasındaki uyuşmazlıkların çözümü çözmek için işlemi."
keywords: "NuGet paket anlaşmazlıklar, NuGet itiraz çözümleme, itiraz çözümleme işlemi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet paket adlarının Anlaşmazlıkların

Bu belge, topluluk üyeleri olan diğer NuGet yayımcı itirazları çözmek için önerilen çözümleme işlemi değil.  

Örneğin, Northwind Traders, istemci sürücüleri kendi Web sitesinden indirilebilir bir MSI olarak sağladıkları CRM sistemine yapar varsayalım. Nancy, bağımsız bir geliştirici, Northwind'ın istemci kitaplığı kullanmayı daha kolay yapmak ister ve adlı bir NuGet paketi renge `NorthwindTraders.Client`. Daha sonra Northwind kendi istemci kitaplığı için kendi resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adı Nancy'nin sahipliğini itiraz etmek istiyor musunuz.

Bu senaryoda, Nancy kötü amaçları ile hareket görünmez, ancak yerine Northwind'ın Araçlar ve müşteriler kendi saat ve kod katkıda bulunarak destekliyor. Aynı anda Northwind Northwind adı yasal sahibidir.

Geliştirici topluluğu hizmet veren her ikisi de ilgileniyor çünkü aşağıdaki işlemi izleyerek, Northwind ve Nancy birlikte uygun bir çözüm çalışabilirsiniz. Genellikle söz konusu hale gelmesi için NuGet ekibi gerekli değildir; İşbirliği genellikle en iyi çalışır. Aslında, tarih NuGet ekibinin dikkatini için duruma her itiraz karar geçmesi gerek takım çalışmıştır.


## <a name="process"></a>İşlem

1. Sahipleri başvurun paketi kullanarak itiraz sahip **kişi sahipleri** bağlantı paketi ayrıntıları sayfasında. Tür ve doğrudan şekilde sorununuzu açıklayın.
2. İletinin bir kopyasını göndermek [ support@nuget.org ](mailto:support@nuget.org) NuGet ve .NET Foundation, itiraz farkında olmasını sağlamak.
3. En fazla bir çözüm için 30 gün bekleyin, bildirim sonra [ support@nuget.org ](mailto:support@nuget.org) yeniden. Nuget.org destek ekibi katın ve İtiraz her iki taraf ile çalışmak deneyin.
