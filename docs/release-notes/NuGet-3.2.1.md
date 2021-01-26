---
title: NuGet 3.2.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.2.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776517"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="9a33d-103">NuGet 3.2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9a33d-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="9a33d-104">[NuGet 3,2 sürüm notları](../release-notes/nuget-3.2.md)  |  [NuGet 3,3 sürüm notları](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="9a33d-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="9a33d-105">Komut satırı için NuGet 3.2.1, 3,2 sürümünde en iyi duruma getirme ve düzeltmeler ile 12 Ekim 2015 ' de yayımlanmıştır ve [Dist.NuGet.org](http://dist.nuget.org/index.html)adresinden edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="9a33d-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="9a33d-106">Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="9a33d-106">Improvements</span></span>

* <span data-ttu-id="9a33d-107">NuGet artık özgün büyük küçük harfe sahip yapılandırma dosyasını kullanır `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="9a33d-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="9a33d-108">Büyük/küçük harfe duyarlı işletim sistemlerinde bu önemli [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="9a33d-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="9a33d-109">NuGet geri yükleme artık `*.xproj` 1227 ile işlenmesi gereken DNX projelerini () yoksayacak `dnu` [](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="9a33d-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="9a33d-110">`index.json`Ve paket kayıt verileriyle çalışırken iyileştirilmiş ağ kullanımı [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="9a33d-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="9a33d-111">V2 Hizmetleri [1448](https://github.com/NuGet/Home/issues/1448) ile daha sağlam olması için geliştirilmiş kaynak indirme işlemesi</span><span class="sxs-lookup"><span data-stu-id="9a33d-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="9a33d-112">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="9a33d-112">Fixes</span></span>

* <span data-ttu-id="9a33d-113">NuGet güncelleştirmesi doğru güncelleştirme `.csproj` / `.vcxproj` başvuruları [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="9a33d-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="9a33d-114">Bir SpecialFolders. UserProfile bulunamıyorsa, artık yerel bir. NuGet klasörünün oluşturulmasını önlüyordur [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="9a33d-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="9a33d-115">İndirme sırasında bozuk yerel önbellekteki paketlerin işlenmesi [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="9a33d-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="9a33d-116">Komut satırı ve Visual Studio uzantısı için ele alınan sorunların tam listesi NuGet GitHub [3.2.1 kilometre taşında](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) bulunabilir</span><span class="sxs-lookup"><span data-stu-id="9a33d-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="9a33d-117">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="9a33d-117">Known Issues</span></span>

<span data-ttu-id="9a33d-118">GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="9a33d-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>