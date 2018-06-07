---
title: NuGet paket adı itiraz çözümleme
description: NuGet paket yayımcılar markası, ticari markaları ve diğer çakışma durumlarında ilgili arasındaki uyuşmazlıkların çözümü çözmek için işlemi.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: f7749dec0726162f122db91397e9581cfad23890
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817551"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="95da1-103">NuGet paket adlarının Anlaşmazlıkların</span><span class="sxs-lookup"><span data-stu-id="95da1-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="95da1-104">Bu makale, topluluk üyeleri olan diğer NuGet yayımcı itirazları çözmek için önerilen çözümleme işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="95da1-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="95da1-105">Örneğin, Northwind Traders, istemci sürücüleri kendi Web sitesinden indirilebilir bir MSI olarak sağladıkları CRM sistemine yapar varsayalım.</span><span class="sxs-lookup"><span data-stu-id="95da1-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="95da1-106">Nancy, bağımsız bir geliştirici, Northwind'ın istemci kitaplığı kullanmayı daha kolay yapmak ister ve adlı bir NuGet paketi renge `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="95da1-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="95da1-107">Daha sonra Northwind kendi istemci kitaplığı için kendi resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adı Nancy'nin sahipliğini itiraz etmek istiyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="95da1-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="95da1-108">Bu senaryoda, Nancy kötü amaçları ile hareket görünmez, ancak yerine Northwind'ın Araçlar ve müşteriler kendi saat ve kod katkıda bulunarak destekliyor.</span><span class="sxs-lookup"><span data-stu-id="95da1-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="95da1-109">Aynı anda Northwind Northwind adı yasal sahibidir.</span><span class="sxs-lookup"><span data-stu-id="95da1-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="95da1-110">Geliştirici topluluğu hizmet veren her ikisi de ilgileniyor çünkü aşağıdaki işlemi izleyerek, Northwind ve Nancy birlikte uygun bir çözüm çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95da1-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="95da1-111">Genellikle söz konusu hale gelmesi için NuGet ekibi gerekli değildir; İşbirliği genellikle en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="95da1-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="95da1-112">Aslında, tarih NuGet ekibinin dikkatini için duruma her itiraz karar geçmesi gerek takım çalışmıştır.</span><span class="sxs-lookup"><span data-stu-id="95da1-112">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="95da1-113">İşlem</span><span class="sxs-lookup"><span data-stu-id="95da1-113">Process</span></span>

1. <span data-ttu-id="95da1-114">Sahipleri başvurun paketi kullanarak itiraz sahip **kişi sahipleri** bağlantı paketi ayrıntıları sayfasında.</span><span class="sxs-lookup"><span data-stu-id="95da1-114">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="95da1-115">Tür ve doğrudan şekilde sorununuzu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="95da1-115">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="95da1-116">İletinin bir kopyasını göndermek [ support@nuget.org ](mailto:support@nuget.org) NuGet ve .NET Foundation, itiraz farkında olmasını sağlamak.</span><span class="sxs-lookup"><span data-stu-id="95da1-116">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="95da1-117">En fazla bir çözüm için 30 gün bekleyin, sonra bildirim [ support@nuget.org ](mailto:support@nuget.org) yeniden.</span><span class="sxs-lookup"><span data-stu-id="95da1-117">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="95da1-118">Nuget.org destek ekibi katın ve İtiraz her iki taraf ile çalışmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="95da1-118">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
