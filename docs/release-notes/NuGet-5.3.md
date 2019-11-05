---
title: NuGet 5.3 Release Notes
description: Release notes for NuGet 5.3 including new features, bug fixes, and DCRs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: e77219d355f73f3bf01f68283ffb2759813af563
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611319"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="ed78a-103">NuGet 5.3 Release Notes</span><span class="sxs-lookup"><span data-stu-id="ed78a-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="ed78a-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="ed78a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ed78a-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="ed78a-105">NuGet version</span></span> | <span data-ttu-id="ed78a-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ed78a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ed78a-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ed78a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ed78a-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="ed78a-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ed78a-109">Visual Studio 2019 version 16.3</span><span class="sxs-lookup"><span data-stu-id="ed78a-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="ed78a-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ed78a-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="ed78a-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="ed78a-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ed78a-112">Visual Studio 2019 sürüm 16.3.6</span><span class="sxs-lookup"><span data-stu-id="ed78a-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="ed78a-113">Gelecek sürüm: 3.0.101</span><span class="sxs-lookup"><span data-stu-id="ed78a-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="ed78a-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span><span class="sxs-lookup"><span data-stu-id="ed78a-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="ed78a-115">Özet: 5,3 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="ed78a-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="ed78a-116">Paket simgesi, harici bir URL [olması yerine pakete gömülebilir](../reference/msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="ed78a-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="ed78a-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="ed78a-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="ed78a-118">SHA izleme ve paketler için zorlama ile geliştirilmiş güvenlik. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="ed78a-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="ed78a-119">Eski/eski NuGet paketlerinin kullanımdan kaldırılması için [#2867](https://github.com/NuGet/Home/issues/2867) | [blog gönderisi](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="ed78a-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed78a-120">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="ed78a-120">Issues fixed in this release</span></span>

<span data-ttu-id="ed78a-121">**Bugs**</span><span class="sxs-lookup"><span data-stu-id="ed78a-121">**Bugs**</span></span>

* <span data-ttu-id="ed78a-122">3\.0.100-preview9 SDK ile oluşturulan NuGet paketleri 2,2 SDK kullanıcıları tarafından kullanılamaz... Saat dilimlerinize bağlı olarak [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="ed78a-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="ed78a-123">QUOTE "YOLDAKI karakterler" yolda geçersiz karakterler "hata oluşmasına neden olur" `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="ed78a-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="ed78a-124">VS: derlemeler tamamen NGen tarafından, kısmen Ngen-Ed değil [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="ed78a-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="ed78a-125">Bellek kullanımını azaltma (etkinliklerden abonelik kaldırma)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="ed78a-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="ed78a-126">"Error_UnableToFindProjectInfo" iletisi dilsiz doğru değil [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="ed78a-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="ed78a-127">NU1403 geliştirmeleri-tüm paketleri doğrula, beklenen/fiili SHA değerlerini dahil et- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="ed78a-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="ed78a-128">`NuGetPackageManager.PreviewUpdatePackagesAsync` - birden çok sabit listesi [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="ed78a-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="ed78a-129">PluginProcess 'de "Public-> Internal" değişikliğini " [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="ed78a-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="ed78a-130">Ispackagesourceprovider. GetSources (...) hatalı tanımlanmış özel durum davranışına sahip- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="ed78a-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="ed78a-131">PluginManager oluşturucusunu bir daha genel yapın- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="ed78a-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="ed78a-132">PM Kullanıcı arabiriminin yenileme oranını izlemek için ölçümler- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="ed78a-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="ed78a-133">Paket Yöneticisi Kullanıcı arabirimi aracılığıyla yüklenirken UI yenilemelerinin sayısını azaltın- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="ed78a-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="ed78a-134">Telemetri: DateTime değerleri kültüre özgü biçimler kullanır- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="ed78a-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="ed78a-135">Paket Yöneticisi Kullanıcı arabirimindeki #6570- [#8339](https://github.com/NuGet/Home/issues/8339) Kullanıcı arabirimi yenilemelerinin azaltın</span><span class="sxs-lookup"><span data-stu-id="ed78a-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="ed78a-136">[Test hatası] "Yapılandırma dosyası ayrıştırılamıyor", iki kez [#8320](https://github.com/NuGet/Home/issues/8320) isteyecek</span><span class="sxs-lookup"><span data-stu-id="ed78a-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="ed78a-137">Müşteri düzeltmelerini (pakette gerekli nuspec dosyası eksik) açıklayan iyi belge sayfasıyla NU5037 hatası oluştur- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="ed78a-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="ed78a-138">Bir projenin Runtimeıdentifier değiştirildiğinde kilitli modda geri yükleme başarısız olur- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="ed78a-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="ed78a-139">VS yavaş [#8156](https://github.com/NuGet/Home/issues/8156) ayarları okuma</span><span class="sxs-lookup"><span data-stu-id="ed78a-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="ed78a-140">`Nuget sources add` gerileme "': ' karakteri, onaltılık değeri 0x3A, bir ada" Errors- [#7948](https://github.com/NuGet/Home/issues/7948) eklenemez</span><span class="sxs-lookup"><span data-stu-id="ed78a-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="ed78a-141">NuGet eklentisi kimlik bilgileri sağlayıcıları-işlem penceresini gizleyin- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="ed78a-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="ed78a-142">PackagePathResolver 'ı zorlama mutlak bir yoldur- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="ed78a-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="ed78a-143">Paket Yöneticisi Kullanıcı arabirimine yönelik Install ve Update sekmelerinde UI yenilemelerini azaltma- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="ed78a-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="ed78a-144">**DCR**</span><span class="sxs-lookup"><span data-stu-id="ed78a-144">**DCR:**</span></span>

* <span data-ttu-id="ed78a-145">Xamarin çerçevelerini NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368) eşlenecek şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ed78a-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="ed78a-146">Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324) Paket Yöneticisi "Önizleme penceresi" içeriğinin kopyalanmasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ed78a-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="ed78a-147">. Proj dosyalarında geri yüklemeyi etkinleştir- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="ed78a-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="ed78a-148">`NUGET_NETFX_PLUGIN_PATHS` ve `NUGET_NETCORE_PLUGIN_PATHS` her ikisi de aynı anda yapılandırmasını desteklemek için [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="ed78a-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="ed78a-149">Sürüm özniteliği aracılığıyla PackageDownload için birden çok sürümü etkinleştirme- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="ed78a-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="ed78a-150">NuGet. exe paketine-SolutionDirectory ve-PackageDirectory seçeneklerini ekleyin- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="ed78a-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="ed78a-151">**[Bu yayında düzeltilen tüm sorunların listesi-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="ed78a-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="ed78a-152">Özet: 5.3.1 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="ed78a-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="ed78a-153">Eklenti: bir görev iptal edildi-iptallerin eklenti örneğini etkilemesine izin verme- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="ed78a-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="ed78a-154">Geri yükleme görevi bir işlemde güvenle iki kez çalıştırılamaz (kimlik bilgileri sağlayıcıları kullanıldığında)- [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="ed78a-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
