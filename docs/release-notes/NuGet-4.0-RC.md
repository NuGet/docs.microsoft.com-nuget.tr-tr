---
title: NuGet 4.0 RC Yayın Notları
description: Bilinen sorunları, hata düzeltmeleri, eklenen özellikler ve DCR'leri içeren NuGet 4.0 RC için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496637"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="066f8-103">NuGet 4.0 RC Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="066f8-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="066f8-104">NuGet 3.5 RTM Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="066f8-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="066f8-105">[Visual Studio 2017 için NuGet 4.0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0) ,NET Core senaryoları için destek eklemeye, önemli müşteri geri bildirimlerini ele almaya ve çeşitli senaryolarda performansı artırmaya odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="066f8-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="066f8-106">Bu sürüm PackageReference desteği, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yükleme ve daha fazlası gibi çeşitli iyileştirmeler getiriyor.</span><span class="sxs-lookup"><span data-stu-id="066f8-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="066f8-107">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="066f8-107">Bug Fixes</span></span>

- <span data-ttu-id="066f8-108">`dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838) davranış değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="066f8-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="066f8-109">nuget.exe geri yükleme vs "15" makine sadece başarısız olur - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="066f8-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="066f8-110">. NETCore dosya yeni proje geri yükleme sırasında yapı engellemelidir - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="066f8-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="066f8-111">ASP.NET Core web uygulaması, VS2015'ten VS "15"e geçti, geri yüklenememiştir.</span><span class="sxs-lookup"><span data-stu-id="066f8-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="066f8-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="066f8-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="066f8-113">[Test Hatası] Paket 'jQuery Doğrulama' PM UI tarafından kaldırılamaz - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="066f8-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="066f8-114">Bir paket UWP'ye `project.json`yüklendiğinde, ana projeler de geri yüklenmelidir - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="066f8-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="066f8-115">Paket kaynaklarını Normal yerine Yüksek ayrıntılı olarak günlüğe kaydetmek için NuGet hedeflerini [değiştirin](https://github.com/NuGet/Home/issues/3719) - #3719</span><span class="sxs-lookup"><span data-stu-id="066f8-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="066f8-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="066f8-116">dotnet</span></span>
  - <span data-ttu-id="066f8-117">dotnetcore pack3 varsayılan olarak XML belgeleri içermelidir - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="066f8-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="066f8-118">Paket olmadan kaynak ilk ve Tüm kaynak seçildiğinde Toplu İşlem Kullanıcı Tarafından başarısız olur - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="066f8-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="066f8-119">Nuget paketi komutu tüm dosyaları içermez - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="066f8-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="066f8-120">OOM sorunu - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="066f8-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="066f8-121">Varlıklar dosyasının ProjectFileDependencyGroups bölümü projeler için kitaplık adlarını kullanmalıdır - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="066f8-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="066f8-122">"dotnet geri yükleme" ve özgünlükleri yineleme - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="066f8-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="066f8-123">Geri yükleme3 hataları hata yerine uyarı olarak günlüğe kaydedilir - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="066f8-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="066f8-124">TFS sorunu: "[dosya]çalışma alanınızda bulunmuyor veya erişim izniniz yok" - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="066f8-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="066f8-125">Vs quicklaunch <packagename>arama kutusunda "nuget" yazmak "nuget" öneki tutar - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="066f8-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="066f8-126">System.Xml.XmlException: Çekirdek Özellikleri bölümünde tanınmayan kök öğesi.</span><span class="sxs-lookup"><span data-stu-id="066f8-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="066f8-127">Satır 2, pozisyon 2.</span><span class="sxs-lookup"><span data-stu-id="066f8-127">Line 2, position 2.</span></span><span data-ttu-id="066f8-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="066f8-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="066f8-129">`.nuspec`kaçan &lt; veya &gt; metin alanlarında artık oluşturur - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="066f8-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="066f8-130">nuget.exe silme kimlik bilgileri için istinamaz (etkileşimli olmayan modda) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="066f8-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="066f8-131">nuget.exe silme hiçbir mantıklı olsa bile, yerel kaynaklar için API Key hakkında uyarır - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="066f8-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="066f8-132">EF -pre paketi yüklerken hata deneyimi zayıf - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="066f8-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="066f8-133">Visual Studio Paket Yöneticisi seçimi değiştirdikten sonra çalışırken çöktü - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="066f8-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="066f8-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="066f8-134">dotnet</span></span>
  - <span data-ttu-id="066f8-135">dotnetcore geri yükleme kayan sürümleri kullanıldığında düz liste yerel depolarda durumda duyarlı Id aramaları gerçekleştirir - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="066f8-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="066f8-136">nuget.exe silme V2 beslemesi için bozuldu - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="066f8-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="066f8-137">nuget.exe push zaman aşımı daha iyi bir hata iletisi ihtiyacı - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="066f8-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="066f8-138">Uygun içeri aktarımlar olmadan araç geri yükleme sessizce başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="066f8-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="066f8-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="066f8-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="066f8-140">NuGet, nuget.org yükleme yaparken bile özel bir besleme olduğunda [#2346](https://github.com/NuGet/Home/issues/2346) kimlik bilgilerini girmek için #2346</span><span class="sxs-lookup"><span data-stu-id="066f8-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="066f8-141">ApplicationInsights 2.0 paketi listelenir ancak henüz yok - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="066f8-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="066f8-142">Vs "15" önizleme 5 şube de UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="066f8-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="066f8-143">İlk OnBuild olay UWP için Build sırasında Geri Yükleme için cevapsız - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="066f8-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="066f8-144">PowerShell5 EntityFramework yüklemek tatili?</span><span class="sxs-lookup"><span data-stu-id="066f8-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="066f8-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="066f8-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="066f8-146">Ayrıntılı günlüğe kaynak ekleyin (3,5 için düşünün) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="066f8-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="066f8-147">Nuget istemci sürümünde onurlandırılmayan NoCache parametresi 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="066f8-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="066f8-148">Bir kimlik bilgisi sağlayıcısı VS yüklemek için başarısız olduğunda, NuGet kırmak yok - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="066f8-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="066f8-149">Özellikler</span><span class="sxs-lookup"><span data-stu-id="066f8-149">Features</span></span>

- <span data-ttu-id="066f8-150">X86 çalıştırmak için CI ayarlayın - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="066f8-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="066f8-151">Otomatik Geri Yükleme 3/3: non engelleme Kullanıcı BiruAr - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="066f8-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="066f8-152">Otomatik Geri Yükleme 2/3: adaylık arka plan geri yükleme - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="066f8-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="066f8-153">Yapı davranışıyla eşleşecek şekilde proje hakemlerini geri yükleme (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="066f8-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="066f8-154">VS "15" DPL desteği - minber - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="066f8-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="066f8-155">Ayarlar dosyasını Program Dosyaları'na taşıma - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="066f8-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="066f8-156">Oluşturulan geri yükleme sahne ve hedefleri çapraz hedefleme katılım desteği gerekir - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="066f8-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="066f8-157">NuGet Geri Destek PackageTargetFallback (f.k.a İthalat) için - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="066f8-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="066f8-158">ToolsRef uygulaması - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="066f8-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="066f8-159">RID için Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="066f8-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="066f8-160">NuGet UI Paketi'nin Ekle/Kaldır/Güncellenisini destekleyecek - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="066f8-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="066f8-161">Otomatik Geri Yükleme 1/3: Önbelleğe Alma Projesi Geri Yükleme Bilgileri ile Adaylık API Implemenation - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="066f8-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="066f8-162">[0] NuGet Geri Yükleme Görev & Hedefleri - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="066f8-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="066f8-163">[1] MSBuild'te Çözüm düzeyi geri yüklemesini etkinleştir - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="066f8-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="066f8-164">Visual Studio'da kamu genişletilebilirliğini destekle - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="066f8-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="066f8-165">Özyinelemeli nuget geri yükleme - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="066f8-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="066f8-166">Microsoft.TeamFoundation.Client'ı dev15'e yükleyemiyorum, Microsoft.TeamFoundation.Client sürümünü VS "15" Önizlemeiçin 15.0 olarak güncelleştirmeli - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="066f8-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="066f8-167">VS "15" Preview'da C++ UWP projesine C++ paketi yükleneme - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="066f8-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="066f8-168">Nupkg \buildCrossTargeting\ klasörünü desteklemesi `.targets`  /  `.props` ve MSBuild kapsamını "çapraz hedefleme" için içe aktarması gerekir.</span><span class="sxs-lookup"><span data-stu-id="066f8-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="066f8-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="066f8-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="066f8-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="066f8-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="066f8-171">`.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455) w/ PackageReferences geri yüklemek için NuGet UI düzeltin</span><span class="sxs-lookup"><span data-stu-id="066f8-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="066f8-172">VS paket yöneticisi ayarlarına net önbellek düğmesi ekleme - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="066f8-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="066f8-173">DCRs</span><span class="sxs-lookup"><span data-stu-id="066f8-173">DCRs</span></span>

