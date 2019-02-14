---
title: NuGet 5.0-preview sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere NuGet 5.0 Önizleme için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247665"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="3e7e3-103">NuGet 5.0 Preview sürüm notları</span><span class="sxs-lookup"><span data-stu-id="3e7e3-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="3e7e3-104">NuGet 5.0 Önizleme sürümleri</span><span class="sxs-lookup"><span data-stu-id="3e7e3-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="3e7e3-105">13 Şubat 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="3e7e3-106">23 Ocak 2019 - [NuGet 5.0 Önizleme 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="3e7e3-107">Özet: NuGet 5.0 Preview 3 yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3e7e3-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3e7e3-108">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3e7e3-108">Issues fixed in this release</span></span> 

<span data-ttu-id="3e7e3-109">**Hataları:**</span><span class="sxs-lookup"><span data-stu-id="3e7e3-109">**Bugs:**</span></span>

* <span data-ttu-id="3e7e3-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="3e7e3-110">nuget.exe /?</span></span> <span data-ttu-id="3e7e3-111">doğru msbuild sürümler - listelemelidir [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="3e7e3-112">NuGet.targets(498,5): hata: Yolun bir bölümü bulunamadı. ' / tmp/NuGetScratch - mono üzerinde- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="3e7e3-113">geri yükleme - makine önbelleğinde başvurulan paketin tüm sürümlerini içeriğini gereksiz yere numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="3e7e3-114">MSBuild otomatik algılamayı 2019 yükleme Önizleme sonra - 16,0 her zaman seçer [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="3e7e3-115">yinelenen girişler için framework - dotnet bir çözüm üzerinde paket listeleme çıkarır [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="3e7e3-116">Özel durum "boş yol adı değil yasal" ne zaman eski üzerinde arama IVsPackageInstaller.InstallPackage projeleri ve klasörü paketler yok.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="3e7e3-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="3e7e3-118">MSBuild/t: Restore en az ayrıntı düzeyi daha az - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="3e7e3-119">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="3e7e3-119">**DCRs**</span></span>

* <span data-ttu-id="3e7e3-120">Derleme varlıklar geçişli davranışı - tanımlamak paket yazarlarının [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="3e7e3-121">Proje çözümün bir parçası değil veya yüklü değil, ancak daha önce yüklendi - başarılı olması için VS geri yükleme etkinleştirme [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="3e7e3-122">Özet: 5.0 Önizleme 2'de yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3e7e3-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3e7e3-123">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3e7e3-123">Issues fixed in this release</span></span>

<span data-ttu-id="3e7e3-124">**Hataları:**</span><span class="sxs-lookup"><span data-stu-id="3e7e3-124">**Bugs:**</span></span>

* <span data-ttu-id="3e7e3-125">VS 16,0'ın NuGet kullanıcı Arabirimi olan renk sorunları - nedeniyle okunamaz sekmeleri [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="3e7e3-126">NuGet.Core & NuGet.Clients License.txt açıklama - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="3e7e3-127">Geri yükleme türü - belirlemek için gereksiz yere genel bir paket klasörüne numaralandırır [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="3e7e3-128">Kilit dosya zorlama hatalarından görünmesini Hata Listesi penceresinde - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="3e7e3-129">NuGet.Configuration sorunlarını gidermek [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="3e7e3-130">MSBuild güncelleştirmeye uyarlar bunu kullanıcının yükleme konumu.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="3e7e3-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="3e7e3-132">Bir geliştirme bağımlılığı - NuGet.Build.Tasks.Pack olmalıdır [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="3e7e3-133">Dahil etmek için paketi uzantı noktası ekleme hata ayıklama sembolleri - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="3e7e3-134">DotNet paketi bağımlılık sürüm aralığında oluşturulan nupkg korumak.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="3e7e3-135">(kayan sürümü kullanılıyorsa bile) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="3e7e3-136">DotNet restore başarısız kaynak kimliği doğrulanmış kullanıcı düzeyinde yapılandırma kaynağı - olduğunda [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="3e7e3-137">Paketi için içerik dosyaları - BuildActions kümesini değil kısıtlama [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="3e7e3-138">Başarılı olması AssetTargetFallback gerektiren bir projectreference kullanarak bildirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="3e7e3-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="3e7e3-140">CPS (CommonProjectSystem) - çağırırken iş parçacığı oluşturma sorunları nedeniyle kilitlenme [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="3e7e3-141">DotNet ekleme paket yerel yapılandırmada - belirtilen bir kaynak için kimlik bilgilerini genel yapılandırmadan kullanmayacağınız [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="3e7e3-142">İş parçacığı oluşturma sorunları olan MEF ile zaman uyumsuz yollarında üzerinde - adlı [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="3e7e3-143">İmzalama: iki kez ve çağrı yığını - olmadan bildirilen hata [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="3e7e3-144">Güvenilmeyen bir imzalama sertifikasıyla imzalanmış paket yükleme hatası: göstermelidir [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="3e7e3-145">NuGet geri yükleme yanlış Noop'ler obj dizinindeki - 2 projeleri paylaşırken [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="3e7e3-146">Kimliği doğrulanmış akışındaki - paketleri ile Linux'ta dotnet restore PAT kullanamazsınız [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="3e7e3-147">DotNet restore başarısız akışı - devre dışı makine nedeniyle geniş [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="3e7e3-148">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="3e7e3-148">**DCRs**</span></span>

* <span data-ttu-id="3e7e3-149">NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="3e7e3-150">NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="3e7e3-151">Spdx alınan lisans meta verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="3e7e3-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="3e7e3-153">Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="3e7e3-154">Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="3e7e3-155">NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="3e7e3-156">PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="3e7e3-157">Bu yayın 5.0.0-preview2 içinde düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="3e7e3-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="3e7e3-158">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3e7e3-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="3e7e3-159">DotNet nuget push--etkileşimli Mac üzerinde bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="3e7e3-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="3e7e3-161">**Sorunu** `--interactive` bağımsız değişken dotnet CLI tarafından iletilmez değil ve sonuçları hata `error: Missing value for option 'interactive'` 
 **geçici çözüm** gibietkileşimliseçeneğiyleherhangibirdotnetkomutunuçalıştırın`dotnet restore --interactive` ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="3e7e3-162">Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="3e7e3-163">Ardından çalıştırın `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="3e7e3-164">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3e7e3-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3e7e3-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="3e7e3-166">**Sorunu** dotnet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3e7e3-167">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="3e7e3-168">**Geçici çözüm** ayarlayarak geri dönüş klasörü kullanımını devre dışı `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="3e7e3-169">`<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e7e3-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
