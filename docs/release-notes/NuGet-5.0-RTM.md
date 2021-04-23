---
title: NuGet 5,0 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve CCR 'ler dahil olmak üzere NuGet 5,0 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901752"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="fc2c3-103">NuGet 5,0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="fc2c3-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="fc2c3-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="fc2c3-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="fc2c3-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="fc2c3-105">NuGet version</span></span> | <span data-ttu-id="fc2c3-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fc2c3-106">Available in Visual Studio version</span></span>| <span data-ttu-id="fc2c3-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fc2c3-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="fc2c3-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="fc2c3-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fc2c3-109">Visual Studio 2019 sürüm 16,0</span><span class="sxs-lookup"><span data-stu-id="fc2c3-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="fc2c3-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fc2c3-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="fc2c3-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="fc2c3-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fc2c3-112">Visual Studio 2019 sürüm 16.0.4</span><span class="sxs-lookup"><span data-stu-id="fc2c3-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="fc2c3-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="fc2c3-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="fc2c3-114"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="fc2c3-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="fc2c3-115"><sup>2</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile isteğe bağlı bir install olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fc2c3-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="fc2c3-116">Özet: 5,0 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="fc2c3-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="fc2c3-117">Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820) [filtrelenmiş çözümleri](/visualstudio/ide/filtered-solutions) geri yükleme desteği</span><span class="sxs-lookup"><span data-stu-id="fc2c3-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="fc2c3-118">`BuildTransitive` klasör, paketlerin, ana bilgisayar projesine hedefe/props 'ın geçişli olarak katkıda bulunmasına olanak sağlar- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="fc2c3-119">NuGet IVS API 'Lerinde PackageReference senaryoları için daha iyi destek [](https://github.com/NuGet/Home/issues/7005)-#7005 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="fc2c3-120">`nuget.exe pack project.json` kullanım dışı bırakıldı- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="fc2c3-121">Gen 1 kimlik bilgisi sağlayıcısı eklentisinin yerini [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) ' den geçti ve yakında kullanım dışı bırakılacak [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="fc2c3-122">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="fc2c3-122">Issues fixed in this release</span></span>

<span data-ttu-id="fc2c3-123">**Hata**</span><span class="sxs-lookup"><span data-stu-id="fc2c3-123">**Bugs**</span></span>

* <span data-ttu-id="fc2c3-124">Bir NoOp geri yükleme işlemi yaparken, obj dizininde yazma sırasında \* .dgspec.jsönleyin- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="fc2c3-125">~/5nuget içinde oluşturulan dosyalardaki izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="fc2c3-126">`dotnet list package --outdated` kimlik doğrulaması gerektiren kaynaklarla çalışmaz [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="fc2c3-127">NuGet. VisualStudio. Ivspackageınstaller-Package başvuruları olmayan bir projede çağırmak, varsayılan, PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005) olarak ayarlanmış olsa bile her zaman packages.config kullanır</span><span class="sxs-lookup"><span data-stu-id="fc2c3-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="fc2c3-128">PMC: listelenen paketlerde yeniden yükleme Update-Package başarısız olur ("paket bulunamıyor").</span><span class="sxs-lookup"><span data-stu-id="fc2c3-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="fc2c3-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="fc2c3-130">Deponuz ve VSıX- [#7409](https://github.com/NuGet/Home/issues/7409) üçüncü taraf bildirimi ekleme</span><span class="sxs-lookup"><span data-stu-id="fc2c3-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="fc2c3-131">Verilen sürüm olmadığında NuGet. VisualStudio. Ivspackageınstaller. InstallPackage en son sürümü yüklemelidir [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="fc2c3-132">--DotNet NuGet Push için etkileşimli destek- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="fc2c3-133">Kilit dosyası ile geri yüklenirken, NU1603 uyarısı çıkarılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="fc2c3-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="fc2c3-135">NuGet, en az günlük kaydı ile geri yükleme sırasında proje yolunu yazdırmamalıdır [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="fc2c3-136">--DotNet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727) için etkileşimli destek</span><span class="sxs-lookup"><span data-stu-id="fc2c3-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="fc2c3-137">TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768) ile NuGet. paketleme. Core ' u geri ekleyin</span><span class="sxs-lookup"><span data-stu-id="fc2c3-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="fc2c3-138">plugins_cache iyi çalışmak için daha kısa bir yol gerektirir [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="fc2c3-139">Kullanıcı belirli MSBuild sürümü için sorun olmadıysa MSBuild Discovery yolunu tercih et- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="fc2c3-140">`nuget.exe /?` doğru MSBuild sürümlerini listelemelidir- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="fc2c3-141">NuGet. targets (498, 5): hata: '/T MP/nugetkaralama-mono- [#7793](https://github.com/NuGet/Home/issues/7793) yolunun bir parçası bulunamadı</span><span class="sxs-lookup"><span data-stu-id="fc2c3-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="fc2c3-142">geri yükleme, makine önbelleğinde başvurulan paketin tüm sürümlerinin içeriğini gereksiz şekilde numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="fc2c3-143">MSBuild otomatik algılama, VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) yüklendikten sonra her zaman 16,0 seçer.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="fc2c3-144">bir çözümde DotNet liste paketi çerçeve [#7607](https://github.com/NuGet/Home/issues/7607) için yinelenen girdileri çıktı</span><span class="sxs-lookup"><span data-stu-id="fc2c3-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="fc2c3-145">Ispackageınstaller. InstallPackage eski projelerde ve paketler klasöründe çağrılırken "boş yol adı geçerli değil" özel durumu yok.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="fc2c3-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="fc2c3-147">MSBuild/t: geri yükleme minimum ayrıntı düzeyi daha az olmalıdır- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="fc2c3-148">VS 16.0 'in NuGet Kullanıcı arabirimi, renk sorunları nedeniyle okunamaz sekmeye sahip- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="fc2c3-149">NuGet. Core & NuGet. clients License.txt Açıklama- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="fc2c3-150">Restore, Type- [#7596](https://github.com/NuGet/Home/issues/7596) belirleme denemesi sırasında genel paket klasörünü gereksiz şekilde numaralandırır</span><span class="sxs-lookup"><span data-stu-id="fc2c3-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="fc2c3-151">Kilit dosyası zorlamasının hataları Hata Listesi pencere [#7429](https://github.com/NuGet/Home/issues/7429) göstermelidir</span><span class="sxs-lookup"><span data-stu-id="fc2c3-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="fc2c3-152">NuGet.Configurlama sorunlarını giderme- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="fc2c3-153">MSBuild 'e, yüklemesinin konumunu güncelleştirme- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="fc2c3-154">NuGet. Build. Tasks. Pack bir geliştirme bağımlılığı olmalıdır- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="fc2c3-155">Hata ayıklama sembolleri dahil olmak üzere paket uzantı noktası Ekle- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="fc2c3-156">`dotnet pack` oluşturulan nupkg 'daki bağımlılık sürümü aralığının korunması gerekir (kayan sürüm kullanılıyorsa bile)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="fc2c3-157">`dotnet restore`Kullanıcı düzeyinde yapılandırma da kaynak [#7209](https://github.com/NuGet/Home/issues/7209) olduğunda kimliği doğrulanmış kaynakta başarısız olur</span><span class="sxs-lookup"><span data-stu-id="fc2c3-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="fc2c3-158">Paket, içerik dosyaları için giriş kümesini kısıtlamamalıdır- [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="fc2c3-159">AssetTargetFallback 'nin başarılı olmasını gerektiren bir ProjectReference kullanmak, uyarı almalıdır.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="fc2c3-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="fc2c3-161">CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103) çağrılırken iş parçacığı sorunları nedeniyle kilitlenme</span><span class="sxs-lookup"><span data-stu-id="fc2c3-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="fc2c3-162">`dotnet add package` Yerel yapılandırmada belirtilen bir kaynak için genel yapılandırmadan kimlik bilgileri kullanmaz- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="fc2c3-163">Zaman uyumsuz kod yollarında MEF ile ilgili sorunları akıtma- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="fc2c3-164">İmzalama: iki kez ve çağrı yığını olmadan hata bildirildi- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="fc2c3-165">Güvenilir olmayan imzalama sertifikasıyla imzalı bir paketin yüklenmesi hata [#6318](https://github.com/NuGet/Home/issues/6318) göstermelidir</span><span class="sxs-lookup"><span data-stu-id="fc2c3-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="fc2c3-166">NuGet geri yükleme 2 proje obj dizinini paylaşırken yanlış bir NoOps [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="fc2c3-167">`dotnet restore`Kimliği doğrulanmış akıştaki paketlerle Linux üzerinde with ile birlikte kullanılamaz- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="fc2c3-168">dotnet restore devre dışı bırakılmış makine genelindeki akış nedeniyle başarısız olur [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="fc2c3-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="fc2c3-169">**DCRs**</span></span>

* <span data-ttu-id="fc2c3-170">"DotNet Pack project.jsüzerinde"- [#7928](https://github.com/NuGet/Home/issues/7928) kaldırma işleminin daha sonra uyarı</span><span class="sxs-lookup"><span data-stu-id="fc2c3-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="fc2c3-171">Gen1 Credential eklentisi için bir kullanımdan kaldırma uyarısı ekleyin- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="fc2c3-172">İmzalama: yeniden depo imzalı olarak her pakette istemci doğrulaması gerektirmek için depoyu devre dışı bırak--yeniden Depoimzalar/5.0.0 kaynak- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="fc2c3-173">NuGet.Config ile kaynak başına http istek sayısını sınırla [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="fc2c3-174">NuGet, Net472 target (VSıX 'in 16,0 derlemesini temizlemesine yardımcı olmak için). [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="fc2c3-175">PMC: OpenPackagePage komutunu kaldırma- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="fc2c3-176">NetCoreApp 3,0 eşlemesini NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762) yapın</span><span class="sxs-lookup"><span data-stu-id="fc2c3-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="fc2c3-177">NuGet. \* Packages- [#6516](https://github.com/NuGet/Home/issues/6516) için Netstandard 2.0 desteği ekleyin</span><span class="sxs-lookup"><span data-stu-id="fc2c3-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="fc2c3-178">Paket yazarlarının derleme varlıkları geçişli davranış tanımlamasına izin ver- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="fc2c3-179">Destek VS 2019 çözüm filtresi özelliği.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="fc2c3-180">Ayrıca, proje çözüm içinde değil veya yüklü projeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="fc2c3-181">Tüm çözümü geri yüklemeniz gerekiyor (CLı veya VS aracılığıyla) ilk [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="fc2c3-182">.NET 4.7.2 gerektirmek için NuGet 5,0 derlemeleri (tfd değişikliği aracılığıyla)- [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="fc2c3-183">NuGet. paketleme 'daki NuGetLicenseData ortak bir tür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="fc2c3-184">Spdx 'den alınan lisans meta verilerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="fc2c3-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="fc2c3-186">Eski ayarları kaldır API 'Leri [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="fc2c3-187">1 CPU- [#6742](https://github.com/NuGet/Home/issues/6742) sistemlerdeki geçici çözüm geri yükleme zaman aşımları</span><span class="sxs-lookup"><span data-stu-id="fc2c3-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="fc2c3-188">NuGet, kimlik bilgileri için kimlik doğrulama türlerini filtrelemek için NuGet.config-yapılandırma Ekle seçeneğinde kimlik bilgileri olsa da NTLM kimlik doğrulamasını tercih eder- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="fc2c3-189">PackageReference için EmbedInteropTypes 'ı etkinleştirin (eşleşen Packages.Config özelliği)- [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="fc2c3-190">**[Bu yayında düzeltilen tüm sorunların listesi-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="fc2c3-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="fc2c3-191">Özet: 5.0.2 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="fc2c3-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="fc2c3-192">Güvenlik (dotnet.exe veya mono.exe aracılığıyla çalıştırıldığında)-obj klasörü doğru izinlerle oluşturulmalıdır [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="fc2c3-193">Mono/MacOS üzerinde geri yükleme nuget.exe özel nuget.config ve `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011) başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="fc2c3-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="fc2c3-194">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="fc2c3-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="fc2c3-195">.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel olarak yüklenir ve imza doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="fc2c3-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="fc2c3-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="fc2c3-197">Sorun</span><span class="sxs-lookup"><span data-stu-id="fc2c3-197">Issue</span></span>
<span data-ttu-id="fc2c3-198">Birden çok hedef netcoreapp 1. x ve netcoreapp 2. x ' i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2. x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="fc2c3-199">Bu, geri yükleme sırasında NuGet paketini geri dönüş klasöründen seçer ve genel paketler klasörüne yüklemeyi dener ve hata veren olağan imza doğrulamasını yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="fc2c3-200">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="fc2c3-200">Workaround</span></span>
<span data-ttu-id="fc2c3-201">Geri dönüş klasörünün kullanımını hiçbir şey olarak ayarlayarak devre dışı bırakın `RestoreAdditionalProjectSources` :</span><span class="sxs-lookup"><span data-stu-id="fc2c3-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="fc2c3-202">Geri dönüş klasöründen geri yüklenecek paketler artık NuGet.org adresinden indirileceği için bunu dikkatli kullanın.</span><span class="sxs-lookup"><span data-stu-id="fc2c3-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>