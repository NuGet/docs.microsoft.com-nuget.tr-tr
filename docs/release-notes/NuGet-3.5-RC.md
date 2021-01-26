---
title: 3,5 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780201"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="1c2f0-103">NuGet 3,5 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="1c2f0-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="1c2f0-104">[NuGet 3,5-beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md)  |  [NuGet 3,5-RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="1c2f0-105">3,5 sürümü, NuGet istemcilerinin kalitesini ve performansını geliştirmeye odaklanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="1c2f0-106">Ayrıca, [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899)için destek, ve ' de [PackageType](https://github.com/NuGet/Home/issues/2476) desteği gibi birkaç özelliği sunuyoruz `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="1c2f0-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="1c2f0-107">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="1c2f0-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="1c2f0-108">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="1c2f0-108">Bug Fixes</span></span>

* <span data-ttu-id="1c2f0-109">Bir paketin yükleme/geri yükleme işlemi "paket birden çok dosya içeriyor" ile başarısız olur `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="1c2f0-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="1c2f0-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1c2f0-111">NuGet paketi, `.tt` ne tür bir içeriğe bakılmaksızın dosyaları içerik klasörüne zorla ekler [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1c2f0-112">`project.json`json dosyasında packOptions ve sahip olmadığında NuGet Pack csproj (WITH) kilitleniyor- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1c2f0-113">için NuGet paketi `project.json` , Summary, yazarlar, Owners vs- [#3161](https://github.com/NuGet/Home/issues/3161) gibi packoptions etiketlerini yoksayar</span><span class="sxs-lookup"><span data-stu-id="1c2f0-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1c2f0-114">NuGet paketi `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145) için çıkışta bağımlılıkları yoksayar</span><span class="sxs-lookup"><span data-stu-id="1c2f0-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1c2f0-115">Birden çok paketin geri alma ile güncelleştirilmesi, projeyi bozuk bir durumda bırakır- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1c2f0-116">Netstandart projeler için any altındaki ContentFiles eklenmez- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1c2f0-117">.NET Standard için kitaplık hedeflemesi doğru paketlenemez- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1c2f0-118">Dosya-> yeni proje-> sınıf kitaplığı (taşınabilir) projesi VS2015 ve Dev15- [#3094](https://github.com/NuGet/Home/issues/3094) içinde başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="1c2f0-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1c2f0-119">NuGet hatası-1.0.0-\* geçerli bir sürüm dizesi değil- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1c2f0-120">Find-Package görüntülenemiyor ancak Install-Package çalışmaları [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1c2f0-121">Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) "Install-Package jQuery. Validation" hatası</span><span class="sxs-lookup"><span data-stu-id="1c2f0-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1c2f0-122">Bir VS 2015 güncelleştirme 3 ' ü, NuGet sürümü 3.5.0 hatası oluşursa [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1c2f0-123">Paket Yöneticisi Kullanıcı arabirimi: bir paket güncelleştirildikten sonra yeni sürüm gösterme- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1c2f0-124">-Delete komut satırındaki ApiKey, 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) içinde okunamaz/gönderilmez</span><span class="sxs-lookup"><span data-stu-id="1c2f0-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1c2f0-125">Hatalı dize: paketin kararlı bir sürümü bir ön sürüm bağımlılığı üzerinde olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1c2f0-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1c2f0-127">PCL (net46 ve Windows 10) projesi oluşturma NullRef özel durumu.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1c2f0-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1c2f0-129">Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından kısıtlanmışsa NuGet güncelleştirmesi bilgilendirici ileti sağlamalıdır- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1c2f0-130">Kimlik bilgisi eklentisi hata ile çıkıldı-1/birden çok kaynağa sahip kimlik bilgisi sağlayıcıları kullanılırken paket indirme hatası- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1c2f0-131">NuGet paketi-paket bağımlılığında Newtonsoft.Jseksik [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="1c2f0-132">Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860) ExecuteSynchronizedCore 'da hata</span><span class="sxs-lookup"><span data-stu-id="1c2f0-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="1c2f0-133">VS yolunda ortam değişkenlerini desteklemez (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1c2f0-134">Erişilebilirlik sorunlarını giderme- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1c2f0-135">Hecelenmiş profiller içeren taşınabilir çerçeveler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1c2f0-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1c2f0-137">NuGet Paket Yöneticisi, paket ayrıntılarındaki seçenekler listesinin #2665 için uygulanmadığından emin olması gerekir `project.json`  -  [](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1c2f0-138">NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. '</span><span class="sxs-lookup"><span data-stu-id="1c2f0-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1c2f0-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1c2f0-140">Mevcut olmayan bir yerel kaynaktan paket yükleme, sahte bir ileti oluşturur [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1c2f0-141">"Upgrade vailable" filtresi, sürüm kısıtlamasını ihlal eden yükseltmeleri gösterir- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="1c2f0-142">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="1c2f0-142">Performance Improvements</span></span>

* <span data-ttu-id="1c2f0-143">Performans: ContentModel hedef çerçevesi ayrıştırmayı geliştirme- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="1c2f0-144">Performans: `runtime.json` RID 'ler [#3150](https://github.com/NuGet/Home/issues/3150)olmayan geri yüklemeler Için dosyaları okumaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="1c2f0-145">CI makinelerinde, örnek bir ASP.NET Web uygulamasının geri yüklenmesi 15 saniye ile 3 saniye arasında azaltılır.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="1c2f0-146">Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="1c2f0-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="1c2f0-147">1 milyon ' den 10 ' a kadar bazı durumlarda iyileştirilmiş PackageManagerConsole 'ı açma süresi.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="1c2f0-148">NuGet Update 'de ReSharper performans sorunlarını çözün- [#3044](https://github.com/NuGet/Home/issues/3044): örnek bir projede, paket 140S 'den 68s 'ye düşürüldü.</span><span class="sxs-lookup"><span data-stu-id="1c2f0-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="1c2f0-149">DCR</span><span class="sxs-lookup"><span data-stu-id="1c2f0-149">DCRs</span></span>

* <span data-ttu-id="1c2f0-150">NuGet 'in kullanıcılara bir DotNet TFM tabanlı PCL 'de yükseltmenin/yüklemenin sorun oluşmasına neden olduğunu bilmesini sağlaması gerekir [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1c2f0-151">"DotNet" projesi için hatalı yüklemeyi/yükseltmeyi uyar = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1c2f0-152">Netcoreapp11 ve netstandard17 desteği ekleme- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1c2f0-153">nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934) NuGet-Warning üst bilgi içeriğini konsola yazdırma</span><span class="sxs-lookup"><span data-stu-id="1c2f0-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="1c2f0-154">Belirteç değişiklikleri için AssemblyMetadata özniteliğiyle yararlanın `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="1c2f0-155">Kilitli özelliği kilit dosyasından kaldır- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1c2f0-156">Sembol paketleri, install veya Update #2807 hiçbir zaman kullanılmamalıdır</span><span class="sxs-lookup"><span data-stu-id="1c2f0-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="1c2f0-157">Özellikler</span><span class="sxs-lookup"><span data-stu-id="1c2f0-157">Features</span></span>

* <span data-ttu-id="1c2f0-158">Geri dönüş paketi klasörleri için destek- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1c2f0-159">Araç paketlerini desteklemek için bir paket türü kavramı tasarlama ve uygulama- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1c2f0-160">Genel paketler klasörünün yolunu almak için API- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1c2f0-161">Yerel paketler güncelleştirme desteği- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1c2f0-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
