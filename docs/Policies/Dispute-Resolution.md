---
title: "NuGet paket adı itiraz çözümleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet paket yayımcılar markası, ticari markaları ve diğer çakışma durumlarında ilgili arasındaki uyuşmazlıkların çözümü çözmek için işlemi."
keywords: "NuGet paket anlaşmazlıklar, NuGet itiraz çözümleme, itiraz çözümleme işlemi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="70902-104">NuGet paket adlarının Anlaşmazlıkların</span><span class="sxs-lookup"><span data-stu-id="70902-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="70902-105">Bu makale, topluluk üyeleri olan diğer NuGet yayımcı itirazları çözmek için önerilen çözümleme işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="70902-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="70902-106">Örneğin, Northwind Traders, istemci sürücüleri kendi Web sitesinden indirilebilir bir MSI olarak sağladıkları CRM sistemine yapar varsayalım.</span><span class="sxs-lookup"><span data-stu-id="70902-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="70902-107">Nancy, bağımsız bir geliştirici, Northwind'ın istemci kitaplığı kullanmayı daha kolay yapmak ister ve adlı bir NuGet paketi renge `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="70902-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="70902-108">Daha sonra Northwind kendi istemci kitaplığı için kendi resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adı Nancy'nin sahipliğini itiraz etmek istiyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="70902-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="70902-109">Bu senaryoda, Nancy kötü amaçları ile hareket görünmez, ancak yerine Northwind'ın Araçlar ve müşteriler kendi saat ve kod katkıda bulunarak destekliyor.</span><span class="sxs-lookup"><span data-stu-id="70902-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="70902-110">Aynı anda Northwind Northwind adı yasal sahibidir.</span><span class="sxs-lookup"><span data-stu-id="70902-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="70902-111">Geliştirici topluluğu hizmet veren her ikisi de ilgileniyor çünkü aşağıdaki işlemi izleyerek, Northwind ve Nancy birlikte uygun bir çözüm çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70902-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="70902-112">Genellikle söz konusu hale gelmesi için NuGet ekibi gerekli değildir; İşbirliği genellikle en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="70902-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="70902-113">Aslında, tarih NuGet ekibinin dikkatini için duruma her itiraz karar geçmesi gerek takım çalışmıştır.</span><span class="sxs-lookup"><span data-stu-id="70902-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="70902-114">İşlem</span><span class="sxs-lookup"><span data-stu-id="70902-114">Process</span></span>

1. <span data-ttu-id="70902-115">Sahipleri başvurun paketi kullanarak itiraz sahip **kişi sahipleri** bağlantı paketi ayrıntıları sayfasında.</span><span class="sxs-lookup"><span data-stu-id="70902-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="70902-116">Tür ve doğrudan şekilde sorununuzu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="70902-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="70902-117">İletinin bir kopyasını göndermek [ support@nuget.org ](mailto:support@nuget.org) NuGet ve .NET Foundation, itiraz farkında olmasını sağlamak.</span><span class="sxs-lookup"><span data-stu-id="70902-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="70902-118">En fazla bir çözüm için 30 gün bekleyin, sonra bildirim [ support@nuget.org ](mailto:support@nuget.org) yeniden.</span><span class="sxs-lookup"><span data-stu-id="70902-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="70902-119">Nuget.org destek ekibi katın ve İtiraz her iki taraf ile çalışmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="70902-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
