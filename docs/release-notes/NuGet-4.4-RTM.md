---
title: NuGet 4.4 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498694"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="0c5d2-103">NuGet 4.4 Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="0c5d2-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="0c5d2-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.4 RTM ile birlikte geliyor.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="0c5d2-105">Özeti: 4.4.0 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="0c5d2-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="0c5d2-106">Özeti: 4.4.2 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="0c5d2-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="0c5d2-107">Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır</span><span class="sxs-lookup"><span data-stu-id="0c5d2-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="0c5d2-108">Özeti: 4.4.3 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="0c5d2-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="0c5d2-109">Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906</span><span class="sxs-lookup"><span data-stu-id="0c5d2-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="0c5d2-110">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="0c5d2-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0c5d2-111">.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="0c5d2-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="0c5d2-112">.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0c5d2-113">[Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="0c5d2-114">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="0c5d2-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="0c5d2-115">Sorun</span><span class="sxs-lookup"><span data-stu-id="0c5d2-115">Issue</span></span>

<span data-ttu-id="0c5d2-116">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="0c5d2-117">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="0c5d2-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="0c5d2-119">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="0c5d2-119">Workaround</span></span>

<span data-ttu-id="0c5d2-120">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="0c5d2-121">Alternatif olarak, silme `project.lock.json` ve yeniden geri deneyin.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="0c5d2-122">Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz</span><span class="sxs-lookup"><span data-stu-id="0c5d2-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="0c5d2-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="0c5d2-123">Issue</span></span>

<span data-ttu-id="0c5d2-124">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="0c5d2-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="0c5d2-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="0c5d2-126">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="0c5d2-126">Workaround</span></span>

<span data-ttu-id="0c5d2-127">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="0c5d2-128">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="0c5d2-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="0c5d2-129">Sorun</span><span class="sxs-lookup"><span data-stu-id="0c5d2-129">Issue</span></span>

<span data-ttu-id="0c5d2-130">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="0c5d2-131">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="0c5d2-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="0c5d2-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="0c5d2-133">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="0c5d2-133">Workaround</span></span>

<span data-ttu-id="0c5d2-134">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="0c5d2-135">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="0c5d2-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="0c5d2-136">Sorun</span><span class="sxs-lookup"><span data-stu-id="0c5d2-136">Issue</span></span>

<span data-ttu-id="0c5d2-137">Bazen, geçersiz imzalı bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' değeriyle ayarlandığında, bu durum paket otomatik geri yüklemesinin sonsuz döngüde çalışmasına neden oluyor (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="0c5d2-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="0c5d2-138">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="0c5d2-138">Workaround</span></span>

<span data-ttu-id="0c5d2-139">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="0c5d2-140">NuGet 4.4 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="0c5d2-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="0c5d2-141">[NuGet 4.3 RTM Yayın Notları](../release-notes/nuget-4.3-RTM.md) - NuGet 4.3 RTM için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="0c5d2-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="0c5d2-142">Özellikler</span><span class="sxs-lookup"><span data-stu-id="0c5d2-142">Features</span></span>

- <span data-ttu-id="0c5d2-143">PMC ve NuGet PM UI senaryolarında Hafif Çözüm Yükü Desteği - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="0c5d2-144">msbuild paketi hedef kendisinden önce kullanıcı hedefleri çalıştırmak için bir kamu kanca olmalıdır - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="0c5d2-145">Özellik: Nuget yüklemeye bağımlılıkeklemeSürümü anahtarı - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="0c5d2-146">uap10.0.TODO.0 NuGet için .NET Standart 2.0 haritası - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="0c5d2-147">Destek Visual Studio Build Tools SKU ile msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="0c5d2-148">Geri yükleme sırasında .NET Standart 2.0 için .NET 4.6.1 desteği gerekiyorsa ancak yüklü değilse hata oluşturma - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="0c5d2-149">Paket Kimlik öneki rezervasyon istemcisi UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="0c5d2-150">dotnet.exe yerelleştirmeyi desteklemek için yerelleştirilmiş nuget bileşenleri sunmak - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="0c5d2-151">Hatalar</span><span class="sxs-lookup"><span data-stu-id="0c5d2-151">Bugs</span></span>

- <span data-ttu-id="0c5d2-152">Farklı proje yolu kovanları PackageReferences kaybetmek geri yükleme neden olabilir - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="0c5d2-153">Uyarı numaraları yla hata kodlarını hata aralığına taşıma - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="0c5d2-154">.NET Standart sürümünün hedef çerçeveyle uyumlu olduğu bilinmediğinde yanıltıcı hata - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="0c5d2-155">Kafa karıştırıcı lisansları olan test dosyaları - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="0c5d2-156">EndToEnd test şablonlarında eksik lisans başlıkları - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="0c5d2-157">packages.config geri yükleme NU1000 olarak hataları gösterir - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="0c5d2-158">nuget.exe yüklemek mono üzerinde DisableParallelProcessing olmalıdır - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="0c5d2-159">nuget.exe yüklemek yanlış önbelleğe alma devre dışı - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="0c5d2-160">VS Geri Yükleme devre dışı bırakıldığında packages.config için geri yükleme komutunu çalıştırma yanlış ileti görüntüler - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="0c5d2-161">VS; Geri Yükleme devre dışı bırakıldığında geri yükleme komutunu çalıştırma kafa karıştırıcı bir ileti görüntüler - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="0c5d2-162">GetRestoreDotnetCliToolsTask sürüm meta veri eksik başarısız olur - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="0c5d2-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="0c5d2-163">dotnet</span></span>
  - <span data-ttu-id="0c5d2-164">dotnetcore paketi eklemek bir csproj boş satırları temizleyebilirsiniz - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="0c5d2-165">NuGet.Config'deki kimlik bilgisi ayarlarının kaynak adları büyük/küçük harf duyarlıdır - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="0c5d2-166">Enableing GeneratePackageOnBuild tüm paket geçmişimi sildi - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="0c5d2-167">Geri yükleme mono.cecil veya semver paketleri geri olmaz, ancak diğer tüm paketler geri olsun.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="0c5d2-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="0c5d2-169">Hatalar ve Uyarılar - bir kaynak kullanılamıyorsa hatalı hata.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="0c5d2-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="0c5d2-171">[DesignTutarlılık] NuGet Yükleme durum metni şu anda karanlık tema üzerinde doğru görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="0c5d2-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="0c5d2-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="0c5d2-173">Tüm projeler için çözüm güncellemelerinde/yüklemelerinde paketleri güncelleştirin - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="0c5d2-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="0c5d2-174">dotnet</span></span>
  - <span data-ttu-id="0c5d2-175">dotnetcore paketi TargetFramework vs TargetFrameworks bağlı olarak farklı çalışır - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="0c5d2-176">Araçlar klasörü içinde DLs dahil uyarılar atmak - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="0c5d2-177">NuGet.ContentModel dize işlemleri için çok fazla bellek tüketir - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="0c5d2-178">RuntimeEnvironmentHelper.IsLinux OSX için doğru döndürür - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="0c5d2-179">'dotnet paketi' obj\Debug yerine obj altında nuspec koyar - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="0c5d2-180">Nuget son derece yavaş paket yükseltme - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="0c5d2-181">CpS, LSL'yi (hafif çözüm geri yükleme) olmayan daha büyük çözümlerle Geri Yükleme ile senkronize değildir - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="0c5d2-182">SemVer 2.0 - sağlanan sürümü ile nuget paketi meta verileri (3.5.0-rtm-1938) yok sayar - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="0c5d2-183">Nuget.exe (3.+) Sürüm numarası ve ExcludeVersion bayrağı ile paketi yüklemek yeni sürüme paketi güncellemez - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="0c5d2-184">Project.json geri yüklemesi, üst düzey paketler kısıtlamaları ihlal ettiğinde uyarmalıdır - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="0c5d2-185">-ConfigFile yükleme komutu özel config ayar değil - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="0c5d2-186">nuget.exe yüklemek '-DisableParallelProcessing' anahtarı onurlandırmaz - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="0c5d2-187">Hala DotNet.exe veya msbuild.exe tarafından kullanılan engelli kaynakları - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="0c5d2-188">Düzeltme LSL senaryoda asılı - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0c5d2-189">DCRs</span><span class="sxs-lookup"><span data-stu-id="0c5d2-189">DCRs</span></span>

- <span data-ttu-id="0c5d2-190">nuget.exe install TargetFramework desteği - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="0c5d2-191">Farklı msbuild görev UserAgent dizeleri (netcore vs masaüstü msbuild) ekleyin - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="0c5d2-192">PackagePathResolver.GetPackageDirectoryName sanal olmalıdır - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="0c5d2-193">[DesignTutarlılık] NuGet paketi eklerken kafa karıştırıcı ileti - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="0c5d2-194">[Uyarılar ve hatalar] NoWarn, P2P referansları aracılığıyla geçişli olarak akmaz - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="0c5d2-195">Hafif Çözüm Yükü: PM UI, PMC ve IV'ler için ortak çekirdek- - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="0c5d2-196">Hafif Çözüm Yükü: Destek - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="0c5d2-197">Visual Studio'nun tetiklediği MSBuild hedefini geri yüklemeden önce destek ekleyin - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="0c5d2-198">Önce Hedefler kullanarak başvurulan nuget.hedeflerine ortak bir hedef ekleyin - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="0c5d2-199">Paket hedefi, yapı eylemleri yle içerik OluşturamazDosyaları doğru bir şekilde oluşturamaz - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="0c5d2-200">RestoreOperationLogger.Do bloklar iplik havuzu konuları - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="0c5d2-201">Docs</span><span class="sxs-lookup"><span data-stu-id="0c5d2-201">Docs</span></span>

- <span data-ttu-id="0c5d2-202">Yükleme komutu Bağımlılık ve Çerçeve bayrakları için Dokümanlar - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="0c5d2-203">NuGet uyarı ve hataları yla ilgili dokümanlara güncelleme - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="0c5d2-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="0c5d2-204">4.4 RTM'de düzeltilen GitHub sorunlarına bağlantılar</span><span class="sxs-lookup"><span data-stu-id="0c5d2-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="0c5d2-205">Sorunlar Listesi 1</span><span class="sxs-lookup"><span data-stu-id="0c5d2-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="0c5d2-206">Sorunlar Listesi 2</span><span class="sxs-lookup"><span data-stu-id="0c5d2-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="0c5d2-207">Sorunlar Listesi 3</span><span class="sxs-lookup"><span data-stu-id="0c5d2-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
