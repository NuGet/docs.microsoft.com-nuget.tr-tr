---
title: NuGet 3.2.1 sürüm notları
description: NuGet 3.2.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548196"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="fd0b5-103">NuGet 3.2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="fd0b5-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="fd0b5-104">[3.2 NuGet sürüm notları](../release-notes/nuget-3.2.md) | [NuGet 3.3 sürüm notları](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="fd0b5-105">Komut satırı için NuGet 3.2.1 12 Ekim 2015 bir küçük iyileştirmeler ve düzeltmeler 3.2 sürümü için yayımlanmıştır ve kullanılabilir [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fd0b5-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="fd0b5-106">Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="fd0b5-106">Improvements</span></span>

* <span data-ttu-id="fd0b5-107">NuGet artık yapılandırma dosyası ile özgün harflendirmeyi kullanan `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="fd0b5-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="fd0b5-108">Bu büyük/küçük harfe işletim sistemlerinde önemlidir [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="fd0b5-109">NuGet geri yükleme artık dnx projelerinin yoksay (`*.xproj`) ile işlenmelidir `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="fd0b5-110">En iyi duruma getirilmiş ağ kullanımı ile çalışırken `index.json` ve paket kayıt verisi [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="fd0b5-111">Geliştirilmiş kaynak indirme v2 hizmetleriyle daha sağlam olması için işleme [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="fd0b5-112">Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="fd0b5-112">Fixes</span></span>

* <span data-ttu-id="fd0b5-113">NuGet güncelleştirme doğru güncelleştirmeleri `.csproj` / `.vcxproj` başvuruları [1483 te](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="fd0b5-114">Artık bir SpecialFolders.UserProfile bulunamıyor, oluşturulan bir yerel .nuget klasör önleme [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="fd0b5-115">Geliştirilmiş indirme sırasında bozuk paketler yerel önbellekte işleme [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="fd0b5-116">Komut satırı ve Visual Studio uzantısı NuGet Github'da bulunabilir giderilen sorunların tam bir listesi [3.2.1 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="fd0b5-117">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="fd0b5-117">Known Issues</span></span>

<span data-ttu-id="fd0b5-118">Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="fd0b5-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>