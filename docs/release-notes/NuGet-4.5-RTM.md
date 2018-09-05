---
title: NuGet 4.5 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 4.5 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548302"
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="daec4-103">NuGet 4.5 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="daec4-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="daec4-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) birlikte [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="daec4-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="daec4-105">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="daec4-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="daec4-106">.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="daec4-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="daec4-107">.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="daec4-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="daec4-108">[Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.</span><span class="sxs-lookup"><span data-stu-id="daec4-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="daec4-109">Görüntülenemiyor, eklenemiyor veya Nuget Paket Yöneticisi'ni kullanarak dotnetclıtools'u başlatamadı</span><span class="sxs-lookup"><span data-stu-id="daec4-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="daec4-110">Sorun</span><span class="sxs-lookup"><span data-stu-id="daec4-110">Issue</span></span>

<span data-ttu-id="daec4-111">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="daec4-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="daec4-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="daec4-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="daec4-113">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="daec4-113">Workaround</span></span>

<span data-ttu-id="daec4-114">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="daec4-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="daec4-115">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="daec4-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="daec4-116">Sorun</span><span class="sxs-lookup"><span data-stu-id="daec4-116">Issue</span></span>

<span data-ttu-id="daec4-117">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="daec4-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="daec4-118">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="daec4-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="daec4-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="daec4-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="daec4-120">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="daec4-120">Workaround</span></span>

<span data-ttu-id="daec4-121">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="daec4-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="daec4-122">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="daec4-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="daec4-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="daec4-123">Issue</span></span>

<span data-ttu-id="daec4-124">Bazen, geçersiz imzalı veya paket sürümü 'DateTime' değeriyle ayarlandığında bir derlemeyi içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde çalışmasına geri neden [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="daec4-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="daec4-125">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="daec4-125">Workaround</span></span>

<span data-ttu-id="daec4-126">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="daec4-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="daec4-127">NuGet 4.5 RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="daec4-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="daec4-128">4.4 NuGet RTM'de düzeltilen sorunları için lütfen başvurmak [NuGet 4.4 RTM sürüm notları](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="daec4-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="daec4-129">Özellikler</span><span class="sxs-lookup"><span data-stu-id="daec4-129">Features</span></span>

- <span data-ttu-id="daec4-130">Otomatik-push sembol package - devre dışı [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="daec4-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="daec4-131">Hatalar</span><span class="sxs-lookup"><span data-stu-id="daec4-131">Bugs</span></span>

- <span data-ttu-id="daec4-132">[Regresyon] içinde 15.5p1: Portable0.0 atlandı - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="daec4-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="daec4-133">Paketleri varlıklarından geri yüklemeden sonra - eksik [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="daec4-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="daec4-134">Eklenti kimlik bilgisi sağlayıcıları ile içeren URI'leri alanları - çalışmaz [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="daec4-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="daec4-135">Paket geri yükleme başarısız olursa hata olsa da en az ayrıntı ON - çıkış yazdırılacağı [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="daec4-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="daec4-136">DotNet</span><span class="sxs-lookup"><span data-stu-id="daec4-136">dotnet</span></span>
  - <span data-ttu-id="daec4-137">Çözüm düzeyinde dotnetcore geri yükleme için rastgele oluşturma hataları - ProjectReference false lider, ReferenceOutputAssembly ile izleyin değil [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="daec4-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="daec4-138">Otomatik Tamamlama yanlış nesne yöntemleri ile-PMC'yi geliştirilme [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="daec4-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="daec4-139">nuget.exe geri yükleme başarısız olursa, Visual Studio 2015 araç takımıyla - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="daec4-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="daec4-140">perf - pmc vs2017'de - örneklemek pahalı [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="daec4-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="daec4-141">Yavaş yavaş bağlantı - bağımlılık bilgi almak [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="daec4-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="daec4-142">birden çok paket ortak bir bağımlılık - paylaşıyorsa - RemoveDependencies çakışabilmektedir kaldırma-package başarısız olur [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="daec4-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="daec4-143">Yayımlama için - NuGet.Core.nupkg Sonlandır [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="daec4-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="daec4-144">NuGet paketi csproj + project.json - için - IncludeProjectReferences kullanıldığında, dizin adı bağımlılık Kimliğinden çözümler [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="daec4-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="daec4-145">Bir özel durum oluştu - türü Başlatıcısı 'NuGet.ProxyCache' oluşturdu [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="daec4-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="daec4-146">nuget geri yükleme performansı kudu - sorun [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="daec4-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="daec4-147">UI istemci başarısız araması önceden kayıt BLOB'lar - olduğunda herhangi bir hata veya uyarı gösterilecek [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="daec4-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="daec4-148">-Güncelleştirmeleri, hatalı bir sorgu oluşturur - Get-paketleri [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="daec4-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="daec4-149">GitHub sorunları 4.5 RTM sürümünde sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="daec4-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="daec4-150">Konu listesi</span><span class="sxs-lookup"><span data-stu-id="daec4-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
