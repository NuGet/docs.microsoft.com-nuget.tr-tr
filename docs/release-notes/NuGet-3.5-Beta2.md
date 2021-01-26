---
title: 3,5 beta2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 Beta 2 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776388"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="e14f8-103">NuGet 3,5 beta2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e14f8-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="e14f8-104">[NuGet 3,5-Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)  |  [NuGet 3,5-RC sürüm notları](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e14f8-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="e14f8-105">NuGet 3,5 Beta 2 RTM, Visual Studio 2013 ve nuget.exe için 27 Haziran 2016 ' de yayımlandı</span><span class="sxs-lookup"><span data-stu-id="e14f8-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="e14f8-106">Tam changelog</span><span class="sxs-lookup"><span data-stu-id="e14f8-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="e14f8-107">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="e14f8-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="e14f8-108">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="e14f8-108">Bug Fixes</span></span>

* <span data-ttu-id="e14f8-109">Kimlik doğrulamalı akışlar için .NET Core 'da parola azaltma desteği nedeniyle hata iletisi güncelleştirildi- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="e14f8-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="e14f8-110">.NET Core projesi açık ise, Paket Yöneticisi konsolu Get-Package başarısız olur [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="e14f8-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="e14f8-111">NuGet Push komutu [#2910](https://github.com/NuGet/Home/issues/2910) 403 yanlış işlemesini düzeltir</span><span class="sxs-lookup"><span data-stu-id="e14f8-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="e14f8-112">Disablesourcecontrolintefinto değeri true olarak ayarlandığında TFS kaynak denetimine yönelik bir çözümde paket kaldırma sorunlarını giderin. [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="e14f8-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="e14f8-113">Paket güncelleştirmesini, hedef olmayan paketleri hesaba alacak şekilde onarma- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="e14f8-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="e14f8-114">NuGet Paket Yöneticisi Kullanıcı Arabirimi eylemleri için günlükçü düzeyini ayarlamak için MSBuild ayrıntı düzeyi 'ni kullanın- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="e14f8-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="e14f8-115">NuGet yapılandırmasını onarma Web sitesi projelerinde geçersiz hata-VS 2015 VSıX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="e14f8-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="e14f8-116">`.csproj`İçerik dosyaları dahil edildiğinde paket sorunlarını giderin- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="e14f8-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="e14f8-117">() İçindeki DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` çalışmıyor- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="e14f8-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="e14f8-118">NuGet 3.4.3 sürümündeki sorunu giderme-değer paket oluşturma sırasında null olamaz- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="e14f8-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="e14f8-119">Restore, VSTS akışları için Nuget.Config depolanan kimlik bilgilerini kullanır- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="e14f8-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="e14f8-120">Performans-sürüm karşılaştırmalarının çok fazla ayırmasını düzeltir- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="e14f8-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="e14f8-121">Birden çok nuget.exe örneği paralel [#2628](https://github.com/NuGet/Home/issues/2628) aynı paketi yüklemeye çalıştığında oluşan sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="e14f8-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="e14f8-122">Çok projeli işlemler için performans önbelleği bağımlılık bilgileri- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="e14f8-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="e14f8-123">Kaynak listesi boş olduğunda paket kaynaklarının ayarlardan eklenebileceği sorunu çözme- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="e14f8-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="e14f8-124">Tasarım zamanı cephe 'e bağlı paketi yüklemeye çalışırken yanıltıcı hatası giderme- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="e14f8-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="e14f8-125">PackageManager konsolundan paket yükleme "All" ayarı yalnızca ilk kaynak- [#2557](https://github.com/NuGet/Home/issues/2557) çalışır</span><span class="sxs-lookup"><span data-stu-id="e14f8-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="e14f8-126">Gelecekte yazma süreleriyle dosyaları olan paketlerle ilgili sorunları giderin (mono) [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="e14f8-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="e14f8-127">Güncelleştirme komutunda projeleri bulmada hata olduğunda özel durum görüntüle- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="e14f8-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="e14f8-128">Paket dosyaları içerdiğinde-NoCache bağımsız değişkenine sahip bir NuGet v 3.3 + akışından bir paket yüklenirken paket içeriği doğru şekilde geri yüklenmedi `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="e14f8-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="e14f8-129">Paket, 1 kaynak üzerinde eksik olduğunda paket yüklemesi (tüm kaynaklar) ile ilgili sorunu giderme [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="e14f8-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="e14f8-130">Tek bir kaynak yetkilendirme başarısız olursa blokları yükler- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="e14f8-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="e14f8-131">`.nuspec` sürüm aralığı geçersiz kılınmalıdır-ınclukıd proje sürümü- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="e14f8-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="e14f8-132">NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. '</span><span class="sxs-lookup"><span data-stu-id="e14f8-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="e14f8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="e14f8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="e14f8-134">nuget.exe güncelleştirme, bütünleştirilmiş kod tanımlayıcı adı ve Private özniteliği bırakır.</span><span class="sxs-lookup"><span data-stu-id="e14f8-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="e14f8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="e14f8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="e14f8-136">"DefaultPushSource" için göreli dosya yoluyla sorunları giderin- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="e14f8-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="e14f8-137">Güncelleştirme Çözümleyicisi hata iletilerini geliştirme- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="e14f8-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="e14f8-138">Özellikler ve davranış değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="e14f8-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="e14f8-139">nuget.exe Push-timeout parametresi çalışmıyor- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="e14f8-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="e14f8-140">nuget.exe geri yükleme `.props` , `.targets` projeler için dosya oluşturmaz ve dosyalar `.nuproj` (v 3.4.3.855 'de gerileme)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="e14f8-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="e14f8-141">Çerçeveleri içeri aktarmaları ile karşılaştırmak için genişletilebilirlik API 'SI gerekir- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="e14f8-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="e14f8-142">#2486 kullanırken bağımlılık seçeneklerini gizle `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="e14f8-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="e14f8-143">Ayrıntılı çıkışta nuget.exe sürüm üst bilgisini Yazdır- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="e14f8-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="e14f8-144">NuGet/Runtimes/{lar}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782) için destek eklemesi gerekir</span><span class="sxs-lookup"><span data-stu-id="e14f8-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>