- <span data-ttu-id="066f8-174">Otomatik geri yükleme olurken Çözüm Geri Yükleme engellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="066f8-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="066f8-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="066f8-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="066f8-176">NuGet Paket Yöneticisi UI netcore yüklemek her TFM yükler , yerine paket destekler olanlar - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="066f8-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="066f8-177">Geri nominator API dotNetCliToolsReferences çok desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="066f8-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="066f8-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="066f8-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="066f8-179">Vs "15" vsix'imizi bir sistem bileşeni olarak [işaretleyin](https://github.com/NuGet/Home/issues/3700) - #3700</span><span class="sxs-lookup"><span data-stu-id="066f8-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="066f8-180">MS'e başvurudan geçirin. Vs. Services.Client - MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="066f8-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="066f8-181">$(RestoreLegacyPackagesDirectory) geri yükleyerek bir proje düzeyinde saygı gösterilmelidir - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="066f8-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="066f8-182">Tek bir TargetFramework ile projeye geri yükleme, sahne koşullandırmamalıdır - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="066f8-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="066f8-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="066f8-183">dotnet</span></span>
  - <span data-ttu-id="066f8-184">dotnetcore restore3 foo.csproj projectref bağımlılıkları takip etmeli ve bu da geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="066f8-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="066f8-185">İnşa etmek gibi.</span><span class="sxs-lookup"><span data-stu-id="066f8-185">Like build.</span></span><span data-ttu-id="066f8-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="066f8-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="066f8-187">"type": Kilit dosyasında "type":"package" olarak temsil edilen "platform" [Bağımlılıkları](https://github.com/NuGet/Home/issues/2695) - #2695</span><span class="sxs-lookup"><span data-stu-id="066f8-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="066f8-188">nuget.exe Verbose modu indirme url göstermelidir - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="066f8-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="066f8-189">Move NuGet xplat Microsoft.NetCore.App ve netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="066f8-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="066f8-190">İtme - Komut satırından iterken sembol sunucusugeçersiz kılmak mümkün olmalıdır - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="066f8-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="066f8-191">Küresel paketler yolunu bulmak için kodu birleştirin - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="066f8-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="066f8-192">SuppressParent daha iyi bir ada ihtiyacınız var - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="066f8-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="066f8-193">MSBuild projeleri için kullanılacak bağımlılık adını belirleme `project.json` - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="066f8-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="066f8-194">NuGet.Core'a SemVer 2.0.0 desteği ekle - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="066f8-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="066f8-195">MSBuild'te kullanılabilir geçişli bağımlılık `.targets` NuPkg'larına izin verin - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="066f8-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="066f8-196">NuGet komut satırından geri yükleme VS'den önemli ölçüde daha yavaştır - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="066f8-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="066f8-197">Paket kimliği ve sürüm karşılaştırma örneği duyarsız olun - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="066f8-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="066f8-198">NoCache seçeneği tabanlı `packages.config` geri yükleme/yükleme (GlobalPackagesFolder) için çalışmıyor - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="066f8-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="066f8-199">FindPackageByIdResource kaynakları varsayılan önbellek bağlamı ve logger gerekir - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="066f8-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
