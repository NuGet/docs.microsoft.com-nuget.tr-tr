---
title: NuGet.org’a genel bakış
description: NuGet.org’a genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427523"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="e169b-103">NuGet.org’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="e169b-103">Overview of NuGet.org</span></span>

<span data-ttu-id="e169b-104">NuGet.org, her gün milyonlarca .NET ve .NET Core geliştiricisi tarafından kullanılan NuGet paketlerinin genel ev sahibidir.</span><span class="sxs-lookup"><span data-stu-id="e169b-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="e169b-105">NuGet ekosisteminde NuGet.org rolü</span><span class="sxs-lookup"><span data-stu-id="e169b-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="e169b-106">Bir kamu ev sahibi olarak rolünde, NuGet.org kendisi [nuget.org](https://www.nuget.org)100.000'den fazla benzersiz paketlerin merkezi deposu tutar. NuGet.org paketler için tek olası ana bilgisayar değildir.</span><span class="sxs-lookup"><span data-stu-id="e169b-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="e169b-107">NuGet teknolojisi ayrıca paketleri bulutta (Azure DevOps'lerde gibi) özel olarak, özel bir ağda ve hatta yalnızca yerel dosya sisteminizde barındırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e169b-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="e169b-108">Farklı bir ev sahibi veya barındırma seçeneğiyle ilgileniyorsanız, [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md)ya da barındırma bakın.</span><span class="sxs-lookup"><span data-stu-id="e169b-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="e169b-109">NuGet.org, NuGet paketleri için herhangi bir ana bilgisayar gibi, paket *yaratıcıları* ve paket *tüketiciler*arasında bağlantı noktası olarak hizmet vermektedir.</span><span class="sxs-lookup"><span data-stu-id="e169b-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="e169b-110">İçerik oluşturucular yararlı NuGet paketleri oluşturur ve bunları yayımlar.</span><span class="sxs-lookup"><span data-stu-id="e169b-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="e169b-111">Tüketiciler daha sonra erişilebilir ana bilgisayarlarda, bu paketleri indirirken ve projelerine dahil ederek kullanışlı ve uyumlu paketleri ararlar.</span><span class="sxs-lookup"><span data-stu-id="e169b-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="e169b-112">Bir projeye yüklendikten sonra, paketlerin API'leri proje kodunun geri kalanı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e169b-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Paket oluşturucular, paket ana bilgisayarlar ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="e169b-114">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="e169b-114">Accounts</span></span>

<span data-ttu-id="e169b-115">Paketleri NuGet.org yayınlamak için önce [bir bireysel (kullanıcı) hesabı](individual-accounts.md)oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e169b-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="e169b-116">Bu NuGet.org üzerinde kimliğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="e169b-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="e169b-117">NuGet.org ayrıca bir [kuruluş hesabı](organizations-on-nuget-org.md)oluşturmanıza da olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e169b-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="e169b-118">Kuruluş hesabının üyeleri olarak bir veya daha fazla ayrı hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="e169b-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="e169b-119">Üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="e169b-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="e169b-120">Bireysel hesabınız aracılığıyla, herhangi bir sayıda kuruluşun üyesi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e169b-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="e169b-121">Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="e169b-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="e169b-122">Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="e169b-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="e169b-123">API anahtarları</span><span class="sxs-lookup"><span data-stu-id="e169b-123">API keys</span></span>

<span data-ttu-id="e169b-124">Bir kez bir NuGet paketi *(.nupkg* dosyası) yayınlamak için, NuGet.org edinilen bir [API anahtarı](scoped-api-keys.md) ile birlikte nuget.exe CLI veya dotnet.exe CLI kullanarak NuGet.org yayımlamak.</span><span class="sxs-lookup"><span data-stu-id="e169b-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="e169b-125">Bir [paket yayımladığınızda,](../create-packages/creating-a-package.md)CLI komutuna API anahtar değerini eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="e169b-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="e169b-126">Kimlik önekleri</span><span class="sxs-lookup"><span data-stu-id="e169b-126">ID prefixes</span></span>

<span data-ttu-id="e169b-127">Paketleri yayımladığınızda, [kimlik önekleri ayırarak](id-prefix-reservation.md)kimliğinizi rezerve edebilir ve koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e169b-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="e169b-128">Paket yüklerken, paket tüketicilerine tükettikleri paketin tanımlayıcı özelliklerinde aldatıcı olmadığını belirten ek bilgiler verilir.</span><span class="sxs-lookup"><span data-stu-id="e169b-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="e169b-129">NuGet.org için API bitiş noktası</span><span class="sxs-lookup"><span data-stu-id="e169b-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="e169b-130">NuGet.org NuGet istemcileriyle paket deposu olarak kullanmak için aşağıdaki V3 API bitiş noktasını kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e169b-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="e169b-131">Eski istemciler hala NuGet.org ulaşmak için V2 protokolünü kullanabilirsiniz. Ancak, lütfen unutmayın, NuGet istemcileri 3.0 veya daha sonra V2 protokolü kullanarak daha yavaş ve daha az güvenilir hizmet olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e169b-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="e169b-132">`https://www.nuget.org/api/v2`(**V2 prototcol azat edilir!**)</span><span class="sxs-lookup"><span data-stu-id="e169b-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
