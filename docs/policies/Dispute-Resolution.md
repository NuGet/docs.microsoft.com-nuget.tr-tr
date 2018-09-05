---
title: NuGet paket adı itiraz çözümleme
description: NuGet paket yayımlayanlar markası, ticari markalar ve diğer çakışma durumlarında ilgili arasında Anlaşmazlıkların işlemi.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550378"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>NuGet paket adları üzerinde Anlaşmazlıkların

Bu makalede bir önerilen çözümleme işlemi ile diğer NuGet yayımcılar Anlaşmazlıkların çözüm yeri topluluk üyeleri için sunulmaktadır.

Örneğin, Northwind Traders'ın kendisi için istemci sürücüleri, Web sitesinden indirilebilir bir MSI olarak sağladıkları bir CRM sistemine yapar varsayalım. Nancy, bağımsız bir geliştirici, Northwind'ın istemci kitaplığını kullanmak daha kolay hale getirmek istediği ve adlı bir NuGet paketi kapatır `NorthwindTraders.Client`. Daha sonra Northwind kendi istemci kitaplığı kendi resmi bir NuGet paketi oluşturmak istiyor ve böylece paket adı Nancy'nin sahipliğini itiraz istiyorsunuz.

Bu senaryoda, Nancy kötü amaçları ile çalışan olması için görünmez, ancak yerine Northwind'ın araçları ve müşterilerin kendi saat ve kod katkıda bulunarak destekliyor. Aynı zamanda, Northwind Northwind adının yasal sahibi ' dir.

Her ikisi de Geliştirici topluluğu hizmet içinde ilgilenen çünkü aşağıdaki işlemi izleyerek, Northwind ve Nancy birlikte uygun bir çözüm için çalışabilir. Genellikle dahil olmak NuGet ekibi için gerekli değildir; işbirliği, genellikle en iyi çalışır. Aslında, tarih NuGet takımın dikkat için her itiraz yükümlülükten geçmesi gerek olmayan takım yarar.

## <a name="process"></a>İşlem

1. Sahipleriyle temas paketi kullanarak itiraz sahip **kişi sahipleri** Paket Ayrıntıları sayfasındaki bağlantı. Sorununuzu bir tür ve doğrudan bir şekilde açıklamaktadır.
2. İletiniz için bir kopyasını gönderip [ support@nuget.org ](mailto:support@nuget.org) NuGet ve .NET Foundation, itiraz uyumlu olmasını sağlamak.
3. En fazla 30 gün içinde bir çözüm için bekleyin ve sonra bildirim [ support@nuget.org ](mailto:support@nuget.org) yeniden. Nuget.org Destek ekibine katılın ve İtiraz her iki taraf ile çalışacak şekilde deneyin.
