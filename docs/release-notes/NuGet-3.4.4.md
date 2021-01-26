---
title: NuGet 3.4.4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.4 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780229"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="90e26-103">NuGet 3.4.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="90e26-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="90e26-104">[NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5-Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="90e26-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="90e26-105">Bu yayının birincil odağında, Visual Studio uzantısı için birkaç düzeltme ile nuget.exe 3.4.3 sürümünün kalitesi geliştirılmıştır.</span><span class="sxs-lookup"><span data-stu-id="90e26-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="90e26-106">Hem VSıX hem [de nuget.exe yükleyebilirsiniz](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="90e26-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="90e26-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="90e26-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="90e26-108">Tam changelog</span><span class="sxs-lookup"><span data-stu-id="90e26-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="90e26-109">Sorunların listesi</span><span class="sxs-lookup"><span data-stu-id="90e26-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="90e26-110">Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="90e26-110">Changes</span></span>

- <span data-ttu-id="90e26-111">Paket geliştirmeleri: paketleme `project.json` ve daha fazla [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606) Ile paketleme simgeleri için geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="90e26-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="90e26-112">Update komutunda projeler bulunurken hata oluştu [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="90e26-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="90e26-113">Girişte paket türünü oku `.nuspec` ve `project.json` paketleme [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="90e26-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="90e26-114">NuGet. Shared bir proje değil.</span><span class="sxs-lookup"><span data-stu-id="90e26-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="90e26-115">\#602</span><span class="sxs-lookup"><span data-stu-id="90e26-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="90e26-116">HTTP yanıt zaman aşımı [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) olarak gönderme zaman aşımını kullanın</span><span class="sxs-lookup"><span data-stu-id="90e26-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="90e26-117">Gelecekteki sürelerle paket dosyalarının süresi kullanılmayacak [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="90e26-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="90e26-118">`NuGet.Core.dll`XML sorununu onarmak için sürüm 2.12.0 güncelleştiriliyor [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="90e26-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="90e26-119">Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="90e26-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="90e26-120">`project.json`Veya `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) olmadan geri yükleme hatasını görüntüle</span><span class="sxs-lookup"><span data-stu-id="90e26-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="90e26-121">Gerekli sürümler farklı olduğunda bağımlılık sürümleri düzeltiliyor [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="90e26-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>