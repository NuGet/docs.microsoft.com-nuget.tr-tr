---
title: NuGet.org genel bakış
description: NuGet.org genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427523"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="0daac-103">NuGet.org genel bakış</span><span class="sxs-lookup"><span data-stu-id="0daac-103">Overview of NuGet.org</span></span>

<span data-ttu-id="0daac-104">NuGet.org, her gün çalışan NuGet paketlerinin milyonlarca .NET ve .NET Core geliştiricileri tarafından ortak bir ana bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="0daac-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="0daac-105">NuGet.org rolünde NuGet ekosistemi</span><span class="sxs-lookup"><span data-stu-id="0daac-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="0daac-106">Ortak bir konak olarak kendi rolünde merkezi depo 100. 000'den benzersiz paket NuGet.org kendisi tutar [nuget.org](https://www.nuget.org). NuGet.org paketler için yalnızca ana bilgisayar değil.</span><span class="sxs-lookup"><span data-stu-id="0daac-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="0daac-107">NuGet teknoloji Ayrıca, özel olarak bulutta paketlerini barındıracak sağlar (gibi Azure DevOps üzerine), özel bir ağda veya hatta yalnızca yerel dosya sisteminize.</span><span class="sxs-lookup"><span data-stu-id="0daac-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="0daac-108">Bir farklı bir konak ya da barındırma seçeneği ilgileniyorsanız bkz [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0daac-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="0daac-109">NuGet.org, NuGet paketleri için herhangi bir ana bilgisayara gibi hizmet paketi arasında bir bağlantı noktası olarak *creators* ve paket *tüketiciler*.</span><span class="sxs-lookup"><span data-stu-id="0daac-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="0daac-110">Creators yararlı NuGet paketleri oluşturun ve yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="0daac-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="0daac-111">Tüketiciler kullanışlı ve uyumlu paketleri indirme ve bu paketleri, projelere dahil etme erişilebilen konaklarda öğesini arayın.</span><span class="sxs-lookup"><span data-stu-id="0daac-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="0daac-112">Bir projede yüklendikten sonra paketleri API'leri proje kodunu geri kalanı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0daac-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Paket oluşturucuları, paket konaklar ve paketi tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="0daac-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="0daac-114">Accounts</span></span>

<span data-ttu-id="0daac-115">Paketleri NuGet.org üzerinde yayımlamak için önce oluşturduğunuz bir [tek (kullanıcı) hesabı](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0daac-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="0daac-116">Bu, kimliğinizi nuget.org olur.</span><span class="sxs-lookup"><span data-stu-id="0daac-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="0daac-117">NuGet.org ayrıca oluşturmanıza imkan tanır bir [kuruluş hesabı](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="0daac-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="0daac-118">Bir kuruluş hesabı, bir veya daha fazla bireysel hesaplar, üyelere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0daac-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="0daac-119">Üyeleri paketleri bir dizi sahipliği için tek bir kimlik korurken yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="0daac-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="0daac-120">Kişisel hesabınıza kuruluşların herhangi bir sayıda üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="0daac-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="0daac-121">Bir paketi tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="0daac-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="0daac-122">Paketi tüketicileri bir bireysel hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.</span><span class="sxs-lookup"><span data-stu-id="0daac-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="0daac-123">API anahtarları</span><span class="sxs-lookup"><span data-stu-id="0daac-123">API keys</span></span>

<span data-ttu-id="0daac-124">Bir NuGet paketini aldıktan sonra ( *.nupkg* dosya) yayımlamak için nuget.org'da nuget.exe CLI veya dotnet.exe CLI ile birlikte kullanarak yayımladığınız bir [API anahtarı](scoped-api-keys.md) NuGet.org adresinden alınan.</span><span class="sxs-lookup"><span data-stu-id="0daac-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="0daac-125">Olduğunda, [paket yayımlama](../create-packages/creating-a-package.md), CLI komutu API anahtar değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="0daac-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="0daac-126">Kimlik ön ekleri</span><span class="sxs-lookup"><span data-stu-id="0daac-126">ID prefixes</span></span>

<span data-ttu-id="0daac-127">Paketleri yayımladığınızda, ayırabilir ve tarafından kimliğinizi korumak [kimliği ön ekleri ayırma](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="0daac-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="0daac-128">Bir paketi yüklerken paketi tüketicileri tüketen paket tanımlayıcı özelliklerini aldatıcı olmadığını belirten ek bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0daac-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="0daac-129">NuGet.org için API uç noktası</span><span class="sxs-lookup"><span data-stu-id="0daac-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="0daac-130">NuGet.org bir paket deposu NuGet istemcileri ile kullanmak için aşağıdaki V3 API uç noktası kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0daac-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="0daac-131">Eski istemciler V2 Protokolü NuGet.org ulaşmak için kullanmaya devam edebilirsiniz. Ancak, lütfen unutmayın, NuGet 3.0 veya üstü istemcilerin daha yavaş ve V2 protokolünü kullanarak güvenilir hizmet daha az olacaktır:</span><span class="sxs-lookup"><span data-stu-id="0daac-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="0daac-132">`https://www.nuget.org/api/v2` (**V2 iletişim kuralı kullanım dışı!** )</span><span class="sxs-lookup"><span data-stu-id="0daac-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
