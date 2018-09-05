---
title: NuGet 3.4 RC sürüm notları
description: NuGet 3.4 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546760"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="6ff7b-103">NuGet 3.4 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6ff7b-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="6ff7b-104">[NuGet 3.3 Sürüm Notları](../release-notes/nuget-3.3.md) | [NuGet 3.4 sürüm notları](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="6ff7b-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="6ff7b-105">NuGet 3.4-RC, 3 Mart 2016'dan Visual Studio 2015 güncelleştirme 2 RC ile birlikte yayımlanan ve aklını içinde birkaç sacayakları derlendiği:</span><span class="sxs-lookup"><span data-stu-id="6ff7b-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="6ff7b-106">Platformlar arası destek</span><span class="sxs-lookup"><span data-stu-id="6ff7b-106">Cross-Platform support</span></span>
* <span data-ttu-id="6ff7b-107">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6ff7b-107">Performance improvements</span></span>
* <span data-ttu-id="6ff7b-108">Küçük bir kullanıcı Arabirimi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6ff7b-108">Minor UI improvements</span></span>

<span data-ttu-id="6ff7b-109">Aşağıdaki özellikler daha 3.4 son sürümlerde sunulması planlanmaktadır bu RC sürümünde mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="6ff7b-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="6ff7b-110">New Features</span></span>

* <span data-ttu-id="6ff7b-111">NuGet istemcileri artık gzip içerik kodlamasını depolarından destekler</span><span class="sxs-lookup"><span data-stu-id="6ff7b-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="6ff7b-112">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="6ff7b-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="6ff7b-113">Derleme eylemleri contentFiles öğesinde iOS ve Android desteği</span><span class="sxs-lookup"><span data-stu-id="6ff7b-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="6ff7b-114">Netstandard ve netstandardapp framework bilinen adlar için destek</span><span class="sxs-lookup"><span data-stu-id="6ff7b-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="6ff7b-115">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="6ff7b-115">New User Interface Features</span></span>

* <span data-ttu-id="6ff7b-116">Yüklü, güncelleştirmeleri ve birleştirme sekmelerinde özellikle önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6ff7b-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="6ff7b-117">Yüklü ve güncelleştirmeleri sekmeleri artık alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="6ff7b-118">Sağlayan bir arama yenilenmesi yenile düğmesine eklendi</span><span class="sxs-lookup"><span data-stu-id="6ff7b-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6ff7b-119">Güncelleştirmeler ve iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="6ff7b-119">Updates and Improvements</span></span>

* <span data-ttu-id="6ff7b-120">Başvurulan paketleri `project.json` sahip kayan sürüm her derleme üzerinde güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="6ff7b-121">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecek `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="6ff7b-122">NuGet Yapılandırması kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırması zorlanır.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="6ff7b-123">NuGet artık paylaşılan projelerde paketleri geri yükler veya bir kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="6ff7b-124">Biz, ağ hatası geliştirdik ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="6ff7b-125">Klavye ve fare davranışlar Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="6ff7b-126">En son artık desteklenmektedir `project.json` DNX şemasında.</span><span class="sxs-lookup"><span data-stu-id="6ff7b-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6ff7b-127">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="6ff7b-127">Known Issues</span></span>

<span data-ttu-id="6ff7b-128">Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6ff7b-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>