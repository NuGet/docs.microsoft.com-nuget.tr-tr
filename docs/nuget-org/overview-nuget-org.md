---
title: NuGet.org’a genel bakış
description: NuGet.org’a genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901882"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="a284e-103">NuGet.org’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a284e-103">Overview of NuGet.org</span></span>

<span data-ttu-id="a284e-104">NuGet.org, her gün milyonlarca .NET ve .NET Core geliştiricisi tarafından çalıştırılan NuGet paketlerinin ortak bir ana konağından oluşur.</span><span class="sxs-lookup"><span data-stu-id="a284e-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="a284e-105">NuGet ekosistemindeki NuGet.org rolü</span><span class="sxs-lookup"><span data-stu-id="a284e-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="a284e-106">Ortak ana bilgisayar olarak rolünde, NuGet.org, [NuGet.org](https://www.nuget.org)adresinden 100.000 benzersiz paketin üzerinden merkezi depoyu saklar. NuGet.org, paketler için mümkün olan tek konak değildir.</span><span class="sxs-lookup"><span data-stu-id="a284e-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="a284e-107">NuGet teknolojisi Ayrıca, paketleri bulutta (Azure DevOps gibi), özel bir ağda veya hatta yalnızca yerel dosya sisteminizde barındırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a284e-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="a284e-108">Farklı bir konak veya barındırma seçeneği ile ilgileniyorsanız, bkz. [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a284e-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="a284e-109">NuGet paketleri için herhangi bir konak gibi NuGet.org, paket *oluşturucular* ve paket *tüketicileri* arasındaki bağlantı noktası olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="a284e-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="a284e-110">Creators Build yararlı NuGet paketleri ve bunları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="a284e-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="a284e-111">Müşteriler daha sonra, bu paketleri projelerinde, indirerek ve dahil olmak üzere erişilebilir konaklarda kullanışlı ve uyumlu paketler arar.</span><span class="sxs-lookup"><span data-stu-id="a284e-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="a284e-112">Bir projeye yüklendikten sonra paketlerin API 'Leri proje kodunun geri kalanı tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a284e-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Paket oluşturucular, paket konakları ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="a284e-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="a284e-114">Accounts</span></span>

<span data-ttu-id="a284e-115">Paketleri NuGet.org üzerinde yayımlamak için önce bir [bireysel (Kullanıcı) hesabı](individual-accounts.md)oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a284e-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="a284e-116">Bu, NuGet.org adresindeki kimliğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="a284e-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="a284e-117">NuGet.org Ayrıca, bir [kuruluş hesabı](organizations-on-nuget-org.md)oluşturmanıza de olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a284e-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="a284e-118">Bir kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="a284e-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="a284e-119">Üyeler, sahiplik için tek bir kimliği koruyarak bir paket kümesini yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="a284e-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="a284e-120">Bireysel hesabınız sayesinde, herhangi bir sayıda kuruluşun üyesi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a284e-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="a284e-121">Bir paket, tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="a284e-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="a284e-122">Paket tüketicileri, tek bir hesap veya kuruluş hesabı arasında herhangi bir farklılık görmez: her ikisi de paket olarak görünürler `owners` .</span><span class="sxs-lookup"><span data-stu-id="a284e-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="a284e-123">API anahtarları</span><span class="sxs-lookup"><span data-stu-id="a284e-123">API keys</span></span>

<span data-ttu-id="a284e-124">Yayımlamak üzere bir NuGet paketine (*. nupkg* dosyası) sahip olduktan sonra, NuGet.org ' den elde edilen bir [API anahtarı](scoped-api-keys.md) ile birlikte nuget.exe CLI veya dotnet.exe CLI kullanarak bunu NuGet.org olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a284e-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="a284e-125">[Bir paket yayımladığınızda](../create-packages/creating-a-package.md), CLı komutuna API anahtarı değerini dahil edersiniz.</span><span class="sxs-lookup"><span data-stu-id="a284e-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="a284e-126">KIMLIK önekleri</span><span class="sxs-lookup"><span data-stu-id="a284e-126">ID prefixes</span></span>

<span data-ttu-id="a284e-127">Paketleri yayımladığınızda kimlik [öneklerini](id-prefix-reservation.md)ayırarak kimliğinizi ayırabilir ve koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a284e-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="a284e-128">Paket yüklerken, paket tüketicileri, kullandıkları paketin kendi tanımlama özelliklerinde yanıltıcı olmadığını belirten ek bilgilerle sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a284e-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="a284e-129">NuGet.org için API uç noktası</span><span class="sxs-lookup"><span data-stu-id="a284e-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="a284e-130">NuGet.org 'i NuGet istemcilerinde bir paket deposu olarak kullanmak için aşağıdaki v3 API uç noktasını kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a284e-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="a284e-131">Daha eski istemciler NuGet.org ulaşmak için v2 protokolünü kullanmaya devam edebilir. Ancak, bkz. NuGet istemcileri 3,0 veya üzeri, v2 protokolünü kullanarak daha yavaş ve daha az güvenilir hizmete sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="a284e-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="a284e-132">`https://www.nuget.org/api/v2` (**V2 Protokolü kullanım dışıdır!**)</span><span class="sxs-lookup"><span data-stu-id="a284e-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
