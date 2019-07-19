---
title: NuGet CLı Yereller komutu
description: NuGet. exe Yereller komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328347"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="65af6-103">Yereller komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="65af6-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="65af6-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="65af6-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="65af6-105">*Http önbelleği*, *genel paketler* klasörü ve temp klasörü gibi yerel NuGet kaynaklarını temizler veya listeler.</span><span class="sxs-lookup"><span data-stu-id="65af6-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="65af6-106">`locals` Komut ayrıca bu konumların bir listesini göstermek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="65af6-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="65af6-107">Daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="65af6-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="65af6-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="65af6-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="65af6-109">Burada `<folder>` `all` `global-packages` `plugins-cache` , ,,`packages-cache` *(3,5 ve öncesi)* ,, `temp` *(3.4 +)* ve *(4.8 +)* ' den biridir. `http-cache`</span><span class="sxs-lookup"><span data-stu-id="65af6-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="65af6-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="65af6-110">Options</span></span>

| <span data-ttu-id="65af6-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="65af6-111">Option</span></span> | <span data-ttu-id="65af6-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="65af6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="65af6-113">Temizle</span><span class="sxs-lookup"><span data-stu-id="65af6-113">Clear</span></span> | <span data-ttu-id="65af6-114">Belirtilen klasörü temizler.</span><span class="sxs-lookup"><span data-stu-id="65af6-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="65af6-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="65af6-115">ConfigFile</span></span> | <span data-ttu-id="65af6-116">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="65af6-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="65af6-117">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65af6-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="65af6-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="65af6-118">ForceEnglishOutput</span></span> | <span data-ttu-id="65af6-119">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="65af6-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="65af6-120">Help</span><span class="sxs-lookup"><span data-stu-id="65af6-120">Help</span></span> | <span data-ttu-id="65af6-121">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="65af6-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="65af6-122">List</span><span class="sxs-lookup"><span data-stu-id="65af6-122">List</span></span> | <span data-ttu-id="65af6-123">Belirtilen klasörün konumunu veya tüm klasörlerin konumlarını, *Tümü*ile birlikte kullanıldığında listeler.</span><span class="sxs-lookup"><span data-stu-id="65af6-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="65af6-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="65af6-124">NonInteractive</span></span> | <span data-ttu-id="65af6-125">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="65af6-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="65af6-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="65af6-126">Verbosity</span></span> | <span data-ttu-id="65af6-127">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="65af6-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="65af6-128">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="65af6-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="65af6-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="65af6-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="65af6-130">Daha fazla örnek için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="65af6-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
