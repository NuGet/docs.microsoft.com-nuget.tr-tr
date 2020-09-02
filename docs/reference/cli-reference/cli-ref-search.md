---
title: NuGet CLı arama komutu
description: nuget.exe Search komutu için başvuru
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 8d63efefb8f14c03fbe3986d8d7eebcc3eb5bcac
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359688"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="079d5-103">Search komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="079d5-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="079d5-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 5,8 +</span><span class="sxs-lookup"><span data-stu-id="079d5-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="079d5-105">Sağlanan sorgu dizesini kullanarak belirli bir kaynağı arar.</span><span class="sxs-lookup"><span data-stu-id="079d5-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="079d5-106">Kaynak belirtilmemişse,% AppData% \NuGet\NuGet.config içinde tanımlanan tüm kaynaklar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="079d5-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="079d5-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="079d5-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="079d5-108">arama koşullarının, paketler, Etiketler ve paket açıklamaları adına, bunları nuget.org 'de kullanırken oldukları gibi, bu adlara uygulandığı yer.</span><span class="sxs-lookup"><span data-stu-id="079d5-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="079d5-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="079d5-109">Options</span></span>

| <span data-ttu-id="079d5-110">Ad</span><span class="sxs-lookup"><span data-stu-id="079d5-110">Name</span></span> | <span data-ttu-id="079d5-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="079d5-111">Description</span></span> | <span data-ttu-id="079d5-112">Kullanım</span><span class="sxs-lookup"><span data-stu-id="079d5-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="079d5-113">Sp1'in</span><span class="sxs-lookup"><span data-stu-id="079d5-113">PreRelease</span></span> | <span data-ttu-id="079d5-114">Yayın öncesi paketleri varsayılan olarak dahil edilmez, ancak bu bağımsız değişken kullanılarak eklenebilir</span><span class="sxs-lookup"><span data-stu-id="079d5-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="079d5-115">-Ön sürüm</span><span class="sxs-lookup"><span data-stu-id="079d5-115">-PreRelease</span></span> |
| <span data-ttu-id="079d5-116">Kaynak</span><span class="sxs-lookup"><span data-stu-id="079d5-116">Source</span></span> | <span data-ttu-id="079d5-117">__nuget.config__ varsayılan kaynakları sorgulamak yerine aranacak belirli paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="079d5-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="079d5-118">-Kaynak `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="079d5-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="079d5-119">Take</span><span class="sxs-lookup"><span data-stu-id="079d5-119">Take</span></span> | <span data-ttu-id="079d5-120">Döndürülecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="079d5-120">The number of results to return.</span></span> <span data-ttu-id="079d5-121">Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="079d5-121">The default value is 20.</span></span> | <span data-ttu-id="079d5-122">-Al `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="079d5-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="079d5-123">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="079d5-123">Verbosity</span></span> | <span data-ttu-id="079d5-124">Çıktıda görüntülenecek ayrıntı düzeyi.</span><span class="sxs-lookup"><span data-stu-id="079d5-124">The level of detail to display in the output.</span></span> <span data-ttu-id="079d5-125">Varsayılan değer _normaldir_.</span><span class="sxs-lookup"><span data-stu-id="079d5-125">The default is _normal_.</span></span> <span data-ttu-id="079d5-126">(Aşağıdaki nota bakın)</span><span class="sxs-lookup"><span data-stu-id="079d5-126">(See the note below)</span></span>  | <span data-ttu-id="079d5-127">-Ayrıntı düzeyi `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="079d5-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="079d5-128">Yardım</span><span class="sxs-lookup"><span data-stu-id="079d5-128">Help</span></span> | <span data-ttu-id="079d5-129">Komut için yardım bilgilerini görüntüler</span><span class="sxs-lookup"><span data-stu-id="079d5-129">Displays help information for the command</span></span> | <span data-ttu-id="079d5-130">-Yardım</span><span class="sxs-lookup"><span data-stu-id="079d5-130">-Help</span></span> |

<span data-ttu-id="079d5-131">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="079d5-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="079d5-132">Ayrıntı düzeyleri:</span><span class="sxs-lookup"><span data-stu-id="079d5-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="079d5-133">_sessiz_ paket kimliği, sürüm</span><span class="sxs-lookup"><span data-stu-id="079d5-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="079d5-134">_normal_ -paket kimliği, sürüm, Indirmeler, açıklama önizlemesi</span><span class="sxs-lookup"><span data-stu-id="079d5-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="079d5-135">_ayrıntılı_ -paket kimliği, sürüm, Indirmeler, tam açıklama, sorgu URL 'Si gibi diğer bilgiler</span><span class="sxs-lookup"><span data-stu-id="079d5-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="079d5-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="079d5-136">Examples</span></span>

<span data-ttu-id="079d5-137">Varsayılan kaynaklardan *günlüğe kaydetme*ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="079d5-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="079d5-138">Ayrıntılı ayrıntı içeren *günlük*ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="079d5-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="079d5-139">*Günlüğe kaydetme*ile ilgili paketleri arayın ve yalnızca ilk 5 sonucu göster:</span><span class="sxs-lookup"><span data-stu-id="079d5-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="079d5-140">Yayın öncesi sürümleri de dahil olmak üzere, belirtilen kaynaktan/akıştan *JSON*ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="079d5-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="079d5-141">Birden çok kaynaktan/akışlardan *JSON*ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="079d5-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
