---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="d63b0-103">locals komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d63b0-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d63b0-104">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="d63b0-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d63b0-105">Temizler veya yerel NuGet kaynaklar gibi listeler *http önbellek*, *paketleri genel* klasörü ve geçici klasör.</span><span class="sxs-lookup"><span data-stu-id="d63b0-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="d63b0-106">`locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d63b0-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d63b0-107">Daha fazla bilgi için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d63b0-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d63b0-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d63b0-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="d63b0-109">Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, ve `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="d63b0-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d63b0-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d63b0-110">Options</span></span>

| <span data-ttu-id="d63b0-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="d63b0-111">Option</span></span> | <span data-ttu-id="d63b0-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d63b0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d63b0-113">Temizle</span><span class="sxs-lookup"><span data-stu-id="d63b0-113">Clear</span></span> | <span data-ttu-id="d63b0-114">Belirtilen klasör temizler.</span><span class="sxs-lookup"><span data-stu-id="d63b0-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="d63b0-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d63b0-115">ConfigFile</span></span> | <span data-ttu-id="d63b0-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d63b0-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d63b0-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d63b0-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d63b0-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d63b0-118">ForceEnglishOutput</span></span> | <span data-ttu-id="d63b0-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="d63b0-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d63b0-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="d63b0-120">Help</span></span> | <span data-ttu-id="d63b0-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d63b0-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d63b0-122">List</span><span class="sxs-lookup"><span data-stu-id="d63b0-122">List</span></span> | <span data-ttu-id="d63b0-123">Belirtilen klasör konumunu veya kullanıldığında tüm klasör konumlarını listeler *tüm*.</span><span class="sxs-lookup"><span data-stu-id="d63b0-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="d63b0-124">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="d63b0-124">NonInteractive</span></span> | <span data-ttu-id="d63b0-125">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="d63b0-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d63b0-126">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="d63b0-126">Verbosity</span></span> | <span data-ttu-id="d63b0-127">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="d63b0-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d63b0-128">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d63b0-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d63b0-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d63b0-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="d63b0-130">Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d63b0-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
