---
title: NuGet 4.3 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496588"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="c6fe1-103">NuGet 4.3 Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="c6fe1-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="c6fe1-104">[Visual Studio 2017 15.3 RTW,](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) .NET Standard 2.0/.NET Core 2.0 gibi yeni senaryolara destek ekleyen, birçok kalite düzeltmesi içeren ve performansı artıran NuGet 4.3 RTM ile birlikte geliyor.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="c6fe1-105">Bu sürüm aynı zamanda Anlamsal Sürüm 2.0.0, NuGet uyarı ve hatalarımsbuild entegrasyonu ve daha fazlası için destek gibi çeşitli iyileştirmeler getiriyor.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="c6fe1-106">Özeti: 4.3.0 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="c6fe1-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="c6fe1-107">Özet: 4.3.1'de Yenilikler</span><span class="sxs-lookup"><span data-stu-id="c6fe1-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="c6fe1-108">Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır</span><span class="sxs-lookup"><span data-stu-id="c6fe1-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="c6fe1-109">Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906</span><span class="sxs-lookup"><span data-stu-id="c6fe1-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="c6fe1-110">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="c6fe1-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="c6fe1-111">NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir</span><span class="sxs-lookup"><span data-stu-id="c6fe1-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="c6fe1-112">Sorun</span><span class="sxs-lookup"><span data-stu-id="c6fe1-112">Issue</span></span>

<span data-ttu-id="c6fe1-113">Aşağıdaki geri yükleme komut satırı teknikleri devre dışı bırakılan paket kaynaklarını etkin olarak ele alır.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="c6fe1-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="c6fe1-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="c6fe1-115">`dotnet restore`(ya dotnet.exe ile vs ile gemi, ya da NetCore SDK 2.0.0 ile birlikte gelen)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="c6fe1-116">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c6fe1-116">Workaround</span></span>

1. <span data-ttu-id="c6fe1-117">Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın</span><span class="sxs-lookup"><span data-stu-id="c6fe1-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="c6fe1-118">Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="c6fe1-119">Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="c6fe1-120">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="c6fe1-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="c6fe1-121">Sorun</span><span class="sxs-lookup"><span data-stu-id="c6fe1-121">Issue</span></span>

<span data-ttu-id="c6fe1-122">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="c6fe1-123">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="c6fe1-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="c6fe1-125">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c6fe1-125">Workaround</span></span>

<span data-ttu-id="c6fe1-126">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="c6fe1-127">Alternatif olarak, silme `project.lock.json` ve yeniden geri deneyin.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="c6fe1-128">Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz</span><span class="sxs-lookup"><span data-stu-id="c6fe1-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="c6fe1-129">Sorun</span><span class="sxs-lookup"><span data-stu-id="c6fe1-129">Issue</span></span>

<span data-ttu-id="c6fe1-130">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="c6fe1-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="c6fe1-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="c6fe1-132">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c6fe1-132">Workaround</span></span>

<span data-ttu-id="c6fe1-133">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="c6fe1-134">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="c6fe1-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="c6fe1-135">Sorun</span><span class="sxs-lookup"><span data-stu-id="c6fe1-135">Issue</span></span>

<span data-ttu-id="c6fe1-136">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="c6fe1-137">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="c6fe1-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="c6fe1-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="c6fe1-139">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="c6fe1-139">Workaround</span></span>

<span data-ttu-id="c6fe1-140">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="c6fe1-141">NuGet 4.3 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="c6fe1-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="c6fe1-142">[NuGet 4.0 RTM Yayın Notları](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="c6fe1-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="c6fe1-143">Özellikler</span><span class="sxs-lookup"><span data-stu-id="c6fe1-143">Features</span></span>

