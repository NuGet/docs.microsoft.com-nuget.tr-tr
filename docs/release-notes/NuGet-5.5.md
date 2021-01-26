---
title: NuGet 5,5 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,5 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780107"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="bc95d-103">NuGet 5,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="bc95d-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="bc95d-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="bc95d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bc95d-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="bc95d-105">NuGet version</span></span> | <span data-ttu-id="bc95d-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="bc95d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="bc95d-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="bc95d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="bc95d-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="bc95d-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bc95d-109">Visual Studio 2019 sürüm 16,5</span><span class="sxs-lookup"><span data-stu-id="bc95d-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bc95d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bc95d-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="bc95d-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="bc95d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="bc95d-112">Özet: 5,5 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="bc95d-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="bc95d-113">Visual Studio 'da NuGet Paket Yöneticisi Kullanıcı arabirimi için geliştirilmiş erişilebilirlik ve ekran okuyucu deneyimi</span><span class="sxs-lookup"><span data-stu-id="bc95d-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="bc95d-114">Ekran okuyucu deneyimlerinde erişilebilirlik sorunları, yüklü metin kutusu için eksik altmetin ve erişilebilir ad, vb. [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="bc95d-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="bc95d-115">Paket listesinde ekran okuyucu deneyimlerinde erişilebilirlik sorunları- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="bc95d-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="bc95d-116">Ekran okuyucu deneyimlerinde "tarama", "Install", "Update" sekmeleri ile ilgili erişilebilirlik sorunları- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="bc95d-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="bc95d-117">Ekran okuyucusu "boş", "hiçbir bağımlılık Ciesi", "NuGet. org", "MIT" bağlantı etiketini duyurmaz [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="bc95d-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="bc95d-118">Yerel akışlar üzerinde barındırılan paketler için Visual Studio Paket Yöneticisi Kullanıcı arabirimindeki kendi kendine içerilen bağımsız simgeler için destek- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="bc95d-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="bc95d-119">`RestoreUseStaticGraphEvaluation`MSBuild statik grafik API 'lerini çağırarak değerlendirmeleri hızlandıran önemli ölçüde geliştirilmiş bir işlem temelli geri yükleme performansı- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="bc95d-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="bc95d-120">Platformlar arası kimlik doğrulama eklentileri ile iyileştirilmiş dotnet.exe güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="bc95d-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="bc95d-121">Taskolaydexception ile başarısız dotnet restore- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="bc95d-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="bc95d-122">Eklenti: "bir görev iptal edildi"-Bu nedenle ADO kimlik doğrulamasında sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="bc95d-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="bc95d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="bc95d-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="bc95d-124">`dotnet nuget <add|remove|update|disable|enable|list> source`Komut Ekle- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="bc95d-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="bc95d-125">`--skip-duplicate`DotNet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778) kullanımı için supmport</span><span class="sxs-lookup"><span data-stu-id="bc95d-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="bc95d-126">`packages.config`MSBuild/restore ile destek- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="bc95d-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bc95d-127">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc95d-127">Issues fixed in this release</span></span>

<span data-ttu-id="bc95d-128">**Hata**</span><span class="sxs-lookup"><span data-stu-id="bc95d-128">**Bugs**</span></span>

* <span data-ttu-id="bc95d-129">V3 API 'lerle Self-Updater yeniden çalışma [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="bc95d-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="bc95d-130">Paket bağımlılığı sürümü ' \* ' olarak ayarlandıysa, paket bağımlılığı sürümü yanlış- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="bc95d-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="bc95d-131">ErrorUnsafePackageEntry hata iletisi, sorun kaynağını işaret etmiyor- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="bc95d-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="bc95d-132">Kilit dosyası "\*" senaryolarında kabul edilmez- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="bc95d-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="bc95d-133">NuGet.exe, PackageReference içinde \* kullanılırken bir paketin en son sürümüne çözümlenmiyor (MSBuild/DotNet/VS geri yükleme do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="bc95d-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="bc95d-134">birden çok hedefleme WPF projesi olan DotNet liste paketi- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="bc95d-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="bc95d-135">ConcurrencyUtilities 'i geliştirme (CPU kullanımını azaltma)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="bc95d-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="bc95d-136">Kaldırılan proje senaryolarında DG Spec Önizleme geri yüklemeler- [#8793](https://github.com/NuGet/Home/issues/8793) yazılmamalıdır</span><span class="sxs-lookup"><span data-stu-id="bc95d-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="bc95d-137">Visual Studio NuGet paketleri (RestoreManagerPackage), çözüm oluşturma olaylarına otomatik olarak yüklenilmesi gerekir- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="bc95d-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="bc95d-138">VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842) kilitlenmesi</span><span class="sxs-lookup"><span data-stu-id="bc95d-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="bc95d-139">Bir proje çözüm klasörüne yerleştirilirse, VisualStudio araç kutusu bir NuGet paketinden doldurulmamış- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="bc95d-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="bc95d-140">VS: çözüm geri yükleme adet sürekli, yarış durumu nedeniyle başarısız oluyor- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="bc95d-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="bc95d-141">Yüklü sekmede "yükleniyor.." sabiti ve "arama</span><span class="sxs-lookup"><span data-stu-id="bc95d-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="bc95d-142">.. "Güncelleştirmeler sekmesinde- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="bc95d-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="bc95d-143">Önbellek süresi dolduktan sonra VS PM Kullanıcı arabiriminde gömülü simgeler eksik- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="bc95d-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="bc95d-144">Fireandur PM UI Startup- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="bc95d-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="bc95d-145">Restore: ıncludeexcludefiles. Equals (...) uygulama yanlış- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="bc95d-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="bc95d-146">Restore: PackageSpec. Clone () eşit olmayan kopya oluşturuyor- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="bc95d-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="bc95d-147">"Derleme hatalarla bittiğinde her zaman Hata Listesi göster" işaretli olmasa da hata listesi gösteriliyor [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="bc95d-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="bc95d-148">Statik grafik geri yükleme boş SolutionPath 'e geçmemelidir- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="bc95d-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="bc95d-149">Geri yükle: her proje için bir kapanış hesaplandı 4 kez [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="bc95d-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="bc95d-150">Restore: DependencyGraphSpec. Load (...), JObject- [#9040](https://github.com/NuGet/Home/issues/9040) gerektirmez</span><span class="sxs-lookup"><span data-stu-id="bc95d-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="bc95d-151">Geri yükleme: büyük nesne yığınında (LOH) büyük dizeler oluşturuldu- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="bc95d-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="bc95d-152">Daha yeni mono 'daki özel nuget.exe, MSBuild SDK 'Sı Çözümleyicisi nedeniyle kesintiye uğramayabilir- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="bc95d-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="bc95d-153">nuget.dgspec.js, başka bir işlem tarafından kullanıldığında geri yükleme başarısız olur "- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="bc95d-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="bc95d-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="bc95d-154">**DCRs**</span></span>

* <span data-ttu-id="bc95d-155">_GetRestoreProjectStyle mantığın bir görevde olması gerekir [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="bc95d-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="bc95d-156">Yüklü sekmesine varsayılan olarak kullanımdan kaldırma bilgilerini ekleyin- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="bc95d-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="bc95d-157">**[Bu yayında düzeltilen tüm sorunların listesi-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="bc95d-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
