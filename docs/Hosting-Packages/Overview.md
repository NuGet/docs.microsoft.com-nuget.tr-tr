---
title: "Kendi NuGet barındırma genel bakış akışları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "Yerel olarak veya uzaktan kendi NuGet paketi akışlarını veya galerileri barındırmak için açılır genel bakış."
keywords: "Akış, NuGet NuGet galerisinde, akış, özel pakette NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="92203-104">Kendi NuGet barındırma akışları</span><span class="sxs-lookup"><span data-stu-id="92203-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="92203-105">Paketleri genel olarak kullanılabilir hale getirme yerine, yalnızca bir sınırlı kitleye, kuruluşunuz ya da çalışma grubu gibi paketleri yayın isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92203-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="92203-106">Ayrıca, bazı şirketler kendi geliştiriciler kullanın ve bu nedenle bir sınırlı paket kaynağı nuget.org yerine çizmek için bu geliştiriciler doğrudan hangi üçüncü taraf kitaplıklar sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92203-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="92203-107">Bu tür amacıyla, NuGet aşağıdaki yollarla özel paket kaynaklarını ayarlama destekler:</span><span class="sxs-lookup"><span data-stu-id="92203-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="92203-108">Yerel akışı: paketler yalnızca yerleştirilir uygun ağ dosya paylaşımında ideal olarak kullanarak `nuget init` ve `nuget add` hiyerarşik bir klasör yapısı (NuGet 3.3 +) oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="92203-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="92203-109">Ayrıntılar için bkz [yerel akışları](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="92203-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="92203-110">NuGet.Server: Paketleri yerel bir HTTP sunucu üzerinden kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="92203-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="92203-111">Ayrıntılar için bkz [NuGet.Server](../hosting-packages/NuGet-Server.md).</span><span class="sxs-lookup"><span data-stu-id="92203-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="92203-112">NuGet galerisinde: Bir sunucu kullanarak Internet üzerindeki paketler barındırılan [NuGet Galerisi projesi](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com'u).</span><span class="sxs-lookup"><span data-stu-id="92203-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="92203-113">NuGet galerisinde, kullanıcı yönetimi ve kapsamlı bir web arama ve paketlerinden nuget.org için benzer tarayıcısından keşfetme veren UI gibi özellikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="92203-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="92203-114">Ayrıca, aşağıdakiler de dahil olmak üzere uzaktan özel akışları destekleyen ürünleri barındırma birkaç NuGet vardır:</span><span class="sxs-lookup"><span data-stu-id="92203-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="92203-115">[Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), olduğu da Team Foundation Server 2017 kullanılabilir ve sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="92203-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="92203-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="92203-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="92203-117">[ProGet](http://inedo.com/proget) Inedo gelen</span><span class="sxs-lookup"><span data-stu-id="92203-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="92203-118">[NuGet sunucu](http://nugetserver.net/), Inedo topluluk projeden</span><span class="sxs-lookup"><span data-stu-id="92203-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="92203-119">[NuGet sunucu (kaynak açın)](http://nuget-server.net), Inedo'nın NuGet sunucuya benzer bir açık kaynak uygulaması</span><span class="sxs-lookup"><span data-stu-id="92203-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="92203-120">[Artifactory](https://www.jfrog.com/artifactory/) JFrog gelen.</span><span class="sxs-lookup"><span data-stu-id="92203-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="92203-121">[Nexus](http://www.sonatype.org/nexus/) Sonatype gelen.</span><span class="sxs-lookup"><span data-stu-id="92203-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="92203-122">[TeamCity](https://www.jetbrains.com/teamcity/) JetBrains gelen.</span><span class="sxs-lookup"><span data-stu-id="92203-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="92203-123">Paketleri nasıl barındırılan bağımsız olarak, kullanılabilir kaynakları listesine ekleyerek erişmesine `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="92203-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="92203-124">Bu Visual Studio'da açıklandığı gibi yapılabilir [paket kaynaklarını](../tools/package-manager-ui.md#package-sources), veya kullanarak komut satırından [ `nuget sources` ](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="92203-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="92203-125">Bir kaynak yolu, bir yerel klasör yol, bir ağ adı veya bir URL olabilir.</span><span class="sxs-lookup"><span data-stu-id="92203-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
