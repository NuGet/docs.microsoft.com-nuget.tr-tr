---
title: NuGet CLı listesi komutu
description: nuget.exe list komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780053"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="c7cf0-103">List komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="c7cf0-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="c7cf0-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="c7cf0-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c7cf0-105">Belirli bir kaynaktaki paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="c7cf0-106">Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%AppData%\NuGet\NuGet.Config` (Windows) veya ' de tanımlanan tüm kaynaklar `~/.nuget/NuGet/NuGet.Config` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="c7cf0-107">`NuGet.Config`Kaynak belirtilmezse, `list` varsayılan akışı kullanır (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="c7cf0-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="c7cf0-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c7cf0-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="c7cf0-109">isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="c7cf0-110">[Arama terimleri](../../consume-packages/finding-and-choosing-packages.md#search-syntax) , paketler, Etiketler ve paket açıklamaları adlarına, bunları NuGet.org 'de kullanırken olduğu gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="c7cf0-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="c7cf0-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="c7cf0-112">Bir paketin tüm sürümlerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-112">List all versions of a package.</span></span> <span data-ttu-id="c7cf0-113">Varsayılan olarak, yalnızca en son paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c7cf0-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c7cf0-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c7cf0-116">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c7cf0-117">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="c7cf0-118">*(3.2 +)* Listelenmemiş paketleri görüntüle.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c7cf0-119">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="c7cf0-120">Listedeki yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="c7cf0-121">Aranacak paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="c7cf0-121">The package source to search.</span></span> <span data-ttu-id="c7cf0-122">Seçeneğini birden çok kez kullanarak birden çok kaynak belirtebilirsiniz `-Source` .</span><span class="sxs-lookup"><span data-stu-id="c7cf0-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c7cf0-123">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c7cf0-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c7cf0-124">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c7cf0-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c7cf0-125">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c7cf0-125">Examples</span></span>

<span data-ttu-id="c7cf0-126">Yapılandırılmış akışlardan tüm paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="c7cf0-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="c7cf0-127">Ayrıntılı ayrıntı düzeyine sahip Azure ile ilgili paketleri listeleyin:</span><span class="sxs-lookup"><span data-stu-id="c7cf0-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="c7cf0-128">Yapılandırılmış akışlardan Azure ile ilgili paketlerin tüm sürümlerini listeleyin:</span><span class="sxs-lookup"><span data-stu-id="c7cf0-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="c7cf0-129">JSON ile ilgili tüm paketlerin sürümlerini belirtilen kaynaktan/akıştan listeleyin:</span><span class="sxs-lookup"><span data-stu-id="c7cf0-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="c7cf0-130">Birden çok kaynaktan/akışlardan JSON ile ilgili paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="c7cf0-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
