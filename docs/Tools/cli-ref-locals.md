---
title: NuGet CLI Yereller komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe Yereller komut başvurusu
keywords: nuget Yereller başvuru, Yereller komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="a1142-104">Yerel öğeler komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a1142-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="a1142-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a1142-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a1142-106">Temizler veya yerel NuGet kaynaklar gibi listeler *http önbellek*, *paketleri genel* klasörü ve geçici klasör.</span><span class="sxs-lookup"><span data-stu-id="a1142-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="a1142-107">`locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a1142-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="a1142-108">Daha fazla bilgi için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a1142-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a1142-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a1142-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="a1142-110">Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, ve `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="a1142-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="a1142-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a1142-111">Options</span></span>

| <span data-ttu-id="a1142-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="a1142-112">Option</span></span> | <span data-ttu-id="a1142-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a1142-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1142-114">Temizle</span><span class="sxs-lookup"><span data-stu-id="a1142-114">Clear</span></span> | <span data-ttu-id="a1142-115">Belirtilen klasör temizler.</span><span class="sxs-lookup"><span data-stu-id="a1142-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="a1142-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a1142-116">ConfigFile</span></span> | <span data-ttu-id="a1142-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a1142-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a1142-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1142-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a1142-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a1142-119">ForceEnglishOutput</span></span> | <span data-ttu-id="a1142-120">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="a1142-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a1142-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="a1142-121">Help</span></span> | <span data-ttu-id="a1142-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a1142-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="a1142-123">List</span><span class="sxs-lookup"><span data-stu-id="a1142-123">List</span></span> | <span data-ttu-id="a1142-124">Belirtilen klasör konumunu veya kullanıldığında tüm klasör konumlarını listeler *tüm*.</span><span class="sxs-lookup"><span data-stu-id="a1142-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="a1142-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="a1142-125">NonInteractive</span></span> | <span data-ttu-id="a1142-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="a1142-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a1142-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="a1142-127">Verbosity</span></span> | <span data-ttu-id="a1142-128">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="a1142-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a1142-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a1142-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a1142-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a1142-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="a1142-131">Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a1142-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
