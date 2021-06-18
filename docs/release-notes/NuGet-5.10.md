---
title: NuGet 5,10 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,10 sürüm notları.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356541"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="ac401-103">NuGet 5,10 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ac401-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="ac401-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="ac401-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ac401-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="ac401-105">NuGet version</span></span> | <span data-ttu-id="ac401-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ac401-106">Available in Visual Studio version</span></span> | <span data-ttu-id="ac401-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ac401-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="ac401-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="ac401-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ac401-109">Visual Studio 2019 sürüm 16,10</span><span class="sxs-lookup"><span data-stu-id="ac401-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="ac401-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ac401-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="ac401-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="ac401-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="ac401-112">Visual Studio 16,10, MSBuild 16,10 ve .NET 5.0.300 + NuGet.exe 5,10 veya üzeri bir sürüm gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ac401-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="ac401-113">Özet: 5,10 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="ac401-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="ac401-114">İmzalama: DotNet güvenilir-signers komutunu uygulama- [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="ac401-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="ac401-115">Varsayılan doğrulamayı Linux üzerinde devre dışı bırak, ancak varsayılan olarak Windows- [#10713](https://github.com/NuGet/Home/issues/10713) 'de etkin yap</span><span class="sxs-lookup"><span data-stu-id="ac401-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="ac401-116">.NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742) 'de paket imzalama doğrulaması IÇIN bir env değişkeni ekleyin</span><span class="sxs-lookup"><span data-stu-id="ac401-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="ac401-117">Büyük çözümler için yeni paket performansını yüklemeyi geliştirme- [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="ac401-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="ac401-118">`nfproj`NUGET CLI Için Supportedprojec_1 listesine proje türünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac401-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="ac401-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="ac401-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ac401-120">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="ac401-120">Issues fixed in this release</span></span>

