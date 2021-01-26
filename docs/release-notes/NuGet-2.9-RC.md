---
title: NuGet 2,9-RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,9 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780320"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="74f06-103">NuGet 2,9-RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="74f06-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="74f06-104">[NuGet 2.8.7 sürüm notları](../release-notes/nuget-2.8.7.md)  |  [NuGet 3,0 Preview sürüm notları](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="74f06-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="74f06-105">NuGet 2,9, Visual Studio 2012 ve 2013 için 2.8.7 VSıX güncelleştirmesi olarak 10 Eylül 2015 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="74f06-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="74f06-106">Bu sürümdeki güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="74f06-106">Updates in this release</span></span>

* <span data-ttu-id="74f06-107">Bu durumda, içerilen `.nuspec` belge hatalı biçimlendirilmiş, [PR8](https://github.com/NuGet/NuGet2/pull/8) işleme paketleri atlanıyor.</span><span class="sxs-lookup"><span data-stu-id="74f06-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="74f06-108">UNIX/Linux senaryoları için \r\n çok partwebrequest işleme düzeltildi- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="74f06-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="74f06-109">Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180) ' deki derleme olaylarıyla tümleştirme düzeltildi</span><span class="sxs-lookup"><span data-stu-id="74f06-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="74f06-110">Bu sürümdeki düzeltmelerin tüm listesi [2.8.8 kilometre taşında](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) GitHub 'da bulunabilir</span><span class="sxs-lookup"><span data-stu-id="74f06-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
