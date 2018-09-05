---
title: 2.2.1 NuGet sürüm notları
description: NuGet 2.2.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550704"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="71422-103">2.2.1 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="71422-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="71422-104">[NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md) | [NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="71422-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="71422-105">NuGet 2.2.1 15 Şubat 2013 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="71422-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="71422-106">VS uzantısı sürüm numarasını 2.2.40116.9051 ' dir.</span><span class="sxs-lookup"><span data-stu-id="71422-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="71422-107">Yerelleştirme yenileme</span><span class="sxs-lookup"><span data-stu-id="71422-107">Localization Refresh</span></span>
<span data-ttu-id="71422-108">NuGet, Visual Studio 2012 bir parçası olarak gönderildiğini, tamamen yerelleştirilmiş İngilizce + 13 dilde.</span><span class="sxs-lookup"><span data-stu-id="71422-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="71422-109">O tarihten sonra NuGet 2.1 ve 2.2 gönderildi ancak yerelleştirme değil yenilenir.</span><span class="sxs-lookup"><span data-stu-id="71422-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="71422-110">NuGet 2.2.1 sürüm bizim yerelleştirme yeniler.</span><span class="sxs-lookup"><span data-stu-id="71422-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="71422-111">NuGet'ın kullanıcı Arabirimi ve PowerShell konsolunda aşağıdaki dilde yerelleştirilmiş:</span><span class="sxs-lookup"><span data-stu-id="71422-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="71422-112">ve</span><span class="sxs-lookup"><span data-stu-id="71422-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="71422-113">seçenekleri yerine</span><span class="sxs-lookup"><span data-stu-id="71422-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="71422-114">Çekçe</span><span class="sxs-lookup"><span data-stu-id="71422-114">Czech</span></span>
1. <span data-ttu-id="71422-115">İngilizce</span><span class="sxs-lookup"><span data-stu-id="71422-115">English</span></span>
1. <span data-ttu-id="71422-116">Fransızca</span><span class="sxs-lookup"><span data-stu-id="71422-116">French</span></span>
1. <span data-ttu-id="71422-117">Almanca</span><span class="sxs-lookup"><span data-stu-id="71422-117">German</span></span>
1. <span data-ttu-id="71422-118">İtalyanca</span><span class="sxs-lookup"><span data-stu-id="71422-118">Italian</span></span>
1. <span data-ttu-id="71422-119">Japonca</span><span class="sxs-lookup"><span data-stu-id="71422-119">Japanese</span></span>
1. <span data-ttu-id="71422-120">Kore Dili</span><span class="sxs-lookup"><span data-stu-id="71422-120">Korean</span></span>
1. <span data-ttu-id="71422-121">Lehçe</span><span class="sxs-lookup"><span data-stu-id="71422-121">Polish</span></span>
1. <span data-ttu-id="71422-122">Portekizce (Brezilya)</span><span class="sxs-lookup"><span data-stu-id="71422-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="71422-123">Rusça</span><span class="sxs-lookup"><span data-stu-id="71422-123">Russian</span></span>
1. <span data-ttu-id="71422-124">İspanyolca</span><span class="sxs-lookup"><span data-stu-id="71422-124">Spanish</span></span>
1. <span data-ttu-id="71422-125">Türkçe</span><span class="sxs-lookup"><span data-stu-id="71422-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="71422-126">Visual Studio şablonları birden çok önceden yüklenmiş paket Depolarınızın destekler.</span><span class="sxs-lookup"><span data-stu-id="71422-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="71422-127">Visual Studio şablonları oluşturmak, için NuGet kullanabilirsiniz [önceden paketleri](../visual-studio-extensibility/visual-studio-templates.md) şablonunun bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="71422-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="71422-128">Şimdiye kadar bu özellik bir sınırlama sahip tüm paketler aynı kaynaktan geldiği için gerekli.</span><span class="sxs-lookup"><span data-stu-id="71422-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="71422-129">2.2.1 NuGet ile birden çok depolarından (içinde şablon, bir VSIX veya kayıt defterinde tanımlanan diskte bir klasörü) yüklü paketleri yine de olabilir.</span><span class="sxs-lookup"><span data-stu-id="71422-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="71422-130">Bu özellik için ana senaryo özel ASP.NET proje şablonları ' dir.</span><span class="sxs-lookup"><span data-stu-id="71422-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="71422-131">Önceden yüklenmiş paketler, yerel disk paketlerden çekme yerleşik ASP.NET şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="71422-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="71422-132">Şimdi, ASP.NET tarafından yüklenmiş var olan paketleri kullanan özel bir ASP.NET proje şablonu oluşturma ancak ek NuGet paketlerini şablonunuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71422-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="71422-133">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="71422-133">Bug Fixes</span></span>
<span data-ttu-id="71422-134">NuGet 2.2.1 birkaç hedeflenen hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="71422-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="71422-135">İş listesi için öğeleri Nuget'te 2.2.1, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="71422-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="71422-136">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="71422-136">Known Issues</span></span>

<span data-ttu-id="71422-137">ASP.NET proje şablonları uzatıyoruz. Gerekirse, tüm önceden yüklenmiş paket depolarınızın için aynı değeri kullanmalısınız `isPreunzipped` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="71422-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
