---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545034"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="071e9-103">Yerel öğeler komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="071e9-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="071e9-104">**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="071e9-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="071e9-105">Temizler veya yerel NuGet kaynakları gibi listeler *http önbellek*, *genel paketleri* klasör ve geçici klasör.</span><span class="sxs-lookup"><span data-stu-id="071e9-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="071e9-106">`locals` Komutu ayrıca kullanılabilir konumların bir listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="071e9-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="071e9-107">Daha fazla bilgi için [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="071e9-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="071e9-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="071e9-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="071e9-109">Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, `temp` *(3.4 ve üzeri)*, ve `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="071e9-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="071e9-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="071e9-110">Options</span></span>

| <span data-ttu-id="071e9-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="071e9-111">Option</span></span> | <span data-ttu-id="071e9-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="071e9-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="071e9-113">Temizle</span><span class="sxs-lookup"><span data-stu-id="071e9-113">Clear</span></span> | <span data-ttu-id="071e9-114">Belirtilen klasör temizler.</span><span class="sxs-lookup"><span data-stu-id="071e9-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="071e9-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="071e9-115">ConfigFile</span></span> | <span data-ttu-id="071e9-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="071e9-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="071e9-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="071e9-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="071e9-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="071e9-118">ForceEnglishOutput</span></span> | <span data-ttu-id="071e9-119">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="071e9-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="071e9-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="071e9-120">Help</span></span> | <span data-ttu-id="071e9-121">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="071e9-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="071e9-122">List</span><span class="sxs-lookup"><span data-stu-id="071e9-122">List</span></span> | <span data-ttu-id="071e9-123">Belirtilen klasör konumunu veya ile kullanıldığında tüm klasör konumlarını listeler *tüm*.</span><span class="sxs-lookup"><span data-stu-id="071e9-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="071e9-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="071e9-124">NonInteractive</span></span> | <span data-ttu-id="071e9-125">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="071e9-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="071e9-126">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="071e9-126">Verbosity</span></span> | <span data-ttu-id="071e9-127">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="071e9-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="071e9-128">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="071e9-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="071e9-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="071e9-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="071e9-130">Diğer örnekler için [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="071e9-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
