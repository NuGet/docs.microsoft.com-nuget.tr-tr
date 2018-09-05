---
title: NuGet 4.4 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548420"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="91139-103">NuGet 4.4 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="91139-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="91139-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 4.4 NuGet RTM ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="91139-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="91139-105">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="91139-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="91139-106">.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="91139-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="91139-107">.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="91139-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="91139-108">[Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.</span><span class="sxs-lookup"><span data-stu-id="91139-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="91139-109">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="91139-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="91139-110">Sorun</span><span class="sxs-lookup"><span data-stu-id="91139-110">Issue</span></span>

<span data-ttu-id="91139-111">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="91139-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="91139-112">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="91139-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="91139-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="91139-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="91139-114">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="91139-114">Workaround</span></span>

<span data-ttu-id="91139-115">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="91139-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="91139-116">Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yüklemeyi.</span><span class="sxs-lookup"><span data-stu-id="91139-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="91139-117">Görüntülenemiyor, eklenemiyor veya Nuget Paket Yöneticisi'ni kullanarak dotnetclıtools'u başlatamadı</span><span class="sxs-lookup"><span data-stu-id="91139-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="91139-118">Sorun</span><span class="sxs-lookup"><span data-stu-id="91139-118">Issue</span></span>

<span data-ttu-id="91139-119">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="91139-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="91139-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="91139-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="91139-121">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="91139-121">Workaround</span></span>

<span data-ttu-id="91139-122">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="91139-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="91139-123">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="91139-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="91139-124">Sorun</span><span class="sxs-lookup"><span data-stu-id="91139-124">Issue</span></span>

<span data-ttu-id="91139-125">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="91139-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="91139-126">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="91139-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="91139-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="91139-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="91139-128">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="91139-128">Workaround</span></span>

<span data-ttu-id="91139-129">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="91139-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="91139-130">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="91139-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="91139-131">Sorun</span><span class="sxs-lookup"><span data-stu-id="91139-131">Issue</span></span>

