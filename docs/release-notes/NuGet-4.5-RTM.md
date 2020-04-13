---
title: NuGet 4.5 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496576"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="c735a-103">NuGet 4.5 Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="c735a-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="c735a-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)ile birlikte geliyor.</span><span class="sxs-lookup"><span data-stu-id="c735a-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="c735a-105">Özeti: 4.5.0 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="c735a-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="c735a-106">Özeti: 4.5.2 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="c735a-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="c735a-107">Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır</span><span class="sxs-lookup"><span data-stu-id="c735a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="c735a-108">Özeti: 4.5.3 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="c735a-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="c735a-109">Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906</span><span class="sxs-lookup"><span data-stu-id="c735a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="c735a-110">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="c735a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="c735a-111">.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="c735a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="c735a-112">.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c735a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="c735a-113">[Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.</span><span class="sxs-lookup"><span data-stu-id="c735a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="c735a-114">Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz</span><span class="sxs-lookup"><span data-stu-id="c735a-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="c735a-115">Sorun</span><span class="sxs-lookup"><span data-stu-id="c735a-115">Issue</span></span>

<span data-ttu-id="c735a-116">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="c735a-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="c735a-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="c735a-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="c735a-118">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c735a-118">Workaround</span></span>

<span data-ttu-id="c735a-119">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c735a-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="c735a-120">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="c735a-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="c735a-121">Sorun</span><span class="sxs-lookup"><span data-stu-id="c735a-121">Issue</span></span>

<span data-ttu-id="c735a-122">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="c735a-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="c735a-123">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="c735a-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="c735a-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="c735a-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="c735a-125">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c735a-125">Workaround</span></span>

<span data-ttu-id="c735a-126">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="c735a-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="c735a-127">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="c735a-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="c735a-128">Sorun</span><span class="sxs-lookup"><span data-stu-id="c735a-128">Issue</span></span>

<span data-ttu-id="c735a-129">Bazen, geçersiz imzaiçeren bir derleme içeren bir paket kullandığınızda veya paket sürümü 'DateTime' işaretleyicisi ile ayarlandığında, paket otomatik geri yüklemesinin sonsuz bir döngü [dotnet/proje sistemi#1457'de](https://github.com/dotnet/project-system/issues/1457)çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="c735a-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="c735a-130">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c735a-130">Workaround</span></span>

<span data-ttu-id="c735a-131">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="c735a-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="c735a-132">NuGet 4.5 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="c735a-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="c735a-133">NuGet 4.4 RTM'de düzeltilen sorunlar için lütfen [NuGet 4.4 RTM Yayın Notları'na](../release-notes/nuget-4.4-RTM.md) bakın</span><span class="sxs-lookup"><span data-stu-id="c735a-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="c735a-134">Özellikler</span><span class="sxs-lookup"><span data-stu-id="c735a-134">Features</span></span>

- <span data-ttu-id="c735a-135">Semboller paketinin otomatik itme devre dışı - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="c735a-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="c735a-136">Hatalar</span><span class="sxs-lookup"><span data-stu-id="c735a-136">Bugs</span></span>

- <span data-ttu-id="c735a-137">[Regresyon] içinde 15.5p1: Portable0.0 atlanır - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="c735a-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="c735a-138">Paketlerden elde edilen varlıklar geri yüklendikten sonra eksik - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="c735a-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="c735a-139">Plugin kimlik bilgileri sağlayıcıları boşluk içeren URI'lerle çalışmaz - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="c735a-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="c735a-140">Paket geri yüklenemediyse, hata en az ayrıntılı on ile bile çıktıya yazdırılmalıdır - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="c735a-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="c735a-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="c735a-141">dotnet</span></span>
  - <span data-ttu-id="c735a-142">çözüm düzeyinde dotnetcore geri yükleme rasgele yapı hataları na yol açan falseOutputAssembly ile ProjectReference takip etmez - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="c735a-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="c735a-143">PMC'de otomatik tamamlama nesne yöntemleriyle yanlış çalışır - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="c735a-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="c735a-144">nuget.exe geri yükleme Visual Studio 2015 araç seti ile başarısız olur - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="c735a-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="c735a-145">perf - pmc vs2017 yılında anlık pahalı - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="c735a-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="c735a-146">Yavaş bağlantı da bağımlılık bilgisi almak için yavaş - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="c735a-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="c735a-147">paketi kaldırma w/ -RemoveDependencies birden fazla paket ortak bir bağımlılık paylaşırsa başarısız olur - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="c735a-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="c735a-148">NuGet.Core.nupkg yayıncılık için Finalize - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="c735a-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="c735a-149">NuGet paketi dizin adından bağımlılık kimliğini giderir -IncludeProjectReferences csproj + project.json için kullanıldığında - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="c735a-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="c735a-150">'NuGet.ProxyÖnbellek' için tür baş harfbir özel durum attı - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="c735a-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="c735a-151">kudu ile nuget geri yükleme performans sorunu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="c735a-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="c735a-152">UI İstemci, arama kayıt lekeleri öncesinde olduğunda herhangi bir hata veya uyarı göstermek için başarısız - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="c735a-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="c735a-153">Get-Packages -Güncelleştirmeler yanlış bir sorgu oluşturur - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="c735a-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="c735a-154">4,5 RTM'de düzeltilen GitHub sorunlarına bağlantılar</span><span class="sxs-lookup"><span data-stu-id="c735a-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="c735a-155">Sorunlar listesi</span><span class="sxs-lookup"><span data-stu-id="c735a-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
