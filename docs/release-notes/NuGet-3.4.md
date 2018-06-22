---
title: NuGet 3.4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 3.4 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820478"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="ce37b-103">NuGet 3.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ce37b-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="ce37b-104">[NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="ce37b-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="ce37b-105">NuGet 3.4 30 Mart 2016 Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü bir parçası olarak yayımlanmıştır ve minds içinde birkaç tenets ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="ce37b-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="ce37b-106">Platformlar arası desteği</span><span class="sxs-lookup"><span data-stu-id="ce37b-106">Cross-Platform support</span></span>
* <span data-ttu-id="ce37b-107">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-107">Performance improvements</span></span>
* <span data-ttu-id="ce37b-108">İkincil UI geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-108">Minor UI improvements</span></span>

<span data-ttu-id="ce37b-109">Aşağıdaki özellikler RC önceden eklendi ve güncelleştirildi veya 3.4 sürüm için tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="ce37b-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="ce37b-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="ce37b-110">New Features</span></span>

* <span data-ttu-id="ce37b-111">Gzip içerik kodlamasına depoları gelen NuGet istemcileri artık destekler</span><span class="sxs-lookup"><span data-stu-id="ce37b-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="ce37b-112">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="ce37b-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="ce37b-113">İOS ve Android derleme eylemleri contentFiles öğesindeki desteği</span><span class="sxs-lookup"><span data-stu-id="ce37b-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="ce37b-114">Netstandard ve netstandardapp bilinen adları framework adları için destek</span><span class="sxs-lookup"><span data-stu-id="ce37b-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ce37b-115">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-115">New User Interface Features</span></span>

* <span data-ttu-id="ce37b-116">Özellikle, yüklü, güncelleştirmeleri ve birleştirme sekmelerde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="ce37b-117">Birleşik 'Tüm paket kaynaklarını' kaynak uygun arama sonucu birleştirme ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ce37b-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="ce37b-118">Yüklü ve güncelleştirmeleri sekmeler şimdi alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="ce37b-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="ce37b-119">Yenilenecek bir arama özelliğine imkan tanıyan bir Yenile düğmesini eklendi</span><span class="sxs-lookup"><span data-stu-id="ce37b-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="ce37b-120">Sürüm listenin en son derleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ce37b-121">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="ce37b-121">Updates and Improvements</span></span>

* <span data-ttu-id="ce37b-122">Başvurulan paketleri `project.json` sahip bir kayan sürüm üzerinde her yapı güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="ce37b-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="ce37b-123">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecektir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ce37b-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="ce37b-124">NuGet yapılandırma kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırma zorlanır.</span><span class="sxs-lookup"><span data-stu-id="ce37b-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="ce37b-125">Artık NuGet paketleri paylaşılan projelerinde yükler veya kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="ce37b-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="ce37b-126">Biz, ağ hatası geliştirildi ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ce37b-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="ce37b-127">Klavye ve fare davranışları Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="ce37b-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="ce37b-128">En son artık desteklenmektedir `project.json` DNX şemada.</span><span class="sxs-lookup"><span data-stu-id="ce37b-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="ce37b-129">Yeni Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="ce37b-129">Breaking Changes</span></span>

* <span data-ttu-id="ce37b-130">Paket sürüm numaralarını şimdi biçimine normalleştirilmiş *ana*. *küçük*. *Düzeltme Eki*-*ön* her birincil, ikincil ve düzeltme eki tamsayı olarak kabul edilir ve hiçbir 2f3b bırakın.</span><span class="sxs-lookup"><span data-stu-id="ce37b-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="ce37b-131">Yayın öncesi bilgiler bir dize olarak kabul edilir ve hiçbir değişiklik için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ce37b-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="ce37b-132">Bu sayı sorgularda NuGet istemcileri ve nuget.org hizmeti tarafından sağlanan arama tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ce37b-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="ce37b-133">Daha fazla ayrıntı NuGet belgeleri altında bulunabilir [yayın öncesi sürümleri](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ce37b-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ce37b-134">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="ce37b-134">Known Issues</span></span>

* <span data-ttu-id="ce37b-135">**Sorun:** sorunları veya hatta bir Visual Studio kilitlenme Visual Studio'da Powershell ile aşağıdaki senaryolarda Windows 10 v1511 kullanıcılar karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ce37b-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="ce37b-136">Yükleme / kaldırma install.ps1 sahip paketleri / uninstall.ps1 komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="ce37b-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="ce37b-137">Init.ps1 betiği (gibi EntityFramework) projeleri yükleniyor</span><span class="sxs-lookup"><span data-stu-id="ce37b-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="ce37b-138">Yayımlama web içeriği</span><span class="sxs-lookup"><span data-stu-id="ce37b-138">Publishing web content</span></span>

* <span data-ttu-id="ce37b-139">**Geçici çözüm:** Windows 10 yüklemenizi uygulanan en son düzeltme eklerini, expecially (KB 3124263) Ocak 2016 veya sonraki bir güncelleştirme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ce37b-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="ce37b-140">Daha fazla ayrıntı kullanılabilir [GitHub sorunu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="ce37b-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="ce37b-141">**Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.</span><span class="sxs-lookup"><span data-stu-id="ce37b-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="ce37b-142">İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="ce37b-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="ce37b-143">**Geçici çözüm:** bu sorunu çözmek için ayarlardaki Paket Deposu URI yeniden yönlendirilen sunucu konumunu gösterecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ce37b-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="ce37b-144">Daha fazla bilgi için bkz: [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="ce37b-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="ce37b-145">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ce37b-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>