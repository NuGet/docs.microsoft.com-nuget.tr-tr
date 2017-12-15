---
title: "NuGet CLI Yardım komutu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe Yardım komut başvurusu"
keywords: "nuget Yardım başvurusu, Yardım komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="4a0c9-104">Yardım veya?</span><span class="sxs-lookup"><span data-stu-id="4a0c9-104">help or ?</span></span> <span data-ttu-id="4a0c9-105">Komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4a0c9-105">command (NuGet CLI)</span></span>

<span data-ttu-id="4a0c9-106">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="4a0c9-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="4a0c9-107">Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="4a0c9-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="4a0c9-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="4a0c9-109">Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="4a0c9-110">Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, Yardım yükleme komutunda alırsınız değil, ancak bunun yerine Yardım adlı paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="4a0c9-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="4a0c9-111">Options</span></span>

| <span data-ttu-id="4a0c9-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="4a0c9-112">Option</span></span> | <span data-ttu-id="4a0c9-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4a0c9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a0c9-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="4a0c9-114">All</span></span> | <span data-ttu-id="4a0c9-115">Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="4a0c9-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4a0c9-116">ConfigFile</span></span> | <span data-ttu-id="4a0c9-117">*(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="4a0c9-118">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4a0c9-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4a0c9-119">ForceEnglishOutput</span></span> | <span data-ttu-id="4a0c9-120">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4a0c9-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="4a0c9-121">Help</span></span> | <span data-ttu-id="4a0c9-122">Bilgi Yardım komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="4a0c9-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="4a0c9-123">Markdown</span></span> | <span data-ttu-id="4a0c9-124">Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="4a0c9-125">Aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="4a0c9-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="4a0c9-126">NonInteractive</span></span> | <span data-ttu-id="4a0c9-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4a0c9-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="4a0c9-128">Verbosity</span></span> | <span data-ttu-id="4a0c9-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="4a0c9-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="4a0c9-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4a0c9-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4a0c9-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="4a0c9-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
