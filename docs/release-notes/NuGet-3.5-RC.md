---
title: 3.5 RC sürüm notları
description: NuGet 3.5 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548544"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="50ff1-103">NuGet 3.5 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="50ff1-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="50ff1-104">[NuGet 3.5-Beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="50ff1-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="50ff1-105">sürüm 3.5 kalitesini ve NuGet istemcilerinin performansını geliştirmeye odaklanır.</span><span class="sxs-lookup"><span data-stu-id="50ff1-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="50ff1-106">Ayrıca, biz desteği gibi bazı özellikler gönderildi [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) desteklemek `.nuspec` ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="50ff1-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="50ff1-107">Sorun listesi</span><span class="sxs-lookup"><span data-stu-id="50ff1-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="50ff1-108">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="50ff1-108">Bug Fixes</span></span>

* <span data-ttu-id="50ff1-109">Paketi yükle/geri yükleme başarısız oluyor "pakette birden çok `.nuspec` dosyalarını."</span><span class="sxs-lookup"><span data-stu-id="50ff1-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="50ff1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="50ff1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="50ff1-111">nuget paketi zorla ekler `.tt` dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="50ff1-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="50ff1-112">nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa kilitleniyor [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="50ff1-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="50ff1-113">nuget paketi için `project.json` packOptions etiketleri özeti, yazarlar, sahipleri - vb. gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="50ff1-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="50ff1-114">nuget paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="50ff1-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="50ff1-115">Geri alma ile birden çok paketlerin güncelleştirilmesi, bozuk bir durumda - proje bırakır [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="50ff1-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="50ff1-116">ContentFiles herhangi netstandard projeleri için - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="50ff1-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="50ff1-117">Kitaplık .net targeting paketlenemiyor standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="50ff1-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="50ff1-118">Dosya -> Yeni Proje -> sınıf kitaplığı (taşınabilir) proje başarısız VS2015 ve - Dev15 [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="50ff1-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="50ff1-119">NuGet hata - 1.0.0-\* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="50ff1-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="50ff1-120">Bul-Package başarısız görünen ancak works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="50ff1-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="50ff1-121">Hata olduğunda "Install-Package jquery.validation" - dev15 [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="50ff1-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="50ff1-122">Yüklü VS 2015 sürümü 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="50ff1-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="50ff1-123">Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürüm görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="50ff1-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="50ff1-124">-ApiKey Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="50ff1-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="50ff1-125">Yanlış dize: bir paketin kararlı bir sürüm öncesi bir bağımlılık olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="50ff1-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="50ff1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="50ff1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="50ff1-127">PCL (net46 ve windows 10) proje get NullRef özel durumu oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="50ff1-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="50ff1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="50ff1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="50ff1-129">Nuget güncelleştirmesi, bilgilendirici ileti sağlamalıdır, daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="50ff1-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="50ff1-130">Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / kimlik bilgisi sağlayıcıları ile birden çok kaynakları - kullanırken paket indirilirken hata [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="50ff1-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="50ff1-131">nuget paketi - paketi bağımlılığı eksik Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="50ff1-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="50ff1-132">Linux/MacOS + Mono - ExecuteSynchronizedCore hatada [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="50ff1-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="50ff1-133">VS içinde repositoryPath ortam değişkenlerini desteklemez (yapar. nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="50ff1-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="50ff1-134">Erişilebilirlik sorunlarını gidermek [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="50ff1-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="50ff1-135">Taşınabilir çerçeveleri tirelerle profilleriyle reddedilir.</span><span class="sxs-lookup"><span data-stu-id="50ff1-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="50ff1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="50ff1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="50ff1-137">NuGet Paket Yöneticisi, bu seçenekler listesinde paketleri ayrıntısı için geçerli değildir Temizle olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="50ff1-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="50ff1-138">NuGet 3.3.0 güncelleştirmesi başarısız ' bir ek kısıtlama... tanımlanan packages.config bu işlemi engeller.'</span><span class="sxs-lookup"><span data-stu-id="50ff1-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="50ff1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="50ff1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="50ff1-140">Sahte bir ileti - paket oluşturur mevcut olmayan bir yerel kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="50ff1-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="50ff1-141">"Yükseltme kullanılabilir" filtre gösterir - sürüm kısıtlamasını ihlal eden yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="50ff1-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="50ff1-142">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="50ff1-142">Performance Improvements</span></span>

* <span data-ttu-id="50ff1-143">: ContentModel hedef framework ayrıştırma - performansı [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="50ff1-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="50ff1-144">Performans: Okuma önlemek `runtime.json` RID'ler olmayan geri yüklemeler için dosyaları [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="50ff1-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="50ff1-145">Örnek projelerimizin 15 saniye 3 saniye için ASP.NET Web uygulaması sınırlı bir CI makinelerde geri.</span><span class="sxs-lookup"><span data-stu-id="50ff1-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="50ff1-146">Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="50ff1-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="50ff1-147">Bazı durumlarda 132s'den 10'luk bloklar için PackageManagerConsole açmak zaman geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="50ff1-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="50ff1-148">NuGet güncelleştirmede - ReSharper performans sorunlarını çözün [#3044](https://github.com/NuGet/Home/issues/3044): örnek proje üzerinde paketleri yüklemek için harcanan süre sınırlı 140s 68s için.</span><span class="sxs-lookup"><span data-stu-id="50ff1-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="50ff1-149">Dcr</span><span class="sxs-lookup"><span data-stu-id="50ff1-149">DCRs</span></span>

* <span data-ttu-id="50ff1-150">Yükseltme/yükleme tabanlı bir dotnet tfm PCL sorunları - neden olabileceğini kullanıcılarınıza gereken NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="50ff1-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="50ff1-151">Hatalı yüklemesi/yükseltmesi tfm ile proje için uyar = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="50ff1-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="50ff1-152">Netcoreapp11 ve netstandard17 desteği - ekleyerek [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="50ff1-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="50ff1-153">Nuget.exe içinde - konsol için NuGet uyarı üst bilgi içeriği Yazdır [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="50ff1-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="50ff1-154">Gücünden yararlanarak AssemblyMetadata özniteliği için `.nuspec` belirteç değiştirme - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="50ff1-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="50ff1-155">Kilitli özelliğin kilit dosyanın - kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="50ff1-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="50ff1-156">Sembol paketleri yüklemede hiç kullanılmamalıdır veya #2807 güncelleştir</span><span class="sxs-lookup"><span data-stu-id="50ff1-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="50ff1-157">Özellikler</span><span class="sxs-lookup"><span data-stu-id="50ff1-157">Features</span></span>

* <span data-ttu-id="50ff1-158">Geri dönüş paket klasörleri - desteği [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="50ff1-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="50ff1-159">Paket türü bir kavramı destek aracı paketlerinin - tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="50ff1-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="50ff1-160">-Genel paketleri klasörüne olan yolu almak için API [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="50ff1-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="50ff1-161">Yerel paketler güncelleştirmesi desteği - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="50ff1-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
