---
title: "NuGet 3.4 RC sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.4 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4 RC sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="2d29b-104">NuGet 3.4 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="2d29b-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="2d29b-105">[NuGet 3.3 Sürüm Notları](../release-notes/nuget-3.3.md) | [NuGet 3.4 sürüm notları](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="2d29b-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="2d29b-106">NuGet 3.4-RC, 3 Mart 2016 Visual Studio 2015 güncelleştirme 2 RC yanında yayımlanmıştır ve minds içinde birkaç tenets ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="2d29b-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="2d29b-107">Platformlar arası desteği</span><span class="sxs-lookup"><span data-stu-id="2d29b-107">Cross-Platform support</span></span>
* <span data-ttu-id="2d29b-108">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="2d29b-108">Performance improvements</span></span>
* <span data-ttu-id="2d29b-109">İkincil UI geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="2d29b-109">Minor UI improvements</span></span>

<span data-ttu-id="2d29b-110">Aşağıdaki özellikler ile daha fazla 3.4 son sürüm için planlı bu RC'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2d29b-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="2d29b-111">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="2d29b-111">New Features</span></span>

* <span data-ttu-id="2d29b-112">Gzip içerik kodlamasına depoları gelen NuGet istemcileri artık destekler</span><span class="sxs-lookup"><span data-stu-id="2d29b-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="2d29b-113">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="2d29b-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="2d29b-114">İOS ve Android derleme eylemleri contentFiles öğesindeki desteği</span><span class="sxs-lookup"><span data-stu-id="2d29b-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="2d29b-115">Netstandard ve netstandardapp bilinen adları framework adları için destek</span><span class="sxs-lookup"><span data-stu-id="2d29b-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="2d29b-116">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="2d29b-116">New User Interface Features</span></span>

* <span data-ttu-id="2d29b-117">Özellikle, yüklü, güncelleştirmeleri ve birleştirme sekmelerde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="2d29b-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="2d29b-118">Yüklü ve güncelleştirmeleri sekmeler şimdi alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="2d29b-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="2d29b-119">Yenilenecek bir arama özelliğine imkan tanıyan bir Yenile düğmesini eklendi</span><span class="sxs-lookup"><span data-stu-id="2d29b-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="2d29b-120">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="2d29b-120">Updates and Improvements</span></span>

* <span data-ttu-id="2d29b-121">Başvurulan paketleri `project.json` sahip bir kayan sürüm üzerinde her yapı güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="2d29b-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="2d29b-122">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecektir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="2d29b-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="2d29b-123">NuGet yapılandırma kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırma zorlanır.</span><span class="sxs-lookup"><span data-stu-id="2d29b-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="2d29b-124">Artık NuGet paketleri paylaşılan projelerinde yükler veya kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="2d29b-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="2d29b-125">Biz, ağ hatası geliştirildi ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="2d29b-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="2d29b-126">Klavye ve fare davranışları Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="2d29b-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="2d29b-127">En son artık desteklenmektedir `project.json` DNX şemada.</span><span class="sxs-lookup"><span data-stu-id="2d29b-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2d29b-128">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="2d29b-128">Known Issues</span></span>

<span data-ttu-id="2d29b-129">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2d29b-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>