---
title: "NuGet 3.4 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 3.4 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="7c37b-104">NuGet 3.4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="7c37b-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="7c37b-105">[NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="7c37b-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="7c37b-106">NuGet 3.4 30 Mart 2016 Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü bir parçası olarak yayımlanmıştır ve minds içinde birkaç tenets ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="7c37b-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="7c37b-107">Platformlar arası desteği</span><span class="sxs-lookup"><span data-stu-id="7c37b-107">Cross-Platform support</span></span>
*  <span data-ttu-id="7c37b-108">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-108">Performance improvements</span></span>
*  <span data-ttu-id="7c37b-109">İkincil UI geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-109">Minor UI improvements</span></span>

<span data-ttu-id="7c37b-110">Aşağıdaki özellikler RC önceden eklendi ve güncelleştirildi veya 3.4 sürüm için tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="7c37b-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="7c37b-111">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="7c37b-111">New Features</span></span>

* <span data-ttu-id="7c37b-112">Gzip içerik kodlamasına depoları gelen NuGet istemcileri artık destekler</span><span class="sxs-lookup"><span data-stu-id="7c37b-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7c37b-113">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="7c37b-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7c37b-114">İOS ve Android derleme eylemleri contentFiles öğesindeki desteği</span><span class="sxs-lookup"><span data-stu-id="7c37b-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7c37b-115">Netstandard ve netstandardapp bilinen adları framework adları için destek</span><span class="sxs-lookup"><span data-stu-id="7c37b-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7c37b-116">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-116">New User Interface Features</span></span>

* <span data-ttu-id="7c37b-117">Özellikle, yüklü, güncelleştirmeleri ve birleştirme sekmelerde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7c37b-118">Birleşik 'Tüm paket kaynaklarını' kaynak uygun arama sonucu birleştirme ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="7c37b-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="7c37b-119">Yüklü ve güncelleştirmeleri sekmeler şimdi alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="7c37b-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7c37b-120">Yenilenecek bir arama özelliğine imkan tanıyan bir Yenile düğmesini eklendi</span><span class="sxs-lookup"><span data-stu-id="7c37b-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="7c37b-121">Sürüm listenin en son derleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7c37b-122">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c37b-122">Updates and Improvements</span></span>

* <span data-ttu-id="7c37b-123">Başvurulan paketleri `project.json` sahip bir kayan sürüm üzerinde her yapı güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="7c37b-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7c37b-124">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecektir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7c37b-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7c37b-125">NuGet yapılandırma kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırma zorlanır.</span><span class="sxs-lookup"><span data-stu-id="7c37b-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7c37b-126">Artık NuGet paketleri paylaşılan projelerinde yükler veya kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="7c37b-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7c37b-127">Biz, ağ hatası geliştirildi ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7c37b-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7c37b-128">Klavye ve fare davranışları Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="7c37b-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7c37b-129">En son artık desteklenmektedir `project.json` DNX şemada.</span><span class="sxs-lookup"><span data-stu-id="7c37b-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="7c37b-130">Yeni Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="7c37b-130">Breaking Changes</span></span>

* <span data-ttu-id="7c37b-131">Paket sürüm numaralarını şimdi biçimine normalleştirilmiş *ana*. *küçük*. *Düzeltme Eki*-*ön* her birincil, ikincil ve düzeltme eki tamsayı olarak kabul edilir ve hiçbir 2f3b bırakın.</span><span class="sxs-lookup"><span data-stu-id="7c37b-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="7c37b-132">Yayın öncesi bilgiler bir dize olarak kabul edilir ve hiçbir değişiklik için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7c37b-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="7c37b-133">Bu sayı sorgularda NuGet istemcileri ve nuget.org hizmeti tarafından sağlanan arama tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c37b-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="7c37b-134">Daha fazla ayrıntı NuGet belgeleri altında bulunabilir [yayın öncesi sürümleri](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7c37b-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="7c37b-135">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="7c37b-135">Known Issues</span></span>

* <span data-ttu-id="7c37b-136">**Sorun:** sorunları veya hatta bir Visual Studio kilitlenme Visual Studio'da Powershell ile aşağıdaki senaryolarda Windows 10 v1511 kullanıcılar karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7c37b-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="7c37b-137">Yükleme / kaldırma install.ps1 sahip paketleri / uninstall.ps1 komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="7c37b-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="7c37b-138">Init.ps1 betiği (gibi EntityFramework) projeleri yükleniyor</span><span class="sxs-lookup"><span data-stu-id="7c37b-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="7c37b-139">Yayımlama web içeriği</span><span class="sxs-lookup"><span data-stu-id="7c37b-139">Publishing web content</span></span>

* <span data-ttu-id="7c37b-140">**Geçici çözüm:** Windows 10 yüklemenizi uygulanan en son düzeltme eklerini, expecially (KB 3124263) Ocak 2016 veya sonraki bir güncelleştirme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7c37b-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="7c37b-141">Daha fazla ayrıntı kullanılabilir [GitHub sorunu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="7c37b-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="7c37b-142">**Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.</span><span class="sxs-lookup"><span data-stu-id="7c37b-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="7c37b-143">İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="7c37b-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="7c37b-144">**Geçici çözüm:** bu sorunu çözmek için ayarlardaki Paket Deposu URI yeniden yönlendirilen sunucu konumunu gösterecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7c37b-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="7c37b-145">Daha fazla bilgi için bkz: [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="7c37b-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="7c37b-146">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7c37b-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>