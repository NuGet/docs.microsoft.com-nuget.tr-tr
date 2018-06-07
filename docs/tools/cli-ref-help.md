---
title: NuGet CLI Yardım komutu
description: Nuget.exe Yardım komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818262"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="44269-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="44269-103">help or ?</span></span> <span data-ttu-id="44269-104">Komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44269-104">command (NuGet CLI)</span></span>

<span data-ttu-id="44269-105">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="44269-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="44269-106">Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.</span><span class="sxs-lookup"><span data-stu-id="44269-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="44269-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="44269-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="44269-108">Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="44269-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="44269-109">Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, yükleme komutunda Yardım çalışmaz, ancak bunun yerine Yardım adlı paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="44269-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="44269-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="44269-110">Options</span></span>

| <span data-ttu-id="44269-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="44269-111">Option</span></span> | <span data-ttu-id="44269-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44269-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44269-113">Tümü</span><span class="sxs-lookup"><span data-stu-id="44269-113">All</span></span> | <span data-ttu-id="44269-114">Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="44269-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="44269-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="44269-115">ConfigFile</span></span> | <span data-ttu-id="44269-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="44269-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="44269-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44269-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="44269-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="44269-118">ForceEnglishOutput</span></span> | <span data-ttu-id="44269-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="44269-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="44269-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="44269-120">Help</span></span> | <span data-ttu-id="44269-121">Bilgi Yardım komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="44269-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="44269-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="44269-122">Markdown</span></span> | <span data-ttu-id="44269-123">Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`.</span><span class="sxs-lookup"><span data-stu-id="44269-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="44269-124">Aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="44269-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="44269-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="44269-125">NonInteractive</span></span> | <span data-ttu-id="44269-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="44269-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="44269-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="44269-127">Verbosity</span></span> | <span data-ttu-id="44269-128">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="44269-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="44269-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="44269-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44269-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="44269-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
