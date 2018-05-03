---
title: NuGet 4.5 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="b5226-103">NuGet 4.5 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b5226-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="b5226-104">[Visual Studio 2017 15,5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="b5226-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b5226-105">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b5226-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="b5226-106">.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları</span><span class="sxs-lookup"><span data-stu-id="b5226-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="b5226-107">.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b5226-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="b5226-108">[Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.</span><span class="sxs-lookup"><span data-stu-id="b5226-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="b5226-109">Görüntüleme, ekleme ya da DotNetCLITools, Nuget Paket Yöneticisi'ni kullanarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b5226-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="b5226-110">Sorun</span><span class="sxs-lookup"><span data-stu-id="b5226-110">Issue</span></span>

<span data-ttu-id="b5226-111">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="b5226-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="b5226-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="b5226-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="b5226-113">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="b5226-113">Workaround</span></span>

<span data-ttu-id="b5226-114">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b5226-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="b5226-115">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="b5226-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="b5226-116">Sorun</span><span class="sxs-lookup"><span data-stu-id="b5226-116">Issue</span></span>

<span data-ttu-id="b5226-117">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="b5226-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="b5226-118">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="b5226-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="b5226-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="b5226-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="b5226-120">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="b5226-120">Workaround</span></span>

<span data-ttu-id="b5226-121">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="b5226-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="b5226-122">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="b5226-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="b5226-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="b5226-123">Issue</span></span>

<span data-ttu-id="b5226-124">Bazen, bir derlemeyi imzası geçersiz olan veya paket sürümü ile 'DateTime' borsa takip ayarlandığında içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde çalıştırılacak geri yükleme neden [dotnet/project-sistem #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="b5226-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="b5226-125">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="b5226-125">Workaround</span></span>

<span data-ttu-id="b5226-126">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="b5226-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="b5226-127">NuGet 4.5 RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b5226-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="b5226-128">4.4 NuGet RTM ile giderilen sorunlar için lütfen [NuGet 4.4 RTM sürüm notları](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="b5226-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="b5226-129">Özellikler</span><span class="sxs-lookup"><span data-stu-id="b5226-129">Features</span></span>

- <span data-ttu-id="b5226-130">Otomatik-itme simgeleri paketinin - devre dışı [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="b5226-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="b5226-131">Hatalar</span><span class="sxs-lookup"><span data-stu-id="b5226-131">Bugs</span></span>

- <span data-ttu-id="b5226-132">[Regresyon] 15.5p1 içinde: Portable0.0 atlandı - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="b5226-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="b5226-133">Paketleri varlıklarından geri yüklendikten sonra - eksik [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="b5226-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="b5226-134">Eklentisi kimlik bilgisi sağlayıcıları URI'ler içeren alanları ile - çalışmıyor [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="b5226-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="b5226-135">Paket geri yükleme işlemi başarısız olursa hata en az ayrıntı ON - çıkışıyla bile yazdırılacağı [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="b5226-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="b5226-136">DotNet</span><span class="sxs-lookup"><span data-stu-id="b5226-136">dotnet</span></span>
  - <span data-ttu-id="b5226-137">Çözüm düzeyinde dotnetcore geri yükleme için rastgele derleme hataları - false başında ReferenceOutputAssembly ile ProjectReference izleyin değil [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="b5226-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="b5226-138">Otomatik Tamamlama PMC işe yanlış yöntemleriyle nesnesi - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="b5226-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="b5226-139">nuget.exe geri yükleme başarısız ile Visual Studio 2015 araç takımı - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="b5226-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="b5226-140">perf - pmc vs2017 içinde - örneği pahalı [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="b5226-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="b5226-141">Yavaş yavaş bağlantı - bağımlılık bilgi almak [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="b5226-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="b5226-142">birden çok paket ortak bir bağımlılık - paylaşıyorsanız - RemoveDependencies içeren kaldırma-package başarısız olur [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="b5226-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="b5226-143">Yayımlama için - NuGet.Core.nupkg Sonlandır [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="b5226-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="b5226-144">NuGet paketi çözümler dizin adı bağımlılık Kimliğinden - IncludeProjectReferences kullanıldığında csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="b5226-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="b5226-145">Bir özel durum oluştu - 'NuGet.ProxyCache' tür başlatıcısı belirtti [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="b5226-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="b5226-146">nuget restore performans sorunu kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="b5226-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="b5226-147">UI istemci başarısız arama kayıt BLOB'lar öncesinde - olduğunda herhangi bir hata veya uyarı göstermek [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="b5226-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="b5226-148">Get-paketler - güncelleştirmeleri, hatalı bir sorgu oluşturur - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="b5226-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="b5226-149">GitHub sorunları 4.5 RTM sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="b5226-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="b5226-150">Konu listesi</span><span class="sxs-lookup"><span data-stu-id="b5226-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
