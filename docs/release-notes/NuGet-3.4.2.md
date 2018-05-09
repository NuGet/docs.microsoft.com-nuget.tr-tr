---
title: NuGet 3.4.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.2 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="4d610-103">NuGet 3.4.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="4d610-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="4d610-104">[NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="4d610-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="4d610-105">NuGet 3.4.2 yayımlanan 8 Nisan 3.4 ve 3.4.1 belirlendi birkaç sorunlarını gidermek üzere 2016 üzerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="4d610-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="4d610-106">nuget.exe 3.4.2 RC artık kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="4d610-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="4d610-107">Nuget.exe 3.4.2 Sürüm Adayı'na indirebilirsiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="4d610-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="4d610-108">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="4d610-108">Updates and Improvements</span></span>

* <span data-ttu-id="4d610-109">Biz, burada derin bağımlılık grafikleri paketlerle güncelleştirmeleri gerçekten uzun sürdü ve Visual Studio askıda belirli bir senaryoda, güncelleştirmelerinin performansını önemli ölçüde iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4d610-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="4d610-110">nuget restore ağ trafiğini olmadan 2,5 x – 3 Visual Studio içinde daha hızlı olur.</span><span class="sxs-lookup"><span data-stu-id="4d610-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="4d610-111">Bu değişiklik ek olarak, size iki kez güncelleştirme getirme sayısı, VS Arabiriminde nerede biz ağ basarsa bir sorunu düzelttikten.</span><span class="sxs-lookup"><span data-stu-id="4d610-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="4d610-112">Bazı zaman aşımı sorunları müşteriler 3.4/3.4.1 deneyimli kısmen sorumlu.</span><span class="sxs-lookup"><span data-stu-id="4d610-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="4d610-113">No_proxy ayarı desteği eklendi</span><span class="sxs-lookup"><span data-stu-id="4d610-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="4d610-114">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="4d610-114">Fixes</span></span>

* <span data-ttu-id="4d610-115">Nuget.org kaynak için 3.4.1 güncelleştirdikten sonra NuGet ayarları veya yapılandırma eksik olduğu bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4d610-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="4d610-116">Bir sorun nerede 3.4.1 FindPackagesById için büyük/küçük harf değişikliği Artifactory keser sabit.</span><span class="sxs-lookup"><span data-stu-id="4d610-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="4d610-117">Nuget.exe ile NuGet geri yükleme ile hataları nedeniyle FIPS ile ilgili bir sorunu düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="4d610-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="4d610-118">Bir kilitlenme geçersiz simge URL'si kaynaklarıyla göz atarken sabit.</span><span class="sxs-lookup"><span data-stu-id="4d610-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="4d610-119">Birleştirme sürümleri ve 'Tüm kaynakları' girişleri ile giderilen sorunlar.</span><span class="sxs-lookup"><span data-stu-id="4d610-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="4d610-120">Bilinen sorunlar 3.4.2 içinde Windows x86 Commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="4d610-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="4d610-121">Bu sorunları erken sonraki biz RTM isabet önce hafta düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="4d610-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="4d610-122">Çözüm dosyası proje dosyalarını daha düşük bir klasör hiyerarşisi yerleştirilen bir çözüm üzerinde çalışan nuget geri yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d610-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="4d610-123">V2 akış kullanarak bir pakete nuget silme komutunu çalıştırarak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4d610-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="4d610-124">V3 akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d610-124">Use V3 feed instead.</span></span>


<span data-ttu-id="4d610-125">Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="4d610-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>