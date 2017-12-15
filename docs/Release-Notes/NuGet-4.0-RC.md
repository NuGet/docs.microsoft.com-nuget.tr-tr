---
title: "NuGet 4.0 RC sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: fa64825d-5908-4abe-9792-d70766d6e2ff
description: "NuGet 4.0 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 4.0 RC sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer: kraigb
ms.openlocfilehash: aa1c43be7ac0640bb5e118a162616acb36d44a83
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="40-rc-release-notes"></a><span data-ttu-id="ce673-104">4.0 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ce673-104">4.0 RC Release Notes</span></span>

[<span data-ttu-id="ce673-105">NuGet 3.5 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ce673-105">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="ce673-106">[NuGet 4.0 RC için Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) .NET Core senaryolar için destek ekleyerek, başlıca müşteri geri bildirimlerine adresleme ve çeşitli senaryolarda performansı iyileştirme odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ce673-106">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="ce673-107">Bu sürüm, NuGet MSBuild hedefleri, arka plan paket geri yükleme ve daha fazlasını komutları PackageReference, desteği gibi çeşitli iyileştirmeler getirir.</span><span class="sxs-lookup"><span data-stu-id="ce673-107">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ce673-108">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="ce673-108">Bug Fixes</span></span>

* <span data-ttu-id="ce673-109">Davranış değişiklikleri `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="ce673-109">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

* <span data-ttu-id="ce673-110">makine "15" yalnızca vs nuget.exe geri yükleme başarısız - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="ce673-110">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

* <span data-ttu-id="ce673-111">. NETCore dosya yeni proje geri yükleme sırasında - yapı engelleme [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="ce673-111">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

* <span data-ttu-id="ce673-112">ASP.NET Core web uygulaması, VS "15", geri yükleyemedi VS2015 geçirildi.</span><span class="sxs-lookup"><span data-stu-id="ce673-112">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="ce673-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="ce673-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

* <span data-ttu-id="ce673-114">[Test hatası] Paket 'jQuery doğrulama' PM UI tarafından - kaldırılamıyor [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="ce673-114">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

* <span data-ttu-id="ce673-115">Bir paket UWP'ye yüklü olduğunda `project.json`, üst projeleri de geri yüklenmelidir - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="ce673-115">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

* <span data-ttu-id="ce673-116">Normal - yerine yüksek ayrıntı olarak paket kaynaklarını oturum NuGet hedefleri değiştirme [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="ce673-116">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

* <span data-ttu-id="ce673-117">Varsayılan olarak - dotnet pack3 XML belgeleri içermelidir [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="ce673-117">dotnet pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

* <span data-ttu-id="ce673-118">Toplu güncelleştirme paketi olmadan kaynağıdır ilk ve tüm kaynak seçildiğinde - kullanıcı Arabiriminden başarısız [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="ce673-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

* <span data-ttu-id="ce673-119">Nuget Paketi komutu tüm dosyaları - içermez [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="ce673-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

* <span data-ttu-id="ce673-120">OOM sorunu - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="ce673-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

* <span data-ttu-id="ce673-121">Varlıklar dosyasının ProjectFileDependencyGroups bölümü, kitaplık adları - projelerde kullanmalıdır [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="ce673-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

* <span data-ttu-id="ce673-122">"dotnet geri yükleme" ve dizinleri - recursing [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="ce673-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

* <span data-ttu-id="ce673-123">Restore3 hataları, uyarıları hataları - yerine olarak kaydedilir [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="ce673-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

* <span data-ttu-id="ce673-124">TFS sorun: "[dosya] çalışma alanında bulunan olmaması veya erişmek için izniniz yok"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="ce673-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

* <span data-ttu-id="ce673-125">Yazarak "nuget <packagename>" vs üzerinde Hızlı Başlat Arama kutusuna "nuget" öneki - tutar [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="ce673-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

* <span data-ttu-id="ce673-126">System.Xml.XmlException: Çekirdek özellikler bölümü tanınmayan kök öğe.</span><span class="sxs-lookup"><span data-stu-id="ce673-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="ce673-127">2 satır, 2 konum.</span><span class="sxs-lookup"><span data-stu-id="ce673-127">Line 2, position 2.</span></span><span data-ttu-id="ce673-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="ce673-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

* <span data-ttu-id="ce673-129">`.nuspec`ile kaçışlı &lt; veya &gt; metin alanları artık oluşturur - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="ce673-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

* <span data-ttu-id="ce673-130">nuget.exe Sil (etkileşimli olmayan modda olduğundan) kimlik bilgilerini - isteyebilir olmaz [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="ce673-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

* <span data-ttu-id="ce673-131">nuget.exe delete uyarır yerel kaynakları için API anahtarı hakkında hiçbir - mantıklıdır olsa bile [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="ce673-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

* <span data-ttu-id="ce673-132">EF - öncesi paket - yüklerken hata deneyimi düşük [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="ce673-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

* <span data-ttu-id="ce673-133">Visual Studio kilitlendi seçimi değiştirdikten sonra çalışırken Paket Yöneticisi'nde - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="ce673-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

* <span data-ttu-id="ce673-134">DotNet geri yükleme kayan sürümleri kullanıldığında - bu büyük küçük harfe duyarlı kimliği aramaları düz liste yerel depoları üzerinde gerçekleştirir [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="ce673-134">Dotnet restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

* <span data-ttu-id="ce673-135">V2 akış için - nuget.exe delete bozulur [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="ce673-135">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

* <span data-ttu-id="ce673-136">nuget.exe gönderme zaman aşımı gerekiyor daha iyi bir hata iletisi - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="ce673-136">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

* <span data-ttu-id="ce673-137">Aracı geri yükleme uygun olmadan sessizce başarısız alır.</span><span class="sxs-lookup"><span data-stu-id="ce673-137">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="ce673-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="ce673-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

* <span data-ttu-id="ce673-139">NuGet ister olduğunda özel bir akış bile nuget.org - yüklerken kimlik bilgilerini girmek için [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="ce673-139">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

* <span data-ttu-id="ce673-140">Applicationınsights 2.0 Paketi listelenir, ancak henüz - yok [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="ce673-140">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

* <span data-ttu-id="ce673-141">UIDelay vs'de "15" preview 5 dal - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="ce673-141">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

* <span data-ttu-id="ce673-142">UWP için-derleme sırasında geri yükleme için ilk OnBuild olay eksik [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="ce673-142">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

* <span data-ttu-id="ce673-143">PowerShell5 sonları EntityFramework yüklensin mi?</span><span class="sxs-lookup"><span data-stu-id="ce673-143">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="ce673-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="ce673-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

* <span data-ttu-id="ce673-145">Kaynağı için ayrıntılı günlük kaydı Ekle (düşünün. 3.5 için) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="ce673-145">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

* <span data-ttu-id="ce673-146">Nuget istemci sürümünün 3.4 + - dikkate alınır değil NoCache parametresi [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="ce673-146">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

* <span data-ttu-id="ce673-147">VS üzerinde yüklemek bir kimlik bilgisi sağlayıcısı başarısız olduğunda, NuGet - kesmeyin [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="ce673-147">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>


## <a name="features"></a><span data-ttu-id="ce673-148">Özellikler</span><span class="sxs-lookup"><span data-stu-id="ce673-148">Features</span></span>

* <span data-ttu-id="ce673-149">CI x86-çalışacak şekilde ayarlanmış [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="ce673-149">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

* <span data-ttu-id="ce673-150">Otomatik geri yükleme 3/3: olmayan engelleme UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="ce673-150">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

* <span data-ttu-id="ce673-151">Otomatik geri yükleme 2/3: arka plan Adaylığı - geri yükleme [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="ce673-151">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

* <span data-ttu-id="ce673-152">Proje başvuruları yapı davranışını (recurse) - eşleşecek şekilde geri [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="ce673-152">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

* <span data-ttu-id="ce673-153">DPL destek VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="ce673-153">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

* <span data-ttu-id="ce673-154">Program dosyaları için - ayarları dosya taşıma [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="ce673-154">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

* <span data-ttu-id="ce673-155">Oluşturulan geri yükleme özellik ve hedefleri gereksinim katılım desteği - arası hedefleme [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="ce673-155">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

* <span data-ttu-id="ce673-156">PackageTargetFallback (f.k.a içeri aktarmalar) - NuGet geri yükleme desteği [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="ce673-156">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

* <span data-ttu-id="ce673-157">ToolsRef uygulama - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="ce673-157">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

* <span data-ttu-id="ce673-158">RID - Restore3 [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="ce673-158">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

* <span data-ttu-id="ce673-159">NuGet Ekle/Kaldır/güncelleştirme PackageRefs - desteklemek için kullanıcı Arabirimi [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="ce673-159">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

* <span data-ttu-id="ce673-160">: Otomatik 1/3 proje önbelleğe alma yoluyla API Adaylığı Implemenation geri bilgisi - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="ce673-160">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

* <span data-ttu-id="ce673-161">[0] NuGet geri görev & hedefleri - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="ce673-161">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

* <span data-ttu-id="ce673-162">[1] etkinleştir çözüm düzeyinde geri yükleme MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="ce673-162">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

* <span data-ttu-id="ce673-163">Visual Studio'da - kimlik bilgisi sağlayıcısı ortak genişletilebilirlik desteği [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="ce673-163">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

* <span data-ttu-id="ce673-164">Özyinelemeli nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="ce673-164">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

* <span data-ttu-id="ce673-165">Gönderilemiyor Microsoft.TeamFoundation.Client dev15 yük, VS "15" için 15.0 Microsoft.TeamFoundation.Client sürüm güncellemeniz gerekiyor Önizleme - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="ce673-165">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

* <span data-ttu-id="ce673-166">Yüklenemiyor C++ pakete C++ UWP projesi VS üzerinde "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="ce673-166">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

* <span data-ttu-id="ce673-167">Nupkg \buildCrossTargeting\ klasör - destekler ve içeri aktarmak için gereksinim duyduğu `.targets`  /  `.props` "crosstargeting" MSBuild kapsam için.</span><span class="sxs-lookup"><span data-stu-id="ce673-167">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="ce673-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="ce673-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

* <span data-ttu-id="ce673-169">ToolsReference tasarım - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="ce673-169">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

* <span data-ttu-id="ce673-170">NuGet içinde PackageReferences ve geri yükleme desteği için kullanıcı Arabirimi düzeltme `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="ce673-170">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

* <span data-ttu-id="ce673-171">VS Paket Yöneticisi ayarları - ekleme Önbelleği Temizle düğmesine [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="ce673-171">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="ce673-172">Dcr</span><span class="sxs-lookup"><span data-stu-id="ce673-172">DCRs</span></span>

* <span data-ttu-id="ce673-173">Otomatik geri yükleme sürerken çözüm geri yükleme engellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="ce673-173">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="ce673-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="ce673-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

* <span data-ttu-id="ce673-175">NuGet Paket Yöneticisi kullanıcı Arabirimi NetCore yükle yükler için paket destekleyen - olanları yerine her TFM [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="ce673-175">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

* <span data-ttu-id="ce673-176">API DotNetCliToolsReferences çok desteklemesi gerekir nominator geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ce673-176">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="ce673-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="ce673-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

* <span data-ttu-id="ce673-178">Bizim VS "15" işaretlemek systemcomponent - olarak VSIX [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="ce673-178">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

* <span data-ttu-id="ce673-179">MS başvuran geçirin. VS. MS Services.Client. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="ce673-179">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

* <span data-ttu-id="ce673-180">$(RestoreLegacyPackagesDirectory) dikkate geri yükleme ile - proje düzeyinde [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="ce673-180">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

* <span data-ttu-id="ce673-181">Tek TargetFramework projeyle geri özellik - değil koşul gerekir [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="ce673-181">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

* <span data-ttu-id="ce673-182">DotNet restore3 foo.csproj projectref bağımlılıkları izleyin ve bu çok geri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce673-182">dotnet restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="ce673-183">Yapı gibi.</span><span class="sxs-lookup"><span data-stu-id="ce673-183">Like build.</span></span><span data-ttu-id="ce673-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="ce673-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

* <span data-ttu-id="ce673-185">"type": "platform" bağımlılıkları temsil "türünde": kilit dosyası - "paketi" [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="ce673-185">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

* <span data-ttu-id="ce673-186">nuget.exe ayrıntılı mod indirme Göster url - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="ce673-186">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

* <span data-ttu-id="ce673-187">NuGet xplat taşıyın Microsoft.NetCore.App ve netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="ce673-187">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

* <span data-ttu-id="ce673-188">Push - olmalıdır simge sunucusunu komut satırından - itme olduğunda geçersiz kılmanıza olanak [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="ce673-188">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

* <span data-ttu-id="ce673-189">Genel bulmak için kod birleştirmek paketleri yol - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="ce673-189">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

* <span data-ttu-id="ce673-190">SuppressParent - daha iyi bir ada ihtiyacınız [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="ce673-190">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

* <span data-ttu-id="ce673-191">Belirlemek `project.json` MSBuild projelerine - kullanılacak bağımlılık adı [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="ce673-191">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

* <span data-ttu-id="ce673-192">SemVer 2.0.0 desteği eklemek için NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="ce673-192">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

* <span data-ttu-id="ce673-193">Geçişli bağımlılık NuPkgs izin ile `.targets` Msbuild'de - kullanılabilir olması için [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="ce673-193">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

* <span data-ttu-id="ce673-194">Komut satırı NuGet geri VS - önemli ölçüde daha yavaş [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="ce673-194">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

* <span data-ttu-id="ce673-195">Paket Kimliğini ve sürümünü karşılaştırmayı büyük küçük harfe duyarlı - yapmak [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="ce673-195">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

* <span data-ttu-id="ce673-196">İçin NoCache seçeneği çalışmıyor `packages.config` tabanlı geri yükleme/yüklemeye (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="ce673-196">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

* <span data-ttu-id="ce673-197">FindPackageByIdResource kaynakları gereken bir varsayılan önbellek içeriği ve Günlükçü - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="ce673-197">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
