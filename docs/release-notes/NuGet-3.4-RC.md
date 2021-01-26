---
title: NuGet 3,4-RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,4 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780235"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="018f6-103">NuGet 3,4-RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="018f6-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="018f6-104">[NuGet 3,3 sürüm notları](../release-notes/nuget-3.3.md)  |  [NuGet 3,4 sürüm notları](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="018f6-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="018f6-105">NuGet 3,4-RC, Visual Studio 2015 güncelleştirme 2 RC 'nin yanı sıra 3 Mart 2016 ' de yayımlanmıştır ve fikirlerini içinde birkaç tenetle oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="018f6-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="018f6-106">Platformlar arası destek</span><span class="sxs-lookup"><span data-stu-id="018f6-106">Cross-Platform support</span></span>
* <span data-ttu-id="018f6-107">Performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="018f6-107">Performance improvements</span></span>
* <span data-ttu-id="018f6-108">Küçük Kullanıcı arabirimi geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="018f6-108">Minor UI improvements</span></span>

<span data-ttu-id="018f6-109">3,4 son sürümü için daha planlı olan bu RC 'de aşağıdaki özellikler mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="018f6-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="018f6-110">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="018f6-110">New Features</span></span>

* <span data-ttu-id="018f6-111">NuGet istemcileri artık depolardaki gzip içerik kodlamasını destekliyor</span><span class="sxs-lookup"><span data-stu-id="018f6-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="018f6-112">Xproj projelerindeki paketlerin pdb 'leri desteği</span><span class="sxs-lookup"><span data-stu-id="018f6-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="018f6-113">ContentFiles öğesinde iOS ve Android derleme eylemleri için destek</span><span class="sxs-lookup"><span data-stu-id="018f6-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="018f6-114">Netstandard ve netstandardapp Framework takma adları için destek</span><span class="sxs-lookup"><span data-stu-id="018f6-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="018f6-115">Yeni Kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="018f6-115">New User Interface Features</span></span>

* <span data-ttu-id="018f6-116">Özellikle yüklü, güncelleştirmeler ve birleştirme sekmelerinde önemli performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="018f6-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="018f6-117">Yüklü ve güncelleştirmeler sekmeleri artık alfabetik olarak sıralanmıştır</span><span class="sxs-lookup"><span data-stu-id="018f6-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="018f6-118">Bir aramanın yenilenmesini sağlayan bir yenileme düğmesi eklendi</span><span class="sxs-lookup"><span data-stu-id="018f6-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="018f6-119">Güncelleştirmeler ve geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="018f6-119">Updates and Improvements</span></span>

* <span data-ttu-id="018f6-120">' De `project.json` bir kayan sürüme başvuruda bulunulan paketler her derlemede güncelmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="018f6-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="018f6-121">Bunun yerine, yalnızca geri yükleme, Temizleme, yeniden oluşturma veya değiştirme zorlandığında güncelleyirler `project.json` .</span><span class="sxs-lookup"><span data-stu-id="018f6-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="018f6-122">NuGet yapılandırma kullanıcı arabirimini kullandığınızda, nuget.org Repository Kaynakları artık proje yapılandırmasına zorlanmaz.</span><span class="sxs-lookup"><span data-stu-id="018f6-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="018f6-123">NuGet artık paylaşılan projelerdeki paketleri geri yüklemez ve bir kilit dosyası yazar.</span><span class="sxs-lookup"><span data-stu-id="018f6-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="018f6-124">Ağ hatasını geliştirdik ve erişilemeyen ya da yavaş yanıt veren sunucular için işlemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="018f6-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="018f6-125">Klavye ve fare davranışları, Visual Studio Paket Yöneticisi Kullanıcı arabiriminde geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="018f6-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="018f6-126">Artık `project.json` DNX 'teki en son şemayı destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="018f6-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="018f6-127">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="018f6-127">Known Issues</span></span>

<span data-ttu-id="018f6-128">GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="018f6-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>