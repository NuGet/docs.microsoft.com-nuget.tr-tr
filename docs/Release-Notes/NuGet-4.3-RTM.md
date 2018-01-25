---
title: "NuGet 4.3 RTM sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.3 RTM için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 4.3 RTM sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 02b8f6df08438db42e73cc761acc486b7fa13919
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="25fd8-104">NuGet 4.3 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="25fd8-104">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="25fd8-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.3 .NET standart 2.0/.NET Core 2.0 gibi yeni senaryolara desteği birçok kalite düzeltmeleri içerir ve performansı artırır ekleyen RTM ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="25fd8-106">Bu sürüm ayrıca anlamsal sürüm oluşturma 2.0.0, MSBuild tümleştirme için destek gibi çeşitli iyileştirmeler NuGet uyarıları ve hataları ve daha fazla getirir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-106">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="25fd8-107">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="25fd8-107">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="25fd8-108">NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir</span><span class="sxs-lookup"><span data-stu-id="25fd8-108">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="25fd8-109">Sorun</span><span class="sxs-lookup"><span data-stu-id="25fd8-109">Issue</span></span>

<span data-ttu-id="25fd8-110">Aşağıdaki geri yükleme komut satırı teknikleri devre dışı bırakılan paketler kaynakları etkin olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="25fd8-110">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="25fd8-111">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="25fd8-111">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="25fd8-112">`dotnet restore`(VS veya bir ile birlikte dotnet.exe ile birlikte gelen 2.0.0 NetCore SDK ile birlikte)</span><span class="sxs-lookup"><span data-stu-id="25fd8-112">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="25fd8-113">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="25fd8-113">Workaround</span></span>

1. <span data-ttu-id="25fd8-114">Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın</span><span class="sxs-lookup"><span data-stu-id="25fd8-114">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="25fd8-115">Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="25fd8-115">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="25fd8-116">Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25fd8-116">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="25fd8-117">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="25fd8-117">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="25fd8-118">Sorun</span><span class="sxs-lookup"><span data-stu-id="25fd8-118">Issue</span></span>

<span data-ttu-id="25fd8-119">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="25fd8-119">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="25fd8-120">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="25fd8-120">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="25fd8-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="25fd8-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="25fd8-122">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="25fd8-122">Workaround</span></span>

<span data-ttu-id="25fd8-123">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="25fd8-123">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="25fd8-124">Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="25fd8-124">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="25fd8-125">Nuget Paket Yöneticisi’ni kullanarak DotNetCLITools’u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="25fd8-125">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="25fd8-126">Sorun</span><span class="sxs-lookup"><span data-stu-id="25fd8-126">Issue</span></span>

<span data-ttu-id="25fd8-127">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="25fd8-127">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="25fd8-128">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="25fd8-128">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="25fd8-129">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="25fd8-129">Workaround</span></span>

<span data-ttu-id="25fd8-130">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-130">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="25fd8-131">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="25fd8-131">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="25fd8-132">Sorun</span><span class="sxs-lookup"><span data-stu-id="25fd8-132">Issue</span></span>

<span data-ttu-id="25fd8-133">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-133">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="25fd8-134">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="25fd8-134">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="25fd8-135">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="25fd8-135">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="25fd8-136">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="25fd8-136">Workaround</span></span>

<span data-ttu-id="25fd8-137">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="25fd8-137">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="25fd8-138">4.3 NuGet RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="25fd8-138">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="25fd8-139">[NuGet 4.0 RTM sürüm notları](../release-notes/nuget-4.0-RTM.md) -NuGet 4.0 RTM için sabit tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="25fd8-139">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="25fd8-140">Özellikler</span><span class="sxs-lookup"><span data-stu-id="25fd8-140">Features</span></span>

