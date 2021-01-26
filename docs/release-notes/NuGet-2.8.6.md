---
title: NuGet 2.8.6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.6 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776708"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="0bae4-103">NuGet 2.8.6 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="0bae4-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="0bae4-104">[NuGet 2.8.5 sürüm notları](../release-notes/nuget-2.8.5.md)  |  [NuGet 2.8.7 sürüm notları](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="0bae4-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="0bae4-105">NuGet 2.8.6, Windows 10 UWP geliştirme modeli desteğiyle birlikte sunulan paketleri desteklemek için bazı hedeflenen düzeltmeler ve geliştirmeler ile 2.8.5 VSıX 2015 Temmuz ' den yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0bae4-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="0bae4-106">NuGet Paket Yöneticisi uzantısının bu sürümü yalnızca Visual Studio 2013 için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="0bae4-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="0bae4-107">Bu sürümde, NuGet Paket Yöneticisi iletişim kutusunda için destek eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="0bae4-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="0bae4-108">Windows 10 uygulama geliştirmeyi desteklemek için UıAP hedef Framework bilinen adı kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="0bae4-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="0bae4-109">NuGet protokol sürümü 3 uç noktaları</span><span class="sxs-lookup"><span data-stu-id="0bae4-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="0bae4-110">Depo kaynaklarında [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion özniteliği için destek.</span><span class="sxs-lookup"><span data-stu-id="0bae4-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="0bae4-111">Varsayılan değer "2"</span><span class="sxs-lookup"><span data-stu-id="0bae4-111">Default value is "2"</span></span>
* <span data-ttu-id="0bae4-112">Gerekli bir paket sürümü yerel önbellekte yoksa uzak depoya geri dönülüyor</span><span class="sxs-lookup"><span data-stu-id="0bae4-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>