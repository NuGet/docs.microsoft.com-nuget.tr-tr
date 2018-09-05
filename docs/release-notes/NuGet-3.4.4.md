---
title: 3.4.4 NuGet sürüm notları
description: NuGet 3.4.4 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547479"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="c05ff-103">3.4.4 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="c05ff-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="c05ff-104">[NuGet 3.4.3 Sürüm Notları](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="c05ff-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="c05ff-105">Bu yayının birincil odağı olan 3.4.3 kalitesi geliştirmeleri ile Visual Studio uzantısını da birkaç düzeltmeler nuget.exe sürümü.</span><span class="sxs-lookup"><span data-stu-id="c05ff-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="c05ff-106">VSIX ve nuget.exe indirebileceğiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c05ff-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="c05ff-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="c05ff-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="c05ff-108">Tam bir Changelog</span><span class="sxs-lookup"><span data-stu-id="c05ff-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="c05ff-109">Sorunların listesi</span><span class="sxs-lookup"><span data-stu-id="c05ff-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="c05ff-110">Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="c05ff-110">Changes</span></span>

- <span data-ttu-id="c05ff-111">Paketi iyileştirmeleri: ile paketleme, sembol paketleme geliştirmeleri `project.json` ve daha fazla [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="c05ff-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="c05ff-112">Güncelleştirme komutunda projeleri bulunurken bir hata olduğunda özel durumu görüntüleme [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="c05ff-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="c05ff-113">Paket türü girdiden okunan `.nuspec` ve `project.json` sevk [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="c05ff-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="c05ff-114">Bir proje NuGet.Shared olun.</span><span class="sxs-lookup"><span data-stu-id="c05ff-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="c05ff-115">\#602</span><span class="sxs-lookup"><span data-stu-id="c05ff-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="c05ff-116">Gönderme zaman aşımı kullanan HTTP yanıt zaman aşımı olarak [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="c05ff-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="c05ff-117">Paket dosyaları geleceğe ile kullanılan süreleri sahip olmaz [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="c05ff-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="c05ff-118">Güncelleştirme `NuGet.Core.dll` 2.12.0 XML sorunu gidermek için sürüm [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="c05ff-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="c05ff-119">./NuGet.CommandLine.XPlat - v desteği \<ayrıntı\> \<modu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="c05ff-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="c05ff-120">Görüntü olmadan hata geri `project.json` veya `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="c05ff-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="c05ff-121">Gerekli sürümlerinden farklı olduğunda bağımlılığı sürümlerini düzeltme [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="c05ff-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>