---
title: NuGet CLı listesi komutu
description: nuget.exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623077"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="dee4f-103">List komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="dee4f-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="dee4f-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="dee4f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="dee4f-105">Belirli bir kaynaktaki paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dee4f-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="dee4f-106">Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%AppData%\NuGet\NuGet.Config` (Windows) veya ' de tanımlanan tüm kaynaklar `~/.nuget/NuGet/NuGet.Config` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dee4f-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="dee4f-107">`NuGet.Config`Kaynak belirtilmezse, `list` varsayılan akışı kullanır (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="dee4f-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="dee4f-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="dee4f-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="dee4f-109">isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek.</span><span class="sxs-lookup"><span data-stu-id="dee4f-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="dee4f-110">[Arama terimleri](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) , paketler, Etiketler ve paket açıklamaları adlarına, bunları NuGet.org 'de kullanırken olduğu gibi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="dee4f-110">[Search terms](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="dee4f-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="dee4f-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="dee4f-112">Bir paketin tüm sürümlerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="dee4f-112">List all versions of a package.</span></span> <span data-ttu-id="dee4f-113">Varsayılan olarak, yalnızca en son paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dee4f-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="dee4f-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="dee4f-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dee4f-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dee4f-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="dee4f-116">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="dee4f-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="dee4f-117">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dee4f-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="dee4f-118">*(3.2 +)* Listelenmemiş paketleri görüntüle.</span><span class="sxs-lookup"><span data-stu-id="dee4f-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="dee4f-119">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="dee4f-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="dee4f-120">Listedeki yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="dee4f-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="dee4f-121">Aranacak paket kaynaklarının bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="dee4f-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="dee4f-122">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="dee4f-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="dee4f-123">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dee4f-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dee4f-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="dee4f-124">Examples</span></span>

<span data-ttu-id="dee4f-125">Yapılandırılmış akışlardan tüm paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="dee4f-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="dee4f-126">Ayrıntılı ayrıntı düzeyine sahip Azure ile ilgili paketleri listeleyin:</span><span class="sxs-lookup"><span data-stu-id="dee4f-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="dee4f-127">Yapılandırılmış akışlardan Azure ile ilgili paketlerin tüm sürümlerini listeleyin:</span><span class="sxs-lookup"><span data-stu-id="dee4f-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="dee4f-128">JSON ile ilgili tüm paketlerin sürümlerini belirtilen kaynaktan/akıştan listeleyin:</span><span class="sxs-lookup"><span data-stu-id="dee4f-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="dee4f-129">Birden çok kaynaktan/akışlardan JSON ile ilgili paketleri Listele:</span><span class="sxs-lookup"><span data-stu-id="dee4f-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
