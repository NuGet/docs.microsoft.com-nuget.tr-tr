---
title: NuGet 3,5 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776351"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="ac7ce-103">NuGet 3,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ac7ce-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="ac7ce-104">[NuGet 3,5-RC sürüm notları](../release-notes/nuget-3.5-RC.md)  |  [NuGet 4,0 RC sürüm notları](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ac7ce-105">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="ac7ce-105">Bug Fixes</span></span>

* <span data-ttu-id="ac7ce-106">Paket, mono [#3550](https://github.com/NuGet/Home/issues/3550) üzerinde MSBuild 14,1 kullanmaz</span><span class="sxs-lookup"><span data-stu-id="ac7ce-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="ac7ce-107">Güncelleştirme sekmesi, güncelleştirmek için kullanılabilir en son sürümü seçmeyin, bunun yerine geçerli yüklü sürümü seçin- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="ac7ce-108">Özel v2 MyGet akışı doğrulandıktan sonra ve "x daha fazla sonuç göster [#3469](https://github.com/NuGet/Home/issues/3469) " seçeneğine tıklayarak kilitlenmeyi düzeltir</span><span class="sxs-lookup"><span data-stu-id="ac7ce-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="ac7ce-109">Günlük iletileri UI- [#3446](https://github.com/NuGet/Home/issues/3446) için ters sırada görünüyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="ac7ce-110">v 3.4.4-NuGet restore "verilen yolun biçimi desteklenmiyor"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="ac7ce-111">NuGet komut 3,6 Beta,-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="ac7ce-112">Büyük projede NuGet ıKVM yavaş yüklemesi- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="ac7ce-113">nuget.exe güncelleştirme-kendi kendini güncelleştirme üzerinde devam eder [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="ac7ce-114">3,5 UNC paylaşımından yükleme/geri yükleme için 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355) performans gerileme bulunur</span><span class="sxs-lookup"><span data-stu-id="ac7ce-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="ac7ce-115">Bir net451 projesi için paket yönetimi kullanıcı arabiriminden moq yüklenirken hata- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="ac7ce-116">Çözüm düzeyinde Install Tab, paketin sürüm- [#3339](https://github.com/NuGet/Home/issues/3339) göstermiyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="ac7ce-117">`project.json`yüklü sekmeden xproj güncelleştirmesi durum [#3303](https://github.com/NuGet/Home/issues/3303) kaybeder</span><span class="sxs-lookup"><span data-stu-id="ac7ce-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="ac7ce-118">Üzerinde NuGet paketi `.csproj` , `.nuspec` dosyadaki dosya [#3257](https://github.com/NuGet/Home/issues/3257) boş dosya öğesini yoksayar</span><span class="sxs-lookup"><span data-stu-id="ac7ce-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="ac7ce-119">IIS 'de barındırılan Web sitesi projeleri geri yüklemenin başarısız olmasına neden olmamalıdır- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="ac7ce-120">V3 uç noktası v2 'ye yeniden yönlendirirse Nuget.Config kimlik bilgileri alınmadı- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="ac7ce-121">NuGet paketi, taşınabilir derleme meta verilerini alırken derlemeyi çözemedi- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="ac7ce-122">NuGet `msbuild.exe` Mono [#3085](https://github.com/NuGet/Home/issues/3085) bulamıyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="ac7ce-123">nuget.exe Pack, [#1743](https://github.com/NuGet/Home/issues/1743) sayılarla başlayan yayın öncesi etiketine izin vermiyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="ac7ce-124">NuGet paketi yüklemesi VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298) başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="ac7ce-125">allowedVersions filtresi çözüm düzeyinde çalışmıyor- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="ac7ce-126">Aynı anahtara sahip bir öğe zaten eklenmiş şekilde geri yükleme rastgele başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="ac7ce-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="ac7ce-128">NuGet. Common `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635) yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="ac7ce-129">Bir v2 kaynağını aramak için Kullanıcı arabirimini kullanırken, Findpackagesbyıd her KIMLIK için iki kez çağırılır [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="ac7ce-130">Paketler projelere bağımlı olamaz- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="ac7ce-131">nuget.exe Pack-exclude belgelenmiştir ancak desteklenmez- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="ac7ce-132">' ContentFiles ' bölümü geçersiz olduğunda hata iletileri ile ilgili sorunlar `.nuspec` geçersiz- [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="ac7ce-133">Gönderim her zaman kimliği doğrulanmış paket kaynaklarıyla tüm paketi iki kez gönderir [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="ac7ce-134">Projede bir #1496 olmadığında nuget.exe Update \*. csproj çağrılırken hiçbir bilgi verilmedi `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="ac7ce-135">`packages.config` yükleme, v2 kaynaklarından 5 xx durum kodu üzerinde yeniden denenmez- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="ac7ce-136">Kaynak dosyasında çift nokta `.nuspec` çalışmıyor- [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="ac7ce-137">CoreCLR geri yüklemenin, şifreleme ile akışları yoksayması gerekiyor [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="ac7ce-138">nuget.exe Push 403 işleme-kimlik bilgileri için yanlış istem- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="ac7ce-139">Paket Yöneticisi üzerinden NuGet güncelleştirmesi `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888) özellikleri kaldırır</span><span class="sxs-lookup"><span data-stu-id="ac7ce-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="ac7ce-140">NuGet. PackageManagement. VisualStudio "NuGet. TeamFoundationServer14" öğesini yüklemeyi deneyin, ancak bu DLL adı "NuGet. TeamFoundationServer" olarak değiştirildi- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="ac7ce-141">Paket Yöneticisi Kullanıcı arabirimi yeni güncelleştirilmiş sürümü göstermiyor [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="ac7ce-142">güncelleştirme-Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771) yerine PackageID, Version kullanmaya çalışan paket.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="ac7ce-143">Proje NuGet (veya) kullanıyorsa NuGet geri yükleme csproj hatası olmalıdır `packages.config` `project.json` - [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="ac7ce-144">"[File] TFS hatası, çalışma alanınızda bulunamadı veya çözüm/proje TFS kaynak denetimine bağlandığında yükseltme veya kaldırma işlemi sırasında" erişim izniniz yok- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="ac7ce-145">güncelleştirme paketi, hedef olmayan paketler için bağımlılıklar almaz- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="ac7ce-146">NuGet Paket Yöneticisi Kullanıcı Arabirimi eylemleri için günlük ayrıntı düzeyi ayarlama yolu yoktur- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="ac7ce-147">NuGet yapılandırması geçersiz-VS 2015 VSıX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="ac7ce-148">() İçindeki DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` çalışmıyor- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="ac7ce-149">NuGet 3.4.3 Release-değer alma paket derlemesinde null olamaz- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="ac7ce-150">restore, VSTS akışları için Nuget.Config depolanan kimlik bilgilerini kullanmıyor [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="ac7ce-151">[dotnet restore]--ConfigFile, cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639) yerine proje dizini 'ne göredir</span><span class="sxs-lookup"><span data-stu-id="ac7ce-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="ac7ce-152">Sürüm karşılaştırmalarda aşırı kullanım kodu- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="ac7ce-153">Aynı paketi paralel olarak yüklemeye çalışan nuget.exe birden çok örneği, Çift yazma [#2628](https://github.com/NuGet/Home/issues/2628) neden olur</span><span class="sxs-lookup"><span data-stu-id="ac7ce-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="ac7ce-154">Bağımlılık bilgileri çoklu proje işlemleri için önbelleğe alınmaz- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="ac7ce-155">Önce paketler klasörünü denetlemeden yükleme paketlerini yükle ve Güncelleştir- [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="ac7ce-156">Paket kaynak listesi boşsa, Kullanıcı arabirimi (NuGet 3.4. x) aracılığıyla paket kaynağı eklenemiyor [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="ac7ce-157">Tasarım zamanı cephe 'e bağlı paketi yüklemeye çalışırken yanıltıcı hata oluştu- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="ac7ce-158">PackageManager konsolundan paket yükleme "All" ayarı yalnızca ilk kaynak- [#2557](https://github.com/NuGet/Home/issues/2557) çalışır</span><span class="sxs-lookup"><span data-stu-id="ac7ce-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="ac7ce-159">En son beta ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="ac7ce-160">VS2015 otomatik olarak oluşturulan NuGet 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="ac7ce-161">Bunu sorsam, Update komutu biraz daha ayrıntılı olabilir...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="ac7ce-162">Yerel olarak oluşturulan VSıX, CI derlemesi ile aynı dll 'Lere ve dosyalara sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="ac7ce-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="ac7ce-164">Derleme [#2396](https://github.com/NuGet/Home/issues/2396) NuGet düşürme uyarılarını çözme</span><span class="sxs-lookup"><span data-stu-id="ac7ce-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="ac7ce-165">Paket kaynağının kimlik doğrulaması başarısız (3 kez), süresiz olarak engellendi [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="ac7ce-166">Paket dosyaları içerdiğinde-NoCache bağımsız değişkenine sahip bir NuGet v 3.3 + akışından bir paket yüklenirken paket içeriği doğru şekilde geri yüklenmedi `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="ac7ce-167">Tüm paket kaynaklarıyla NuGet yüklemesi, ancak 1 kaynakta paket eksik, başarısız- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="ac7ce-168">[PerfWatson] Uıdelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="ac7ce-169">Tek bir kaynak yetkilendirme başarısız olursa blokları yükler- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="ac7ce-170">`.nuspec` sürüm aralığı geçersiz kılınmalıdır-ınclukıd proje sürümü- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="ac7ce-171">Update-Package Super yavaş-"bağımlılık bilgilerini toplamaya çalışılıyor"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="ac7ce-172">Toplu işlem, bağımlılıklarını güncelleştirirken NuGet gizli eski sürüme sahip des paketi- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="ac7ce-173">nuget.exe güncelleştirme, bütünleştirilmiş kod tanımlayıcı adı ve Private özniteliği bırakır.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="ac7ce-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="ac7ce-175">"DefaultPushSource" için göreli dosya yolu- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="ac7ce-176">Çözümleyici hata iletilerini geliştirme- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="ac7ce-177">v3 'teki güncelleştirme paketi, belirtilen kaynak [#1013](https://github.com/NuGet/Home/issues/1013) olmayan paketlerle başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="ac7ce-178">Paket kaynakları için göreli yolların kullanılması sorunlu [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="ac7ce-179">Daha düşük bir sürüm gereksinimiyle zaten bir dolaylı bağımlılık varsa, projeden oluşturulan NUPKG-File içinde eksik bağımlılık var- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="ac7ce-180">Bir projenin silinmesi, ilgili Kullanıcı arabirimi penceresini kapatır, ancak projenin yeniden adlandırılması Kullanıcı arabirimi penceresini yeniden adlandırmaz.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="ac7ce-181">PMC 'nin proje yeniden adlandırma ve proje kaldırma olaylarını dinler- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="ac7ce-182">[Soldüşük Web Iş yükü] Razor V3 WSP kilitleniyor- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="ac7ce-183">Belirli bir paketi yükleme/geri yükleme işlemi "Package birden çok nuspec dosyası içeriyor" ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="ac7ce-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="ac7ce-185">Küçük kodlar & `packages.config` senaryolar- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="ac7ce-186">[3,5-beta2] Paket geri yükleme "eski" paketleri geri yüklemeyi yapamıyor- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="ac7ce-187">NuGet Pack,. tt dosyalarını, ne tür şeyler [#3203](https://github.com/NuGet/Home/issues/3203) , içerik klasörüne zorla ekler</span><span class="sxs-lookup"><span data-stu-id="ac7ce-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="ac7ce-188">Update-ASP.NET Web App paketi, dosyayla ilgili bir uyarı oluşturur: kaynak- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="ac7ce-189">`project.json`json dosyasında packOptions ve sahip olmadığında NuGet Pack csproj (WITH) kilitleniyor- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="ac7ce-190">için NuGet paketi `project.json` , Summary, yazarlar, Owners vs- [#3161](https://github.com/NuGet/Home/issues/3161) gibi packoptions etiketlerini yoksayar</span><span class="sxs-lookup"><span data-stu-id="ac7ce-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="ac7ce-191">NuGet. paketleme. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160) aracılığıyla NullReferenceException</span><span class="sxs-lookup"><span data-stu-id="ac7ce-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="ac7ce-192">NuGet paketi `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145) için çıkışta bağımlılıkları yoksayar</span><span class="sxs-lookup"><span data-stu-id="ac7ce-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="ac7ce-193">Birden çok paketin geri alma ile güncelleştirilmesi, projeyi bozuk bir durumda bırakır- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="ac7ce-194">Netstandart projeler için any altındaki ContentFiles eklenmez- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="ac7ce-195">.NET Standard için kitaplık hedeflemesi doğru paketlenemez- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="ac7ce-196">Dosya-> yeni proje-> sınıf kitaplığı (taşınabilir) projesi VS2015 ve Dev15- [#3094](https://github.com/NuGet/Home/issues/3094) içinde başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="ac7ce-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="ac7ce-197">nuGet hatası-1.0.0-\* geçerli bir sürüm dizesi değil- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="ac7ce-198">Find-Package görüntülenemiyor ancak Install-Package çalışmaları [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="ac7ce-199">Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) "Install-Package jQuery. Validation" hatası</span><span class="sxs-lookup"><span data-stu-id="ac7ce-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="ac7ce-200">xproj NuGet paketi geçersiz hedef yoluna sahip- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="ac7ce-201">Bir VS 2015 güncelleştirme 3 ' ü, NuGet sürümü 3.5.0 hatası oluşursa [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="ac7ce-202">İçindeki "packages.config tarafından engellendi" `project.json` (UWP, a. k. derleme tümleşik) projesi- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="ac7ce-203">derleme betiği tarafından yüklenen DotNet CLI, resmi preview2 derlemesi olan preview2-003121 öğesine güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="ac7ce-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="ac7ce-205">Paket Yöneticisi Kullanıcı arabirimi: bir paket güncelleştirildikten sonra yeni sürüm gösterme- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="ac7ce-206">-Delete komut satırındaki ApiKey, 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) içinde okunamaz/gönderilmez</span><span class="sxs-lookup"><span data-stu-id="ac7ce-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="ac7ce-207">Hatalı dize: paketin kararlı bir sürümü bir ön sürüm bağımlılığı üzerinde olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="ac7ce-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="ac7ce-209">OptimizedZipPackage önbelleği boş klasörleri bırakır- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="ac7ce-210">PCL (net46 ve Windows 10) projesi oluşturma NullRef özel durumu.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="ac7ce-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="ac7ce-212">Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından kısıtlanmışsa NuGet güncelleştirmesi bilgilendirici ileti sağlamalıdır- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="ac7ce-213">NuGet v3 geri yükleme sorunları- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="ac7ce-214">Kimlik bilgisi eklentisi hata ile çıkıldı-1/birden çok kaynağa sahip kimlik bilgisi sağlayıcıları kullanılırken paket indirme hatası- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="ac7ce-215">`project.json` NuGet geri yükleme hiçbir şey değiştirilmezse yeniden derlemeye neden olur- [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="ac7ce-216">Semboller paketleri, Install veya Update- [#2807](https://github.com/NuGet/Home/issues/2807) içinde hiç kullanılmamalıdır</span><span class="sxs-lookup"><span data-stu-id="ac7ce-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="ac7ce-217">VS yolunda ortam değişkenlerini desteklemez (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="ac7ce-218">Erişilebilirlik için Package Manager Kullanıcı arabirimindeki etiketli UIElements 'i etiketleme- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="ac7ce-219">Hecelenmiş profiller içeren taşınabilir çerçeveler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="ac7ce-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="ac7ce-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="ac7ce-221">NuGet Paket Yöneticisi, paket ayrıntılarındaki seçenekler listesinin #2665 için uygulanmadığından emin olması gerekir `project.json`  -  [](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="ac7ce-222">nuget.exe gönderme/silme API anahtarını kullanmaz- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="ac7ce-223">Kilitli özelliği kilit dosyasından kaldır- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="ac7ce-224">NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. '</span><span class="sxs-lookup"><span data-stu-id="ac7ce-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="ac7ce-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="ac7ce-226">Mevcut olmayan bir yerel kaynaktan paket yükleme, sahte bir ileti oluşturur [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="ac7ce-227">"Yükseltme kullanılabilir" filtresi, sürüm kısıtlamasını ihlal eden yükseltmeleri gösterir- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="ac7ce-228">Yerel paketler güncelleştirilemiyor- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="ac7ce-229">Özellikler</span><span class="sxs-lookup"><span data-stu-id="ac7ce-229">Features</span></span>

* <span data-ttu-id="ac7ce-230">NuGet- [#329](https://github.com/NuGet/Home/issues/329) tarafından eklenen başvurularda CopyLocal ayarını false olarak ayarlama desteği</span><span class="sxs-lookup"><span data-stu-id="ac7ce-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="ac7ce-231">MSBuild 15 için nuget.exe desteği [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="ac7ce-232">İçin paket desteği.`csproj`</span><span class="sxs-lookup"><span data-stu-id="ac7ce-232">Pack support for .`csproj`</span></span><span data-ttu-id="ac7ce-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="ac7ce-234">Yürütülen kullanıcı eylemleri olduğunda kullanıcı eylemini devre dışı bırak- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="ac7ce-235">NuGet #2782 için destek eklemesi gerekir `runtimes/{rid}/nativeassets/{txm}/`  -  [](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="ac7ce-236">NuGet 2. x (zaten 3. x içinde olan) ile uyumlu çerçeve uyumluluk ekleme- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="ac7ce-237">Geri dönüş paketi klasörleri için destek- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="ac7ce-238">Araç paketlerini desteklemek için bir paket türü kavramı tasarlama ve uygulama- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="ac7ce-239">Genel paketler klasörünün yolunu almak için bir API ekleyin- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="ac7ce-240">[#3356](https://github.com/NuGet/Home/issues/3356) semver 2.0.0 'ı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ac7ce-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="ac7ce-241">DCR</span><span class="sxs-lookup"><span data-stu-id="ac7ce-241">DCRs</span></span>

* <span data-ttu-id="ac7ce-242">nuget.exe Push-timeout parametresi çalışmıyor- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="ac7ce-243">Paket açıklama metni seçilebilir olmalıdır [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="ac7ce-244">nuget.exe `.props` ve `.targets` projeleri için dosyalar oluşturmak üzere `.nuproj` etkinleştirin [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="ac7ce-245">Çerçeveleri içeri aktarmaları ile karşılaştırmak için genişletilebilirlik API 'SI ekleme- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="ac7ce-246">#2486 kullanırken bağımlılık seçeneklerini gizle `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="ac7ce-247">Ayrıntılı çıkışta nuget.exe sürüm üst bilgisini Yazdır- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="ac7ce-248">NuGet 'in kullanıcılara bir DotNet TFM tabanlı PCL 'de yükseltmenin/yüklemenin sorun oluşmasına neden olduğunu bilmesini sağlaması gerekir [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="ac7ce-249">"DotNet" projesi için hatalı yüklemeyi/yükseltmeyi uyar = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="ac7ce-250">Güncelleştirme için yeniden şekilsiz ve NuGet ile performans sorunlarını giderin- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="ac7ce-251">Netcoreapp11 ve netstandard17 desteği ekleme- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="ac7ce-252">Belirteç değişiklikleri için AssemblyMetadata özniteliğiyle yararlanın `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="ac7ce-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
