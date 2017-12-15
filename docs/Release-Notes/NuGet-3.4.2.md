---
title: "NuGet 3.4.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.2 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="d12f9-104">NuGet 3.4.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d12f9-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="d12f9-105">[NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="d12f9-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="d12f9-106">NuGet 3.4.2 yayımlanan 8 Nisan 3.4 ve 3.4.1 belirlendi birkaç sorunlarını gidermek üzere 2016 üzerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="d12f9-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="d12f9-107">nuget.exe 3.4.2 RC artık kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="d12f9-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="d12f9-108">Nuget.exe 3.4.2 Sürüm Adayı'na indirebilirsiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="d12f9-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="d12f9-109">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="d12f9-109">Updates and Improvements</span></span>

* <span data-ttu-id="d12f9-110">Biz, burada derin bağımlılık grafikleri paketlerle güncelleştirmeleri gerçekten uzun sürdü ve Visual Studio askıda belirli bir senaryoda, güncelleştirmelerinin performansını önemli ölçüde iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d12f9-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="d12f9-111">nuget restore ağ trafiğini olmadan 2,5 x – 3 Visual Studio içinde daha hızlı olur.</span><span class="sxs-lookup"><span data-stu-id="d12f9-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="d12f9-112">Bu değişiklik ek olarak, size iki kez güncelleştirme getirme sayısı, VS Arabiriminde nerede biz ağ basarsa bir sorunu düzelttikten.</span><span class="sxs-lookup"><span data-stu-id="d12f9-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="d12f9-113">Bazı zaman aşımı sorunları müşteriler 3.4/3.4.1 deneyimli kısmen sorumlu.</span><span class="sxs-lookup"><span data-stu-id="d12f9-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="d12f9-114">No_proxy ayarı desteği eklendi</span><span class="sxs-lookup"><span data-stu-id="d12f9-114">Added support for no_proxy setting</span></span>

##<a name="fixes"></a><span data-ttu-id="d12f9-115">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="d12f9-115">Fixes</span></span>

* <span data-ttu-id="d12f9-116">Nuget.org kaynak için 3.4.1 güncelleştirdikten sonra NuGet ayarları veya yapılandırma eksik olduğu bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d12f9-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="d12f9-117">Bir sorun nerede 3.4.1 FindPackagesById için büyük/küçük harf değişikliği Artifactory keser sabit.</span><span class="sxs-lookup"><span data-stu-id="d12f9-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="d12f9-118">Nuget.exe ile NuGet geri yükleme ile hataları nedeniyle FIPS ile ilgili bir sorunu düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="d12f9-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="d12f9-119">Bir kilitlenme geçersiz simge URL'si kaynaklarıyla göz atarken sabit.</span><span class="sxs-lookup"><span data-stu-id="d12f9-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="d12f9-120">Birleştirme sürümleri ve 'Tüm kaynakları' girişleri ile giderilen sorunlar.</span><span class="sxs-lookup"><span data-stu-id="d12f9-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="d12f9-121">Bilinen sorunlar 3.4.2 içinde Windows x86 Commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="d12f9-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="d12f9-122">Bu sorunları erken sonraki biz RTM isabet önce hafta düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="d12f9-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="d12f9-123">Çözüm dosyası proje dosyalarını daha düşük bir klasör hiyerarşisi yerleştirilen bir çözüm üzerinde çalışan nuget geri yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d12f9-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="d12f9-124">V2 akış kullanarak bir pakete nuget silme komutunu çalıştırarak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d12f9-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="d12f9-125">V3 akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d12f9-125">Use V3 feed instead.</span></span>


<span data-ttu-id="d12f9-126">Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="d12f9-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>