- <span data-ttu-id="25fd8-141">NuGet Restore Perf - uygulama akıllı sekmeyi komut satırı geri yükleme - ve VS artırmak [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="25fd8-141">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="25fd8-142">NET çekirdek 2.0: VS/Dotnet CLI varolan NuGet işlevini kullanarak başlamanız gerekir: geri dönüş klasörleri - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="25fd8-142">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="25fd8-143">NET çekirdek 2.0: Etkinleştirmek belirli geri yükleme uyarılarını gözardı (veya hata yükseltmek) - kullanıcılar [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="25fd8-143">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="25fd8-144">NET çekirdek 2.0: CLI yerelleştirilmiş derlemeler - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="25fd8-144">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="25fd8-145">NET çekirdek 2.0: tüm uyarılar/hataları (PackageTargetFallback dahil) - varlıklar dosyaya Kaydet [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="25fd8-145">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="25fd8-146">TFM desteğini etkinleştirin: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="25fd8-146">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="25fd8-147">NuGet.Core NuGet.Client projeleri (ve dolayısıyla DLL'ler) - sayısını azaltın [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="25fd8-147">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="25fd8-148">Nuget uyarıları hata - olarak işaretlemek için özelliğini ekler [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="25fd8-148">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="25fd8-149">Hatalar</span><span class="sxs-lookup"><span data-stu-id="25fd8-149">Bugs</span></span>

- <span data-ttu-id="25fd8-150">MSBuild /t:pack başarısız "DevelopmentDependency" parametresi "PackTask" görevi tarafından - desteklenmiyor [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="25fd8-150">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="25fd8-151">İçerik dosyaları için dizin yapısını düzleştirilmiş Windows dizin ayırıcı ise PackagePath - sonunda eklenmiyor varsa [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="25fd8-151">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="25fd8-152">netcore projeleri ayarı developmentDependency - olarak desteklemez [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="25fd8-152">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="25fd8-153">RestoreManagerPackage yükleniyor zaman uyumlu olarak engellenen kullanıcı Arabirimi iş parçacığı ve VS - karşılıklı [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="25fd8-153">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="25fd8-154">DotNet geri yükleme (ve bu nedenle msbuild /t:restore) bir açık çözüm proje bağımlılığı projelerle atlar [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="25fd8-154">dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="25fd8-155">Çözümünüzü farklı büyük/küçük harf, aynı projenin başvurduğu projectreferences varsa geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="25fd8-156">Bu da büyük/küçük harf - fark olmadan farklı göreli yollar etkiler [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="25fd8-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="25fd8-157">NuGet paketleri geri yürütülebilir .NET Core 2.0 ile - yürütülebilir dosyalar artık [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="25fd8-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="25fd8-158">Çözüm dosyası - ayrıştırılırken özel durum ayrıntılarını NuGet.exe yuttuğu [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="25fd8-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="25fd8-159">Paketi Windows - '/' ile biten bir yolu ContentTargetFolders içeriyorsa, bu içerik dosyalarını yanlış konuma yerleştirir [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="25fd8-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="25fd8-160">Bu hedefleri netcoreapp1.1 - bir Araçları Paketi için bir DotNetCliToolReference geri yükleyemezsiniz [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="25fd8-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="25fd8-161">Proje dosyası (C++) - Nuget güncelleştirme CLI bırakır eski Paket sürümü koşulu [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="25fd8-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="25fd8-162">Dcr</span><span class="sxs-lookup"><span data-stu-id="25fd8-162">DCRs</span></span>

- <span data-ttu-id="25fd8-163">CPS nomation - gelen okuma DotnetCliToolTargetFramework [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="25fd8-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="25fd8-164">TPMinV onay pj stili UWP - çalışmalıdır [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="25fd8-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="25fd8-165">AutoReferenced paketler - UI açıklamasını artırmak [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="25fd8-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="25fd8-166">NuGet restore derleme varlıklar çalışma zamanı bölümünden seçmektir.</span><span class="sxs-lookup"><span data-stu-id="25fd8-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="25fd8-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="25fd8-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="25fd8-168">Bağımlılık tanılama kilit dosyası - put [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="25fd8-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="25fd8-169">GitHub sorunları 4.3 RTM'de sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="25fd8-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="25fd8-170">Konu listesi</span><span class="sxs-lookup"><span data-stu-id="25fd8-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
