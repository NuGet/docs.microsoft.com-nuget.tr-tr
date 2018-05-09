---
title: NuGet 3.5 Beta sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.5 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="16b02-103">NuGet 3.5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="16b02-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="16b02-104">[NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="16b02-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="16b02-105">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="16b02-105">Bug Fixes</span></span>

* <span data-ttu-id="16b02-106">Paketi mono üzerinde - MSBuild 14.1 kullanıyorsanız değil [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="16b02-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="16b02-107">Bunun yerine select geçerli yüklü sürümü - güncelleştirmek için en son sürüme güncelleştirme sekmesini seçin değil [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="16b02-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="16b02-108">Kilitlenme MyGet akış özel v2 kimlik doğrulaması ve "Daha fazla sonuç x Göster" düğmesini sonra düzeltme- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="16b02-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="16b02-109">Günlük iletilerini gözükmüyor ters sırada için kullanıcı Arabirimi - [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="16b02-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="16b02-110">V3.4.4 - Nuget restore oluşturur "verilen yolun biçimi desteklenmiyor" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="16b02-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="16b02-111">NuGet cmdLine 3.6 beta dikkate almayabilir - Prop yapılandırma yayın - = [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="16b02-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="16b02-112">Nuget IKVM yavaş yüklemek büyük projede - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="16b02-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="16b02-113">nuget.exe - Self tutar üzerinde güncelleştirme kendisini - güncelleştirme [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="16b02-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="16b02-114">3.5 yükleme/geri yükleme UNC paylaşımından sahip performansı regresyon 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="16b02-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="16b02-115">Moq net451 proje - paket Yönetimi kullanıcı Arabirimi yüklenirken bir hata oluştu [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="16b02-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="16b02-116">Çözüm düzeyinde yükleme sekmesini paketin sürümü - göster değil [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="16b02-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="16b02-117">xproj `project.json` yüklü sekmesinden güncelleştirme durumunu - kaybederse [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="16b02-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="16b02-118">NuGet paketine `.csproj` boş dosyaları öğesinde yoksayar `.nuspec` dosyası - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="16b02-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="16b02-119">IIS barındırılan Web sitesi projelerine neden olmaz geri yükleme başarısız olmasına - [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="16b02-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="16b02-120">Kimlik bilgileri v3 uç noktası için v2 - yönlendirildiklerinde Nuget.Config alınmamış [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="16b02-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="16b02-121">NuGet paketi başarısız taşınabilir derleme meta verilerini - alınırken derleme çözülemedi [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="16b02-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="16b02-122">Nuget bulamıyor `msbuild.exe` Mono üzerinde- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="16b02-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="16b02-123">nuget.exe paketi numaralarıyla - başlayan bir yayım öncesi etiketi izin vermez [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="16b02-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="16b02-124">nuget paketi yüklemesi başarısız VS2015E üzerinde - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="16b02-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="16b02-125">allowedVersions filtre değil çalışma çözüm düzeyinde - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="16b02-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="16b02-126">Geri yükleme rastgele başarısız bir öğesiyle aynı anahtarı zaten eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="16b02-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="16b02-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="16b02-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="16b02-128">İçinde Nuget.Common yükleyemezsiniz `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="16b02-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="16b02-129">Kullanıcı arabirimini kullanarak V2 kaynak aramak için iki kez her kimliği için - FindPackagesById adlı [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="16b02-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="16b02-130">Paketler projelerde - bağımlı [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="16b02-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="16b02-131">-Exclude belgelenen ancak desteklenmiyor - nuget.exe paketi [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="16b02-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="16b02-132">Hata ile ilgili sorunları iletileri 'Content ' dosyaları bölümünü `.nuspec` geçersiz - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="16b02-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="16b02-133">Anında iletme her zaman gönderir tüm paketi iki kez ile kimlik doğrulaması paket kaynaklarını - [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="16b02-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="16b02-134">Proje sırasında nuget.exe güncelleştirme \*.csproj çağırma olmadığı zaman hiçbir bilgi verilen bir `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="16b02-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="16b02-135">`packages.config` geri yükleme 5xx durum kodları V2 kaynaklardan - yeniden [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="16b02-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="16b02-136">Dosya src çift nokta `.nuspec` çalışmıyor - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="16b02-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="16b02-137">CoreCLR geri yükleme gereken şifreleme - akışlarıyla yoksaymak [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="16b02-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="16b02-138">nuget.exe push - yanlış kimlik bilgileri - 403 işleme [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="16b02-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="16b02-139">NuGet Paket Yöneticisi Update'de kaldırır özelliklerinden `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="16b02-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="16b02-140">NuGet.PackageManagement.VisualStudio deneyin "NuGet.TeamFoundationServer14" ancak DLL adı "NuGet.TeamFoundationServer" - değiştirilen yüklemek [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="16b02-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="16b02-141">Paket Yöneticisi kullanıcı Arabirimi olmayan Göster yeni güncelleştirilmiş sürümünü - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="16b02-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="16b02-142">güncelleştirme paketi PackageId, kullanmayı denemek yerine package.version - sürüm [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="16b02-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="16b02-143">nuget restore csproj gereken hata nuget proje kullanıyorsa (`packages.config` veya `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="16b02-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="16b02-144">TFS hata "[dosya] çalışma alanında bulunan olmaması veya erişmek için izniniz yok" sırasında yükseltmeniz veya kaldırmanız için TFS kaynak denetimindeki - çözüm/proje bağlandığında [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="16b02-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="16b02-145">güncelleştirme paketi hedef olmayan paket için-bağımlılıklar açılmıyor [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="16b02-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="16b02-146">Nuget Paket Yöneticisi kullanıcı Arabirimi eylemlerini - günlükleri ayrıntı düzeyini ayarlamak için bir yolu yoktur [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="16b02-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="16b02-147">nuget yapılandırması geçersiz - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="16b02-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="16b02-148">İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) çalışmıyor - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="16b02-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="16b02-149">nuget 3.4.3 yayın - değerini alırken üzerinde paket oluşturma - null olamaz [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="16b02-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="16b02-150">geri yükleme için VSTS akışları - Nuget.Config depolanan kimlik bilgilerini değil kullanıyor [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="16b02-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="16b02-151">[dotnet geri yükleme]--configfile olan proje dir cmd dir - yerine göre [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="16b02-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="16b02-152">Sürüm karşılaştırma kodu - aşırı ayırma [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="16b02-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="16b02-153">Birden çok örneğini aynı yüklemeye çalıştığınız nuget.exe içinde paralel nedenler çift yazma - paketini [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="16b02-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="16b02-154">Birden çok proje işlemleri için - bağımlılık bilgileri önbelleğe alınmaz [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="16b02-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="16b02-155">Yükleme ve güncelleştirme yükleme paketleri paketler klasörü önce - denetlemeden [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="16b02-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="16b02-156">Paket kaynak liste boşsa, kullanıcı Arabirimi aracılığıyla paket kaynağı eklenemiyor (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="16b02-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="16b02-157">Tasarım zamanı cepheleri üzerinde - bağlıdır paketini yüklemeye çalışırken hata yanıltıcı [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="16b02-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="16b02-158">Bir paketi "Tümü" ayar PackageManager konsolundan yükleme çalışır yalnızca ilk kaynak - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="16b02-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="16b02-159">Değil olan son beta ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="16b02-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="16b02-160">Kendi kendine yerleşik NuGet 3.4.1 - başlangıçta VS2015 kilitlenme [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="16b02-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="16b02-161">Güncelleştirme komutu i gerçekleştiremezler... - olmasını isteyin, biraz daha ayrıntılı olabilir [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="16b02-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="16b02-162">Yerel olarak oluşturulmuş VSIX aynı DLL'ler ve dosyaları CI yapı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="16b02-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="16b02-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="16b02-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="16b02-164">Yapı - NuGet indirgeme uyarılarını düzeltmenize [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="16b02-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="16b02-165">Paket kaynağı (3 kez) kimlik doğrulaması gerçekleştiremeyen engellenmiş sonsuza kadar - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="16b02-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="16b02-166">Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 +'dan yükleme bağımsız değişkeniyle akış zaman - NoCache paketi içeriyorsa `.nupkg` dosyaları - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="16b02-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="16b02-167">Tüm paket kaynaklarını, ancak paket 1 kaynağından eksik olan Nuget yükleme başarısız - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="16b02-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="16b02-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="16b02-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="16b02-169">Tek bir kaynak yetkilendirme - blokları yükleyin [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="16b02-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="16b02-170">`.nuspec` Aralık - IncludeReferencedProjects sürümü - geçersiz kıl sürüm [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="16b02-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="16b02-171">Güncelleştirme paketi Süper yavaş - "bağımlılık bilgileri toplanmaya çalışılıyor" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="16b02-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="16b02-172">Gizlilik downgrades NuGet paketini toplu bağımlılıklarını - güncelleştirme [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="16b02-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="16b02-173">nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır.</span><span class="sxs-lookup"><span data-stu-id="16b02-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="16b02-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="16b02-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="16b02-175">"DefaultPushSource" - için göreli dosya yolu [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="16b02-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="16b02-176">Çözümleyici hata iletileri - artırmak [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="16b02-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="16b02-177">v3 güncelleştirme paketine başarısız değil, belirtilen kaynak - paketleriyle [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="16b02-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="16b02-178">Paket kaynaklarını için göreli yollar kullanılarak kullanılacak - sorunlu [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="16b02-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="16b02-179">Eksik bağımlılık NUPKG dosyasına dolaylı bağımlılık ile daha düşük bir sürüm gereksinimini - zaten varsa projeden oluşturulan [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="16b02-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="16b02-180">Bir projeyi silmek, karşılık gelen UI penceresi kapanır, ancak projeyi yeniden adlandırma UI pencere yeniden adlandırmak değil.</span><span class="sxs-lookup"><span data-stu-id="16b02-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="16b02-181">Not PMC projeyi yeniden adlandırma ile proje kaldırma olaylarını - dinler [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="16b02-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="16b02-182">[Willow Web iş yükü] Razor v3 WSP oluşturma askıda - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="16b02-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="16b02-183">"Birden fazla nuspec dosyası pakette ile." belirli bir paketin yükleme/geri yükleme başarısız olur</span><span class="sxs-lookup"><span data-stu-id="16b02-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="16b02-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="16b02-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="16b02-185">Küçük harf kimlikleri & `packages.config` senaryoları - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="16b02-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="16b02-186">[3.5-beta2] Paket geri yüklemesi başarısız "eski" paketlerini - geri yüklemek [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="16b02-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="16b02-187">nuget paketi zorla ekler .tt dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="16b02-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="16b02-188">güncelleştirme paketi, ASP.NET web uygulaması oluşturur dosyasına ilgili uyarı: kaynak - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="16b02-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="16b02-189">nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa çöküyor [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="16b02-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="16b02-190">nuget paketini `project.json` packOptions etiketleri özeti, yazarlar, sahipleri vb. - gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="16b02-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="16b02-191">NullReferenceException NuGet.Packaging.PhysicalPackageFile.GetStream - aracılığıyla [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="16b02-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="16b02-192">NuGet paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="16b02-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="16b02-193">Bozuk durumda - bırakır projeyi geri alma ile birden çok paket güncelleştirme [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="16b02-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="16b02-194">Content altında bulunan dosyaları netstandard projelerde - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="16b02-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="16b02-195">.NET hedefleme kitaplığı paketleyemez standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="16b02-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="16b02-196">Dosya -> Yeni Proje VS2015 ve Dev15 - sınıf kitaplığı (taşınabilir) proje başarısız -> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="16b02-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="16b02-197">nuGet hata - 1.0.0-\* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="16b02-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="16b02-198">Bul-Package başarısız görünen ancak Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="16b02-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="16b02-199">Hata olduğunda "Install-Package jquery.validation" dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="16b02-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="16b02-200">xproj nuget paketi için geçersiz hedef yol - varsayarak [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="16b02-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="16b02-201">Yüklü VS 2015 sürüm 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="16b02-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="16b02-202">"Packages.config tarafından engellendi" `project.json` (UWP, tümleşik a.k.a yapı) proje - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="16b02-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="16b02-203">Resmi preview2 yapıdır preview2-003121, yapı komut dosyası tarafından yüklenen dotnet CLI güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="16b02-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="16b02-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="16b02-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="16b02-205">Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürümü görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="16b02-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="16b02-206">-Apikey ile yapılan Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="16b02-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="16b02-207">Yanlış dize: bir paketin durağan sürümü bir ön sürüm bağımlılığı olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="16b02-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="16b02-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="16b02-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="16b02-209">OptimizedZipPackage önbellek bırakır boş klasörler - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="16b02-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="16b02-210">PCL (net46 ve windows 10) proje get NullRef özel durum oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="16b02-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="16b02-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="16b02-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="16b02-212">Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda, Nuget güncelleştirme bilgilendirici ileti temin etmelidir [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="16b02-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="16b02-213">Nuget v3 geri yükleme sorunları - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="16b02-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="16b02-214">Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / hata indirme paketini kimlik bilgisi sağlayıcıları birden çok kaynaklarıyla - kullanırken [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="16b02-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="16b02-215">`project.json` nuget restore neden olan bir şey olduğunda değiştirilen - yeniden derlenmek [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="16b02-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="16b02-216">Simgeler paketleri hiç olmamalıdır yükleme veya güncelleştirme - kullanılan [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="16b02-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="16b02-217">VS repositoryPath içinde ortam değişkenlerini desteklemez (nuget.exe yapar) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="16b02-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="16b02-218">Paket Yöneticisi arabiriminde etiketlenmemiş UIElements için erişilebilirlik - etiket [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="16b02-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="16b02-219">Tirelenmiş profilleriyle taşınabilir çerçeveleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="16b02-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="16b02-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="16b02-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="16b02-221">NuGet Paket Yöneticisi, bu paketleri ayrıntı için geçerli olmayan Seçenekler listesinde temizleyin olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="16b02-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="16b02-222">nuget.exe itme/silme, API anahtarı - kullanmayacağınız [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="16b02-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="16b02-223">Kilit dosyasından - kilitli özelliği kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="16b02-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="16b02-224">NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.'</span><span class="sxs-lookup"><span data-stu-id="16b02-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="16b02-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="16b02-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="16b02-226">Sahte bir ileti - paketini atar mevcut olmayan yerel bir kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="16b02-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="16b02-227">"Kullanılabilir yükseltme" filtre gösterir - sürüm kısıtlamayı ihlal yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="16b02-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="16b02-228">Yerel paketler - güncelleştirilemiyor [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="16b02-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="16b02-229">Özellikler</span><span class="sxs-lookup"><span data-stu-id="16b02-229">Features</span></span>

* <span data-ttu-id="16b02-230">NuGet tarafından - eklenen başvuruları false ayarı CopyLocal desteği [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="16b02-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="16b02-231">MSBuild 15 - nuget.exe desteği [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="16b02-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="16b02-232">Paketi desteği.`csproj`</span><span class="sxs-lookup"><span data-stu-id="16b02-232">Pack support for .`csproj`</span></span><span data-ttu-id="16b02-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="16b02-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="16b02-234">Yürütülmekte olan kullanıcı eylemlerini olduğunda kullanıcı eylemi devre dışı bırak- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="16b02-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="16b02-235">NuGet desteği ekleme `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="16b02-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="16b02-236">NuGet içinde eksik framework uyumluluğunu ekleyin (olan zaten 3.x içinde) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="16b02-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="16b02-237">Geri dönüş paketi klasörlerinin - desteği [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="16b02-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="16b02-238">Aracı paketler - desteklemek için paket türü kavramını tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="16b02-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="16b02-239">Genel paketler klasörüne - yolu bir API ekleme [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="16b02-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="16b02-240">SemVer 2.0.0 paketinde - etkinleştirmek [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="16b02-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="16b02-241">Dcr</span><span class="sxs-lookup"><span data-stu-id="16b02-241">DCRs</span></span>

* <span data-ttu-id="16b02-242">nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="16b02-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="16b02-243">Paket açıklama metnini seçilebilir - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="16b02-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="16b02-244">Üretmek nuget.exe etkinleştirmek `.props` ve `.targets` dosyalarını `.nuproj` projeleri [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="16b02-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="16b02-245">Genişletilebilirlik içeri aktarmalar - çerçeveleri karşılaştırmak için API'sı ekleme [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="16b02-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="16b02-246">Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="16b02-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="16b02-247">Ayrıntılı bir çıkış - nuget.exe sürüm üstbilgisinde çıkışı yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="16b02-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="16b02-248">NuGet gereken yükseltme/yükleme dayalı dotnet tfm PCL sorunları - neden olabilecek olduğunu bilmesini sağlamak üzere [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="16b02-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="16b02-249">Hatalı yükleme/yükseltme tfm içeren projesi için uyar "dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="16b02-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="16b02-250">Güncelleştirmesi - ReShaper ve NuGet ile performans sorunlarını çözün [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="16b02-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="16b02-251">Netcoreapp11 ve netstandard17 desteği - eklemek [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="16b02-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="16b02-252">Dengeleme AssemblyMetadata özniteliği için `.nuspec` belirteci değişikliklerini - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="16b02-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
