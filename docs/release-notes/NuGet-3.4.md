---
title: NuGet 3.4 sürüm notları
description: NuGet 3.4 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551197"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="573df-103">NuGet 3.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="573df-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="573df-104">[NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md) | [3.4.1 NuGet sürüm notları](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="573df-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="573df-105">NuGet 3.4, 30 Mart 2016'dan Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü bir parçası olarak yayımlanmıştır ve aklını içinde birkaç sacayakları derlendiği:</span><span class="sxs-lookup"><span data-stu-id="573df-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="573df-106">Platformlar arası destek</span><span class="sxs-lookup"><span data-stu-id="573df-106">Cross-Platform support</span></span>
* <span data-ttu-id="573df-107">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="573df-107">Performance improvements</span></span>
* <span data-ttu-id="573df-108">Küçük bir kullanıcı Arabirimi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="573df-108">Minor UI improvements</span></span>

<span data-ttu-id="573df-109">Aşağıdaki özellikler RC'de daha önce eklenen ve güncelleştirildi veya 3.4 sürümü için tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="573df-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="573df-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="573df-110">New Features</span></span>

* <span data-ttu-id="573df-111">NuGet istemcileri artık gzip içerik kodlamasını depolarından destekler</span><span class="sxs-lookup"><span data-stu-id="573df-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="573df-112">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="573df-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="573df-113">Derleme eylemleri contentFiles öğesinde iOS ve Android desteği</span><span class="sxs-lookup"><span data-stu-id="573df-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="573df-114">Netstandard ve netstandardapp framework bilinen adlar için destek</span><span class="sxs-lookup"><span data-stu-id="573df-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="573df-115">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="573df-115">New User Interface Features</span></span>

* <span data-ttu-id="573df-116">Yüklü, güncelleştirmeleri ve birleştirme sekmelerinde özellikle önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="573df-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="573df-117">Toplama 'Tüm paket kaynakları' kaynak uygun arama sonucu birleştirme ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="573df-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="573df-118">Yüklü ve güncelleştirmeleri sekmeleri artık alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="573df-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="573df-119">Sağlayan bir arama yenilenmesi yenile düğmesine eklendi</span><span class="sxs-lookup"><span data-stu-id="573df-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="573df-120">Sürüm listenin üst kısmındaki en son derleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="573df-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="573df-121">Güncelleştirmeler ve iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="573df-121">Updates and Improvements</span></span>

* <span data-ttu-id="573df-122">Başvurulan paketleri `project.json` sahip kayan sürüm her derleme üzerinde güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="573df-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="573df-123">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecek `project.json`.</span><span class="sxs-lookup"><span data-stu-id="573df-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="573df-124">NuGet Yapılandırması kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırması zorlanır.</span><span class="sxs-lookup"><span data-stu-id="573df-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="573df-125">NuGet artık paylaşılan projelerde paketleri geri yükler veya bir kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="573df-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="573df-126">Biz, ağ hatası geliştirdik ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="573df-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="573df-127">Klavye ve fare davranışlar Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="573df-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="573df-128">En son artık desteklenmektedir `project.json` DNX şemasında.</span><span class="sxs-lookup"><span data-stu-id="573df-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="573df-129">Yeni Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="573df-129">Breaking Changes</span></span>

* <span data-ttu-id="573df-130">Paket sürüm numaraları artık biçimine normalleştirilmiş *ana*. *küçük*. *Düzeltme Eki*-*ön* her birincil, ikincil ve düzeltme eki tamsayı olarak kabul edilir ve hiçbir 2f3b bırakın.</span><span class="sxs-lookup"><span data-stu-id="573df-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="573df-131">Yayın öncesi bilgiler bir dize olarak kabul edilir ve değişiklikler için uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="573df-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="573df-132">Bu numaraları NuGet istemcileri ve nuget.org hizmet tarafından sağlanan arama sorguları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="573df-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="573df-133">NuGet belgeleri altında daha fazla ayrıntı bulunabilir [yayın öncesi sürümler](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="573df-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="573df-134">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="573df-134">Known Issues</span></span>

* <span data-ttu-id="573df-135">**Sorun:** sorunları veya hatta bir Visual Studio kilitlenmesi Visual Studio'da Powershell ile aşağıdaki senaryolarda Windows 10 v1511 kullanıcıları karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="573df-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="573df-136">Yükleme / kaldırma install.ps1 olan paketleri / uninstall.ps1 betikleri</span><span class="sxs-lookup"><span data-stu-id="573df-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="573df-137">(EntityFramework gibi) bir init.ps1 betiği içeren projeleri yükleniyor</span><span class="sxs-lookup"><span data-stu-id="573df-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="573df-138">Web içerik yayımlama</span><span class="sxs-lookup"><span data-stu-id="573df-138">Publishing web content</span></span>

* <span data-ttu-id="573df-139">**Geçici çözüm:** Windows 10 yüklemenizi uygulanan en son düzeltme eklerinin, expecially Ocak 2016 (KB 3124263) veya daha yeni bir güncelleştirme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="573df-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="573df-140">Daha fazla bilgi edinilebilir [GitHub sorunu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="573df-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="573df-141">**Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.</span><span class="sxs-lookup"><span data-stu-id="573df-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="573df-142">İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="573df-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="573df-143">**Geçici çözüm:** bu sorunu çözmek için yeniden yönlendirilen sunucu konumunu gösterecek şekilde ayarlardaki Paket Deposu URI yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="573df-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="573df-144">Daha fazla bilgi için [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="573df-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="573df-145">Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="573df-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>