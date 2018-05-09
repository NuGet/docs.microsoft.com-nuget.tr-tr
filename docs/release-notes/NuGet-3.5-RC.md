---
title: 3.5 RC sürüm notları
description: NuGet 3.5 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="814cc-103">NuGet 3.5 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="814cc-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="814cc-104">[NuGet 3.5 Beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-sürüm notları RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="814cc-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="814cc-105">NuGet istemcileri, kalite ve performansını geliştirmeye 3.5 sürüm odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="814cc-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="814cc-106">Ayrıca, biz desteği gibi birkaç özellikleri gönderilen [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) desteklemek `.nuspec` ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="814cc-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="814cc-107">Konu listesi</span><span class="sxs-lookup"><span data-stu-id="814cc-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="814cc-108">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="814cc-108">Bug Fixes</span></span>

* <span data-ttu-id="814cc-109">Paketi yükle/geri yükleme başarısız oluyor "pakette birden çok `.nuspec` dosyaları."</span><span class="sxs-lookup"><span data-stu-id="814cc-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="814cc-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="814cc-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="814cc-111">nuget paketi zorla ekler `.tt` dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="814cc-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="814cc-112">nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa çöküyor [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="814cc-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="814cc-113">nuget paketini `project.json` packOptions etiketleri özeti, yazarlar, sahipleri vb. - gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="814cc-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="814cc-114">nuget paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="814cc-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="814cc-115">Bozuk durumda - bırakır projeyi geri alma ile birden çok paket güncelleştirme [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="814cc-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="814cc-116">Content altında bulunan dosyaları netstandard projelerde - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="814cc-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="814cc-117">.NET hedefleme kitaplığı paketleyemez standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="814cc-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="814cc-118">Dosya -> Yeni Proje VS2015 ve Dev15 - sınıf kitaplığı (taşınabilir) proje başarısız -> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="814cc-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="814cc-119">nuGet hata - 1.0.0-\* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="814cc-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="814cc-120">Bul-Package başarısız görünen ancak Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="814cc-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="814cc-121">Hata olduğunda "Install-Package jquery.validation" dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="814cc-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="814cc-122">Yüklü VS 2015 sürüm 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="814cc-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="814cc-123">Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürümü görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="814cc-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="814cc-124">-Apikey ile yapılan Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="814cc-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="814cc-125">Yanlış dize: bir paketin durağan sürümü bir ön sürüm bağımlılığı olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="814cc-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="814cc-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="814cc-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="814cc-127">PCL (net46 ve windows 10) proje get NullRef özel durum oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="814cc-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="814cc-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="814cc-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="814cc-129">Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda, Nuget güncelleştirme bilgilendirici ileti temin etmelidir [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="814cc-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="814cc-130">Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / hata indirme paketini kimlik bilgisi sağlayıcıları birden çok kaynaklarıyla - kullanırken [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="814cc-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="814cc-131">nuget paketi - eksik Newtonsoft.Json paket bağımlılığı - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="814cc-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="814cc-132">Linux/MacOS + Mono - üzerinde ExecuteSynchronizedCore hatada [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="814cc-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="814cc-133">VS repositoryPath içinde ortam değişkenlerini desteklemez (nuget.exe yapar) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="814cc-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="814cc-134">Erişilebilirlik sorunları - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="814cc-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="814cc-135">Tirelenmiş profilleriyle taşınabilir çerçeveleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="814cc-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="814cc-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="814cc-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="814cc-137">NuGet Paket Yöneticisi, bu paketleri ayrıntı için geçerli olmayan Seçenekler listesinde temizleyin olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="814cc-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="814cc-138">NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.'</span><span class="sxs-lookup"><span data-stu-id="814cc-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="814cc-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="814cc-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="814cc-140">Sahte bir ileti - paketini atar mevcut olmayan yerel bir kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="814cc-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="814cc-141">"Yükseltme ullanılabilir" filtre gösterir - sürüm kısıtlamayı ihlal yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="814cc-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="814cc-142">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="814cc-142">Performance Improvements</span></span>

* <span data-ttu-id="814cc-143">: ContentModel hedef framework ayrıştırma - performansı [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="814cc-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="814cc-144">Performans: Okuma kaçının `runtime.json` RID olmayan geri yükleme dosyaları [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="814cc-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="814cc-145">CI makinelerde 3 saniye için 15 saniye aşırı derecede ASP.NET Web uygulaması sınırlı bir örnek geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="814cc-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="814cc-146">Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="814cc-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="814cc-147">Bazı durumlarda 132s'den 10'luk için PackageManagerConsole açmak zaman geliştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="814cc-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="814cc-148">NuGet güncelleştirmesi - ReSharper performans sorunları çözmek [#3044](https://github.com/NuGet/Home/issues/3044): bir örnek proje üzerinde paketleri yüklemek için harcanan süre sınırlı 140s 68s için.</span><span class="sxs-lookup"><span data-stu-id="814cc-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="814cc-149">Dcr</span><span class="sxs-lookup"><span data-stu-id="814cc-149">DCRs</span></span>

* <span data-ttu-id="814cc-150">NuGet gereken yükseltme/yükleme dayalı dotnet tfm PCL sorunları - neden olabilecek olduğunu bilmesini sağlamak üzere [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="814cc-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="814cc-151">Hatalı yükleme/yükseltme tfm içeren projesi için uyar "dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="814cc-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="814cc-152">Netcoreapp11 ve netstandard17 desteği - eklemek [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="814cc-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="814cc-153">Nuget.exe içinde - konsol için NuGet uyarı üstbilgi içeriği Yazdır [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="814cc-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="814cc-154">Dengeleme AssemblyMetadata özniteliği için `.nuspec` belirteci değişikliklerini - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="814cc-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="814cc-155">Kilit dosyasından - kilitli özelliği kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="814cc-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="814cc-156">Sembol paketlerini yüklemek için hiç kullanılmamalıdır veya #2807 güncelleştir</span><span class="sxs-lookup"><span data-stu-id="814cc-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="814cc-157">Özellikler</span><span class="sxs-lookup"><span data-stu-id="814cc-157">Features</span></span>

* <span data-ttu-id="814cc-158">Geri dönüş paketi klasörlerinin - desteği [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="814cc-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="814cc-159">Aracı paketler - desteklemek için paket türü kavramını tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="814cc-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="814cc-160">Genel paketler klasörüne - yolu API [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="814cc-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="814cc-161">Güncelleştirme desteği - yerel paketleri [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="814cc-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
