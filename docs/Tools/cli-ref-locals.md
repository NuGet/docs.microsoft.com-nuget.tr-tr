---
title: NuGet CLI Yereller komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe Yereller komut başvurusu"
keywords: "nuget Yereller başvuru, Yereller komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c5442-104">Yerel öğeler komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c5442-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c5442-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c5442-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c5442-106">Temizler veya http isteği önbelleği, paketleri önbellek ve makine genelinde genel paketler klasörü gibi yerel NuGet kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="c5442-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="c5442-107">`locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c5442-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c5442-108">Daha fazla bilgi için bkz: [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="c5442-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c5442-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c5442-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="c5442-110">Burada `<cache>` biri `all`, `http-cache`, `packages-cache`, `global-packages`, ve `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="c5442-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c5442-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="c5442-111">Options</span></span>

| <span data-ttu-id="c5442-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="c5442-112">Option</span></span> | <span data-ttu-id="c5442-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c5442-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c5442-114">Temizle</span><span class="sxs-lookup"><span data-stu-id="c5442-114">Clear</span></span> | <span data-ttu-id="c5442-115">Belirtilen önbellek temizler.</span><span class="sxs-lookup"><span data-stu-id="c5442-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="c5442-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c5442-116">ConfigFile</span></span> | <span data-ttu-id="c5442-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c5442-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c5442-118">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c5442-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c5442-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c5442-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c5442-120">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="c5442-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c5442-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="c5442-121">Help</span></span> | <span data-ttu-id="c5442-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c5442-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c5442-123">List</span><span class="sxs-lookup"><span data-stu-id="c5442-123">List</span></span> | <span data-ttu-id="c5442-124">Belirtilen önbellek konumunu veya kullanıldığında tüm önbellekleri konumlarını listeler *tüm*.</span><span class="sxs-lookup"><span data-stu-id="c5442-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="c5442-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="c5442-125">NonInteractive</span></span> | <span data-ttu-id="c5442-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="c5442-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c5442-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="c5442-127">Verbosity</span></span> | <span data-ttu-id="c5442-128">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="c5442-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c5442-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c5442-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c5442-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c5442-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
