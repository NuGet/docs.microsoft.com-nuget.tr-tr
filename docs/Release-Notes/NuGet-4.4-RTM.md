---
title: "NuGet 4.4 RTM sürüm notları | Microsoft Docs"
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
ms.openlocfilehash: 1ef62b53eda4b71871e3bff855fdc5c64b04c20b
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="28ed7-104">NuGet 4,4 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="28ed7-104">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="28ed7-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.4 RTM ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="28ed7-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="28ed7-106">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="28ed7-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="28ed7-107">.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları</span><span class="sxs-lookup"><span data-stu-id="28ed7-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="28ed7-108">.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="28ed7-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="28ed7-109">[Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.</span><span class="sxs-lookup"><span data-stu-id="28ed7-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="28ed7-110">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="28ed7-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="28ed7-111">Sorun</span><span class="sxs-lookup"><span data-stu-id="28ed7-111">Issue</span></span>

<span data-ttu-id="28ed7-112">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="28ed7-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="28ed7-113">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="28ed7-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="28ed7-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="28ed7-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="28ed7-115">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="28ed7-115">Workaround</span></span>

<span data-ttu-id="28ed7-116">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="28ed7-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="28ed7-117">Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="28ed7-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="28ed7-118">Nuget Paket Yöneticisi’ni kullanarak DotNetCLITools’u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="28ed7-118">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="28ed7-119">Sorun</span><span class="sxs-lookup"><span data-stu-id="28ed7-119">Issue</span></span>

<span data-ttu-id="28ed7-120">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="28ed7-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="28ed7-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="28ed7-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="28ed7-122">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="28ed7-122">Workaround</span></span>

<span data-ttu-id="28ed7-123">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="28ed7-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="28ed7-124">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="28ed7-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="28ed7-125">Sorun</span><span class="sxs-lookup"><span data-stu-id="28ed7-125">Issue</span></span>

<span data-ttu-id="28ed7-126">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="28ed7-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="28ed7-127">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="28ed7-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="28ed7-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="28ed7-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="28ed7-129">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="28ed7-129">Workaround</span></span>

<span data-ttu-id="28ed7-130">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="28ed7-130">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="28ed7-131">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="28ed7-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="28ed7-132">Sorun</span><span class="sxs-lookup"><span data-stu-id="28ed7-132">Issue</span></span>

