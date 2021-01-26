---
title: NuGet 4,0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,0 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780187"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="eca8c-103">NuGet 4,0 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="eca8c-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="eca8c-104">NuGet 3,5 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="eca8c-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="eca8c-105">[Visual Studio 2017 Için NuGet 4,0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0) , .NET Core senaryoları için destek eklemeye, önemli müşteri geri bildirimlerine adresleme ve çeşitli senaryolarda performansı iyileştirmeye odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eca8c-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="eca8c-106">Bu sürüm, PackageReference için destek, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yükleme ve daha fazlası gibi çeşitli geliştirmeler sunar.</span><span class="sxs-lookup"><span data-stu-id="eca8c-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="eca8c-107">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="eca8c-107">Bug Fixes</span></span>

- <span data-ttu-id="eca8c-108">#3838 davranış değişiklikleri `dotnet pack --version-suffix foo`  -  [](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="eca8c-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="eca8c-109">Vs "15" makinesinde geri yükleme nuget.exe başarısız oldu- [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="eca8c-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="eca8c-110">. NETCore dosyası yeni proje geri yükleme sırasında derlemeyi engellemelidir- [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="eca8c-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="eca8c-111">VS2015 öğesinden VS "15" öğesine geçirilen Web uygulaması ASP.NET Core geri yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="eca8c-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="eca8c-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="eca8c-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="eca8c-113">[Test hatası] ' JQuery doğrulaması ' paketi PM Kullanıcı arabirimi tarafından kaldırılamaz- [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="eca8c-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="eca8c-114">UWP 'ye bir paket yüklendiğinde `project.json` , üst projelerin de geri yüklenmesi gerekir [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="eca8c-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="eca8c-115">NuGet hedeflerini, paket kaynaklarını normal [#3719](https://github.com/NuGet/Home/issues/3719) yerine yüksek düzeyde ayrıntı olarak günlüğe kaydetmek üzere değiştirin</span><span class="sxs-lookup"><span data-stu-id="eca8c-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="eca8c-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="eca8c-116">dotnet</span></span>
  - <span data-ttu-id="eca8c-117">dotnetcore Pack3, varsayılan olarak XML belgeleri içermelidir [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="eca8c-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="eca8c-118">Paket olmadan kaynak ilk kez ve tüm kaynak seçildiğinde, Batch güncelleştirmesi kullanıcı arabiriminden başarısız olur [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="eca8c-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="eca8c-119">NuGet paketi komutu tüm dosyaları kapsamaz- [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="eca8c-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="eca8c-120">OOM sorun- [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="eca8c-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="eca8c-121">Varlıklar dosyasının ProjectFileDependencyGroups bölümü, projeler için kitaplık adları kullanmalıdır- [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="eca8c-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="eca8c-122">"dotnet restore" ve yinelenen dizinler- [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="eca8c-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="eca8c-123">Restore3 hataları hatalar yerine uyarı olarak günlüğe kaydedilir- [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="eca8c-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="eca8c-124">TFS sorunu: "[dosya] çalışma alanınızda bulunamadı, ya da ona erişmek için izniniz yok"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="eca8c-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="eca8c-125"><packagename>Vs Hızlı Başlat arama kutusunda "NuGet" yazıldığında "NuGet" öneki- [#2719](https://github.com/NuGet/Home/issues/2719) kalır</span><span class="sxs-lookup"><span data-stu-id="eca8c-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="eca8c-126">System.Xml.Xmlözel durum: çekirdek Özellikler bölümünde tanınmayan kök öğe.</span><span class="sxs-lookup"><span data-stu-id="eca8c-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="eca8c-127">2. satır, konum 2.</span><span class="sxs-lookup"><span data-stu-id="eca8c-127">Line 2, position 2.</span></span><span data-ttu-id="eca8c-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="eca8c-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="eca8c-129">`.nuspec` kaçışlı &lt; veya &gt; metin alanlarında artık derleme [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="eca8c-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="eca8c-130">nuget.exe silme, kimlik bilgilerini istemez (etkileşimli olmayan modda) [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="eca8c-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="eca8c-131">nuget.exe DELETE, yerel kaynaklar için API anahtarı hakkında, hiçbir [#2625](https://github.com/NuGet/Home/issues/2625) anlamlı olmasa da</span><span class="sxs-lookup"><span data-stu-id="eca8c-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="eca8c-132">EF-Package- [#2566](https://github.com/NuGet/Home/issues/2566) yüklenirken hata deneyimi zayıf</span><span class="sxs-lookup"><span data-stu-id="eca8c-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="eca8c-133">Paket Yöneticisi 'nde Seçimi değiştirdikten sonra Visual Studio kilitlendi- [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="eca8c-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="eca8c-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="eca8c-134">dotnet</span></span>
  - <span data-ttu-id="eca8c-135">dotnetcore geri yükleme, kayan sürümler kullanıldığında düz liste yerel depolarında büyük/küçük harfe duyarlı kimlik aramaları gerçekleştirir- [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="eca8c-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="eca8c-136">nuget.exe DELETE, v2 akışı için bozuk [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="eca8c-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="eca8c-137">nuget.exe gönderme zaman aşımı, daha iyi bir hata iletisi gerektirir [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="eca8c-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="eca8c-138">Uygun içeri aktarmalar olmadan araç geri yükleme sessizce başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="eca8c-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="eca8c-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="eca8c-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="eca8c-140">Nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346) ' den yükleme sırasında bile özel akış olduğunda NuGet kimlik bilgilerini girmesi istenir</span><span class="sxs-lookup"><span data-stu-id="eca8c-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="eca8c-141">ApplicationInsights 2,0 paketi listeleniyor ancak henüz mevcut değil- [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="eca8c-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="eca8c-142">Iıdelay, VS "15" Preview 5 dal- [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="eca8c-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="eca8c-143">UWP- [#3489](https://github.com/NuGet/Home/issues/3489) için derleme sırasında Ilk onbuild olayı geri yükleme için eksik</span><span class="sxs-lookup"><span data-stu-id="eca8c-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="eca8c-144">PowerShell5, EntityFramework yüklemesi mi?</span><span class="sxs-lookup"><span data-stu-id="eca8c-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="eca8c-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="eca8c-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="eca8c-146">Kaynakları ayrıntılı günlüğe ekleme (3,5 için göz önünde bulundurun)- [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="eca8c-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="eca8c-147">NuGet istemci sürümü 3.4 +- [#3074](https://github.com/NuGet/Home/issues/3074) NoCache parametresi kabul edilmez</span><span class="sxs-lookup"><span data-stu-id="eca8c-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="eca8c-148">Bir kimlik bilgisi sağlayıcısı VS 'de yükleme başarısız olduğunda, NuGet 'yi bozmayın [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="eca8c-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="eca8c-149">Özellikler</span><span class="sxs-lookup"><span data-stu-id="eca8c-149">Features</span></span>

- <span data-ttu-id="eca8c-150">CI 'yi x86- [#3868](https://github.com/NuGet/Home/issues/3868) çalıştırmak için ayarlama</span><span class="sxs-lookup"><span data-stu-id="eca8c-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="eca8c-151">Otomatik geri yükleme 3/3: engellenmeyen Kullanıcı arabirimi- [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="eca8c-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="eca8c-152">Otomatik geri yükleme 2/3: aday için arka planda geri yükleme- [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="eca8c-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="eca8c-153">Proje refs öğesini derleme davranışıyla eşleşecek şekilde geri yükleme (recurse)- [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="eca8c-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="eca8c-154">VS "15"-Minbar- [#3614](https://github.com/NuGet/Home/issues/3614) ile DPL desteği</span><span class="sxs-lookup"><span data-stu-id="eca8c-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="eca8c-155">Ayarlar dosyasını program dosyalarına Taşı- [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="eca8c-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="eca8c-156">Oluşturulan geri yükleme props ve hedefleri için çapraz hedefleme katılım desteği gerekir- [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="eca8c-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="eca8c-157">PackageTargetFallback için NuGet geri yükleme desteği (f. k. a Imports)- [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="eca8c-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="eca8c-158">Araçları başvuru uygulama- [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="eca8c-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="eca8c-159">RID- [#3465](https://github.com/NuGet/Home/issues/3465) için Restore3</span><span class="sxs-lookup"><span data-stu-id="eca8c-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="eca8c-160">PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457) ekleme/kaldırma/güncelleştirme desteği için NuGet Kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="eca8c-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="eca8c-161">Otomatik geri yükleme 1/3: proje geri yükleme bilgilerini önbelleğe alma yoluyla aday API 'nin uygulaması- [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="eca8c-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="eca8c-162">[0] NuGet geri yükleme görevi & hedefleri- [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="eca8c-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="eca8c-163">[1] MSBuild- [#2993](https://github.com/NuGet/Home/issues/2993) çözüm düzeyinde geri yüklemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="eca8c-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="eca8c-164">Visual Studio 'da kimlik bilgisi sağlayıcısı genel genişletilebilirliği desteği- [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="eca8c-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="eca8c-165">Yinelemeli NuGet geri yükleme- [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="eca8c-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="eca8c-166">Microsoft. TeamFoundation. Client dev15 üzerinde yüklenemiyor, VS "15" Preview- [#2392](https://github.com/NuGet/Home/issues/2392) için Microsoft. TeamFoundation. client sürümünün 15,0 olarak güncelleştirilmesi gerekiyor</span><span class="sxs-lookup"><span data-stu-id="eca8c-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="eca8c-167">C++ paketi, VS "15" Preview- [#2369](https://github.com/NuGet/Home/issues/2369) ' de c++ UWP projesine yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="eca8c-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="eca8c-168">Nupkg 'ın \buildnel stargeting\ Folder 'ı desteklemesi ve `.targets`  /  `.props` "çapraz başlangıç" MSBuild kapsamı için içeri aktarılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eca8c-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="eca8c-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="eca8c-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="eca8c-170">Araçları başvuru tasarımı- [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="eca8c-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="eca8c-171">NuGet Kullanıcı arabirimini, #3455 geri yüklemeyi/packagereferlenimleri destekleyecek şekilde düzeltir `.csproj`  -  [](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="eca8c-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="eca8c-172">VS Paket Yöneticisi ayarlarına önbellek temizle düğmesi ekleme- [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="eca8c-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="eca8c-173">DCR</span><span class="sxs-lookup"><span data-stu-id="eca8c-173">DCRs</span></span>

- <span data-ttu-id="eca8c-174">Otomatik geri yükleme gerçekleşirken çözüm geri yüklemesi engellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="eca8c-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="eca8c-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="eca8c-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="eca8c-176">NuGet Paket Yöneticisi kullanıcı arabiriminden NetCore yüklemesi, paketin destekleyenler yerine her TFı 'ye yüklenir- [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="eca8c-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="eca8c-177">Nominator API 'sini geri yükleme, Dotnetclienaraçları 'nın da başvurularını desteklemesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eca8c-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="eca8c-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="eca8c-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="eca8c-179">VS "15" VSIX 'i bir SystemComponent olarak işaretleyin- [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="eca8c-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="eca8c-180">Başvuruda bulunan MS 'den geçiş. Anlara. Services. Client-MS. Anlara. Services. Client. Interactive- [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="eca8c-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="eca8c-181">$ (RestoreLegacyPackagesDirectory), restore- [#3618](https://github.com/NuGet/Home/issues/3618) tarafından bir proje düzeyinde dikkate alınmalıdır</span><span class="sxs-lookup"><span data-stu-id="eca8c-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="eca8c-182">Tek TargetFramework ile projeye geri yükleme koşul props- [#3588](https://github.com/NuGet/Home/issues/3588) olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="eca8c-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="eca8c-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="eca8c-183">dotnet</span></span>
  - <span data-ttu-id="eca8c-184">dotnetcore restore3 foo. csproj, projectref bağımlılıklarını izlemelidir ve bunları geri yükler.</span><span class="sxs-lookup"><span data-stu-id="eca8c-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="eca8c-185">Yapı gibi.</span><span class="sxs-lookup"><span data-stu-id="eca8c-185">Like build.</span></span><span data-ttu-id="eca8c-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="eca8c-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="eca8c-187">"tür": "Platform" bağımlılıkları, kilit dosyasında "tür": "Package" olarak temsil edilir- [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="eca8c-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="eca8c-188">nuget.exe verbose modu indirme URL 'sini göstermelidir- [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="eca8c-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="eca8c-189">NuGet xplat 'yi Microsoft. NetCore. App ve netcoreapp 1.0 'a taşıyın- [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="eca8c-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="eca8c-190">Gönderim- [#2348](https://github.com/NuGet/Home/issues/2348) komut satırından gönderilirken sembol sunucusunu geçersiz kılmak mümkün olmalıdır</span><span class="sxs-lookup"><span data-stu-id="eca8c-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="eca8c-191">Genel paket yolunu bulmak için kodu birleştirme- [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="eca8c-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="eca8c-192">SuppressParent- [#2196](https://github.com/NuGet/Home/issues/2196) daha iyi bir ad gerekiyor</span><span class="sxs-lookup"><span data-stu-id="eca8c-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="eca8c-193">`project.json`MSBuild projeleri için kullanılacak bağımlılık adını belirle- [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="eca8c-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="eca8c-194">NuGet. Core- [#3383](https://github.com/NuGet/Home/issues/3383) semver 2.0.0 desteği ekleyin</span><span class="sxs-lookup"><span data-stu-id="eca8c-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="eca8c-195">MSBuild 'de kullanılabilir olan geçişli bağımlılık NuPkgs 'e izin ver `.targets` [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="eca8c-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="eca8c-196">Komut satırında NuGet geri yükleme, VS- [#3330](https://github.com/NuGet/Home/issues/3330) göre önemli ölçüde yavaştır</span><span class="sxs-lookup"><span data-stu-id="eca8c-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="eca8c-197">Paket KIMLIĞI ve sürümü karşılaştırma büyük/küçük harfe duyarsız- [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="eca8c-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="eca8c-198">NoCache seçeneği `packages.config` tabanlı geri yükleme/yükleme (GlobalPackagesFolder) için çalışmıyor- [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="eca8c-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="eca8c-199">Findpackagebyıdresource kaynakları için varsayılan önbellek bağlamı ve günlükçü- [#1357](https://github.com/NuGet/Home/issues/1357) gerekir</span><span class="sxs-lookup"><span data-stu-id="eca8c-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
