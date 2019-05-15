---
title: NuGet 5.0 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 5.0 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610665"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="b73c6-103">NuGet 5.0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b73c6-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="b73c6-104">NuGet dağıtım araçları:</span><span class="sxs-lookup"><span data-stu-id="b73c6-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="b73c6-105">NuGet sürüm</span><span class="sxs-lookup"><span data-stu-id="b73c6-105">NuGet version</span></span> | <span data-ttu-id="b73c6-106">Visual Studio sürümü içinde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="b73c6-106">Available in Visual Studio version</span></span>| <span data-ttu-id="b73c6-107">.NET SDK'sı sürümünü kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="b73c6-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="b73c6-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="b73c6-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="b73c6-109">Visual Studio 2019 16,0 sürümü</span><span class="sxs-lookup"><span data-stu-id="b73c6-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="b73c6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b73c6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="b73c6-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="b73c6-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="b73c6-112">Visual Studio 2019 16.0.4 sürümü</span><span class="sxs-lookup"><span data-stu-id="b73c6-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="b73c6-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b73c6-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="b73c6-114"><sup>1</sup>.NET Core iş yüküyle Visual Studio 2019 ile yüklü</span><span class="sxs-lookup"><span data-stu-id="b73c6-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="b73c6-115"><sup>2</sup>.NET Core iş yüküyle Visual Studio 2019 ile isteğe bağlı bir yükleme olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="b73c6-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="b73c6-116">Özet: 5. 0'yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="b73c6-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="b73c6-117">Geri yükleme desteği [çözümleri filtrelenmiş](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) Visual Studio 2019 içinde- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="b73c6-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="b73c6-118">`BuildTransitive` Klasör sağlayan geçişli hedefleri/özellikler - ana projeye katkıda bulunmak paketleri [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="b73c6-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="b73c6-119">NuGet Iv'ler API'lerindeki - PackageReference senaryoları için daha iyi destek [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="b73c6-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="b73c6-120">`nuget.exe pack project.json` kullanım dışı - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="b73c6-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="b73c6-121">1. nesil kimlik bilgisi sağlayıcı eklentisi yerini tarafından [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) ve yakında kullanımdan - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="b73c6-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b73c6-122">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b73c6-122">Issues fixed in this release</span></span>

<span data-ttu-id="b73c6-123">**Hataları**</span><span class="sxs-lookup"><span data-stu-id="b73c6-123">**Bugs**</span></span>

* <span data-ttu-id="b73c6-124">NoOp geri yükleme yaparken önlemek \*. obj dizinindeki - dgspec.json yazma [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="b73c6-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="b73c6-125">~/.Nuget içinde oluşturulan dosyalarda izinleri çok açık - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="b73c6-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="b73c6-126">`dotnet list package --outdated` kimlik doğrulama - gereken kaynakları ile işe yaramazsa [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="b73c6-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="b73c6-127">NuGet.VisualStudio.IVsPackageInstaller - arama bir projede yok Paketle başvuran her zaman kullandığı packages.config Packagereference'a - varsayılan olarak ayarlanmış olsa bile [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="b73c6-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="b73c6-128">PMC: Update-Package başarısız olursa ("paketi bulmak için yapılandırılamıyor") delisted paketleri yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b73c6-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="b73c6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="b73c6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="b73c6-130">Bizim depo ve VSIX - üçüncü taraf bildirimi eklemek [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="b73c6-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="b73c6-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage verilen - sürüm, en son sürümünü yüklemelisiniz [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="b73c6-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="b73c6-132">--dotnet nuget gönderim için etkileşimli desteği - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="b73c6-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="b73c6-133">Kilit dosyasıyla geri yüklerken NU1603 uyarı oluşturuldu olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b73c6-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="b73c6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="b73c6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="b73c6-135">NuGet yazdırma proje yolu en az günlük ile-geri yükleme işlemi sırasında [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="b73c6-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="b73c6-136">--dotnet etkileşimli desteğini kaldırmak paket - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="b73c6-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="b73c6-137">Ekleme ile TypeForwardedTo attrs - NuGet.Packaging.Core geri [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="b73c6-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="b73c6-138">plugins_cache iyi - çalışması için daha kısa bir yol gerekiyor [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="b73c6-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="b73c6-139">Kullanıcı için belirli msbuild sürümü - istememiş msbuild bulma yolunu tercih [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="b73c6-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="b73c6-140">`nuget.exe /?` doğru msbuild sürümler - listelemelidir [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="b73c6-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="b73c6-141">NuGet.targets(498,5): hata: Yolun bir bölümü bulunamadı. ' / tmp/NuGetScratch - mono üzerinde- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="b73c6-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="b73c6-142">geri yükleme - makine önbelleğinde başvurulan paketin tüm sürümlerini içeriğini gereksiz yere numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="b73c6-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="b73c6-143">MSBuild otomatik algılamayı 2019 yükleme Önizleme sonra - 16,0 her zaman seçer [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="b73c6-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="b73c6-144">yinelenen girişler için framework - dotnet bir çözüm üzerinde paket listeleme çıkarır [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="b73c6-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="b73c6-145">Özel durum "boş yol adı değil yasal" ne zaman eski üzerinde arama IVsPackageInstaller.InstallPackage projeleri ve klasörü paketler yok.</span><span class="sxs-lookup"><span data-stu-id="b73c6-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="b73c6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="b73c6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="b73c6-147">MSBuild/t: Restore en az ayrıntı düzeyi daha az - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="b73c6-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="b73c6-148">VS 16,0'ın NuGet kullanıcı Arabirimi olan renk sorunları - nedeniyle okunamaz sekmeleri [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="b73c6-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="b73c6-149">NuGet.Core & NuGet.Clients License.txt açıklama - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="b73c6-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="b73c6-150">Geri yükleme türü - belirlemek için gereksiz yere genel bir paket klasörüne numaralandırır [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="b73c6-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="b73c6-151">Kilit dosya zorlama hatalarından görünmesini Hata Listesi penceresinde - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="b73c6-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="b73c6-152">NuGet.Configuration sorunlarını gidermek [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="b73c6-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="b73c6-153">MSBuild'e, yükleme güncelleştirme uyum konumu - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="b73c6-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="b73c6-154">Bir geliştirme bağımlılığı - NuGet.Build.Tasks.Pack olmalıdır [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="b73c6-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="b73c6-155">Dahil etmek için paketi uzantı noktası ekleme hata ayıklama sembolleri - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="b73c6-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="b73c6-156">`dotnet pack` oluşturulan nupkg bağımlılık sürüm aralığında (kayan sürümü kullanılıyorsa bile) - korumak [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="b73c6-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="b73c6-157">`dotnet restore` Kullanıcı düzeyinde yapılandırma kaynağı - varken kimliği doğrulanmış kaynak başarısız [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="b73c6-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="b73c6-158">Paketi için içerik dosyaları - BuildActions kümesini değil kısıtlama [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="b73c6-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="b73c6-159">Başarılı olması AssetTargetFallback gerektiren bir ProjectReference kullanarak bildirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b73c6-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="b73c6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="b73c6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="b73c6-161">CPS (CommonProjectSystem) - çağırırken iş parçacığı oluşturma sorunları nedeniyle kilitlenme [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="b73c6-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="b73c6-162">`dotnet add package` Yerel yapılandırmada - belirtilen bir kaynak için kimlik bilgilerini genel yapılandırmadan kullanmaz [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="b73c6-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="b73c6-163">MEF zaman uyumsuz olarak çağrılan ile iş parçacığı oluşturma sorunları kod yolları - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="b73c6-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="b73c6-164">İmzalama: iki kez ve çağrı yığını - olmadan bildirilen hata [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="b73c6-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="b73c6-165">Güvenilmeyen bir imzalama sertifikasıyla imzalanmış paket yükleme hatası: göstermelidir [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="b73c6-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="b73c6-166">NuGet geri yükleme yanlış Noop'ler obj dizinindeki - 2 projeleri paylaşırken [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="b73c6-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="b73c6-167">PAT ile kullanamazsınız `dotnet restore` kimliği doğrulanmış akışındaki - paketleri ile Linux'ta [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="b73c6-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="b73c6-168">DotNet restore başarısız akışı - devre dışı makine nedeniyle geniş [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="b73c6-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="b73c6-169">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="b73c6-169">**DCRs**</span></span>

* <span data-ttu-id="b73c6-170">"Dotnet paketi project.json" - gelecekteki kaldırılmasını uyar [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="b73c6-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="b73c6-171">Bir Gen1 kimlik bilgisi eklentisi için-kullanımdan kaldırılma uyarısı Ekle [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="b73c6-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="b73c6-172">İmzalama: Etkin depo depo olarak her paketi, istemci doğrulama gerektirecek şekilde imzalanmış--RepositorySignatures/5.0.0 kaynağı aracılığıyla - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="b73c6-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="b73c6-173">http isteği aracılığıyla NuGet.Config - kaynak sayısı sınırlamak [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="b73c6-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="b73c6-174">NuGet (temizleme VSIX'in 16,0 derleme yardımcı olmak için) Net472 - hedef [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="b73c6-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="b73c6-175">PMC: -OpenPackagePage komutu kaldırmak [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="b73c6-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="b73c6-176">NetStandard 2.1 - yapma NetCoreApp 3.0 eşlemesine [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="b73c6-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="b73c6-177">NuGet.\* paketlere - netstandard2.0 desteği Ekle [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="b73c6-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="b73c6-178">Derleme varlıklar geçişli davranışı - tanımlamak paket yazarlarının [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="b73c6-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="b73c6-179">VS 2019 çözüm filtreleme özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="b73c6-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="b73c6-180">Ayrıca, proje çözümde değil veya yüklenmemiş projeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b73c6-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="b73c6-181">Eksiksiz bir çözüm (aracılığıyla, CLI veya VS) ilk - geri yüklemeniz [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="b73c6-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="b73c6-182">NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="b73c6-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="b73c6-183">NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b73c6-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="b73c6-184">Spdx alınan lisans meta verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b73c6-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="b73c6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="b73c6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="b73c6-186">Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="b73c6-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="b73c6-187">Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="b73c6-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="b73c6-188">NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="b73c6-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="b73c6-189">PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="b73c6-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="b73c6-190">**[Bu sürümde - 5.0 RTM düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="b73c6-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="b73c6-191">Özet: 5.0.2 yenilikler</span><span class="sxs-lookup"><span data-stu-id="b73c6-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="b73c6-192">Güvenlik - (dotnet.exe veya mono.exe aracılığıyla çalıştırdığınızda) obj klasörü doğru izinler ile oluşturulması gereken [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="b73c6-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="b73c6-193">mono/macos'ta nuget.exe geri yükleme ile özel nuget.config başarısız olur ve `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="b73c6-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="b73c6-194">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b73c6-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="b73c6-195">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="b73c6-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="b73c6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="b73c6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="b73c6-197">Sorun</span><span class="sxs-lookup"><span data-stu-id="b73c6-197">Issue</span></span>
<span data-ttu-id="b73c6-198">DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b73c6-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="b73c6-199">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="b73c6-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="b73c6-200">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="b73c6-200">Workaround</span></span>
<span data-ttu-id="b73c6-201">Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing:</span><span class="sxs-lookup"><span data-stu-id="b73c6-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="b73c6-202">Geri dönüş klasöründen geri paketleri NuGet.org adresinden artık yüklenebilir olarak bunu dikkatli kullanın.</span><span class="sxs-lookup"><span data-stu-id="b73c6-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
