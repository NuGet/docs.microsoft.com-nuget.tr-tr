---
title: NuGet CLI Listele komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Başvuru için nuget.exe Listele komutu"
keywords: "nuget listesi başvurusu, liste paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="f23c0-104">LIST komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f23c0-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="f23c0-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="f23c0-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f23c0-106">Belirli bir kaynaktan alınan paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f23c0-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="f23c0-107">Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f23c0-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="f23c0-108">Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.</span><span class="sxs-lookup"><span data-stu-id="f23c0-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="f23c0-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="f23c0-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="f23c0-110">Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek.</span><span class="sxs-lookup"><span data-stu-id="f23c0-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="f23c0-111">Arama terimleri paketler, etiketler ve paket açıklamaları adlarını uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f23c0-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="f23c0-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="f23c0-112">Options</span></span>
| <span data-ttu-id="f23c0-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="f23c0-113">Option</span></span> | <span data-ttu-id="f23c0-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f23c0-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f23c0-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f23c0-115">AllVersions</span></span> | <span data-ttu-id="f23c0-116">Bir paketin tüm sürümleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="f23c0-116">List all versions of a package.</span></span> <span data-ttu-id="f23c0-117">Varsayılan olarak, yalnızca son Paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f23c0-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="f23c0-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f23c0-118">ConfigFile</span></span> | <span data-ttu-id="f23c0-119">*(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="f23c0-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="f23c0-120">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f23c0-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f23c0-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f23c0-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f23c0-122">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="f23c0-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f23c0-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="f23c0-123">Help</span></span> | <span data-ttu-id="f23c0-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f23c0-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f23c0-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="f23c0-125">IncludeDelisted</span></span> | <span data-ttu-id="f23c0-126">*(3.2 +)*  Listelenmemiş paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f23c0-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="f23c0-127">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="f23c0-127">NonInteractive</span></span> | <span data-ttu-id="f23c0-128">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="f23c0-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f23c0-129">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="f23c0-129">PreRelease</span></span> | <span data-ttu-id="f23c0-130">Ön sürüm paketlerini listede içerir.</span><span class="sxs-lookup"><span data-stu-id="f23c0-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="f23c0-131">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f23c0-131">Source</span></span> | <span data-ttu-id="f23c0-132">Aranacak paket kaynaklarının listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f23c0-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="f23c0-133">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="f23c0-133">Verbosity</span></span> | <span data-ttu-id="f23c0-134">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="f23c0-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="f23c0-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f23c0-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f23c0-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f23c0-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
