---
title: 2.8.5 NuGet sürüm notları
description: NuGet 2.8.5 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548631"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="162f6-103">2.8.5 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="162f6-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="162f6-104">[NuGet 2.8.3 sürüm notlarına](../release-notes/nuget-2.8.3.md) | [2.8.6 NuGet sürüm notları](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="162f6-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="162f6-105">NuGet 2.8.5, 30 Mart 2015 kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="162f6-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="162f6-106">Küçük bir güncelleştirmesidir bizim 2.8.3 için VSIX bazı düzeltmeleri hedeflenen.</span><span class="sxs-lookup"><span data-stu-id="162f6-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="162f6-107">NuGet Paket Yöneticisi iletişim kutusu için destek eklendi bu sürümde, [DNX hedef çerçeve bilinen adlar](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="162f6-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="162f6-108">Desteklenen bu yeni framework takma adlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="162f6-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="162f6-109">**core50** - A 'base' hedef çerçeve adı (TFM) Core CLR ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="162f6-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="162f6-110">**dnx452** - tam 4.5.2 kullanarak bir TFM belirli DNX tabanlı uygulamaları framework sürümü</span><span class="sxs-lookup"><span data-stu-id="162f6-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="162f6-111">**dnx46** - framework'ün tam 4.6 sürümünü kullanarak bir TFM DNX tabanlı özel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="162f6-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="162f6-112">**dnxcore50** - framework Core 5.0 sürümü kullanarak bir TFM DNX tabanlı özel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="162f6-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="162f6-113">Bir hatanın düzeltilip FSharp projelere düzgün bir şekilde yüklenmesini önlenmiş bu paketleri:</span><span class="sxs-lookup"><span data-stu-id="162f6-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400