<span data-ttu-id="91139-132">Bazen, geçersiz imzalı veya paket sürümü 'DateTime' değeriyle ayarlandığında bir derlemeyi içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde (dotnet/project-system #1457) çalıştırmak geri neden olur.</span><span class="sxs-lookup"><span data-stu-id="91139-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="91139-133">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="91139-133">Workaround</span></span>

<span data-ttu-id="91139-134">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="91139-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="91139-135">4.4 NuGet RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="91139-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="91139-136">[NuGet 4.3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -4.3 NuGet RTM için sabit tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="91139-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="91139-137">Özellikler</span><span class="sxs-lookup"><span data-stu-id="91139-137">Features</span></span>

- <span data-ttu-id="91139-138">Basit çözüm yükü desteği senaryolarda - PMC ve NuGet PM UI [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="91139-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="91139-139">Msbuild paketi hedef kendisini önce-çalışan kullanıcı hedefleri için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="91139-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="91139-140">Özellik: nuget yüklemesi için - dependencyVersion anahtar ekleme [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="91139-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="91139-141">uap10.0.TODO.0 .NET Standard 2.0 NuGet için - harita [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="91139-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="91139-142">Msbuild/t: Restore ile - Visual Studio derleme araçları SKU'nun Destek [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="91139-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="91139-143">.NET Standard 2.0 gerekli ancak yüklenmeyen - .NET 4.6.1 desteği, geri yükleme sırasında bir hata oluşturur. [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="91139-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="91139-144">Paket kimliği ön eki ayırma istemci kullanıcı Arabirimi - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="91139-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="91139-145">yerelleştirilmiş nuget bileşenlerini dotnet.exe yerelleştirme - desteklemek için teslim [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="91139-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="91139-146">Hatalar</span><span class="sxs-lookup"><span data-stu-id="91139-146">Bugs</span></span>

- <span data-ttu-id="91139-147">Farklı proje yolu büyük, geri yükleme - PackageReferences kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="91139-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="91139-148">Hata aralığı - uyarı numaralarını hata kodlarıyla taşıma [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="91139-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="91139-149">.NET Standard sürümünü hedef çerçeve ile - uyumlu olacak şekilde bilinmiyor, hata yanıltıcı [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="91139-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="91139-150">Test dosyaları kafa karıştırıcı lisansların - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="91139-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="91139-151">Şablonlar - EndToEnd eksik lisans üstbilgilerinde test [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="91139-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="91139-152">Packages.config geri yükleme - NU1000 hatalar gösterir [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="91139-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="91139-153">nuget.exe yüklemesi üzerinde mono - DisableParallelProcessing olmalıdır [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="91139-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="91139-154">nuget.exe yüklemesi hatalı devre dışı bırakır önbelleğe alma - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="91139-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="91139-155">Yanlış ileti - geri yükleme devre dışı bırakıldığında packages.config görüntüler için restore komutu çalıştıran VS [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="91139-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="91139-156">VS; Geri yükleme devre dışı bırakıldığında geri yükleme komutu çalıştırılarak - kafa karıştırıcı bir ileti görüntüler [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="91139-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="91139-157">Başarısız GetRestoreDotnetCliToolsTask sürümü meta veriler eksik - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="91139-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="91139-158">DotNet</span><span class="sxs-lookup"><span data-stu-id="91139-158">dotnet</span></span>
  - <span data-ttu-id="91139-159">dotnetcore ekleme paket bir csproj - boş satırları temizleyerek [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="91139-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="91139-160">Kimlik bilgileri ayarları NuGet.Config içinde kaynak adlarını büyük küçük harfe duyarlıdır - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="91139-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="91139-161">Silinmiş paketler - tüm geçmişim GeneratePackageOnBuild etkinleştirme [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="91139-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="91139-162">Geri yükleme mono.cecil veya semver paketleri geri yüklemez, ancak diğer tüm paketleri geri.</span><span class="sxs-lookup"><span data-stu-id="91139-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="91139-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="91139-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="91139-164">Hataları ve Uyarıları - hatalı hata bir kaynak zaman içinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="91139-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="91139-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="91139-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="91139-166">[DesignConsistency] Şu anda NuGet yüklemesi durum metni koyu tema doğru görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="91139-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="91139-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="91139-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="91139-168">Güncelleştirme paketleri, çözüm güncelleştirmeleri/yükler için tüm projeleri için - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="91139-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="91139-169">DotNet</span><span class="sxs-lookup"><span data-stu-id="91139-169">dotnet</span></span>
  - <span data-ttu-id="91139-170">dotnetcore paketi TargetFramework vs TargetFrameworks - bağlı olarak farklı şekilde davranan [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="91139-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="91139-171">DLL Araçlar klasörü throw uyarıları - dahil [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="91139-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="91139-172">NuGet.ContentModel - dize işlemleri için çok fazla bellek tüketir [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="91139-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="91139-173">RuntimeEnvironmentHelper.IsLinux true döndürürse OSX için - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="91139-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="91139-174">'dotnet paketi' obj obj\Debug - yerine altında nuspec koyar [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="91139-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="91139-175">Nuget paket yükseltmesi - çok yavaş [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="91139-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="91139-176">Geri yükleme işlemi (Basit çözüm geri yükleme) - LSL üzerinde açık henüz büyük çözümleri ile eşitlenmemiş CPS [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="91139-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="91139-177">2.0 - SemVer nuget paketi ile sağlanan sürüm meta verileri (3.5.0-rtm-1938) - yoksayar [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="91139-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="91139-178">Nuget.exe (3. +), sürüm numarasıyla paketini yükleyin ve ExcludeVersion bayrağı olmayan güncelleştirme paketinin daha yeni bir sürüme - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="91139-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="91139-179">Project.JSON geri yükleme üst düzey paketleri kısıtlamaları - ihlal olduğunda uyar [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="91139-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="91139-180">-ConfigFile ayarlamıyor özel yapılandırma yükleme komutunda - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="91139-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="91139-181">nuget.exe yüklemesi değil dikkate '-DisableParallelProcessing' anahtarı - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="91139-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="91139-182">Hala DotNet.exe veya msbuild.exe - tarafından kullanılan kaynakları devre dışı [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="91139-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="91139-183">LSL senaryoda - askıda düzeltme [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="91139-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="91139-184">Dcr</span><span class="sxs-lookup"><span data-stu-id="91139-184">DCRs</span></span>

- <span data-ttu-id="91139-185">nuget.exe TargetFramework desteği - yükleme [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="91139-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="91139-186">Farklı bir msbuild görevi UserAgent dizeleri (netcore vs Masaüstü msbuild) - ekleme [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="91139-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="91139-187">PackagePathResolver.GetPackageDirectoryName sanal - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="91139-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="91139-188">[DesignConsistency] Bir NuGet paketi - eklerken ileti kafa karıştırıcı [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="91139-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="91139-189">[Uyarılar ve hatalar] NoWarn akan geçişli P2P başvuruları - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="91139-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="91139-190">Basit çözüm yükü: Ortak çekirdek PM Kullanıcı Arabirimi, PMC ve Iv'lerin-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="91139-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="91139-191">Basit çözüm yükü: Desteği - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="91139-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="91139-192">İçin destek ekleyerek Visual Studio tetikler - MSBuild hedefi önceden geri [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="91139-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="91139-193">Ortak bir hedef BeforeTargets kullanılarak başvurulabilen NuGet.targets Ekle- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="91139-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="91139-194">Paketi hedef oluşturamıyor contentFiles yapı eylemleri ile doğru şekilde - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="91139-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="91139-195">İş parçacığı havuzu iş parçacıkları - RestoreOperationLogger.Do engeller [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="91139-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="91139-196">Docs</span><span class="sxs-lookup"><span data-stu-id="91139-196">Docs</span></span>

- <span data-ttu-id="91139-197">Docs yüklenmesi için komut bayrakları DependencyVersion ve Framework - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="91139-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="91139-198">Güncelleştirme için NuGet uyarı ve hataları - docs [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="91139-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="91139-199">GitHub sorunları 4.4 RTM'de sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="91139-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="91139-200">1 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="91139-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="91139-201">2 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="91139-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="91139-202">3 sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="91139-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
