---
title: NuGet 2.8.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776767"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="30dcc-103">NuGet 2.8.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="30dcc-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="30dcc-104">[NuGet 2,8 sürüm notları](../release-notes/nuget-2.8.md)  |  [NuGet 2.8.2 sürüm notları](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="30dcc-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="30dcc-105">NuGet 2.8.1, 2 Nisan 2014 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="30dcc-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="30dcc-106">Yayındaki önemli özellikler</span><span class="sxs-lookup"><span data-stu-id="30dcc-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="30dcc-107">Windows Phone 8,1 projeleri için destek</span><span class="sxs-lookup"><span data-stu-id="30dcc-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="30dcc-108">Bu sürüm artık Windows Phone 8,1 projelerini hedeflemek için kullanılabilecek aşağıdaki yeni hedef çerçeve bilinen adlarını desteklemektedir:</span><span class="sxs-lookup"><span data-stu-id="30dcc-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="30dcc-109">WindowsPhone81/WP81 (Silverlight tabanlı Windows Phone projeleri için)</span><span class="sxs-lookup"><span data-stu-id="30dcc-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="30dcc-110">WindowsPhoneApp81/WPA81 (WinRT tabanlı Windows Phone uygulama projeleri için)</span><span class="sxs-lookup"><span data-stu-id="30dcc-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="30dcc-111">NuGet WebMatrix uzantısının güncelleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="30dcc-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="30dcc-112">Bu sürüm WebMatrix 'te bulunan NuGet istemcisini [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 olarak güncelleştirir ve xdt dönüştürmeleri gibi BT özellikleriyle birlikte getirir.</span><span class="sxs-lookup"><span data-stu-id="30dcc-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="30dcc-113">Daha da önemlisi, 2.6.1 Core Update, WebMatrix istemcisinin, `.nuspec` ASP.net NuGet paketlerini içeren, şemanın daha yeni sürümlerini Içeren NuGet paketlerini yüklemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="30dcc-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="30dcc-114">WebMatrix uzantısı güncelleştirmesi hakkında daha fazla bilgi için, bkz. ilgili [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="30dcc-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="30dcc-115">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="30dcc-115">Bug Fixes</span></span>
<span data-ttu-id="30dcc-116">Bu özelliklere ek olarak, NuGet 'in bu sürümü diğer hata düzeltmelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="30dcc-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="30dcc-117">Yayında oluşan 16 Toplam sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="30dcc-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="30dcc-118">NuGet 2.8.1 'te düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="30dcc-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="30dcc-119">Visual Studio "14" CTP ile reshipping</span><span class="sxs-lookup"><span data-stu-id="30dcc-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="30dcc-120">Visual Studio "14" CTP 'de 3 Haziran 2014 ' de yayınlanan NuGet 2.8.1, kutuya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="30dcc-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="30dcc-121">Desteklediği özellikler, Visual Studio 2013 için bir diğeri gibi diğer 2.8.1 sanal parçalar ile eşit olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="30dcc-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
