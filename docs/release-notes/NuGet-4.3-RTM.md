---
title: NuGet 4,3 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,3 RTM için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780173"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="d1fa7-103">NuGet 4,3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d1fa7-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="d1fa7-104">[Visual Studio 2017 15,3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , .NET Standard 2.0/. NET Core 2,0 gibi yeni senaryolar için destek ekleyen NUGET 4,3 RTM ile gelir ve birçok kalite düzeltmesi içerir ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="d1fa7-105">Bu sürüm ayrıca, anlamsal sürüm oluşturma 2.0.0, NuGet uyarıları ve hatalarının MSBuild tümleştirmesi ve daha fazlası için destek gibi çeşitli geliştirmeler de getirir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="d1fa7-106">Özet: 4.3.0 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d1fa7-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="d1fa7-107">Özet: 4.3.1 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="d1fa7-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="d1fa7-108">Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="d1fa7-109">Güvenlik onarımı: NUPKGs içindeki dosyaların, NUPKG dizininin üzerinde göreli bir yolu olabilir [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="d1fa7-110">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="d1fa7-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="d1fa7-111">NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir</span><span class="sxs-lookup"><span data-stu-id="d1fa7-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="d1fa7-112">Sorun</span><span class="sxs-lookup"><span data-stu-id="d1fa7-112">Issue</span></span>

<span data-ttu-id="d1fa7-113">Aşağıdaki geri yükleme komut satırı teknikleri devre dışı paket kaynaklarını etkin olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="d1fa7-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="d1fa7-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="d1fa7-115">`dotnet restore` (VS ile birlikte gelen dotnet.exe veya NetCore SDK 2.0.0 ile birlikte gelen bir ile birlikte)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="d1fa7-116">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="d1fa7-116">Workaround</span></span>

1. <span data-ttu-id="d1fa7-117">Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın</span><span class="sxs-lookup"><span data-stu-id="d1fa7-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="d1fa7-118">Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="d1fa7-119">Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="d1fa7-120">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="d1fa7-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="d1fa7-121">Sorun</span><span class="sxs-lookup"><span data-stu-id="d1fa7-121">Issue</span></span>

<span data-ttu-id="d1fa7-122">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="d1fa7-123">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="d1fa7-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="d1fa7-125">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="d1fa7-125">Workaround</span></span>

<span data-ttu-id="d1fa7-126">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="d1fa7-127">Alternatif olarak, ' yi silmeyi `project.lock.json` ve geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="d1fa7-128">NuGet Paket Yöneticisi 'Ni kullanarak Dotnetclıtools 'u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="d1fa7-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="d1fa7-129">Sorun</span><span class="sxs-lookup"><span data-stu-id="d1fa7-129">Issue</span></span>

<span data-ttu-id="d1fa7-130">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="d1fa7-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="d1fa7-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="d1fa7-132">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="d1fa7-132">Workaround</span></span>

<span data-ttu-id="d1fa7-133">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="d1fa7-134">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="d1fa7-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="d1fa7-135">Sorun</span><span class="sxs-lookup"><span data-stu-id="d1fa7-135">Issue</span></span>

<span data-ttu-id="d1fa7-136">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="d1fa7-137">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="d1fa7-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="d1fa7-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="d1fa7-139">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="d1fa7-139">Workaround</span></span>

<span data-ttu-id="d1fa7-140">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="d1fa7-141">NuGet 4,3 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="d1fa7-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="d1fa7-142">[Nuget 4,0 RTM sürüm notları](../release-notes/nuget-4.0-RTM.md) -NUGET 4,0 RTM için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="d1fa7-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="d1fa7-143">Özellikler</span><span class="sxs-lookup"><span data-stu-id="d1fa7-143">Features</span></span>

- <span data-ttu-id="d1fa7-144">NuGet geri yükleme performansını iyileştirme-komut satırı geri yüklemeleri ve VS- [#5080](https://github.com/NuGet/Home/issues/5080) için daha akıllı noop uygulayın</span><span class="sxs-lookup"><span data-stu-id="d1fa7-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="d1fa7-145">NET Core 2,0: VS/DotNet CLı var olan NuGet işlevlerini kullanmaya başlamalıdır: geri dönüş klasörleri- [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="d1fa7-146">NET Core 2,0: kullanıcıların belirli geri yükleme uyarılarını yok saymasını sağlama (veya hataya yükseltme)- [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="d1fa7-147">NET Core 2,0: CLı yerelleştirilmiş derlemeler- [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="d1fa7-148">NET Core 2,0: varlıklar dosyasına tüm uyarıları/hataları Kaydet (PackageTargetFallback dahil)- [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="d1fa7-149">TFı desteğini etkinleştir: NetStandard 2.0, Tizen- [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="d1fa7-150">NuGet. Core ve NuGet. Client projelerinin (ve bu nedenle dll 'Ler) sayısını azaltın- [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="d1fa7-151">NuGet uyarılarını hata olarak işaretleme özelliği ekleyin- [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="d1fa7-152">Hatalar</span><span class="sxs-lookup"><span data-stu-id="d1fa7-152">Bugs</span></span>

- <span data-ttu-id="d1fa7-153">MSBuild/t: paket "DevelopmentDependency" parametresi ile başarısız olur "Pacgörevinin SK" görevi- [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="d1fa7-154">PackagePath- [#4795](https://github.com/NuGet/Home/issues/4795) sonunda Windows dizin ayırıcı EKİF ise düzleştirilmiş içerik dosyaları için dizin yapısı</span><span class="sxs-lookup"><span data-stu-id="d1fa7-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="d1fa7-155">netcore projeleri, [#4694](https://github.com/NuGet/Home/issues/4694) developmentDependency olarak ayarlamayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="d1fa7-156">RestoreManagerPackage, engellenen UI iş parçacığı ve kilitlenen VS- [#4679](https://github.com/NuGet/Home/issues/4679) zaman uyumlu olarak yüklendi</span><span class="sxs-lookup"><span data-stu-id="d1fa7-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="d1fa7-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="d1fa7-157">dotnet</span></span>
  - <span data-ttu-id="d1fa7-158">dotnetcore geri yükleme (& bu nedenle MSBuild/t: restore) açık bir çözüm proje bağımlılığı olan projeleri atlar [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="d1fa7-159">Çözümünüz farklı bir büyük harfe sahip aynı projeye başvuruda bulunan başvuruları 'a sahipse, geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="d1fa7-160">Bu, büyük/küçük harf farklılığı olmadan farklı göreli yolları da etkiler [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="d1fa7-161">NuGet paketlerinden geri yüklenen yürütülebilir dosyalar artık .NET Core 2,0 ile yürütülebilir değildir [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="d1fa7-162">NuGet.exe SWA, çözüm dosyası ayrıştırılırken özel durumun ayrıntılarına izin veriyor- [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="d1fa7-163">ContentTargetFolders, Windows 'de '/' ile biten bir yol içeriyorsa, paket içerik dosyalarını yanlış konuma koyar. [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="d1fa7-164">Netcoreapp 1.1 'i hedefleyen bir Araçlar paketi için Dotnetclientoolreference geri yüklenemiyor- [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="d1fa7-165">NuGet güncelleştirme CLı, proje dosyasında (C++) eski paket sürümü koşulunu bırakır- [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="d1fa7-166">DCR</span><span class="sxs-lookup"><span data-stu-id="d1fa7-166">DCRs</span></span>

- <span data-ttu-id="d1fa7-167">CPS nouç- [#5397](https://github.com/NuGet/Home/issues/5397) DotnetCliToolTargetFramework 'ü okuyun</span><span class="sxs-lookup"><span data-stu-id="d1fa7-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="d1fa7-168">TPMinV Check, PJ stili UWP- [#4763](https://github.com/NuGet/Home/issues/4763) için çalışmalıdır</span><span class="sxs-lookup"><span data-stu-id="d1fa7-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="d1fa7-169">Oto başvurulan paketler için Kullanıcı arabirimi açıklamasını iyileştirme- [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="d1fa7-170">NuGet geri yükleme, çalışma zamanı 'ndan varlıkları derle bölümünde seçiliyor.</span><span class="sxs-lookup"><span data-stu-id="d1fa7-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="d1fa7-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="d1fa7-172">Kilit dosyasına bağımlılık tanılamayı yerleştir- [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="d1fa7-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="d1fa7-173">4,3 RTM 'de düzeltilen GitHub sorunlarına yönelik bağlantılar</span><span class="sxs-lookup"><span data-stu-id="d1fa7-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="d1fa7-174">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="d1fa7-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
