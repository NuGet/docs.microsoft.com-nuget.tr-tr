---
title: NuGet 3,4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,4 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776412"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="a66cc-103">NuGet 3,4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="a66cc-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="a66cc-104">[NuGet 3,4-RC sürüm notları](../release-notes/nuget-3.4-RC.md)  |  [NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="a66cc-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="a66cc-105">NuGet 3,4, Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümünün bir parçası olarak 30 Mart 2016 ' de yayımlanmıştır ve fikirlerini ' de birkaç tenetle oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="a66cc-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="a66cc-106">Platformlar arası destek</span><span class="sxs-lookup"><span data-stu-id="a66cc-106">Cross-Platform support</span></span>
* <span data-ttu-id="a66cc-107">Performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="a66cc-107">Performance improvements</span></span>
* <span data-ttu-id="a66cc-108">Küçük Kullanıcı arabirimi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="a66cc-108">Minor UI improvements</span></span>

<span data-ttu-id="a66cc-109">Aşağıdaki özellikler daha önce RC 'ye eklenmiştir ve 3,4 sürümü için güncelleştirilmiştir veya tamamlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="a66cc-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="a66cc-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="a66cc-110">New Features</span></span>

* <span data-ttu-id="a66cc-111">NuGet istemcileri artık depolardaki gzip içerik kodlamasını destekliyor</span><span class="sxs-lookup"><span data-stu-id="a66cc-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="a66cc-112">Xproj projelerindeki paketlerin pdb 'leri desteği</span><span class="sxs-lookup"><span data-stu-id="a66cc-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="a66cc-113">ContentFiles öğesinde iOS ve Android derleme eylemleri için destek</span><span class="sxs-lookup"><span data-stu-id="a66cc-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="a66cc-114">Netstandard ve netstandardapp Framework takma adları için destek</span><span class="sxs-lookup"><span data-stu-id="a66cc-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a66cc-115">Yeni Kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="a66cc-115">New User Interface Features</span></span>

* <span data-ttu-id="a66cc-116">Özellikle yüklü, güncelleştirmeler ve birleştirme sekmelerinde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="a66cc-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="a66cc-117">Toplu ' tüm paket kaynakları ' kaynağı uygun arama sonucu birleştirme ile kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="a66cc-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="a66cc-118">Yüklü ve güncelleştirmeler sekmeleri artık alfabetik olarak sıralanmıştır</span><span class="sxs-lookup"><span data-stu-id="a66cc-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="a66cc-119">Bir aramanın yenilenmesini sağlayan bir yenileme düğmesi eklendi</span><span class="sxs-lookup"><span data-stu-id="a66cc-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="a66cc-120">Sürüm listesinin en üstünde bulunan en son derleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="a66cc-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a66cc-121">Güncelleştirmeler ve geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="a66cc-121">Updates and Improvements</span></span>

* <span data-ttu-id="a66cc-122">' De `project.json` bir kayan sürüme başvuruda bulunulan paketler her derlemede güncelmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="a66cc-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="a66cc-123">Bunun yerine, yalnızca geri yükleme, Temizleme, yeniden oluşturma veya değiştirme zorlandığında güncelleyirler `project.json` .</span><span class="sxs-lookup"><span data-stu-id="a66cc-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="a66cc-124">NuGet yapılandırma kullanıcı arabirimini kullandığınızda, nuget.org Repository Kaynakları artık proje yapılandırmasına zorlanmaz.</span><span class="sxs-lookup"><span data-stu-id="a66cc-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="a66cc-125">NuGet artık paylaşılan projelerdeki paketleri geri yüklemez ve bir kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="a66cc-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="a66cc-126">Ağ hatasını geliştirdik ve erişilemeyen ya da yavaş yanıt veren sunucular için işlemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a66cc-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="a66cc-127">Klavye ve fare davranışları, Visual Studio Paket Yöneticisi Kullanıcı arabiriminde geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a66cc-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="a66cc-128">Artık `project.json` DNX 'teki en son şemayı destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="a66cc-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="a66cc-129">Hataya Neden Olan Değişiklikler</span><span class="sxs-lookup"><span data-stu-id="a66cc-129">Breaking Changes</span></span>

* <span data-ttu-id="a66cc-130">Paket sürüm numaraları artık *birincil* biçime normalleştirilir. *küçük*. *Düzeltme Eki* - *ön sürüm*   Ana, alt ve yayama her biri tamsayılar olarak değerlendirilir ve öndeki sıfırlar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a66cc-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="a66cc-131">Ön sürüm bilgileri bir dize olarak değerlendirilir ve buna hiçbir değişiklik uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="a66cc-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="a66cc-132">Bu sayılar, NuGet istemcilerine ve nuget.org hizmeti tarafından sunulan aramaya göre sorgularda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a66cc-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="a66cc-133">Daha fazla ayrıntı, NuGet belgeleri altında [yayın öncesi sürümler](../create-packages/prerelease-packages.md)altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a66cc-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a66cc-134">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="a66cc-134">Known Issues</span></span>

* <span data-ttu-id="a66cc-135">**Sorun:** Windows 10 v1511 kullanıcıları, aşağıdaki senaryolarda, Visual Studio 'da PowerShell ile birlikte Visual Studio kilitlenmesi veya sorunlar yaşayabilir:</span><span class="sxs-lookup"><span data-stu-id="a66cc-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="a66cc-136">install.ps1/uninstall.ps1 betiklerine sahip paketleri yükleme/kaldırma</span><span class="sxs-lookup"><span data-stu-id="a66cc-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="a66cc-137">init.ps1 betiği olan projeler (EntityFramework gibi) yükleniyor</span><span class="sxs-lookup"><span data-stu-id="a66cc-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="a66cc-138">Web içeriği yayımlanıyor</span><span class="sxs-lookup"><span data-stu-id="a66cc-138">Publishing web content</span></span>

* <span data-ttu-id="a66cc-139">**Geçici çözüm:** Windows 10 yüklemesinin en son düzeltme eklerinin uygulanmış olduğundan emin olun, expecially Ocak 2016 (KB 3124263) veya sonraki bir güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="a66cc-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="a66cc-140">[GitHub sorunundan](http://github.com/nuget/home/issues/1638) daha fazla ayrıntı bulabilirsiniz #1638</span><span class="sxs-lookup"><span data-stu-id="a66cc-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="a66cc-141">**Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.</span><span class="sxs-lookup"><span data-stu-id="a66cc-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="a66cc-142">İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="a66cc-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="a66cc-143">**Geçici çözüm:**  Bu sorunu geçici olarak çözmek için, Ayarlar ' da paket deposu URI 'sini yeniden yönlendirilen sunucu konumunu gösterecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a66cc-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="a66cc-144">Daha fazla bilgi için bkz. [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="a66cc-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="a66cc-145">GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a66cc-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>