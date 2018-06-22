---
title: NuGet 3.4 RC sürüm notları
description: NuGet 3.4 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820826"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="7c4b8-103">NuGet 3.4 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="7c4b8-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="7c4b8-104">[NuGet 3.3 Sürüm Notları](../release-notes/nuget-3.3.md) | [NuGet 3.4 sürüm notları](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="7c4b8-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="7c4b8-105">NuGet 3.4-RC, 3 Mart 2016 Visual Studio 2015 güncelleştirme 2 RC yanında yayımlanmıştır ve minds içinde birkaç tenets ile oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="7c4b8-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="7c4b8-106">Platformlar arası desteği</span><span class="sxs-lookup"><span data-stu-id="7c4b8-106">Cross-Platform support</span></span>
* <span data-ttu-id="7c4b8-107">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c4b8-107">Performance improvements</span></span>
* <span data-ttu-id="7c4b8-108">İkincil UI geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c4b8-108">Minor UI improvements</span></span>

<span data-ttu-id="7c4b8-109">Aşağıdaki özellikler ile daha fazla 3.4 son sürüm için planlı bu RC'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="7c4b8-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="7c4b8-110">New Features</span></span>

* <span data-ttu-id="7c4b8-111">Gzip içerik kodlamasına depoları gelen NuGet istemcileri artık destekler</span><span class="sxs-lookup"><span data-stu-id="7c4b8-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7c4b8-112">Xproj projelerindeki paketlerden PDB'leri için destek</span><span class="sxs-lookup"><span data-stu-id="7c4b8-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7c4b8-113">İOS ve Android derleme eylemleri contentFiles öğesindeki desteği</span><span class="sxs-lookup"><span data-stu-id="7c4b8-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7c4b8-114">Netstandard ve netstandardapp bilinen adları framework adları için destek</span><span class="sxs-lookup"><span data-stu-id="7c4b8-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7c4b8-115">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="7c4b8-115">New User Interface Features</span></span>

* <span data-ttu-id="7c4b8-116">Özellikle, yüklü, güncelleştirmeleri ve birleştirme sekmelerde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c4b8-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7c4b8-117">Yüklü ve güncelleştirmeleri sekmeler şimdi alfabetik olarak sıralanır.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7c4b8-118">Yenilenecek bir arama özelliğine imkan tanıyan bir Yenile düğmesini eklendi</span><span class="sxs-lookup"><span data-stu-id="7c4b8-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7c4b8-119">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="7c4b8-119">Updates and Improvements</span></span>

* <span data-ttu-id="7c4b8-120">Başvurulan paketleri `project.json` sahip bir kayan sürüm üzerinde her yapı güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7c4b8-121">Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecektir `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7c4b8-122">NuGet yapılandırma kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırma zorlanır.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7c4b8-123">Artık NuGet paketleri paylaşılan projelerinde yükler veya kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7c4b8-124">Biz, ağ hatası geliştirildi ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7c4b8-125">Klavye ve fare davranışları Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7c4b8-126">En son artık desteklenmektedir `project.json` DNX şemada.</span><span class="sxs-lookup"><span data-stu-id="7c4b8-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7c4b8-127">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="7c4b8-127">Known Issues</span></span>

<span data-ttu-id="7c4b8-128">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7c4b8-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>