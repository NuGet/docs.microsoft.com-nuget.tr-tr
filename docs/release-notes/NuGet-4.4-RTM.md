---
title: NuGet 4,4 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,4 RTM için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901713"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="6264a-103">NuGet 4,4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6264a-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="6264a-104">[Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , NUGET 4,4 RTM ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6264a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="6264a-105">Özet: 4.4.0 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="6264a-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="6264a-106">Özet: 4.4.2 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="6264a-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="6264a-107">Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="6264a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="6264a-108">Özet: 4.4.3 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="6264a-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="6264a-109">Güvenlik onarımı: NUPKGs içindeki dosyaların, NUPKG dizininin üzerinde göreli bir yolu olabilir [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="6264a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6264a-110">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="6264a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6264a-111">.NET Framework & NuGet ile .NET Standard 2,0 ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="6264a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6264a-112">.NET Standard & aracı .NET Framework, .NET Standard 2,0 veya önceki sürümleri hedefleyen projeler & NuGet paketlerini tüketebileceği şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6264a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6264a-113">[Bu belgede, bu](https://github.com/dotnet/standard/issues/481) senaryonun etrafındaki sorunlar, bunları ele almak için plan ve BT 'nin araç durumuyla birlikte dağıtabileceğiniz geçici çözümler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="6264a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="6264a-114">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="6264a-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="6264a-115">Sorun</span><span class="sxs-lookup"><span data-stu-id="6264a-115">Issue</span></span>

<span data-ttu-id="6264a-116">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="6264a-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="6264a-117">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="6264a-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="6264a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="6264a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="6264a-119">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6264a-119">Workaround</span></span>

<span data-ttu-id="6264a-120">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="6264a-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="6264a-121">Alternatif olarak, ' yi silmeyi `project.lock.json` ve geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6264a-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6264a-122">NuGet Paket Yöneticisi 'Ni kullanarak Dotnetclıtools 'u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="6264a-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6264a-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="6264a-123">Issue</span></span>

<span data-ttu-id="6264a-124">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="6264a-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6264a-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6264a-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6264a-126">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6264a-126">Workaround</span></span>

<span data-ttu-id="6264a-127">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="6264a-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6264a-128">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="6264a-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6264a-129">Sorun</span><span class="sxs-lookup"><span data-stu-id="6264a-129">Issue</span></span>

<span data-ttu-id="6264a-130">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="6264a-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6264a-131">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="6264a-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6264a-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6264a-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6264a-133">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6264a-133">Workaround</span></span>

<span data-ttu-id="6264a-134">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="6264a-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="6264a-135">.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor</span><span class="sxs-lookup"><span data-stu-id="6264a-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="6264a-136">Sorun</span><span class="sxs-lookup"><span data-stu-id="6264a-136">Issue</span></span>

<span data-ttu-id="6264a-137">Bazen, geçersiz imzalı bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' değeriyle ayarlandığında, bu durum paket otomatik geri yüklemesinin sonsuz döngüde çalışmasına neden oluyor (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="6264a-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="6264a-138">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6264a-138">Workaround</span></span>

<span data-ttu-id="6264a-139">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="6264a-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="6264a-140">NuGet 4,4 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="6264a-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="6264a-141">[Nuget 4,3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -NUGET 4,3 RTM için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="6264a-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="6264a-142">Özellikler</span><span class="sxs-lookup"><span data-stu-id="6264a-142">Features</span></span>

- <span data-ttu-id="6264a-143">PMC ve NuGet PM Kullanıcı arabirimi senaryolarında basit çözüm yükü desteği- [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="6264a-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="6264a-144">MSBuild paketi hedefinin, Kullanıcı hedeflerini kendisinden önce çalıştırmak için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="6264a-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="6264a-145">Özellik: NuGet yüklemesine dependencyVersion anahtarı ekleme- [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="6264a-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="6264a-146">uıap 10.0. TODO. 0, NuGet- [#5684](https://github.com/NuGet/Home/issues/5684) için .NET Standard 2,0 ile eşleşmelidir</span><span class="sxs-lookup"><span data-stu-id="6264a-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="6264a-147">MSBuild/t: restore- [#5562](https://github.com/NuGet/Home/issues/5562) Ile Visual Studio derleme araçları SKU desteği</span><span class="sxs-lookup"><span data-stu-id="6264a-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="6264a-148">Geri yükleme sırasında .NET Standard 2,0 için .NET 4.6.1 desteği gerekliyse ancak yüklü değilse bir hata oluşturun [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="6264a-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="6264a-149">Paket KIMLIĞI ön ek ayırma istemci kullanıcı arabirimi- [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="6264a-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="6264a-150">dotnet.exe yerelleştirmeyi desteklemek için yerelleştirilmiş NuGet bileşenleri sunun [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="6264a-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="6264a-151">Hatalar</span><span class="sxs-lookup"><span data-stu-id="6264a-151">Bugs</span></span>

- <span data-ttu-id="6264a-152">Farklı proje yolu casler, geri yüklemenin Packagereferleri kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="6264a-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="6264a-153">Hata aralığına uyarı numarası ile hata kodları taşıma- [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="6264a-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="6264a-154">.NET Standard sürümünün hedef Framework ile uyumlu olduğu bilinmediği için yanıltıcı hata [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="6264a-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="6264a-155">Dosyaları kafa karıştırıcı lisanslarla test etme- [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="6264a-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="6264a-156">EndToEnd test şablonlarında eksik lisans üstbilgileri- [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="6264a-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="6264a-157">packages.config geri yükleme hataları NU1000 olarak gösterir- [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="6264a-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="6264a-158">nuget.exe yüklemesi, mono [#5741](https://github.com/NuGet/Home/issues/5741) üzerinde DisableParallelProcessing içermelidir</span><span class="sxs-lookup"><span data-stu-id="6264a-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="6264a-159">nuget.exe yüklemesi, önbelleğe almayı yanlışlıkla devre dışı bırakır- [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="6264a-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="6264a-160">Geri yükleme devre dışı olduğunda packages.config için restore komutunun çalıştırılması, yanlış ileti [#5718](https://github.com/NuGet/Home/issues/5718) görüntülüyor</span><span class="sxs-lookup"><span data-stu-id="6264a-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="6264a-161">ANLARA Restore devre dışı bırakıldığında restore komutunun çalıştırılması, karışık bir ileti [#5659](https://github.com/NuGet/Home/issues/5659) görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6264a-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="6264a-162">GetRestoreDotnetCliToolsTask eksik sürüm meta verileri olmadığında başarısız olur [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="6264a-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="6264a-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="6264a-163">dotnet</span></span>
  - <span data-ttu-id="6264a-164">dotnetcore ekleme paketi, bir csproj [#5697](https://github.com/NuGet/Home/issues/5697) boş satırları temizleyebilir</span><span class="sxs-lookup"><span data-stu-id="6264a-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="6264a-165">NuGet.Config kimlik bilgileri ayarlarının kaynak adları büyük/küçük harfe duyarlıdır [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="6264a-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="6264a-166">GeneratePackageOnBuild etkinleştiriliyor, tüm paket geçmişimin silinmesini- [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="6264a-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="6264a-167">Restore, mono. Cecil veya semver paketlerini geri yüklemeden, ancak diğer tüm paketler geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6264a-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="6264a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="6264a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="6264a-169">Hatalar ve uyarılar-bir kaynak kullanılamadığında hatalı hata.</span><span class="sxs-lookup"><span data-stu-id="6264a-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="6264a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="6264a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="6264a-171">[Designtutarlılığı] NuGet yükleme durumu metni şu anda koyu Temada doğru görünmüyor.</span><span class="sxs-lookup"><span data-stu-id="6264a-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="6264a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="6264a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="6264a-173">Tüm projeler için çözüm güncelleştirmelerinde/yüklemelerde paketleri Güncelleştir- [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="6264a-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="6264a-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="6264a-174">dotnet</span></span>
  - <span data-ttu-id="6264a-175">dotnetcore paketi, TargetFramework vs Targetçerçeveler 'e göre farklı davranır- [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="6264a-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="6264a-176">Araçlar klasörünün içindeki dahil edilen dll 'Ler uyarı oluştur- [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="6264a-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="6264a-177">NuGet. ContentModel dize işlemleri için çok fazla bellek tüketir- [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="6264a-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="6264a-178">RuntimeEnvironmentHelper. ıslinux, OSX [#4648](https://github.com/NuGet/Home/issues/4648) için true döndürüyor</span><span class="sxs-lookup"><span data-stu-id="6264a-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="6264a-179">' DotNet Pack ', nuspec öğesini obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644) yerine obj altına koyar</span><span class="sxs-lookup"><span data-stu-id="6264a-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="6264a-180">NuGet son derece yavaş paket yükseltmesi- [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="6264a-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="6264a-181">CPS, LSL (hafif çözüm geri yükleme) ile etkinleştirilmemiş daha büyük çözümlerle geri yükleme ile eşitlenmemiş. [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="6264a-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="6264a-182">SemVer 2,0-belirtilen sürüme sahip bir NuGet paketi meta verileri yoksayar (3.5.0-RTM-1938)- [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="6264a-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="6264a-183">Nuget.exe (3. +) sürüm numarası ve ExcludeVersion bayrağıyla paket yüklemesi, paketi daha yeni sürüme güncelleştirmez [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="6264a-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="6264a-184">En üst düzey paketler kısıtlamaları ihlal ediyor durumunda geri yükleme Project.jsuyarı almalıdır [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="6264a-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="6264a-185">-ConfigFile, install komutunda özel yapılandırma ayarlamadır- [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="6264a-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="6264a-186">nuget.exe yüklemesi '-DisableParallelProcessing ' anahtarını kabul etmez [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="6264a-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="6264a-187">DotNet.exe veya msbuild.exe tarafından hala kullanılan devre dışı kaynaklar [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="6264a-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="6264a-188">LSL senaryosunda onarım kilitleniyor- [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="6264a-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="6264a-189">DCR</span><span class="sxs-lookup"><span data-stu-id="6264a-189">DCRs</span></span>

- <span data-ttu-id="6264a-190">nuget.exe TargetFramework desteğini Install- [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="6264a-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="6264a-191">Farklı MSBuild görev UserAgent dizeleri (netcore vs Desktop MSBuild) ekleme- [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="6264a-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="6264a-192">PackagePathResolver. GetPackageDirectoryName sanal- [#5700](https://github.com/NuGet/Home/issues/5700) olmalıdır</span><span class="sxs-lookup"><span data-stu-id="6264a-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="6264a-193">[Designtutarlılığı] NuGet paketi eklenirken kafa karıştırıcı iletisi- [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="6264a-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="6264a-194">[Uyarılar ve hatalar] NoWarn, P2P başvuruları aracılığıyla geçişli olarak akış yapmaz [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="6264a-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="6264a-195">Hafif çözüm yükü: PM Kullanıcı arabirimi, PMC ve IVS-- [#5057](https://github.com/NuGet/Home/issues/5057) Için ortak çekirdek</span><span class="sxs-lookup"><span data-stu-id="6264a-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="6264a-196">Hafif çözüm yükü: destek-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="6264a-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="6264a-197">Visual Studio 'Nun tetiklediği ön geri yükleme MSBuild hedefi için destek ekleme ( [#4781](https://github.com/NuGet/Home/issues/4781) )</span><span class="sxs-lookup"><span data-stu-id="6264a-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="6264a-198">NuGet. targets öğesine BeforeTargets kullanılarak başvurulabilen bir genel hedef ekleyin- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="6264a-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="6264a-199">Paket hedefi, derleme eylemleri doğru şekilde contentFiles oluşturamaz- [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="6264a-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="6264a-200">RestoreOperationLogger.Do blokları iş parçacığı havuzu iş parçacıkları- [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="6264a-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="6264a-201">Docs</span><span class="sxs-lookup"><span data-stu-id="6264a-201">Docs</span></span>

- <span data-ttu-id="6264a-202">Install komutu DependencyVersion ve Framework bayrakları- [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="6264a-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="6264a-203">NuGet uyarıları ve hatalarıyla ilgili belgeleri güncelleştirme- [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="6264a-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="6264a-204">4,4 RTM 'de düzeltilen GitHub sorunlarına yönelik bağlantılar</span><span class="sxs-lookup"><span data-stu-id="6264a-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="6264a-205">Sorun listesi 1</span><span class="sxs-lookup"><span data-stu-id="6264a-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="6264a-206">Sorun listesi 2</span><span class="sxs-lookup"><span data-stu-id="6264a-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="6264a-207">Sorun listesi 3</span><span class="sxs-lookup"><span data-stu-id="6264a-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
