---
title: NuGet 5.0-preview sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere NuGet 5.0 Önizleme için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196206"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="643d9-103">NuGet 5.0 Preview sürüm notları</span><span class="sxs-lookup"><span data-stu-id="643d9-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="643d9-104">NuGet 5.0 Önizleme sürümleri</span><span class="sxs-lookup"><span data-stu-id="643d9-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="643d9-105">27 Şubat 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="643d9-105">February 27, 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span></span>
* <span data-ttu-id="643d9-106">13 Şubat 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="643d9-106">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="643d9-107">23 Ocak 2019 - [NuGet 5.0 Önizleme 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="643d9-107">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="643d9-108">Özet: NuGet 5.0 Preview 4 sürümünde yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="643d9-108">Summary: What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="643d9-109">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="643d9-109">Issues fixed in this release</span></span>

<span data-ttu-id="643d9-110">**Hataları:**</span><span class="sxs-lookup"><span data-stu-id="643d9-110">**Bugs:**</span></span>

* <span data-ttu-id="643d9-111">NuGet.VisualStudio.IVsPackageInstaller - arama bir projede yok Paketle başvuran her zaman kullandığı packages.config Packagereference'a - varsayılan olarak ayarlanmış olsa bile [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="643d9-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="643d9-112">PMC: Update-Package başarısız olursa ("paketi bulmak için yapılandırılamıyor") delisted paketleri yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="643d9-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="643d9-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="643d9-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="643d9-114">Bizim depo ve VSIX - üçüncü taraf bildirimi eklemek [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="643d9-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="643d9-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage verilen - sürüm, en son sürümünü yüklemelisiniz [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="643d9-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="643d9-116">--dotnet nuget gönderim için etkileşimli desteği - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="643d9-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="643d9-117">Kilit dosyasıyla geri yüklerken NU1603 uyarı oluşturuldu olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="643d9-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="643d9-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="643d9-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="643d9-119">NuGet yazdırma proje yolu en az günlük ile-geri yükleme işlemi sırasında [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="643d9-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="643d9-120">--dotnet etkileşimli desteğini kaldırmak paket - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="643d9-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="643d9-121">Ekleme ile TypeForwardedTo attrs - NuGet.Packaging.Core geri [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="643d9-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="643d9-122">plugins_cache iyi - çalışması için daha kısa bir yol gerekiyor [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="643d9-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="643d9-123">Kullanıcı için belirli msbuild sürümü - istememiş msbuild bulma yolunu tercih [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="643d9-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="643d9-124">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="643d9-124">**DCRs:**</span></span>

* <span data-ttu-id="643d9-125">http isteği aracılığıyla NuGet.Config - kaynak sayısı sınırlamak [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="643d9-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="643d9-126">NuGet (temizleme VSIX'in 16,0 derleme yardımcı olmak için) Net472 - hedef [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="643d9-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="643d9-127">PMC: -OpenPackagePage komutu kaldırmak [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="643d9-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="643d9-128">NetStandard 2.1 - yapma NetCoreApp 3.0 eşlemesine [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="643d9-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="643d9-129">NuGet.\* paketlere - netstandard2.0 desteği Ekle [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="643d9-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="643d9-130">Özet: NuGet 5.0 Preview 3 yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="643d9-130">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="643d9-131">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="643d9-131">Issues fixed in this release</span></span> 

<span data-ttu-id="643d9-132">**Hataları:**</span><span class="sxs-lookup"><span data-stu-id="643d9-132">**Bugs:**</span></span>

* <span data-ttu-id="643d9-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="643d9-133">nuget.exe /?</span></span> <span data-ttu-id="643d9-134">doğru msbuild sürümler - listelemelidir [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="643d9-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="643d9-135">NuGet.targets(498,5): hata: Yolun bir bölümü bulunamadı. ' / tmp/NuGetScratch - mono üzerinde- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="643d9-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="643d9-136">geri yükleme - makine önbelleğinde başvurulan paketin tüm sürümlerini içeriğini gereksiz yere numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="643d9-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="643d9-137">MSBuild otomatik algılamayı 2019 yükleme Önizleme sonra - 16,0 her zaman seçer [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="643d9-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="643d9-138">yinelenen girişler için framework - dotnet bir çözüm üzerinde paket listeleme çıkarır [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="643d9-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="643d9-139">Özel durum "boş yol adı değil yasal" ne zaman eski üzerinde arama IVsPackageInstaller.InstallPackage projeleri ve klasörü paketler yok.</span><span class="sxs-lookup"><span data-stu-id="643d9-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="643d9-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="643d9-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="643d9-141">MSBuild/t: Restore en az ayrıntı düzeyi daha az - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="643d9-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="643d9-142">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="643d9-142">**DCRs:**</span></span>

* <span data-ttu-id="643d9-143">Derleme varlıklar geçişli davranışı - tanımlamak paket yazarlarının [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="643d9-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="643d9-144">Proje çözümün bir parçası değil veya yüklü değil, ancak daha önce yüklendi - başarılı olması için VS geri yükleme etkinleştirme [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="643d9-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="643d9-145">Özet: 5.0 Önizleme 2'de yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="643d9-145">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="643d9-146">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="643d9-146">Issues fixed in this release</span></span>

<span data-ttu-id="643d9-147">**Hataları:**</span><span class="sxs-lookup"><span data-stu-id="643d9-147">**Bugs:**</span></span>

* <span data-ttu-id="643d9-148">VS 16,0'ın NuGet kullanıcı Arabirimi olan renk sorunları - nedeniyle okunamaz sekmeleri [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="643d9-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="643d9-149">NuGet.Core & NuGet.Clients License.txt açıklama - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="643d9-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="643d9-150">Geri yükleme türü - belirlemek için gereksiz yere genel bir paket klasörüne numaralandırır [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="643d9-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="643d9-151">Kilit dosya zorlama hatalarından görünmesini Hata Listesi penceresinde - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="643d9-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="643d9-152">NuGet.Configuration sorunlarını gidermek [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="643d9-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="643d9-153">MSBuild güncelleştirmeye uyarlar bunu kullanıcının yükleme konumu.</span><span class="sxs-lookup"><span data-stu-id="643d9-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="643d9-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="643d9-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="643d9-155">Bir geliştirme bağımlılığı - NuGet.Build.Tasks.Pack olmalıdır [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="643d9-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="643d9-156">Dahil etmek için paketi uzantı noktası ekleme hata ayıklama sembolleri - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="643d9-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="643d9-157">DotNet paketi bağımlılık sürüm aralığında oluşturulan nupkg korumak.</span><span class="sxs-lookup"><span data-stu-id="643d9-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="643d9-158">(kayan sürümü kullanılıyorsa bile) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="643d9-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="643d9-159">DotNet restore başarısız kaynak kimliği doğrulanmış kullanıcı düzeyinde yapılandırma kaynağı - olduğunda [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="643d9-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="643d9-160">Paketi için içerik dosyaları - BuildActions kümesini değil kısıtlama [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="643d9-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="643d9-161">Başarılı olması AssetTargetFallback gerektiren bir projectreference kullanarak bildirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="643d9-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="643d9-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="643d9-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="643d9-163">CPS (CommonProjectSystem) - çağırırken iş parçacığı oluşturma sorunları nedeniyle kilitlenme [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="643d9-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="643d9-164">DotNet ekleme paket yerel yapılandırmada - belirtilen bir kaynak için kimlik bilgilerini genel yapılandırmadan kullanmayacağınız [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="643d9-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="643d9-165">İş parçacığı oluşturma sorunları olan MEF ile zaman uyumsuz yollarında üzerinde - adlı [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="643d9-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="643d9-166">İmzalama: iki kez ve çağrı yığını - olmadan bildirilen hata [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="643d9-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="643d9-167">Güvenilmeyen bir imzalama sertifikasıyla imzalanmış paket yükleme hatası: göstermelidir [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="643d9-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="643d9-168">NuGet geri yükleme yanlış Noop'ler obj dizinindeki - 2 projeleri paylaşırken [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="643d9-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="643d9-169">Kimliği doğrulanmış akışındaki - paketleri ile Linux'ta dotnet restore PAT kullanamazsınız [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="643d9-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="643d9-170">DotNet restore başarısız akışı - devre dışı makine nedeniyle geniş [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="643d9-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="643d9-171">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="643d9-171">**DCRs:**</span></span>

* <span data-ttu-id="643d9-172">NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="643d9-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="643d9-173">NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="643d9-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="643d9-174">Spdx alınan lisans meta verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="643d9-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="643d9-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="643d9-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="643d9-176">Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="643d9-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="643d9-177">Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="643d9-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="643d9-178">NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="643d9-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="643d9-179">PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="643d9-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="643d9-180">Bu yayın 5.0.0-preview2 içinde düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="643d9-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="643d9-181">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="643d9-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="643d9-182">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="643d9-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="643d9-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="643d9-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="643d9-184">**Sorunu** dotnet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="643d9-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="643d9-185">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="643d9-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="643d9-186">**Geçici çözüm** ayarlayarak geri dönüş klasörü kullanımını devre dışı `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="643d9-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="643d9-187">`<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.</span><span class="sxs-lookup"><span data-stu-id="643d9-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
