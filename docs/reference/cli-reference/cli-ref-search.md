---
title: NuGet CLI arama komutu
description: nuget.exe search komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323667"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="a3a3b-103">search komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a3a3b-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="a3a3b-104">**Uygulama: paket** tüketimi &bullet; **Desteklenen sürümler:** 5.8+</span><span class="sxs-lookup"><span data-stu-id="a3a3b-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="a3a3b-105">Sağlanan sorgu dizesini kullanarak verilen kaynağı arar.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="a3a3b-106">Kaynak belirtilmezse%AppData%\NuGet\NuGet.Config tanımlanan tüm kaynaklar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="a3a3b-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a3a3b-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="a3a3b-108">burada arama terimlerinin, paketlerin, etiketlerin ve paket açıklamalarının adları, bu terimlerin kullanıcı adlarında olduğu gibi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="a3a3b-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a3a3b-109">Options</span></span>

| <span data-ttu-id="a3a3b-110">Ad</span><span class="sxs-lookup"><span data-stu-id="a3a3b-110">Name</span></span> | <span data-ttu-id="a3a3b-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3a3b-111">Description</span></span> | <span data-ttu-id="a3a3b-112">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a3a3b-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="a3a3b-113">Önkeser</span><span class="sxs-lookup"><span data-stu-id="a3a3b-113">PreRelease</span></span> | <span data-ttu-id="a3a3b-114">Yayın öncesi paketler varsayılan olarak dahil değildir, ancak bu bağımsız değişken kullanılarak dahil olabilir</span><span class="sxs-lookup"><span data-stu-id="a3a3b-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="a3a3b-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="a3a3b-115">-PreRelease</span></span> |
| <span data-ttu-id="a3a3b-116">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a3a3b-116">Source</span></span> | <span data-ttu-id="a3a3b-117">Kaynaklarda varsayılan kaynakları sorgulamak yerine aranacak belirli paket __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="a3a3b-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="a3a3b-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="a3a3b-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="a3a3b-119">Take</span><span class="sxs-lookup"><span data-stu-id="a3a3b-119">Take</span></span> | <span data-ttu-id="a3a3b-120">Geri dönecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-120">The number of results to return.</span></span> <span data-ttu-id="a3a3b-121">Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-121">The default value is 20.</span></span> | <span data-ttu-id="a3a3b-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="a3a3b-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="a3a3b-123">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="a3a3b-123">Verbosity</span></span> | <span data-ttu-id="a3a3b-124">Çıkışta görüntülenmek için ayrıntı düzeyi.</span><span class="sxs-lookup"><span data-stu-id="a3a3b-124">The level of detail to display in the output.</span></span> <span data-ttu-id="a3a3b-125">Varsayılan değer _normaldir._</span><span class="sxs-lookup"><span data-stu-id="a3a3b-125">The default is _normal_.</span></span> <span data-ttu-id="a3a3b-126">(Aşağıdaki nota bakın)</span><span class="sxs-lookup"><span data-stu-id="a3a3b-126">(See the note below)</span></span>  | <span data-ttu-id="a3a3b-127">-Ayrıntılılık `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="a3a3b-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="a3a3b-128">Help</span><span class="sxs-lookup"><span data-stu-id="a3a3b-128">Help</span></span> | <span data-ttu-id="a3a3b-129">Komutun yardım bilgilerini görüntüler</span><span class="sxs-lookup"><span data-stu-id="a3a3b-129">Displays help information for the command</span></span> | <span data-ttu-id="a3a3b-130">-Help</span><span class="sxs-lookup"><span data-stu-id="a3a3b-130">-Help</span></span> |

<span data-ttu-id="a3a3b-131">Ayrıca [bkz. Ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a3a3b-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="a3a3b-132">AyrıntılıLık Düzeyleri:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="a3a3b-133">_quiet_ - Paket Kimliği, Sürüm</span><span class="sxs-lookup"><span data-stu-id="a3a3b-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="a3a3b-134">_normal_ - Paket Kimliği, Sürüm, İndirmeler, Açıklama Önizlemesi</span><span class="sxs-lookup"><span data-stu-id="a3a3b-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="a3a3b-135">_ayrıntılı_ - Paket Kimliği, Sürüm, İndirmeler, Tam Açıklama, Sorgu URL'si gibi diğer bilgiler</span><span class="sxs-lookup"><span data-stu-id="a3a3b-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="a3a3b-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a3a3b-136">Examples</span></span>

<span data-ttu-id="a3a3b-137">Varsayılan kaynaklardan *günlük* kaydı ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="a3a3b-138">Ayrıntılı *ayrıntılı* günlük kaydı ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="a3a3b-139">İlgili *paketleri günlüğe* kaydetme araması ve yalnızca ilk 5 sonucu gösterme:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="a3a3b-140">Belirtilen *kaynak/akıştan* yayın öncesi sürümler de dahil olmak üzere JSON ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="a3a3b-141">Birden çok *kaynak/akıştan JSON* ile ilgili paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="a3a3b-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
