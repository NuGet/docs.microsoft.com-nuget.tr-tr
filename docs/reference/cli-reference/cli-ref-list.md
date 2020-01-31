---
title: NuGet CLı listesi komutu
description: NuGet. exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813344"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="31942-103">List komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="31942-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="31942-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="31942-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="31942-105">Belirli bir kaynaktaki paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="31942-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="31942-106">Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında tanımlanan tüm kaynaklar `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`kullanılır.</span><span class="sxs-lookup"><span data-stu-id="31942-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="31942-107">`NuGet.Config` kaynak belirtiyorsa `list` varsayılan akışı kullanır (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="31942-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="31942-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="31942-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="31942-109">isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek.</span><span class="sxs-lookup"><span data-stu-id="31942-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="31942-110">Arama terimleri, paketler, Etiketler ve paket açıklamaları adlarına, bunları nuget.org 'de kullanırken olduğu gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="31942-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="31942-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="31942-111">Options</span></span>

| <span data-ttu-id="31942-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="31942-112">Option</span></span> | <span data-ttu-id="31942-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="31942-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31942-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="31942-114">AllVersions</span></span> | <span data-ttu-id="31942-115">Bir paketin tüm sürümlerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="31942-115">List all versions of a package.</span></span> <span data-ttu-id="31942-116">Varsayılan olarak, yalnızca en son paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="31942-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="31942-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="31942-117">ConfigFile</span></span> | <span data-ttu-id="31942-118">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="31942-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="31942-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="31942-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="31942-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="31942-120">ForceEnglishOutput</span></span> | <span data-ttu-id="31942-121">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="31942-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="31942-122">Yardım</span><span class="sxs-lookup"><span data-stu-id="31942-122">Help</span></span> | <span data-ttu-id="31942-123">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="31942-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="31942-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="31942-124">IncludeDelisted</span></span> | <span data-ttu-id="31942-125">*(3.2 +)* Listelenmemiş paketleri görüntüle.</span><span class="sxs-lookup"><span data-stu-id="31942-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="31942-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="31942-126">NonInteractive</span></span> | <span data-ttu-id="31942-127">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="31942-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="31942-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="31942-128">PreRelease</span></span> | <span data-ttu-id="31942-129">Listedeki yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="31942-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="31942-130">Kaynak</span><span class="sxs-lookup"><span data-stu-id="31942-130">Source</span></span> | <span data-ttu-id="31942-131">Aranacak paket kaynaklarının bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="31942-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="31942-132">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="31942-132">Verbosity</span></span> | <span data-ttu-id="31942-133">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="31942-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="31942-134">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="31942-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="31942-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="31942-135">Examples</span></span>

<span data-ttu-id="31942-136">Yapılandırılmış akışlardan tüm paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="31942-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="31942-137">Ayrıntılı ayrıntı düzeyine sahip Azure ile ilgili paketleri listeleyin:</span><span class="sxs-lookup"><span data-stu-id="31942-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="31942-138">Yapılandırılmış akışlardan Azure ile ilgili paketlerin tüm sürümlerini listeleyin:</span><span class="sxs-lookup"><span data-stu-id="31942-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="31942-139">JSON ile ilgili tüm paketlerin sürümlerini belirtilen kaynaktan/akıştan listeleyin:</span><span class="sxs-lookup"><span data-stu-id="31942-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="31942-140">Birden çok kaynaktan/akışlardan JSON ile ilgili paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="31942-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

