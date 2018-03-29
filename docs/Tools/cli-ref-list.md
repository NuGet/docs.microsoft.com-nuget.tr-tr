---
title: NuGet CLI Listele komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Başvuru için nuget.exe Listele komutu
keywords: nuget listesi başvurusu, liste paketleri komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="96bf3-104">LIST komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="96bf3-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="96bf3-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="96bf3-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="96bf3-106">Belirli bir kaynaktan alınan paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96bf3-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="96bf3-107">Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96bf3-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="96bf3-108">Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.</span><span class="sxs-lookup"><span data-stu-id="96bf3-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="96bf3-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="96bf3-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="96bf3-110">Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek.</span><span class="sxs-lookup"><span data-stu-id="96bf3-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="96bf3-111">Nuget.org üzerinde kullanırken, olduğu gibi arama terimlerini paketler, etiketler ve paket açıklamaları adlarını uygulanır.</span><span class="sxs-lookup"><span data-stu-id="96bf3-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="96bf3-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="96bf3-112">Options</span></span>

| <span data-ttu-id="96bf3-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="96bf3-113">Option</span></span> | <span data-ttu-id="96bf3-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96bf3-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96bf3-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="96bf3-115">AllVersions</span></span> | <span data-ttu-id="96bf3-116">Bir paketin tüm sürümleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="96bf3-116">List all versions of a package.</span></span> <span data-ttu-id="96bf3-117">Varsayılan olarak, yalnızca son Paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="96bf3-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="96bf3-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="96bf3-118">ConfigFile</span></span> | <span data-ttu-id="96bf3-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="96bf3-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="96bf3-120">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96bf3-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="96bf3-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="96bf3-121">ForceEnglishOutput</span></span> | <span data-ttu-id="96bf3-122">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="96bf3-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="96bf3-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="96bf3-123">Help</span></span> | <span data-ttu-id="96bf3-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96bf3-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="96bf3-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="96bf3-125">IncludeDelisted</span></span> | <span data-ttu-id="96bf3-126">*(3.2 +)*  Listelenmemiş paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96bf3-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="96bf3-127">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="96bf3-127">NonInteractive</span></span> | <span data-ttu-id="96bf3-128">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="96bf3-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="96bf3-129">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="96bf3-129">PreRelease</span></span> | <span data-ttu-id="96bf3-130">Ön sürüm paketlerini listede içerir.</span><span class="sxs-lookup"><span data-stu-id="96bf3-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="96bf3-131">Kaynak</span><span class="sxs-lookup"><span data-stu-id="96bf3-131">Source</span></span> | <span data-ttu-id="96bf3-132">Aranacak paket kaynaklarının listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="96bf3-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="96bf3-133">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="96bf3-133">Verbosity</span></span> | <span data-ttu-id="96bf3-134">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="96bf3-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="96bf3-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="96bf3-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="96bf3-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="96bf3-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
