---
title: NuGet 3.4.4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.4 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="2abda-103">NuGet 3.4.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="2abda-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="2abda-104">[NuGet 3.4.3 Sürüm Notları](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="2abda-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="2abda-105">Bu sürümü birincil odağı 3.4.3 kalitesini düzenlenmesiydi nuget.exe de Visual Studio uzantısı için birkaç düzeltmeleriyle sürümü.</span><span class="sxs-lookup"><span data-stu-id="2abda-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="2abda-106">VSIX ve nuget.exe indirebilirsiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2abda-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="2abda-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="2abda-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="2abda-108">Tam bir değişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="2abda-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="2abda-109">Sorunların listesi</span><span class="sxs-lookup"><span data-stu-id="2abda-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="2abda-110">Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="2abda-110">Changes</span></span>

- <span data-ttu-id="2abda-111">Paketi iyileştirmeleri: ile paket sembolleri sevk geliştirmeleri `project.json` ve daha fazla [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="2abda-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="2abda-112">Güncelleştirme komutunda projeleri bulunurken bir hata olduğunda özel durumu görüntüleme [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="2abda-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="2abda-113">Paket türü girdiden okunan `.nuspec` ve `project.json` sevk [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="2abda-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="2abda-114">Bir proje NuGet.Shared olun.</span><span class="sxs-lookup"><span data-stu-id="2abda-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="2abda-115">\#602</span><span class="sxs-lookup"><span data-stu-id="2abda-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="2abda-116">HTTP yanıtı zaman aşımı olarak gönderme zaman aşımı kullanmak [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="2abda-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="2abda-117">Paket dosyaları gelecekteki sürelerine sahip kullanılan zamanları sahip olmaz [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="2abda-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="2abda-118">Güncelleştirme `NuGet.Core.dll` XML sorunu düzeltmek için 2.12.0 sürüme [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="2abda-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="2abda-119">./NuGet.CommandLine.XPlat - v Destek \<ayrıntı\> \<modu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="2abda-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="2abda-120">Görüntü olmadan geri yükleme `project.json` veya `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="2abda-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="2abda-121">Gerekli sürümlerinden farklı olduğunda bağımlılık sürümleri düzelttikten [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="2abda-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>