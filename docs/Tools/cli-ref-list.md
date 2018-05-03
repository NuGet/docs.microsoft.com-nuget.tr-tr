---
title: NuGet CLI Listele komutu
description: Başvuru için nuget.exe Listele komutu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="842a5-103">LIST komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="842a5-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="842a5-104">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="842a5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="842a5-105">Belirli bir kaynaktan alınan paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="842a5-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="842a5-106">Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="842a5-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="842a5-107">Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.</span><span class="sxs-lookup"><span data-stu-id="842a5-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="842a5-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="842a5-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="842a5-109">Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek.</span><span class="sxs-lookup"><span data-stu-id="842a5-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="842a5-110">Nuget.org üzerinde kullanırken, olduğu gibi arama terimlerini paketler, etiketler ve paket açıklamaları adlarını uygulanır.</span><span class="sxs-lookup"><span data-stu-id="842a5-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="842a5-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="842a5-111">Options</span></span>

| <span data-ttu-id="842a5-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="842a5-112">Option</span></span> | <span data-ttu-id="842a5-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="842a5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="842a5-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="842a5-114">AllVersions</span></span> | <span data-ttu-id="842a5-115">Bir paketin tüm sürümleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="842a5-115">List all versions of a package.</span></span> <span data-ttu-id="842a5-116">Varsayılan olarak, yalnızca son Paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="842a5-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="842a5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="842a5-117">ConfigFile</span></span> | <span data-ttu-id="842a5-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="842a5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="842a5-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="842a5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="842a5-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="842a5-120">ForceEnglishOutput</span></span> | <span data-ttu-id="842a5-121">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="842a5-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="842a5-122">Yardım</span><span class="sxs-lookup"><span data-stu-id="842a5-122">Help</span></span> | <span data-ttu-id="842a5-123">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="842a5-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="842a5-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="842a5-124">IncludeDelisted</span></span> | <span data-ttu-id="842a5-125">*(3.2 +)*  Listelenmemiş paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="842a5-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="842a5-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="842a5-126">NonInteractive</span></span> | <span data-ttu-id="842a5-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="842a5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="842a5-128">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="842a5-128">PreRelease</span></span> | <span data-ttu-id="842a5-129">Ön sürüm paketlerini listede içerir.</span><span class="sxs-lookup"><span data-stu-id="842a5-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="842a5-130">Kaynak</span><span class="sxs-lookup"><span data-stu-id="842a5-130">Source</span></span> | <span data-ttu-id="842a5-131">Aranacak paket kaynaklarının listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="842a5-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="842a5-132">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="842a5-132">Verbosity</span></span> | <span data-ttu-id="842a5-133">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="842a5-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="842a5-134">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="842a5-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="842a5-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="842a5-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
