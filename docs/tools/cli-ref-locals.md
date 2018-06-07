---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818207"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="1f190-103">Yerel öğeler komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1f190-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="1f190-104">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="1f190-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1f190-105">Temizler veya yerel NuGet kaynaklar gibi listeler *http önbellek*, *paketleri genel* klasörü ve geçici klasör.</span><span class="sxs-lookup"><span data-stu-id="1f190-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="1f190-106">`locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f190-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="1f190-107">Daha fazla bilgi için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1f190-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1f190-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1f190-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="1f190-109">Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, ve `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="1f190-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="1f190-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="1f190-110">Options</span></span>

| <span data-ttu-id="1f190-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="1f190-111">Option</span></span> | <span data-ttu-id="1f190-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1f190-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f190-113">Temizle</span><span class="sxs-lookup"><span data-stu-id="1f190-113">Clear</span></span> | <span data-ttu-id="1f190-114">Belirtilen klasör temizler.</span><span class="sxs-lookup"><span data-stu-id="1f190-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="1f190-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f190-115">ConfigFile</span></span> | <span data-ttu-id="1f190-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="1f190-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f190-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f190-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f190-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f190-118">ForceEnglishOutput</span></span> | <span data-ttu-id="1f190-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="1f190-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f190-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="1f190-120">Help</span></span> | <span data-ttu-id="1f190-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1f190-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f190-122">List</span><span class="sxs-lookup"><span data-stu-id="1f190-122">List</span></span> | <span data-ttu-id="1f190-123">Belirtilen klasör konumunu veya kullanıldığında tüm klasör konumlarını listeler *tüm*.</span><span class="sxs-lookup"><span data-stu-id="1f190-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="1f190-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f190-124">NonInteractive</span></span> | <span data-ttu-id="1f190-125">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="1f190-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f190-126">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="1f190-126">Verbosity</span></span> | <span data-ttu-id="1f190-127">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="1f190-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1f190-128">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1f190-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1f190-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1f190-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="1f190-130">Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1f190-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