- <span data-ttu-id="c6fe1-144">NuGet Geri Yükleme Perf'i geliştirin - Komut satırı geri yüklemeleri ve VS için akıllı NoOp [uygulayın](https://github.com/NuGet/Home/issues/5080) - #5080</span><span class="sxs-lookup"><span data-stu-id="c6fe1-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="c6fe1-145">NET Core 2.0: VS/Dotnet CLI mevcut NuGet işlevselliğini kullanmaya başlamalı: FallBack klasörleri - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="c6fe1-146">NET Core 2.0: Kullanıcıların belirli geri yükleme uyarılarını (veya hataya yükseltmeyi) yok saymalarını sağlama [- #4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="c6fe1-147">NET Core 2.0: CLI lokalize derlemeler - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="c6fe1-148">NET Core 2.0: tüm uyarıları/hataları varlık dosyasına kaydedin (PackageTargetFallback dahil) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="c6fe1-149">TFM desteğini etkinleştirin: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="c6fe1-150">NuGet.Core ve NuGet.Client projelerinin (ve dolayısıyla DL'lerin) sayısını #2446 [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="c6fe1-151">Nuget uyarılarını hata olarak işaretleme özelliği ekleme - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="c6fe1-152">Hatalar</span><span class="sxs-lookup"><span data-stu-id="c6fe1-152">Bugs</span></span>

- <span data-ttu-id="c6fe1-153">msbuild /t:pack "DevelopmentDependency" parametresi ile başarısız olur "PackTask" görevi tarafından desteklenmez - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="c6fe1-154">PackagePath sonunda Windows dizin ayırıcı sıyrık değilse düzleştirilmiş içerik dosyaları için dizin yapısı - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="c6fe1-155">netcore projeleri kalkınmaBağımlılık olarak ayarı desteklemiyor - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="c6fe1-156">RestoreManagerPackage, Kullanıcı BirA ipliği ve kilitlenmemiş VS'yi engelleyen senkronize olarak yükleniyor - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="c6fe1-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="c6fe1-157">dotnet</span></span>
  - <span data-ttu-id="c6fe1-158">dotnetcore Geri Yükleme (& nedenle msbuild /t:restore) açık bir çözüm proje bağımlılığı ile projeleri atlar [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="c6fe1-159">Çözümünüzde aynı projeye atıfta bulunan ve farklı kasalarla başvuru yapan proje referansları varsa, geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="c6fe1-160">Bu da kasa bir fark olmadan, farklı göreli yolları etkiler - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="c6fe1-161">NuGet paketlerinden geri yüklenen çalıştırılabilir ler artık .NET Core 2.0 ile çalıştırılamaz - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="c6fe1-162">NuGet.exe çözüm dosyasını ayrıştırken istisnanın ayrıntılarını yutar - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="c6fe1-163">ContentTargetFolders Windows'da '/' ile biten bir yol içeriyorsa Paket içerik dosyalarını yanlış konuma getirir - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="c6fe1-164">Netcoreapp1.1 hedefleyen bir araç paketi için Bir DotNetCliToolReference geri [yükleyemezsiniz](https://github.com/NuGet/Home/issues/4396) - #4396</span><span class="sxs-lookup"><span data-stu-id="c6fe1-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="c6fe1-165">Nuget güncelleştirmecli proje dosyasında (C++) eski paket sürüm koşulu bırakır - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="c6fe1-166">DCRs</span><span class="sxs-lookup"><span data-stu-id="c6fe1-166">DCRs</span></span>

- <span data-ttu-id="c6fe1-167">CPS nomation gelen DotnetCliToolTargetFramework okuyun - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="c6fe1-168">TPMinV kontrol pj tarzı UWP için çalışması gerekir - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="c6fe1-169">Otomatik Başvurulan paketler için Ara Kullanma Arabirimi açıklamasını geliştirme - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="c6fe1-170">NuGet geri yükleme çalışma zamanı bölümünden varlıkları derleme seçiyor.</span><span class="sxs-lookup"><span data-stu-id="c6fe1-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="c6fe1-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="c6fe1-172">Bağımlılık tanılamayı kilit dosyasına koyun - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="c6fe1-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="c6fe1-173">4.3 RTM'de düzeltilen GitHub sorunlarına bağlantılar</span><span class="sxs-lookup"><span data-stu-id="c6fe1-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="c6fe1-174">Sorunlar Listesi</span><span class="sxs-lookup"><span data-stu-id="c6fe1-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
