---
title: NuGet 2.8.1 ile sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.1 ile dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="5a214-103">NuGet 2.8.1 ile sürüm notları</span><span class="sxs-lookup"><span data-stu-id="5a214-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="5a214-104">[NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 sürüm notları](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="5a214-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="5a214-105">NuGet 2.8.1 ile 2 Nisan 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5a214-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="5a214-106">Sürümdeki dikkat çekici özellikleri</span><span class="sxs-lookup"><span data-stu-id="5a214-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="5a214-107">Windows Phone 8.1 projeleri için desteği</span><span class="sxs-lookup"><span data-stu-id="5a214-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="5a214-108">Bu sürümde artık hedef Windows Phone 8.1 projeleri için kullanılabilen aşağıdaki yeni hedef framework adlar destekler:</span><span class="sxs-lookup"><span data-stu-id="5a214-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="5a214-109">WindowsPhone81 / WP81 (Windows Phone Silverlight tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="5a214-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="5a214-110">WindowsPhoneApp81 / WPA81 (Windows Phone Uygulama WinRT tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="5a214-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="5a214-111">NuGet WebMatrix uzantısının güncelleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="5a214-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="5a214-112">Bu sürüm için WebMatrix bulunan NuGet istemcisi güncelleştirmelerini [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 ve getirir ile XDT dönüşümleri gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="5a214-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="5a214-113">Daha da önemlisi, 2.6.1 çekirdek güncelleştirme sağlar, daha yeni sürümlerinde içeren NuGet paketlerini yüklemek WebMatrix istemci `.nuspec` şeması, ASP.NET NuGet paketlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="5a214-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="5a214-114">WebMatrix genişletmesi güncelleştirme hakkında daha fazla bilgi için belirli bir olanlar bkz [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="5a214-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="5a214-115">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="5a214-115">Bug Fixes</span></span>
<span data-ttu-id="5a214-116">Bu özelliklerine ek olarak, bu sürümü NuGet, diğer hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5a214-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="5a214-117">Sürümde ele 16 toplam sorunları vardı.</span><span class="sxs-lookup"><span data-stu-id="5a214-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="5a214-118">Tam bir listesi için iş öğeleri NuGet 2.8.1 ile Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="5a214-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="5a214-119">Visual Studio ile "14" CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="5a214-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="5a214-120">3 Haziran 2014'te yayımlanan Visual Studio "14" TEM'de, kutusuna NuGet 2.8.1 ile birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5a214-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="5a214-121">Destekleyen özellikler nominal kalır diğer 2.8.1 ile birlikte bir Visual Studio 2013 gibi VSIXes.</span><span class="sxs-lookup"><span data-stu-id="5a214-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
