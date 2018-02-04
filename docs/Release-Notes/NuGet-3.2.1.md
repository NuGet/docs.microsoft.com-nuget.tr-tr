---
title: "NuGet 3.2.1 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.2.1 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.2.1 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="6cd06-104">NuGet 3.2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6cd06-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="6cd06-105">[NuGet 3.2 sürüm notları](../release-notes/nuget-3.2.md) | [NuGet 3.3 sürüm notları](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="6cd06-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="6cd06-106">Komut satırı için NuGet 3.2.1 12 Ekim 2015 en iyi duruma getirme ve düzeltmeleri 3.2 sürümü sayıda ile serbest bırakıldı ve kullanılabilir [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6cd06-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="6cd06-107">Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6cd06-107">Improvements</span></span>

* <span data-ttu-id="6cd06-108">NuGet özgün büyük küçük harf kullanımını ile artık yapılandırma dosyasını kullanır `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="6cd06-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="6cd06-109">Bu büyük küçük harfe duyarlı işletim sistemlerinde önemlidir [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="6cd06-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="6cd06-110">NuGet restore şimdi dnx projelerini yoksay (`*.xproj`) ile işlenmelidir `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="6cd06-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="6cd06-111">En iyi duruma getirilmiş ağ kullanımı ile çalışırken `index.json` ve paket kayıt verileri [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="6cd06-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="6cd06-112">Geliştirilmiş kaynak indirme v2 Hizmetleri ile daha sağlam olması için işleme [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="6cd06-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="6cd06-113">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="6cd06-113">Fixes</span></span>

* <span data-ttu-id="6cd06-114">NuGet güncelleştirme doğru güncelleştirmeleri `.csproj` / `.vcxproj` başvuruları [1483 te](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="6cd06-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="6cd06-115">Şimdi bir SpecialFolders.UserProfile bulunamıyor zaman oluşturulan bir yerel .nuget klasörü önleme [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="6cd06-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="6cd06-116">Yükleme sırasında bozuk paketler yerel önbellekteki işlenmesini geliştirilmiş [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="6cd06-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="6cd06-117">Komut satırı ve Visual Studio uzantısı NuGet Github'da bulunabilir ele sorunların tam listesi [3.2.1 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="6cd06-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6cd06-118">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="6cd06-118">Known Issues</span></span>

<span data-ttu-id="6cd06-119">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6cd06-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>