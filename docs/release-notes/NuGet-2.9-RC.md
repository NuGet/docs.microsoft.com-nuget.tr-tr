---
title: NuGet 2.9 RC sürüm notları
description: NuGet 2.9 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548330"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="e45c8-103">NuGet 2.9 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e45c8-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="e45c8-104">[2.8.7 NuGet sürüm notları](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Önizleme sürüm notları](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="e45c8-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="e45c8-105">NuGet 2.9 bırakıldığını 10 Eylül 2015'te 2.8.7 bir güncelleştirme olarak VSIX Visual Studio 2012 ve 2013.</span><span class="sxs-lookup"><span data-stu-id="e45c8-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="e45c8-106">Bu sürümdeki güncelleştirmelerin</span><span class="sxs-lookup"><span data-stu-id="e45c8-106">Updates in this release</span></span>

* <span data-ttu-id="e45c8-107">İşleme paketleri varsa atlanıyor. artık kendi içerilen `.nuspec` belge hatalı biçimlendirilmiş - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="e45c8-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="e45c8-108">UNIX/Linux senaryoları - \r\n multipartwebrequest işlenmesini düzeltildi [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="e45c8-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="e45c8-109">Visual Studio 2013 Community Edition - derleme olayları ile tümleştirme düzeltildi [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="e45c8-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="e45c8-110">Bu sürümdeki düzeltmeler tam listesi Github'da bulunabilir [2.8.8 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="e45c8-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
