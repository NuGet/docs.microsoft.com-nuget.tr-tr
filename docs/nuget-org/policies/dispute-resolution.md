---
title: NuGet paket adı Itiraz çözümlemesi
description: Marka, ticari markalar ve diğer çakışma durumlarında ilgili NuGet paket yayımcıları arasında anlaşmazlıkların çözümlenme işlemi.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 7e725d8114cde3de189dc3a648bc5a6c0b0e785b
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367953"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="1dc2a-103">NuGet paket adları üzerinden anlaşmazlıklar çözümleniyor</span><span class="sxs-lookup"><span data-stu-id="1dc2a-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="1dc2a-104">Bu makalede, topluluk üyelerinin diğer NuGet yayımcılarla anlaşmazlıkların çözülmesi için önerilen bir çözüm süreci sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="1dc2a-105">Örneğin, Northwind Traders 'ın, Web sitelerinden indirilebilir bir MSI olarak istemci sürücüleri sundukları bir CRM sistemi oluşturduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="1dc2a-106">Bağımsız bir geliştirici olan Gamze, Northwind 'nin istemci kitaplığını kullanmayı kolaylaştırmak istiyor ve adlı bir NuGet paketine dönüştürür `NorthwindTraders.Client` .</span><span class="sxs-lookup"><span data-stu-id="1dc2a-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="1dc2a-107">Daha sonra, Northwind kendi istemci kitaplıkları için kendi kendine ait resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adının sahipliğinin itirazlarını sağlamak istiyor.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="1dc2a-108">Bu senaryoda, Gamze kötü amaçları ile hareket ediyor gibi görünüyor, ancak kendi zaman ve koduna katkıda bulunan Northwind 'nin araç ve müşterilerini desteklerken.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="1dc2a-109">Aynı zamanda Northwind, Northwind adının meşru sahibidir.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="1dc2a-110">Aşağıdaki işlemi uygulayarak, her ikisi de geliştirici topluluğu 'na hizmet etmek ilgilendiği için Northwind ve Gamze uygun bir çözünürlükte birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="1dc2a-111">Genellikle NuGet ekibinin dahil olması gerekmez; işbirliği genellikle en iyi şekilde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span>

## <a name="process"></a><span data-ttu-id="1dc2a-112">İşleme</span><span class="sxs-lookup"><span data-stu-id="1dc2a-112">Process</span></span>

1. <span data-ttu-id="1dc2a-113">Paket ayrıntıları sayfasındaki **Ilgili sahipler** bağlantısını kullanarak itiraz ettiğiniz paketin sahiplerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-113">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="1dc2a-114">Sorununuzu bir tür ve doğrudan şekilde açıklayın.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-114">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="1dc2a-115">NuGet ve .NET Foundation 'ın, anlaşmazlarınızın farkında olması için iletinizin bir kopyasını gönderin [support@nuget.org](mailto:support@nuget.org) .</span><span class="sxs-lookup"><span data-stu-id="1dc2a-115">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="1dc2a-116">Bir çözüm için en fazla 30 gün bekleyip [support@nuget.org](mailto:support@nuget.org) yeniden uyarın.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-116">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="1dc2a-117">Nuget.org destek ekibi dahil edilir ve her iki taraf ile itiraz aracılığıyla çalışmayı dener.</span><span class="sxs-lookup"><span data-stu-id="1dc2a-117">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
