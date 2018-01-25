---
title: "NuGet 2.8.1 ile sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.1 ile dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.1 ile sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="2c2bf-104">NuGet 2.8.1 ile sürüm notları</span><span class="sxs-lookup"><span data-stu-id="2c2bf-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="2c2bf-105">[NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 sürüm notları](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="2c2bf-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="2c2bf-106">NuGet 2.8.1 ile 2 Nisan 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="2c2bf-107">Sürümdeki dikkat çekici özellikleri</span><span class="sxs-lookup"><span data-stu-id="2c2bf-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="2c2bf-108">Windows Phone 8.1 projeleri için desteği</span><span class="sxs-lookup"><span data-stu-id="2c2bf-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="2c2bf-109">Bu sürümde artık hedef Windows Phone 8.1 projeleri için kullanılabilen aşağıdaki yeni hedef framework adlar destekler:</span><span class="sxs-lookup"><span data-stu-id="2c2bf-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="2c2bf-110">WindowsPhone81 / WP81 (Windows Phone Silverlight tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="2c2bf-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="2c2bf-111">WindowsPhoneApp81 / WPA81 (Windows Phone Uygulama WinRT tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="2c2bf-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="2c2bf-112">NuGet WebMatrix uzantısının güncelleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="2c2bf-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="2c2bf-113">Bu sürüm için WebMatrix bulunan NuGet istemcisi güncelleştirmelerini [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 ve getirir ile XDT dönüşümleri gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="2c2bf-114">Daha da önemlisi, 2.6.1 çekirdek güncelleştirme sağlar, daha yeni sürümlerinde içeren NuGet paketlerini yüklemek WebMatrix istemci `.nuspec` şeması, ASP.NET NuGet paketlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="2c2bf-115">WebMatrix genişletmesi güncelleştirme hakkında daha fazla bilgi için belirli bir olanlar bkz [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="2c2bf-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="2c2bf-116">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="2c2bf-116">Bug Fixes</span></span>
<span data-ttu-id="2c2bf-117">Bu özelliklerine ek olarak, bu sürümü NuGet, diğer hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="2c2bf-118">Sürümde ele 16 toplam sorunları vardı.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="2c2bf-119">Tam bir listesi için iş öğeleri NuGet 2.8.1 ile Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="2c2bf-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="2c2bf-120">Visual Studio ile "14" CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="2c2bf-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="2c2bf-121">3 Haziran 2014'te yayımlanan Visual Studio "14" TEM'de, kutusuna NuGet 2.8.1 ile birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="2c2bf-122">Destekleyen özellikler nominal kalır diğer 2.8.1 ile birlikte bir Visual Studio 2013 gibi VSIXes.</span><span class="sxs-lookup"><span data-stu-id="2c2bf-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
