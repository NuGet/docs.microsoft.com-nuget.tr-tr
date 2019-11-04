---
title: NuGet CLı listesi komutu
description: NuGet. exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328326"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="c805a-103">List komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="c805a-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="c805a-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="c805a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c805a-105">Belirli bir kaynaktaki paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c805a-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="c805a-106">Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`' de tanımlanan tüm kaynaklar kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c805a-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="c805a-107">Kaynak belirtilmezse, varsayılan akışı kullanır (NuGet.org). `list` `NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="c805a-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="c805a-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c805a-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="c805a-109">isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek.</span><span class="sxs-lookup"><span data-stu-id="c805a-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="c805a-110">Arama terimleri, paketler, Etiketler ve paket açıklamaları adlarına, bunları nuget.org 'de kullanırken olduğu gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c805a-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="c805a-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="c805a-111">Options</span></span>

| <span data-ttu-id="c805a-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="c805a-112">Option</span></span> | <span data-ttu-id="c805a-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c805a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c805a-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="c805a-114">AllVersions</span></span> | <span data-ttu-id="c805a-115">Bir paketin tüm sürümlerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="c805a-115">List all versions of a package.</span></span> <span data-ttu-id="c805a-116">Varsayılan olarak, yalnızca en son paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c805a-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="c805a-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c805a-117">ConfigFile</span></span> | <span data-ttu-id="c805a-118">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c805a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c805a-119">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c805a-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c805a-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c805a-120">ForceEnglishOutput</span></span> | <span data-ttu-id="c805a-121">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="c805a-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c805a-122">Help</span><span class="sxs-lookup"><span data-stu-id="c805a-122">Help</span></span> | <span data-ttu-id="c805a-123">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c805a-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="c805a-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="c805a-124">IncludeDelisted</span></span> | <span data-ttu-id="c805a-125">*(3.2 +)* Listelenmemiş paketleri görüntüle.</span><span class="sxs-lookup"><span data-stu-id="c805a-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="c805a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c805a-126">NonInteractive</span></span> | <span data-ttu-id="c805a-127">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="c805a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c805a-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="c805a-128">PreRelease</span></span> | <span data-ttu-id="c805a-129">Listedeki yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c805a-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="c805a-130">Source</span><span class="sxs-lookup"><span data-stu-id="c805a-130">Source</span></span> | <span data-ttu-id="c805a-131">Aranacak paket kaynaklarının bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c805a-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="c805a-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c805a-132">Verbosity</span></span> | <span data-ttu-id="c805a-133">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="c805a-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c805a-134">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c805a-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c805a-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c805a-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
