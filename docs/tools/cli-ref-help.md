---
title: NuGet CLI Yardım komutu
description: Nuget.exe Yardım komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546569"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="8728a-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="8728a-103">help or ?</span></span> <span data-ttu-id="8728a-104">Komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8728a-104">command (NuGet CLI)</span></span>

<span data-ttu-id="8728a-105">**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler**: tüm</span><span class="sxs-lookup"><span data-stu-id="8728a-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8728a-106">Genel görüntüler, bilgi yardımcı olmak ve özel komutlar hakkında bilgi yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8728a-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8728a-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8728a-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="8728a-108">Burada [komut] Yardım görüntülemek istediğiniz belirli bir komutu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8728a-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="8728a-109">Bazı komutlarla belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`nuget.org adresinden "help" adlı bir paketi olduğundan. Komutunu verirseniz `nuget install help`, Yardım yükleme komutunu vermeyeceğiz ancak bunun yerine Yardım adlı paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="8728a-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="8728a-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="8728a-110">Options</span></span>

| <span data-ttu-id="8728a-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="8728a-111">Option</span></span> | <span data-ttu-id="8728a-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8728a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8728a-113">Tümü</span><span class="sxs-lookup"><span data-stu-id="8728a-113">All</span></span> | <span data-ttu-id="8728a-114">Tüm kullanılabilir komutları için yazdırma ayrıntılı Yardım; belirli bir komut verildi yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="8728a-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="8728a-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8728a-115">ConfigFile</span></span> | <span data-ttu-id="8728a-116">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="8728a-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8728a-117">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8728a-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8728a-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8728a-118">ForceEnglishOutput</span></span> | <span data-ttu-id="8728a-119">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="8728a-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8728a-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="8728a-120">Help</span></span> | <span data-ttu-id="8728a-121">Bilgi Yardım komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8728a-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="8728a-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="8728a-122">Markdown</span></span> | <span data-ttu-id="8728a-123">Ayrıntılı Yardımı ile kullanıldığında, markdown biçiminde yazdırma `-All`.</span><span class="sxs-lookup"><span data-stu-id="8728a-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="8728a-124">Aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="8728a-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="8728a-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8728a-125">NonInteractive</span></span> | <span data-ttu-id="8728a-126">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="8728a-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8728a-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="8728a-127">Verbosity</span></span> | <span data-ttu-id="8728a-128">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="8728a-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8728a-129">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8728a-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8728a-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="8728a-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
