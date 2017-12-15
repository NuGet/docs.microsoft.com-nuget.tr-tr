---
title: "NuGet 2.9 RC sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "NuGet 2.9 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.9 RC sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="57e07-104">NuGet 2.9 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="57e07-104">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="57e07-105">[NuGet 2.8.7 Sürüm Notları](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview sürüm notları](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="57e07-105">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="57e07-106">NuGet 2.9 yayımlanan 10 Eylül 2015 2.8.7 için bir güncelleştirme olarak Visual Studio 2012 ve 2013 için VSIX.</span><span class="sxs-lookup"><span data-stu-id="57e07-106">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="57e07-107">Bu sürümde güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="57e07-107">Updates in this release</span></span>

* <span data-ttu-id="57e07-108">İşleme paketleri varsa atlanıyor artık kendi kapsanan `.nuspec` belge hatalı biçimlendirilmiş - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="57e07-108">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="57e07-109">UNIX/Linux senaryolarında - \r\n multipartwebrequest işlenmesi düzeltilmiştir [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="57e07-109">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="57e07-110">Visual Studio 2013 Community Edition - derleme olayları ile tümleştirme düzeltildi [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="57e07-110">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="57e07-111">Bu sürümde düzeltmeleri tam listesi Github'da bulunabilir [2.8.8 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="57e07-111">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
