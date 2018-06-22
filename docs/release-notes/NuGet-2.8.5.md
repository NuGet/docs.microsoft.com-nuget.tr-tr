---
title: NuGet 2.8.5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.5 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820085"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="6078f-103">NuGet 2.8.5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6078f-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="6078f-104">[NuGet 2.8.3 Sürüm Notları](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 sürüm notları](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="6078f-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="6078f-105">NuGet 2.8.5, 30 Mart 2015 yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6078f-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="6078f-106">Küçük bir güncelleştirmesidir bizim 2.8.3 VSIX bazı düzeltmeler hedeflenen.</span><span class="sxs-lookup"><span data-stu-id="6078f-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="6078f-107">Bu sürümde için NuGet Paket Yöneticisi iletişim için destek eklenmiştir [DNX hedef Framework adlar](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="6078f-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="6078f-108">Desteklenen bu yeni framework adları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6078f-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="6078f-109">**core50** - A 'base' hedef framework ad (TFM) çekirdek CLR ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="6078f-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="6078f-110">**dnx452** - tam 4.5.2 kullanarak A TFM DNX tabanlı belirli uygulamaları framework sürümü</span><span class="sxs-lookup"><span data-stu-id="6078f-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="6078f-111">**dnx46** - framework'ün tam 4.6 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6078f-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="6078f-112">**dnxcore50** - framework çekirdek 5.0 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6078f-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="6078f-113">Bir hata FSharp projelere düzgün şekilde yüklenmesini önlenmiş bu paketleri düzeltildi:</span><span class="sxs-lookup"><span data-stu-id="6078f-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400