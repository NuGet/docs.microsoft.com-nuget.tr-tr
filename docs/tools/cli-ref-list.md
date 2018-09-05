---
title: NuGet CLI Listele komutu
description: Nuget.exe Listele komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549807"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="28df2-103">Liste komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="28df2-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="28df2-104">**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="28df2-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="28df2-105">Paketlerin belirli bir kaynaktan bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="28df2-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="28df2-106">Kaynağı yok belirtilirse, genel yapılandırma dosyasında tanımlanan tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır.</span><span class="sxs-lookup"><span data-stu-id="28df2-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="28df2-107">Varsa `NuGet.Config` kaynağı yok, ardından belirtir `list` varsayılan akışı (nuget.org) kullanır.</span><span class="sxs-lookup"><span data-stu-id="28df2-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="28df2-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="28df2-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="28df2-109">İsteğe bağlı arama terimlerini görüntülenen listeyi filtrelemek burada.</span><span class="sxs-lookup"><span data-stu-id="28df2-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="28df2-110">Bunları nuget.org adresinden kullanırken olduğu gibi arama terimlerini paketleri, etiketleri ve açıklamaları paket adları için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="28df2-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="28df2-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="28df2-111">Options</span></span>

| <span data-ttu-id="28df2-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="28df2-112">Option</span></span> | <span data-ttu-id="28df2-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="28df2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28df2-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="28df2-114">AllVersions</span></span> | <span data-ttu-id="28df2-115">Bir paketin tüm sürümlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="28df2-115">List all versions of a package.</span></span> <span data-ttu-id="28df2-116">Varsayılan olarak, yalnızca en son Paket sürümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="28df2-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="28df2-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="28df2-117">ConfigFile</span></span> | <span data-ttu-id="28df2-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="28df2-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="28df2-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="28df2-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="28df2-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="28df2-120">ForceEnglishOutput</span></span> | <span data-ttu-id="28df2-121">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="28df2-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="28df2-122">Yardım</span><span class="sxs-lookup"><span data-stu-id="28df2-122">Help</span></span> | <span data-ttu-id="28df2-123">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="28df2-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="28df2-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="28df2-124">IncludeDelisted</span></span> | <span data-ttu-id="28df2-125">*(3.2 +)*  Listelenmemiş paketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="28df2-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="28df2-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="28df2-126">NonInteractive</span></span> | <span data-ttu-id="28df2-127">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="28df2-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="28df2-128">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="28df2-128">PreRelease</span></span> | <span data-ttu-id="28df2-129">Yayın öncesi paketleri listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="28df2-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="28df2-130">Kaynak</span><span class="sxs-lookup"><span data-stu-id="28df2-130">Source</span></span> | <span data-ttu-id="28df2-131">Aranacak paket kaynaklarını listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="28df2-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="28df2-132">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="28df2-132">Verbosity</span></span> | <span data-ttu-id="28df2-133">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="28df2-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="28df2-134">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="28df2-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="28df2-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="28df2-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
