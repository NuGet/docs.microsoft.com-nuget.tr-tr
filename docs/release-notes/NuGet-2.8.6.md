---
title: 2.8.6 NuGet sürüm notları
description: NuGet 2.8.6 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546497"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="e28e4-103">2.8.6 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e28e4-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="e28e4-104">[2.8.5 NuGet sürüm notları](../release-notes/nuget-2.8.5.md) | [2.8.7 NuGet sürüm notları](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="e28e4-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="e28e4-105">NuGet 2.8.6 bırakıldığını 20 Temmuz 2015 bizim 2.8.5 küçük bir güncelleştirme olarak bazı VSIX hedeflenen düzeltmeler ve teslim edilebilir paketleri Windows 10 UWP geliştirme modeli desteği ile desteklemeye yönelik geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="e28e4-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="e28e4-106">NuGet Paket Yöneticisi uzantısı'nın bu sürümü, yalnızca Visual Studio 2013 için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="e28e4-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="e28e4-107">Bu sürümde, NuGet Paket Yöneticisi iletişim için eklenen destek sahipti:</span><span class="sxs-lookup"><span data-stu-id="e28e4-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="e28e4-108">Windows 10 için uygulama geliştirme desteği için UAP hedef çerçeve adı kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="e28e4-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="e28e4-109">NuGet Protokolü sürüm 3 uç noktaları</span><span class="sxs-lookup"><span data-stu-id="e28e4-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="e28e4-110">Destek [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) depo kaynakları protocolVersion özniteliği.</span><span class="sxs-lookup"><span data-stu-id="e28e4-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="e28e4-111">Varsayılan değer: "2"</span><span class="sxs-lookup"><span data-stu-id="e28e4-111">Default value is "2"</span></span>
* <span data-ttu-id="e28e4-112">Gerekli Paket sürümü yerel önbellek üzerinde kullanılabilir değilse, uzak depoya geri dönülüyor</span><span class="sxs-lookup"><span data-stu-id="e28e4-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>