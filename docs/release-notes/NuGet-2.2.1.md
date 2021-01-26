---
title: NuGet 2.2.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.2.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776812"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="9e506-103">NuGet 2.2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9e506-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="9e506-104">[NuGet 2,2 sürüm notları](../release-notes/nuget-2.2.md)  |  [NuGet 2,5 sürüm notları](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="9e506-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="9e506-105">NuGet 2.2.1 15 Şubat 2013 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9e506-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="9e506-106">VS uzantısı sürüm numarası 2.2.40116.9051 ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e506-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="9e506-107">Yerelleştirme yenilemesi</span><span class="sxs-lookup"><span data-stu-id="9e506-107">Localization Refresh</span></span>
<span data-ttu-id="9e506-108">NuGet, Visual Studio 2012 ' in bir parçası olarak sevk edildiğinde, Ingilizce + 13 diğer dillere tamamen yerelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="9e506-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="9e506-109">Bu tarihten sonra, NuGet 2,1 ve 2,2 sevk edildi ancak yerelleştirme yenilenmedi.</span><span class="sxs-lookup"><span data-stu-id="9e506-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="9e506-110">NuGet 2.2.1 sürümü yerelleştirmeyi yeniler.</span><span class="sxs-lookup"><span data-stu-id="9e506-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="9e506-111">NuGet 'in Kullanıcı arabirimi ve PowerShell konsolu aşağıdaki dillerde yerelleştirilir:</span><span class="sxs-lookup"><span data-stu-id="9e506-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="9e506-112">Basitleştirilmiş Çince</span><span class="sxs-lookup"><span data-stu-id="9e506-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="9e506-113">Geleneksel Çince</span><span class="sxs-lookup"><span data-stu-id="9e506-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="9e506-114">Çekçe</span><span class="sxs-lookup"><span data-stu-id="9e506-114">Czech</span></span>
1. <span data-ttu-id="9e506-115">İngilizce</span><span class="sxs-lookup"><span data-stu-id="9e506-115">English</span></span>
1. <span data-ttu-id="9e506-116">Fransızca</span><span class="sxs-lookup"><span data-stu-id="9e506-116">French</span></span>
1. <span data-ttu-id="9e506-117">Almanca</span><span class="sxs-lookup"><span data-stu-id="9e506-117">German</span></span>
1. <span data-ttu-id="9e506-118">İtalyanca</span><span class="sxs-lookup"><span data-stu-id="9e506-118">Italian</span></span>
1. <span data-ttu-id="9e506-119">Japonca</span><span class="sxs-lookup"><span data-stu-id="9e506-119">Japanese</span></span>
1. <span data-ttu-id="9e506-120">Korece</span><span class="sxs-lookup"><span data-stu-id="9e506-120">Korean</span></span>
1. <span data-ttu-id="9e506-121">Lehçe</span><span class="sxs-lookup"><span data-stu-id="9e506-121">Polish</span></span>
1. <span data-ttu-id="9e506-122">Portekizce (Brezilya)</span><span class="sxs-lookup"><span data-stu-id="9e506-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="9e506-123">Rusça</span><span class="sxs-lookup"><span data-stu-id="9e506-123">Russian</span></span>
1. <span data-ttu-id="9e506-124">İspanyolca</span><span class="sxs-lookup"><span data-stu-id="9e506-124">Spanish</span></span>
1. <span data-ttu-id="9e506-125">Türkçe</span><span class="sxs-lookup"><span data-stu-id="9e506-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="9e506-126">Visual Studio şablonları birden çok önceden yüklenmiş paket depolarını destekler</span><span class="sxs-lookup"><span data-stu-id="9e506-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="9e506-127">Visual Studio şablonları oluşturursanız, bir şablon parçası olarak [paketleri önceden yüklemek](../visual-studio-extensibility/visual-studio-templates.md) için NuGet kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e506-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="9e506-128">Bu özellik şu anda aynı kaynaktan gelmesi için gereken tüm paketlerin bir sınırlaması içeriyordu.</span><span class="sxs-lookup"><span data-stu-id="9e506-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="9e506-129">NuGet 2.2.1 de, birden çok depodan (şablon, bir VSıX veya kayıt defterinde tanımlanan disk üzerinde bir klasör) paketlerin yüklü olmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e506-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="9e506-130">Bu özelliğin ana senaryosu özel ASP.NET proje şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="9e506-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="9e506-131">Yerleşik ASP.NET şablonları önceden yüklenmiş paketleri kullanarak yerel diskten paket çekmesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e506-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="9e506-132">Artık ASP.NET tarafından yüklenen mevcut paketleri kullanan özel bir ASP.NET proje şablonu oluşturabilir, ancak şablonunuza ek NuGet paketleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e506-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9e506-133">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="9e506-133">Bug Fixes</span></span>
<span data-ttu-id="9e506-134">NuGet 2.2.1, bazı hedeflenen hata düzeltmelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="9e506-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="9e506-135">NuGet 2.2.1 'te düzeltilen iş öğelerinin listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="9e506-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="9e506-136">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="9e506-136">Known Issues</span></span>

<span data-ttu-id="9e506-137">ASP.NET proje şablonlarını uzatıyorsunuz, önceden yüklenmiş tüm paket depolarında öznitelik için aynı değer kullanılmalıdır `isPreunzipped` .</span><span class="sxs-lookup"><span data-stu-id="9e506-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
