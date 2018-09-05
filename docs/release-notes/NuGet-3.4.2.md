---
title: 3.4.2 NuGet sürüm notları
description: NuGet 3.4.2 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549157"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="123ff-103">3.4.2 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="123ff-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="123ff-104">[3.4.1 NuGet sürüm notları](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="123ff-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="123ff-105">NuGet 3.4.2 8 Nisan 3.4 ve 3.4.1 içinde tanımlanan çeşitli sorunları ele almak için 2016 bırakıldığını bırakın.</span><span class="sxs-lookup"><span data-stu-id="123ff-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="123ff-106">nuget.exe 3.4.2 RC kullanıma sunuldu</span><span class="sxs-lookup"><span data-stu-id="123ff-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="123ff-107">Nuget.exe 3.4.2 Sürüm Adayı indirebileceğiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="123ff-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="123ff-108">Güncelleştirmeler ve iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="123ff-108">Updates and Improvements</span></span>

* <span data-ttu-id="123ff-109">Kapsamlı bağımlılık grafikleri paketlerle güncelleştirmeleri nerede gerçekten uzun sürdü ve Visual Studio askıda belirli bir senaryoda, güncelleştirmeleri performansını önemli ölçüde geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="123ff-110">nuget geri yükleme ağ trafiğini olmadan 2,5 x – 3 Visual Studio'da daha hızlı olur.</span><span class="sxs-lookup"><span data-stu-id="123ff-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="123ff-111">Bu değişiklik ek olarak, bir sorun iki kez güncelleştirme getirilirken sayarken VS Arabiriminde nerede biz ağ ulaşmaktan düzelttik.</span><span class="sxs-lookup"><span data-stu-id="123ff-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="123ff-112">Bu, kısmen 3.4/3.4.1 deneyimli bazı zaman aşımı sorunları müşteriler için sorumluydu.</span><span class="sxs-lookup"><span data-stu-id="123ff-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="123ff-113">No_proxy ayarı desteği eklendi</span><span class="sxs-lookup"><span data-stu-id="123ff-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="123ff-114">Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="123ff-114">Fixes</span></span>

* <span data-ttu-id="123ff-115">Nuget.org kaynak için 3.4.1 güncelleştirdikten sonra NuGet ayarları veya yapılandırma eksik olduğu bir sorun düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="123ff-116">Burada 3.4.1 FindPackagesById için büyük/küçük harf değişikliği Artifactory keser bir sorun düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="123ff-117">Nuget.exe ile NuGet geri yükleme ile hatalarına neden olan FIPS ile ilgili bir sorun düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="123ff-118">Geçersiz simge URL'si kaynaklarıyla göz atılırken bir kilitlenme düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="123ff-119">Sürümleri ve Girişleri 'Tüm kaynakları' ndan birleştirme ile sorunlar düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="123ff-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="123ff-120">Bilinen sorunlar 3.4.2 içinde x86 Windows komut satırı (RC)</span><span class="sxs-lookup"><span data-stu-id="123ff-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="123ff-121">Bu sorunları erken sonraki biz RTM isabet önce hafta düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="123ff-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="123ff-122">Çözüm dosyası proje dosyalarını daha düşük bir klasör hiyerarşisi yerleştirilen bir çözüm üzerinde çalışan nuget geri yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="123ff-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="123ff-123">V2 akışı kullanarak bir pakete nuget delete komutu çalıştırma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="123ff-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="123ff-124">V3 akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="123ff-124">Use V3 feed instead.</span></span>


<span data-ttu-id="123ff-125">Düzeltmeleri ve geliştirmeleri bu sürümde tam listesi için sorunların listeye bir göz atın [burada](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="123ff-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>