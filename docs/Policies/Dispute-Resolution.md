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
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="4bdd7-104">NuGet paket adlarının Anlaşmazlıkların</span><span class="sxs-lookup"><span data-stu-id="4bdd7-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="4bdd7-105">Bu belge, topluluk üyeleri olan diğer NuGet yayımcı itirazları çözmek için önerilen çözümleme işlemi değil.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="4bdd7-106">Örneğin, Northwind Traders, istemci sürücüleri kendi Web sitesinden indirilebilir bir MSI olarak sağladıkları CRM sistemine yapar varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="4bdd7-107">Nancy, bağımsız bir geliştirici, Northwind'ın istemci kitaplığı kullanmayı daha kolay yapmak ister ve adlı bir NuGet paketi renge `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="4bdd7-108">Daha sonra Northwind kendi istemci kitaplığı için kendi resmi bir NuGet paketi oluşturmak istiyor ve bu nedenle paket adı Nancy'nin sahipliğini itiraz etmek istiyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="4bdd7-109">Bu senaryoda, Nancy kötü amaçları ile hareket görünmez, ancak yerine Northwind'ın Araçlar ve müşteriler kendi saat ve kod katkıda bulunarak destekliyor.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="4bdd7-110">Aynı anda Northwind Northwind adı yasal sahibidir.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="4bdd7-111">Geliştirici topluluğu hizmet veren her ikisi de ilgileniyor çünkü aşağıdaki işlemi izleyerek, Northwind ve Nancy birlikte uygun bir çözüm çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="4bdd7-112">Genellikle söz konusu hale gelmesi için NuGet ekibi gerekli değildir; İşbirliği genellikle en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="4bdd7-113">Aslında, tarih NuGet ekibinin dikkatini için duruma her itiraz karar geçmesi gerek takım çalışmıştır.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="4bdd7-114">İşlem</span><span class="sxs-lookup"><span data-stu-id="4bdd7-114">Process</span></span>

1. <span data-ttu-id="4bdd7-115">Sahipleri başvurun paketi kullanarak itiraz sahip **kişi sahipleri** bağlantı paketi ayrıntıları sayfasında.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="4bdd7-116">Tür ve doğrudan şekilde sorununuzu açıklayın.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="4bdd7-117">İletinin bir kopyasını göndermek [ support@nuget.org ](mailto:support@nuget.org) NuGet ve .NET Foundation, itiraz farkında olmasını sağlamak.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="4bdd7-118">En fazla bir çözüm için 30 gün bekleyin, bildirim sonra [ support@nuget.org ](mailto:support@nuget.org) yeniden.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="4bdd7-119">Nuget.org destek ekibi katın ve İtiraz her iki taraf ile çalışmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="4bdd7-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
