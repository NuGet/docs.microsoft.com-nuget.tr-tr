---
title: "3.5 Beta2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "NuGet 3.5 Beta 2 bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.5 Beta 2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a><span data-ttu-id="b598d-104">3.5 Beta2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b598d-104">3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="b598d-105">[NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="b598d-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="b598d-106">NuGet 3.5 Beta 2 RTM, 27 Haziran 2016 Visual Studio 2013 ve nuget.exe için yayımlanan</span><span class="sxs-lookup"><span data-stu-id="b598d-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="b598d-107">Tam bir değişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="b598d-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="b598d-108">Konu listesi</span><span class="sxs-lookup"><span data-stu-id="b598d-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a><span data-ttu-id="b598d-109">Önemli değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="b598d-109">Notable Changes</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b598d-110">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="b598d-110">Bug Fixes</span></span>

* <span data-ttu-id="b598d-111">Güncelleştirilmiş hata iletisi için kimliği doğrulanmış akışları - parola decrpytion .NET Core içinde desteğinin [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="b598d-111">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="b598d-112">Paket Yöneticisi konsolu Get-Package başarısız .NET Core proje açıksa - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="b598d-112">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="b598d-113">NuGet itme komutta 403 hatalı işlenmesi düzeltme [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="b598d-113">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="b598d-114">Paketleri disableSourceControlIntegration ayarlandığında TFS kaynak denetimine bağlı bir çözümde kaldırma sorunlarını gidermek true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="b598d-114">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="b598d-115">Paket güncelleştirme hesabı hedef olmayan paketlere - gerçekleştirilecek düzeltme [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="b598d-115">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="b598d-116">MSBuild ayrıntı düzeyi UI eylemlerini - Nuget Paket Yöneticisi Günlükçü düzeyini ayarlamak için kullanma [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="b598d-116">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="b598d-117">Düzeltme NuGet yapılandırmadır Web sitesi projelerine - VS 2015 VSIX (v3.4.3) - geçersiz hata [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="b598d-117">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="b598d-118">Paketi sorunlarını düzeltmek `.csproj` içerik dosyaları dahil - olduğunda [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="b598d-118">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="b598d-119">İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) çalışmıyor - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="b598d-119">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="b598d-120">-Değer üzerinde paket oluşturma null olamaz - Nuget 3.4.3 sürümdeki sorunu düzeltin [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="b598d-120">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="b598d-121">Geri yükleme için VSTS akışları - Nuget.Config depolanan kimlik bilgilerini kullanır [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="b598d-121">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="b598d-122">Performans - sürüm karşılaştırma kodu düzeltme aşırı ayırmaları - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="b598d-122">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="b598d-123">Birden çok örneğini nuget.exe çalıştığında paralel olarak - aynı paketini yüklemek ilgili sorunları giderme [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="b598d-123">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="b598d-124">Performans - birden çok proje işlemleri için önbellek bağımlılık bilgi - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="b598d-124">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="b598d-125">Sorunu düzeltmek kaynak listesi boşken - paket kaynaklarını adlı ayarlarından eklenmesi burada [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="b598d-125">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="b598d-126">Tasarım zamanı cepheleri üzerinde - bağlıdır paketini yüklemeye çalışırken Misleading hatayı düzeltmek [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="b598d-126">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="b598d-127">Bir paketi "Tümü" ayar PackageManager konsolundan yükleme çalışır yalnızca ilk kaynak - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="b598d-127">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="b598d-128">Gelecekte yazma sürelerine sahip (Mono) - dosyalarınız paketlerle ilgili sorunları giderme [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="b598d-128">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="b598d-129">Güncelleştirme komutunda - bulma projeleri bir hata olduğunda özel durumu görüntülemek [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="b598d-129">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="b598d-130">Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 +'dan yükleme bağımsız değişkeniyle akış zaman - NoCache paketi içeriyorsa `.nupkg` dosyaları - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="b598d-130">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="b598d-131">Düzeltme sorunu paketini yükleyin (tüm kaynakları) paket 1 kaynağından - eksik olduğunda [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="b598d-131">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="b598d-132">Tek bir kaynak yetkilendirme - blokları yükleyin [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="b598d-132">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="b598d-133">`.nuspec`Aralık - IncludeReferencedProjects sürümü - geçersiz kıl sürüm [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="b598d-133">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="b598d-134">NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.'</span><span class="sxs-lookup"><span data-stu-id="b598d-134">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="b598d-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="b598d-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="b598d-136">nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır.</span><span class="sxs-lookup"><span data-stu-id="b598d-136">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="b598d-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="b598d-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="b598d-138">"DefaultPushSource için" - göreli dosya yolu ile ilgili sorunları giderme [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="b598d-138">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="b598d-139">Güncelleştirme çözümleyici hata iletileri - artırmak [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="b598d-139">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="b598d-140">Özellikler ve davranış değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="b598d-140">Features and Behavior Changes</span></span>

* <span data-ttu-id="b598d-141">nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="b598d-141">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="b598d-142">değil nuget.exe geri yükleme üretmek `.props` ve `.targets` dosyalarını `.nuproj` projeleri (v3.4.3.855 gerileme) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="b598d-142">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="b598d-143">Genişletilebilirlik API içeri aktarmalar - çerçeveleri karşılaştırmak için gereken [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="b598d-143">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="b598d-144">Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="b598d-144">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="b598d-145">Ayrıntılı bir çıkış - nuget.exe sürüm üstbilgisinde çıkışı yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="b598d-145">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="b598d-146">NuGet {RID} /runtimes/ /nativeassets/ {txm} için destek eklemek / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="b598d-146">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>