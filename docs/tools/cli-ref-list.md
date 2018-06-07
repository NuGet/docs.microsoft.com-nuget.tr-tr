---
title: NuGet CLI Listele komutu
description: Başvuru için nuget.exe Listele komutu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818444"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b35cf-103">LIST komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b35cf-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="b35cf-104">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="b35cf-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b35cf-105">Belirli bir kaynaktan alınan paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b35cf-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b35cf-106">Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b35cf-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b35cf-107">Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b35cf-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b35cf-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="b35cf-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b35cf-109">Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek.</span><span class="sxs-lookup"><span data-stu-id="b35cf-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b35cf-110">Nuget.org üzerinde kullanırken, olduğu gibi arama terimlerini paketler, etiketler ve paket açıklamaları adlarını uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b35cf-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="b35cf-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b35cf-111">Options</span></span>

| <span data-ttu-id="b35cf-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="b35cf-112">Option</span></span> | <span data-ttu-id="b35cf-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b35cf-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b35cf-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b35cf-114">AllVersions</span></span> | <span data-ttu-id="b35cf-115">Bir paketin tüm sürümleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="b35cf-115">List all versions of a package.</span></span> <span data-ttu-id="b35cf-116">Varsayılan olarak, yalnızca son Paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b35cf-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b35cf-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b35cf-117">ConfigFile</span></span> | <span data-ttu-id="b35cf-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="b35cf-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b35cf-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b35cf-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b35cf-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b35cf-120">ForceEnglishOutput</span></span> | <span data-ttu-id="b35cf-121">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="b35cf-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b35cf-122">Yardım</span><span class="sxs-lookup"><span data-stu-id="b35cf-122">Help</span></span> | <span data-ttu-id="b35cf-123">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b35cf-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="b35cf-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b35cf-124">IncludeDelisted</span></span> | <span data-ttu-id="b35cf-125">*(3.2 +)*  Listelenmemiş paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b35cf-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b35cf-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b35cf-126">NonInteractive</span></span> | <span data-ttu-id="b35cf-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="b35cf-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b35cf-128">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="b35cf-128">PreRelease</span></span> | <span data-ttu-id="b35cf-129">Ön sürüm paketlerini listede içerir.</span><span class="sxs-lookup"><span data-stu-id="b35cf-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b35cf-130">Kaynak</span><span class="sxs-lookup"><span data-stu-id="b35cf-130">Source</span></span> | <span data-ttu-id="b35cf-131">Aranacak paket kaynaklarının listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b35cf-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b35cf-132">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="b35cf-132">Verbosity</span></span> | <span data-ttu-id="b35cf-133">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="b35cf-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b35cf-134">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b35cf-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b35cf-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b35cf-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
