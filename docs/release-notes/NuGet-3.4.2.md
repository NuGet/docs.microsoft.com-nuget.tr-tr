---
title: NuGet 3.4.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780254"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="b85c6-103">NuGet 3.4.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b85c6-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="b85c6-104">[NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)  |  [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="b85c6-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="b85c6-105">NuGet 3.4.2, 3,4 Nisan 2016 ' de ve 3.4.1 sürümünde tanımlanan çeşitli sorunları gidermek için yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b85c6-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="b85c6-106">nuget.exe 3.4.2 RC artık kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="b85c6-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="b85c6-107">nuget.exe 3.4.2 sürüm adayını [buradan](https://dist.nuget.org/index.html)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b85c6-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b85c6-108">Güncelleştirmeler ve geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="b85c6-108">Updates and Improvements</span></span>

* <span data-ttu-id="b85c6-109">Belirli bir senaryoda güncelleştirmelerin performansını önemli ölçüde geliştirdik. Bu durumda, ayrıntılı bağımlılık grafiklerine sahip paketlerin güncelleştirmeleri gerçekten uzun zaman aldığı ve Visual Studio 'Yu askıya aldık.</span><span class="sxs-lookup"><span data-stu-id="b85c6-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="b85c6-110">ağ trafiği olmayan NuGet geri yükleme işlemi, Visual Studio içinde 2,5 x-3x daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="b85c6-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="b85c6-111">Bu değişikliğe ek olarak, VS Kullanıcı arabirimindeki güncelleştirme sayısını alırken ağı iki kez vurduğumuz bir sorunu düzelttik.</span><span class="sxs-lookup"><span data-stu-id="b85c6-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="b85c6-112">Bu, 3.4/3.4.1 ' de karşılaşılan bazı zaman aşımı sorunları için kısmen sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b85c6-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="b85c6-113">No_proxy ayarı için destek eklendi</span><span class="sxs-lookup"><span data-stu-id="b85c6-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="b85c6-114">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="b85c6-114">Fixes</span></span>

* <span data-ttu-id="b85c6-115">3.4.1 'e güncelleştirildikten sonra NuGet ayarlarında veya yapılandırmada nuget.org kaynağının bulunmadığı bir sorun düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="b85c6-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="b85c6-116">3.4.1 sonlarının Artifactory içindeki Findpackagesbyıd 'e büyük küçük harf değişikliği sorunu düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="b85c6-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="b85c6-117">nuget.exe ile NuGet geri yükleme hatalarıyla kaynaklanan FIPS ile ilgili bir sorun düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="b85c6-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="b85c6-118">Geçersiz simge URL 'SI olan kaynaklara göz atarken kilitlenme düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="b85c6-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="b85c6-119">' Tüm kaynaklar ' ile ilgili sürümleri ve girdileri birleştirmeye yönelik sorunlar düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="b85c6-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="b85c6-120">3.4.2 Windows x86 komut satırı 'nda (RC) bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b85c6-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="b85c6-121">Bu sorunlar, RTM 'ye vurmadan önce sonraki haftada bir daha erken düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="b85c6-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="b85c6-122">Çözüm dosyası proje dosyalarından daha düşük bir klasör hiyerarşisine yerleştirilirse çözüm üzerinde NuGet geri yükleme çalıştırmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b85c6-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="b85c6-123">V2 akışını kullanan bir pakette NuGet Delete komutunun çalıştırılması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b85c6-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="b85c6-124">Bunun yerine v3 akışını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b85c6-124">Use V3 feed instead.</span></span>


<span data-ttu-id="b85c6-125">Bu sürümdeki düzeltmelerin ve geliştirmelerin tüm listesi için [buradaki](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)sorun listesini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b85c6-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>