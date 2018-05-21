---
title: NuGet CLI Yardım komutu
description: Nuget.exe Yardım komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="97cf1-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="97cf1-103">help or ?</span></span> <span data-ttu-id="97cf1-104">komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97cf1-104">command (NuGet CLI)</span></span>

<span data-ttu-id="97cf1-105">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="97cf1-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="97cf1-106">Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="97cf1-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="97cf1-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="97cf1-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="97cf1-108">Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="97cf1-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="97cf1-109">Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, yükleme komutunda Yardım çalışmaz, ancak bunun yerine Yardım adlı paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="97cf1-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="97cf1-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="97cf1-110">Options</span></span>

| <span data-ttu-id="97cf1-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="97cf1-111">Option</span></span> | <span data-ttu-id="97cf1-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97cf1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97cf1-113">Tümü</span><span class="sxs-lookup"><span data-stu-id="97cf1-113">All</span></span> | <span data-ttu-id="97cf1-114">Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="97cf1-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="97cf1-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="97cf1-115">ConfigFile</span></span> | <span data-ttu-id="97cf1-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="97cf1-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="97cf1-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97cf1-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="97cf1-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="97cf1-118">ForceEnglishOutput</span></span> | <span data-ttu-id="97cf1-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="97cf1-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="97cf1-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="97cf1-120">Help</span></span> | <span data-ttu-id="97cf1-121">Bilgi Yardım komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="97cf1-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="97cf1-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="97cf1-122">Markdown</span></span> | <span data-ttu-id="97cf1-123">Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`.</span><span class="sxs-lookup"><span data-stu-id="97cf1-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="97cf1-124">Aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="97cf1-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="97cf1-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="97cf1-125">NonInteractive</span></span> | <span data-ttu-id="97cf1-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="97cf1-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="97cf1-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="97cf1-127">Verbosity</span></span> | <span data-ttu-id="97cf1-128">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="97cf1-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="97cf1-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="97cf1-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="97cf1-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="97cf1-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
