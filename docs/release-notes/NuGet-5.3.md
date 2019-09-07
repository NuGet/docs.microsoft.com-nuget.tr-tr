---
title: NuGet 5,3 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774103"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="75850-103">NuGet 5,3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="75850-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="75850-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="75850-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="75850-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="75850-105">NuGet version</span></span> | <span data-ttu-id="75850-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="75850-106">Available in Visual Studio version</span></span>| <span data-ttu-id="75850-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="75850-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="75850-108">**5.3.0-preview3**</span><span class="sxs-lookup"><span data-stu-id="75850-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="75850-109">Visual Studio 2019 sürüm 16,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="75850-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="75850-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="75850-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="75850-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="75850-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="75850-112">Özetleme 5,3 Preview 3 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="75850-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="75850-113">Paket simgesi, harici bir URL [olması yerine pakete gömülebilir](../reference/msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="75850-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="75850-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="75850-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="75850-115">SHA izleme ve paketler için zorlama ile geliştirilmiş güvenlik. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="75850-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="75850-116">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="75850-116">Issues fixed in this release</span></span>

<span data-ttu-id="75850-117">**Hata**</span><span class="sxs-lookup"><span data-stu-id="75850-117">**Bugs**</span></span>

* <span data-ttu-id="75850-118">VS: derlemeler tamamen NGen tarafından, kısmen Ngen-Ed değil [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="75850-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="75850-119">Bellek kullanımını azaltma (etkinliklerden abonelik kaldırma)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="75850-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="75850-120">"Error_UnableToFindProjectInfo" iletisi dilsiz doğru değil [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="75850-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="75850-121">NU1403 geliştirmeleri-tüm paketleri doğrula, beklenen/fiili SHA değerlerini dahil et- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="75850-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="75850-122">NuGetPackageManager. Modelupdatepackagesasync- [#8401](https://github.com/NuGet/Home/issues/8401) içinde birden çok sabit listesi</span><span class="sxs-lookup"><span data-stu-id="75850-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="75850-123">PluginProcess 'de "Public-> Internal" değişikliğini " [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="75850-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="75850-124">Ispackagesourceprovider. GetSources (...) hatalı tanımlanmış özel durum davranışına sahip- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="75850-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="75850-125">PluginManager oluşturucusunu bir daha genel yapın- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="75850-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="75850-126">PM Kullanıcı arabiriminin yenileme oranını izlemek için ölçümler- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="75850-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="75850-127">Paket Yöneticisi Kullanıcı arabirimi aracılığıyla yüklenirken UI yenilemelerinin sayısını azaltın- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="75850-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="75850-128">Telemetri: DateTime değerleri kültüre özgü biçimler kullanır- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="75850-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="75850-129">Paket Yöneticisi Kullanıcı arabirimindeki #6570- [#8339](https://github.com/NuGet/Home/issues/8339) Kullanıcı arabirimi yenilemelerinin azaltın</span><span class="sxs-lookup"><span data-stu-id="75850-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="75850-130">[Test hatası] "Yapılandırma dosyası ayrıştırılamıyor", iki kez [#8320](https://github.com/NuGet/Home/issues/8320) isteyecek</span><span class="sxs-lookup"><span data-stu-id="75850-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="75850-131">Müşteri düzeltmelerini (pakette gerekli nuspec dosyası eksik) açıklayan iyi belge sayfasıyla NU5037 hatası oluştur- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="75850-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="75850-132">Bir projenin Runtimeıdentifier değiştirildiğinde kilitli modda geri yükleme başarısız olur- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="75850-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="75850-133">VS yavaş [#8156](https://github.com/NuGet/Home/issues/8156) ayarları okuma</span><span class="sxs-lookup"><span data-stu-id="75850-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="75850-134">' NuGet kaynakları ekleme ' içindeki gerileme "': ' karakteri, onaltılık değeri 0x3A, bir ada" Errors- [#7948](https://github.com/NuGet/Home/issues/7948) eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="75850-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="75850-135">NuGet eklentisi kimlik bilgileri sağlayıcıları-işlem penceresini gizleyin- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="75850-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="75850-136">PackagePathResolver 'ı zorlama mutlak bir yoldur- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="75850-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="75850-137">Paket Yöneticisi Kullanıcı arabirimine yönelik Install ve Update sekmelerinde UI yenilemelerini azaltma- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="75850-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="75850-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="75850-138">**DCR:**</span></span>

* <span data-ttu-id="75850-139">Xamarin çerçevelerini NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368) eşlenecek şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="75850-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="75850-140">Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324) Paket Yöneticisi "Önizleme penceresi" içeriğinin kopyalanmasını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="75850-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="75850-141">. Proj dosyalarında geri yüklemeyi etkinleştir- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="75850-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="75850-142">Her `NUGET_NETFX_PLUGIN_PATHS` ikisinin `NUGET_NETCORE_PLUGIN_PATHS` de aynı anda yapılandırmasını tanıtın ve bu yapılandırmayı destekler [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="75850-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="75850-143">Sürüm özniteliği aracılığıyla PackageDownload için birden çok sürümü etkinleştirme- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="75850-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="75850-144">NuGet. exe paketine-SolutionDirectory ve-PackageDirectory seçeneklerini ekleyin- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="75850-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="75850-145">NuGet paketini belirleyici olacak şekilde etkinleştirin- [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="75850-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="75850-146">**[Bu yayında düzeltilen tüm sorunların listesi-5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="75850-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
