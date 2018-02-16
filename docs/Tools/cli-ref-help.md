---
title: "NuGet CLI Yardım komutu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe Yardım komut başvurusu"
keywords: "nuget Yardım başvurusu, Yardım komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="79ab1-104">Yardım veya?</span><span class="sxs-lookup"><span data-stu-id="79ab1-104">help or ?</span></span> <span data-ttu-id="79ab1-105">Komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="79ab1-105">command (NuGet CLI)</span></span>

<span data-ttu-id="79ab1-106">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="79ab1-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="79ab1-107">Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79ab1-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="79ab1-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="79ab1-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="79ab1-109">Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="79ab1-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="79ab1-110">Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, yükleme komutunda Yardım çalışmaz, ancak bunun yerine Yardım adlı paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="79ab1-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="79ab1-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="79ab1-111">Options</span></span>

| <span data-ttu-id="79ab1-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="79ab1-112">Option</span></span> | <span data-ttu-id="79ab1-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79ab1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="79ab1-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="79ab1-114">All</span></span> | <span data-ttu-id="79ab1-115">Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="79ab1-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="79ab1-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="79ab1-116">ConfigFile</span></span> | <span data-ttu-id="79ab1-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="79ab1-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="79ab1-118">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="79ab1-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="79ab1-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="79ab1-119">ForceEnglishOutput</span></span> | <span data-ttu-id="79ab1-120">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="79ab1-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="79ab1-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="79ab1-121">Help</span></span> | <span data-ttu-id="79ab1-122">Bilgi Yardım komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79ab1-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="79ab1-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="79ab1-123">Markdown</span></span> | <span data-ttu-id="79ab1-124">Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`.</span><span class="sxs-lookup"><span data-stu-id="79ab1-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="79ab1-125">Aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="79ab1-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="79ab1-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="79ab1-126">NonInteractive</span></span> | <span data-ttu-id="79ab1-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="79ab1-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="79ab1-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="79ab1-128">Verbosity</span></span> | <span data-ttu-id="79ab1-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="79ab1-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="79ab1-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="79ab1-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="79ab1-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="79ab1-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
