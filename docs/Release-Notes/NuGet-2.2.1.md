---
title: "NuGet 2.2.1 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.2.1 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.2.1 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="8eebc-104">NuGet 2.2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="8eebc-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="8eebc-105">[NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md) | [NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="8eebc-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="8eebc-106">NuGet 2.2.1 15 Şubat 2013'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8eebc-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="8eebc-107">VS uzantısı sürüm 2.2.40116.9051 sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="8eebc-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="8eebc-108">Yerelleştirme yenileme</span><span class="sxs-lookup"><span data-stu-id="8eebc-108">Localization Refresh</span></span>
<span data-ttu-id="8eebc-109">NuGet Visual Studio 2012 bir parçası olarak gönderilir, bunu tamamen yerelleştirilmiş İngilizce + 13 diğer diller.</span><span class="sxs-lookup"><span data-stu-id="8eebc-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="8eebc-110">O tarihten sonra NuGet 2.1 ve 2.2 gönderilen ancak yerelleştirme değil yenilenir.</span><span class="sxs-lookup"><span data-stu-id="8eebc-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="8eebc-111">NuGet 2.2.1 sürüm bizim yerelleştirme yeniler.</span><span class="sxs-lookup"><span data-stu-id="8eebc-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="8eebc-112">NuGet'ın kullanıcı Arabirimi ve PowerShell konsolunda aşağıdaki dillere yerelleştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8eebc-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="8eebc-113">ve</span><span class="sxs-lookup"><span data-stu-id="8eebc-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="8eebc-114">seçenekleri yerine</span><span class="sxs-lookup"><span data-stu-id="8eebc-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="8eebc-115">Çekçe</span><span class="sxs-lookup"><span data-stu-id="8eebc-115">Czech</span></span>
1. <span data-ttu-id="8eebc-116">İngilizce</span><span class="sxs-lookup"><span data-stu-id="8eebc-116">English</span></span>
1. <span data-ttu-id="8eebc-117">Fransızca</span><span class="sxs-lookup"><span data-stu-id="8eebc-117">French</span></span>
1. <span data-ttu-id="8eebc-118">Almanca</span><span class="sxs-lookup"><span data-stu-id="8eebc-118">German</span></span>
1. <span data-ttu-id="8eebc-119">İtalyanca</span><span class="sxs-lookup"><span data-stu-id="8eebc-119">Italian</span></span>
1. <span data-ttu-id="8eebc-120">Japonca</span><span class="sxs-lookup"><span data-stu-id="8eebc-120">Japanese</span></span>
1. <span data-ttu-id="8eebc-121">Kore Dili</span><span class="sxs-lookup"><span data-stu-id="8eebc-121">Korean</span></span>
1. <span data-ttu-id="8eebc-122">Lehçe</span><span class="sxs-lookup"><span data-stu-id="8eebc-122">Polish</span></span>
1. <span data-ttu-id="8eebc-123">Portekizce (Brezilya)</span><span class="sxs-lookup"><span data-stu-id="8eebc-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="8eebc-124">Rusça</span><span class="sxs-lookup"><span data-stu-id="8eebc-124">Russian</span></span>
1. <span data-ttu-id="8eebc-125">İspanyolca</span><span class="sxs-lookup"><span data-stu-id="8eebc-125">Spanish</span></span>
1. <span data-ttu-id="8eebc-126">Türkçe</span><span class="sxs-lookup"><span data-stu-id="8eebc-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="8eebc-127">Visual Studio şablonları birden çok önceden yüklenmiş paket depoları desteği</span><span class="sxs-lookup"><span data-stu-id="8eebc-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="8eebc-128">Visual Studio şablonları oluşturmak, için NuGet kullanabilirsiniz [önceden paketleri](../visual-studio-extensibility/visual-studio-templates.md) şablonunun parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="8eebc-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="8eebc-129">Şimdiye kadar bu özellik bir sınırlama sahip tüm paketler aynı kaynaktan geldiği gerekiyordu.</span><span class="sxs-lookup"><span data-stu-id="8eebc-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="8eebc-130">2.2.1 NuGet ile yine de (içinde şablonu, bir VSIX veya kayıt defterinde tanımlanan diskteki bir klasöre) birden çok depoları yüklenen paketler olabilir.</span><span class="sxs-lookup"><span data-stu-id="8eebc-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="8eebc-131">Bu özellik için ana senaryo özel ASP.NET proje şablonları ' dir.</span><span class="sxs-lookup"><span data-stu-id="8eebc-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="8eebc-132">Yerel disk paketlerinden çekme önceden yüklenen paketler yerleşik ASP.NET şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="8eebc-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="8eebc-133">Şimdi, ASP.NET tarafından yüklenen var olan paketler kullanan bir özel ASP.NET proje şablonu oluşturma ancak şablonunuza fazladan NuGet paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8eebc-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="8eebc-134">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8eebc-134">Bug Fixes</span></span>
<span data-ttu-id="8eebc-135">NuGet 2.2.1 birkaç hedeflenen hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8eebc-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="8eebc-136">İş listesi için öğeleri NuGet 2.2.1, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="8eebc-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="8eebc-137">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="8eebc-137">Known Issues</span></span>

<span data-ttu-id="8eebc-138">ASP.NET proje şablonları genişletme, tüm önceden yüklenmiş paket depoları için aynı değeri kullanmalısınız `isPreunzipped` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="8eebc-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
