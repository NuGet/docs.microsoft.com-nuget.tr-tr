---
title: 2.8.1 NuGet sürüm notları
description: NuGet 2.8.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545245"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="b716e-103">2.8.1 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b716e-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="b716e-104">[NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md) | [2.8.2 NuGet sürüm notları](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="b716e-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="b716e-105">NuGet 2.8.1 2 Nisan 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b716e-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="b716e-106">Sürümündeki önemli özelliklere</span><span class="sxs-lookup"><span data-stu-id="b716e-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="b716e-107">Windows Phone 8.1 projeleri için destek</span><span class="sxs-lookup"><span data-stu-id="b716e-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="b716e-108">Bu sürüm, artık hedef Windows Phone 8.1 projeleri için kullanılabilen aşağıdaki yeni hedef çerçeve bilinen adlar destekler:</span><span class="sxs-lookup"><span data-stu-id="b716e-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="b716e-109">WindowsPhone81 / WP81 (Windows Phone Silverlight tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="b716e-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="b716e-110">WindowsPhoneApp81 / WPA81 (Windows Phone Uygulama WinRT tabanlı projelerde)</span><span class="sxs-lookup"><span data-stu-id="b716e-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="b716e-111">NuGet WebMatrix genişletmesi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b716e-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="b716e-112">Bu sürüm için WebMatrix bulunan NuGet istemcisi güncelleştirmelerini [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 ve getirir ile XDT dönüşümleri gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b716e-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="b716e-113">2.6.1 daha da önemlisi, çekirdek güncelleştirme sağlar, daha yeni sürümlerini içeren NuGet paketlerini yüklemek WebMatrix istemci `.nuspec` ASP.NET NuGet paketlerini içeren şema.</span><span class="sxs-lookup"><span data-stu-id="b716e-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="b716e-114">WebMatrix genişletmesi güncelleştirme hakkında daha fazla bilgi için bu belirli bkz [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="b716e-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="b716e-115">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="b716e-115">Bug Fixes</span></span>
<span data-ttu-id="b716e-116">Bu özelliklerin yanı sıra, bu sürüm nuget diğer hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b716e-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="b716e-117">Sürümünde giderilen 16 toplam sorunlar oluştu.</span><span class="sxs-lookup"><span data-stu-id="b716e-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="b716e-118">Tam bir listesi için iş öğeleri Nuget'te 2.8.1, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="b716e-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="b716e-119">Visual Studio "14" CTP reshipping</span><span class="sxs-lookup"><span data-stu-id="b716e-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="b716e-120">3 Haziran 2014'te yayımlanan Visual Studio "14" CTP içinde NuGet 2.8.1 kutuya sevk edilir.</span><span class="sxs-lookup"><span data-stu-id="b716e-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="b716e-121">Par destekleyen özellikler kalan diğer 2.8.1 ile VSIXes gibi Visual Studio 2013 için.</span><span class="sxs-lookup"><span data-stu-id="b716e-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