* <span data-ttu-id="ac401-121"><requireLicenseAcceptance>Proje paketleme sırasında öğeyi bastır- [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="ac401-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="ac401-122">[CPVM] Önizleme uyarısı DotNet CLI- [#10226](https://github.com/NuGet/Home/issues/10226) gösterilmelidir</span><span class="sxs-lookup"><span data-stu-id="ac401-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="ac401-123">PMUı 'nin arka plan ve ön plan rengi belirteçlerini, CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608) güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ac401-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="ac401-124">[Hata Bash] "İşlem Kullanıcı tarafından iptal edildi" hatası, PM Kullanıcı arabiriminde hızla sekmeler arasında geçiş yaparken Hata Listesi penceresinde göster [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="ac401-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="ac401-125">PM Kullanıcı arabirimi: çözüm düzeyinde paket yükleme performansını Iyileştirme- [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="ac401-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="ac401-126">GetService 'i NuGet. clients [#3784](https://github.com/NuGet/Home/issues/3784) her yerde GetServiceAsync değiştirin</span><span class="sxs-lookup"><span data-stu-id="ac401-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="ac401-127">`..`Göreli yol ile [#5016](https://github.com/NuGet/Home/issues/5016) paketi performans sorunu NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="ac401-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="ac401-128">"NuGet Pack" performansı, kaynak yollarında artan düzeyler ile düşüyor- [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="ac401-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="ac401-129">Yinelenen dosyalarla nuspec paketleme sırasında NuGet hata vermez.</span><span class="sxs-lookup"><span data-stu-id="ac401-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="ac401-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="ac401-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="ac401-131">NuGet paketi "belirtilen DateTimeOffset bir zip dosyası zaman damgasına dönüştürülemez"- [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="ac401-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="ac401-132">Paketlenmiş paketin dosyasının zaman damgaları, saat dilimi tarafından kaydırılacağı [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="ac401-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="ac401-133">NU1004 daha fazla işlem yapılabilir bilgi içermelidir [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="ac401-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="ac401-134">[Hata Bash] [Test hatası] Boş/hatalı biçimlendirilmiş kilit dosyası ' dotnet restore--Use-Lock-File--kilitli-Mode '- [#8640](https://github.com/NuGet/Home/issues/8640) çalıştırılırken güncelleştirilmeyecek</span><span class="sxs-lookup"><span data-stu-id="ac401-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="ac401-135">NuGetVersionRange, mantıksal olarak yanlış aralıkların ayrıştırılmasını sağlar- [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="ac401-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="ac401-136">PM Kullanıcı arabirimi, seçili ve vurgulanan paket kaynakları arasında ayırt edilemeyen bir arka plan rengi gösteremez- [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="ac401-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="ac401-137">Yüklenecek projeleri, ekran okuyucu tarafından okunmayacak şekilde seçme onay kutusu- [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="ac401-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="ac401-138">Ayrıntılar bölmesi sürümler açılan menüsü varsayılan seçimi, yüklü/güncelleştirmeler sekmelerinde yüklü/yerinde olmalıdır- [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="ac401-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="ac401-139">Bazı .NET 5 SDK 'ları için geçici çözüm hesabını kaldırma #9913 targetplatformbilinen adı ` ,Version= `  -  [](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="ac401-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="ac401-140">DotNet NuGet doğrulaması çok sessiz- [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="ac401-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="ac401-141">VersionRange tek basamaklı aralıkları ayrıştıramıyor- [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="ac401-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="ac401-142">VS Solution Manager, hata ayıklama sırasında için null özel durumu oluşturur- [#10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="ac401-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="ac401-143">CLı özel durum iletilerini dize kaynak dosyalarına taşıma- [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="ac401-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="ac401-144">Ölü kodu Kaldır (TabItemButtonAutomationPeer)- [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="ac401-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="ac401-145">Bağlam menüsünü Güncelleştir- [#10498](https://github.com/NuGet/Home/issues/10498) ilk seçili öğeye kaydırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="ac401-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="ac401-146">Çözüm PMUI ayrıntıları çakışan yatay çubuğa sahip [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="ac401-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="ac401-147">İmzalama: sertifikanın süre dolduğunda ve zaman damgası güvenilir değil olduğunda birincil imza ayrıntıları gösterilmez. [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="ac401-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="ac401-148">Etkin olmayan hiçbir kaynak olması, PM Kullanıcı arabiriminin şunu göstermesini önler [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="ac401-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="ac401-149">Paket meta verileri (Ayrıntılar, kullanımdan kaldırma) bazen CodeSpaces 'daki nuget.org 'tan çekilmemelidir [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="ac401-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="ac401-150">Hata ayıklama oturumu sırasında PMUI başlatması özel durumla başarısız oluyor- [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="ac401-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="ac401-151">big endian sistem [#10567](https://github.com/NuGet/Home/issues/10567) üzerinde bir paket bütünlük denetimi hatasına yönelik NuGet geri yükleme sonuçları</span><span class="sxs-lookup"><span data-stu-id="ac401-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="ac401-152">PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595) yerine FormatException oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="ac401-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="ac401-153">CPVM-grafik yürüme algoritmasındaki eşzamanlılık sorunları- [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="ac401-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="ac401-154">PMC PowerShell sürüm telemetrisi ekleme- [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="ac401-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="ac401-155">NuGetVersion sıralama performansını iyileştirme- [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="ac401-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="ac401-156">Güvenilir-sonuçcılar ekleme işlemi tutarsız bağımsız değişkenlere sahip- [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="ac401-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="ac401-157">Vs2019 v 16.9.0: NuGet Paket Yöneticisi 'ndeki sekmelerin "Updates" iken "yüklü" olarak değiştirilmesi çerçeveyi güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="ac401-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="ac401-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="ac401-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="ac401-159">"V" öğesini PMUI- [#10677](https://github.com/NuGet/Home/issues/10677) sürüm numarasından kaldır</span><span class="sxs-lookup"><span data-stu-id="ac401-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="ac401-160">Inugetprojectservice. Getınstalınstaltesync, CPS proje sistemi aday [#10681](https://github.com/NuGet/Home/issues/10681) almadan önce oluşturur</span><span class="sxs-lookup"><span data-stu-id="ac401-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="ac401-161">Katıştırılmış simgeler, "Microsoft Visual Studio çevrimdışı paketler" kaynağından, gezinme sekmesinde erişim engellendi- [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="ac401-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="ac401-162">Msbuildprojectsınspath ayarlandığında ınugetprojectservice. Getınstallationpackagesasync oluşturulur [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="ac401-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="ac401-163">"DotNet NuGet Remove Source nuget.org" ilk [#10745](https://github.com/NuGet/Home/issues/10745) çalışmaz</span><span class="sxs-lookup"><span data-stu-id="ac401-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="ac401-164">NuGet zaman uyumsuz bir yöntemde işlem parçacığı iş parçacığını engeller- [#10775](https://github.com/NuGet/Home/issues/10775) zaman uyumlu bir çağrı yapar</span><span class="sxs-lookup"><span data-stu-id="ac401-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="ac401-165">Araçlar-> seçenekler-> NuGet Paket Yöneticisi dizesi kesildi- [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="ac401-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="ac401-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` etkin olmayan kod ve performans için [#10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="ac401-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="ac401-167">NuGet SDK paketlerinde Embedded simgesini kullanın- [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="ac401-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="ac401-168">SPDX lisans listesini güncelleştirme- [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="ac401-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="ac401-169">**[Bu yayında düzeltilen tüm sorunların listesi-5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="ac401-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="ac401-170">**[Bu sürümdeki işlemelerin listesi-5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="ac401-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="ac401-171">Topluluk katkıları</span><span class="sxs-lookup"><span data-stu-id="ac401-171">Community contributions</span></span>

<span data-ttu-id="ac401-172">Bu NuGet yayınını harika hale getirmek için size yardımcı olan tüm katkıda bulunanlar için teşekkürler!</span><span class="sxs-lookup"><span data-stu-id="ac401-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="ac401-173">Sağlayan</span><span class="sxs-lookup"><span data-stu-id="ac401-173">Who</span></span>|<span data-ttu-id="ac401-174">PR 'ler</span><span class="sxs-lookup"><span data-stu-id="ac401-174">PRs</span></span>|<span data-ttu-id="ac401-175">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="ac401-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="ac401-176">louo-z</span><span class="sxs-lookup"><span data-stu-id="ac401-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="ac401-177">3991</span><span class="sxs-lookup"><span data-stu-id="ac401-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="ac401-178">VersionRange tek basamaklı aralıkları ayrıştıramıyor- [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="ac401-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="ac401-179">omajıd</span><span class="sxs-lookup"><span data-stu-id="ac401-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="ac401-180">3860</span><span class="sxs-lookup"><span data-stu-id="ac401-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="ac401-181">NuGet. Client build.sh bozuk [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="ac401-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="ac401-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="ac401-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="ac401-183">3623</span><span class="sxs-lookup"><span data-stu-id="ac401-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="ac401-184">NuGet. Client build.sh bozuk [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="ac401-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="ac401-185">BlackICE</span><span class="sxs-lookup"><span data-stu-id="ac401-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="ac401-186">3953</span><span class="sxs-lookup"><span data-stu-id="ac401-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="ac401-187">"NuGet Pack" performansı, kaynak yollarında artan düzeyler ile düşüyor- [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="ac401-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="ac401-188">BlackICE</span><span class="sxs-lookup"><span data-stu-id="ac401-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="ac401-189">3953</span><span class="sxs-lookup"><span data-stu-id="ac401-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="ac401-190">İle NuGet.exe paketi performans sorunu..</span><span class="sxs-lookup"><span data-stu-id="ac401-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="ac401-191">göreli yol- [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="ac401-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="ac401-192">Marcin-kronyıstianc</span><span class="sxs-lookup"><span data-stu-id="ac401-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="ac401-193">3940</span><span class="sxs-lookup"><span data-stu-id="ac401-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="ac401-194">CPVM-grafik yürüme algoritmasındaki eşzamanlılık sorunları- [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="ac401-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="ac401-195">josesimoes</span><span class="sxs-lookup"><span data-stu-id="ac401-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="ac401-196">3943</span><span class="sxs-lookup"><span data-stu-id="ac401-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="ac401-197">Nfproj proje türünü NuGet CLı için Supportedprojec_1 listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac401-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="ac401-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="ac401-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="ac401-199">Geri bildirim hoş geldiniz</span><span class="sxs-lookup"><span data-stu-id="ac401-199">Feedback welcome</span></span>

<span data-ttu-id="ac401-200">Görüşleriniz bizim için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="ac401-200">Your feedback is important to us.</span></span>  <span data-ttu-id="ac401-201">Bu sürümle ilgili herhangi bir sorun varsa GitHub Sorunları [sayfamızı ve mevcut Visual Studio Geliştirici Topluluğu](https://github.com/NuGet/Home/issues) bakın. [](https://developercommunity.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="ac401-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="ac401-202">NuGet içindeki yeni sorunlar için lütfen bir [GitHub Sorunu rapor edin.](https://github.com/NuGet/Home/issues/new)</span><span class="sxs-lookup"><span data-stu-id="ac401-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="ac401-203">Genel NuGet deneyimi sorunları için Yardım [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ve Sorun Bildir altında sık kullanılan IDE'niz içinde bulunan **bir sorun > bize bildirebilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="ac401-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