<span data-ttu-id="28ed7-133">Bazen, bir derlemeyi imzası geçersiz olan veya paket sürümü ile 'DateTime' borsa takip ayarlandığında içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde (dotnet/project-sistem #1457) çalıştırmak geri yükle neden olur.</span><span class="sxs-lookup"><span data-stu-id="28ed7-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="28ed7-134">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="28ed7-134">Workaround</span></span>

<span data-ttu-id="28ed7-135">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="28ed7-135">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="28ed7-136">4.4 NuGet RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="28ed7-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="28ed7-137">[NuGet 4.3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -NuGet 4.3 RTM için sabit tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="28ed7-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="28ed7-138">Özellikler</span><span class="sxs-lookup"><span data-stu-id="28ed7-138">Features</span></span>

- <span data-ttu-id="28ed7-139">Basit çözüm yük desteği senaryolarda - PMC ve NuGet PM UI [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="28ed7-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="28ed7-140">Msbuild paketi hedef kendisini önce-çalışan kullanıcı hedefleri için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="28ed7-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="28ed7-141">Özelliği: nuget yüklemek için - dependencyVersion anahtar eklemek [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="28ed7-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="28ed7-142">uap10.0.TODO.0 .NET standart 2.0 için NuGet - eşleme [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="28ed7-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="28ed7-143">Msbuild /t:restore ile - Visual Studio derleme araçları SKU Destek [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="28ed7-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="28ed7-144">.NET standart 2.0 gerekli ancak yüklenmeyen - .NET 4.6.1 desteği olursa geri yükleme sırasında bir hata oluştur [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="28ed7-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="28ed7-145">Paket kimliği öneki ayırma istemci UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="28ed7-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="28ed7-146">yerelleştirilmiş nuget bileşenleri dotnet.exe yerelleştirme - desteklemek için teslim [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="28ed7-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="28ed7-147">Hatalar</span><span class="sxs-lookup"><span data-stu-id="28ed7-147">Bugs</span></span>

- <span data-ttu-id="28ed7-148">Farklı proje yolu kasası geri PackageReferences - kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="28ed7-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="28ed7-149">Hata kodları uyarı numaralarıyla hata aralığa - taşıma [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="28ed7-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="28ed7-150">.NET standart sürümü ile hedef framework - uyumlu olacak şekilde bilinmiyor olduğunda hata yanıltıcı [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="28ed7-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="28ed7-151">Test dosyalarını kafa karıştırıcı lisansların - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="28ed7-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="28ed7-152">EndToEnd eksik lisans üstbilgilerinde test şablonları - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="28ed7-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="28ed7-153">Packages.config geri yükleme hataları NU1000 - gösterir [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="28ed7-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="28ed7-154">nuget.exe yükleme mono üzerinde - DisableParallelProcessing olmalıdır [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="28ed7-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="28ed7-155">nuget.exe yükleme yanlış devre dışı bırakır önbelleğe alma - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="28ed7-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="28ed7-156">Geri yükleme devre dışı bırakıldığında packages.config hatalı ileti - görüntüler için restore komutu çalıştıran VS [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="28ed7-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="28ed7-157">VS; Geri yükleme devre dışı bırakıldığında geri yükleme komutu çalıştırılarak görüntüler kafa karıştırıcı bir ileti - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="28ed7-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="28ed7-158">GetRestoreDotnetCliToolsTask başarısız eksik sürüm meta verileri - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="28ed7-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="28ed7-159">DotNet eklemek paket csproj - boş satırları temizlemek [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="28ed7-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="28ed7-160">NuGet.Config kimlik bilgisi ayarları kaynak adları büyük küçük harf duyarlı - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="28ed7-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="28ed7-161">Silinen paketler - tüm my geçmişini GeneratePackageOnBuild etkinleştirme [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="28ed7-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="28ed7-162">Geri yükleme mono.cecil veya semver paket geri yüklemez, ancak diğer tüm paketler geri.</span><span class="sxs-lookup"><span data-stu-id="28ed7-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="28ed7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="28ed7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="28ed7-164">Hatalar ve uyarılar - bozuk hata bir kaynak yokken kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="28ed7-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="28ed7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="28ed7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="28ed7-166">[DesignConsistency] Şu anda NuGet yükleme durumu metni koyu tema doğru görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="28ed7-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="28ed7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="28ed7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="28ed7-168">Güncelleştirme paketleri çözüm güncelleştirmeleri/yüklemelerinde tüm projeleri - adresindeki [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="28ed7-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="28ed7-169">DotNet paketi TargetFramework vs TargetFrameworks - bağlı olarak farklı şekilde davranan [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="28ed7-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="28ed7-170">DLL'leri içinde Araçlar klasörü throw uyarılar - dahil [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="28ed7-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="28ed7-171">NuGet.ContentModel dize işlemleri için-çok fazla bellek tüketir [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="28ed7-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="28ed7-172">RuntimeEnvironmentHelper.IsLinux döndürür true OSX için - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="28ed7-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="28ed7-173">'dotnet pack' koyar obj obj\Debug - yerine altında nuspec [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="28ed7-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="28ed7-174">Nuget paket yükseltme - son derece yavaş [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="28ed7-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="28ed7-175">Geri yükleme (Basit çözüm geri yükle) - LSL üzerinde açık henüz büyük çözümlerle ile eşitlenmemiş CPS [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="28ed7-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="28ed7-176">SemVer 2.0 - nuget paketi ile meta veriler (3.5.0-rtm-1938) - sürüm yoksayar sağlanan [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="28ed7-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="28ed7-177">Nuget.exe (3. +), sürüm numarasıyla paketini yükleyin ve ExcludeVersion bayrağı değil güncelleştirme paketinin daha yeni sürüme - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="28ed7-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="28ed7-178">Project.JSON geri yükleme üst düzey paketleri kısıtlamaları - ihlal olduğunda uyar [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="28ed7-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="28ed7-179">-ConfigFile değil ayarı özel yapılandırma yükleme komutunda - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="28ed7-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="28ed7-180">nuget.exe yükleme dikkate değil '-DisableParallelProcessing' geçiş - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="28ed7-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="28ed7-181">Devre dışı hala DotNet.exe veya msbuild.exe - tarafından kullanılan kaynakları [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="28ed7-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="28ed7-182">Askıda LSL senaryoda - düzeltme [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="28ed7-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="28ed7-183">Dcr</span><span class="sxs-lookup"><span data-stu-id="28ed7-183">DCRs</span></span>

- <span data-ttu-id="28ed7-184">nuget.exe yükleme TargetFramework desteği - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="28ed7-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="28ed7-185">Farklı msbuild görev UserAgent dizeleri (netcore vs Masaüstü msbuild) - eklemek [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="28ed7-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="28ed7-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="28ed7-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="28ed7-187">[DesignConsistency] Bir NuGet paketi - eklerken ileti kafa karıştırıcı [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="28ed7-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="28ed7-188">[Uyarı ve hataların] NoWarn akan geçişli P2P başvurular arasında - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="28ed7-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="28ed7-189">Basit çözüm yük: Ortak çekirdek PM UI, PMC ve Iv'ler-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="28ed7-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="28ed7-190">Basit çözüm yük: Destek - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="28ed7-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="28ed7-191">İçin destek eklemek Visual Studio tetikler - MSBuild hedef önceden geri [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="28ed7-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="28ed7-192">Ortak bir hedef BeforeTargets kullanarak başvurulabilir NuGet.targets Ekle- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="28ed7-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="28ed7-193">Paketi hedef oluşturamıyor Content dosyaları yapı eylemleri ile doğru - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="28ed7-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="28ed7-194">RestoreOperationLogger.Do engeller iş parçacığı havuzu iş parçacıkları - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="28ed7-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="28ed7-195">Docs</span><span class="sxs-lookup"><span data-stu-id="28ed7-195">Docs</span></span>

- <span data-ttu-id="28ed7-196">Yükleme için belgeleri komut DependencyVersion ve Framework bayrakları - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="28ed7-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="28ed7-197">Belgeleri NuGet uyarıları ve hataları - güncelleştirmeye [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="28ed7-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="28ed7-198">GitHub sorunları 4,4 RTM'de sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="28ed7-198">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="28ed7-199">1 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="28ed7-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="28ed7-200">2 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="28ed7-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="28ed7-201">3 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="28ed7-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
