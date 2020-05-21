---
title: NuGet 5,6 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,6 sürüm notları.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727823"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="66f9f-103">NuGet 5,6 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="66f9f-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="66f9f-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="66f9f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="66f9f-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="66f9f-105">NuGet version</span></span> | <span data-ttu-id="66f9f-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="66f9f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="66f9f-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="66f9f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="66f9f-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="66f9f-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="66f9f-109">Visual Studio 2019 sürüm 16,6</span><span class="sxs-lookup"><span data-stu-id="66f9f-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="66f9f-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="66f9f-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="66f9f-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="66f9f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="66f9f-112">Özet: 5,6 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="66f9f-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="66f9f-113">Kayan sürümler içeren ön sürüm paketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="66f9f-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="66f9f-114">`Version="*-*"`, `Version="1.*-*"` ve, belirtilen Aralık içinde ön sürüm sürümleri de dahil olmak üzere en son sürümlere benzer float [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="66f9f-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="66f9f-115">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="66f9f-115">Issues fixed in this release</span></span>

<span data-ttu-id="66f9f-116">**Hatalar:**</span><span class="sxs-lookup"><span data-stu-id="66f9f-116">**Bugs:**</span></span>

* <span data-ttu-id="66f9f-117">`nuget push *.nupkg`snupkg yoksa başarısız olur- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="66f9f-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="66f9f-118">Paket ve diğer birçok kod yolu, yerel ayara bağımlı olur.</span><span class="sxs-lookup"><span data-stu-id="66f9f-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="66f9f-119">RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246) kullanın</span><span class="sxs-lookup"><span data-stu-id="66f9f-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="66f9f-120">Perf: kaldırılan proje senaryoları için DG Spec Önizleme geri yüklemeler- [#8793](https://github.com/NuGet/Home/issues/8793) yazılmamalıdır</span><span class="sxs-lookup"><span data-stu-id="66f9f-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="66f9f-121">Geri yükle: önbelleğe alma çözüm bağımlılığı Graph spec- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="66f9f-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="66f9f-122">PM konsolu ile bir paket yüklendikten sonra, PM Kullanıcı arabirimi SDK stil projeleri için çalışmıyor- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="66f9f-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="66f9f-123">Katıştırılmış simge, yerel paket akışı ile PM Kullanıcı arabiriminde gösterilemez; bağlı/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="66f9f-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="66f9f-124">Ayrıştırma başarısız olursa, NuGetVersion. TryParseStrict () yanlış döndürmelidir [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="66f9f-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="66f9f-125">`nuget.exe push`kaynak `-source` URL 'si değil, kaynak adı kullanımının önerilmeye yönelik yardım. [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="66f9f-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="66f9f-126">`dotnet nuget add package SourceUri`Hatalı varsayılan paket kaynağı adı oluşturur- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="66f9f-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="66f9f-127">Ekran okuyucu "arama..." duyurusu yapmaz sekmeleri değiştirirken ileti- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="66f9f-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="66f9f-128">Erişilebilirlik: odak dikdörtgeni rengine erişilebilir değil koyu temadaki Kullanıcı arabirimi sekmeleri [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="66f9f-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="66f9f-129">NuGet. exe 5,5, MSBuild 14 veya altında geri yükleme yapamıyor- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="66f9f-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="66f9f-130">Geri yükleme iletilerinde milisaniyelik süreleri günlüğe kaydetme- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="66f9f-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="66f9f-131">Ioutputconsole zaman uyumsuz yap- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="66f9f-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="66f9f-132">MSBuild sürüm seçme, İngilizce olmayan bazı kültürler üzerinde kötü bir şekilde çalışacak [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="66f9f-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="66f9f-133">#9337 için varsayılan biçim yok `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="66f9f-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="66f9f-134">Perf: Restoreoperationgünlükçü gereksiz iş parçacığı benzeşimine sahip- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="66f9f-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="66f9f-135">Komutlar için otomatik belgeler oluşturma `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="66f9f-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="66f9f-136">Varsayılan ayrıntı düzeyi her projenin noop geri yükleme- [#8792](https://github.com/NuGet/Home/issues/8792) raporlanmamalıdır</span><span class="sxs-lookup"><span data-stu-id="66f9f-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="66f9f-137">`-DependencyVersion`İçin destek parametresi `NuGet.exe update` , install komutuna benzer- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="66f9f-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="66f9f-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="66f9f-138">**DCRs:**</span></span>

* <span data-ttu-id="66f9f-139">NET 5.0 hedef çerçevesi için başlangıç desteğini ekleme- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="66f9f-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="66f9f-140">PM UI- [#9278](https://github.com/NuGet/Home/issues/9278) Updates SEKMESINDE paketleri kimliğe göre sırala</span><span class="sxs-lookup"><span data-stu-id="66f9f-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="66f9f-141">**[Bu yayında düzeltilen tüm sorunların listesi-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="66f9f-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
