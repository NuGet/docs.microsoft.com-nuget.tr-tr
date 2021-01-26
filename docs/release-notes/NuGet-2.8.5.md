---
title: NuGet 2.8.5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.5 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780356"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="76dec-103">NuGet 2.8.5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="76dec-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="76dec-104">[NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)  |  [NuGet 2.8.6 sürüm notları](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="76dec-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="76dec-105">NuGet 2.8.5 30 Mart 2015 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="76dec-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="76dec-106">2.8.3 VSıX 'in bazı hedeflenen düzeltmeleri içeren küçük bir güncelleştirmedir.</span><span class="sxs-lookup"><span data-stu-id="76dec-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="76dec-107">Bu sürümde, [DNX hedef çerçeve adları](https://github.com/aspnet/dnx)Için NuGet paket yöneticisi desteği iletişim kutusu eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="76dec-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="76dec-108">Desteklenen bu yeni çerçeve bilinen adları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="76dec-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="76dec-109">**core50** -çekirdek clr ile uyumlu bir ' Base ' hedef çerçeve bilinen adı (tfd).</span><span class="sxs-lookup"><span data-stu-id="76dec-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="76dec-110">**dnx452** -Framework 'ün tam 4.5.2 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd</span><span class="sxs-lookup"><span data-stu-id="76dec-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="76dec-111">**dnx46** -Framework 'ün tam 4,6 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd</span><span class="sxs-lookup"><span data-stu-id="76dec-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="76dec-112">**adlar** -Framework 'ün Core 5,0 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd</span><span class="sxs-lookup"><span data-stu-id="76dec-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="76dec-113">Paketlerin FSharp projelerine düzgün şekilde yüklenmesini önleyen bir hata düzeltildi:</span><span class="sxs-lookup"><span data-stu-id="76dec-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400