---
title: NuGet CLı yardım komutu
description: NuGet. exe yardım komutu başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328344"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="33954-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="33954-103">help or ?</span></span> <span data-ttu-id="33954-104">komut (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="33954-104">command (NuGet CLI)</span></span>

<span data-ttu-id="33954-105">**Uygulama hedefi:** &bullet; tüm **Desteklenen sürümler**: tümü</span><span class="sxs-lookup"><span data-stu-id="33954-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="33954-106">Belirli komutlarla ilgili genel yardım bilgilerini ve yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="33954-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="33954-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="33954-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="33954-108">Burada [komut], yardım görüntülenecek belirli bir komutu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="33954-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="33954-109">Bazı komutlarla, NuGet.org üzerinde "Help" adlı bir  paket olduğu için, `nuget help install`' da olduğu gibi öncelikle yardım 'ı belirtmek için küçük bir değer belirleyin. Komuta `nuget install help`sahipseniz, install komutuyla ilgili yardım almaz, ancak bunun yerine yardım adlı paketi yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="33954-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="33954-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="33954-110">Options</span></span>

| <span data-ttu-id="33954-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="33954-111">Option</span></span> | <span data-ttu-id="33954-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="33954-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="33954-113">Tümü</span><span class="sxs-lookup"><span data-stu-id="33954-113">All</span></span> | <span data-ttu-id="33954-114">Tüm kullanılabilir komutlar için ayrıntılı yardım Yazdır; belirli bir komut verildiyse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="33954-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="33954-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="33954-115">ConfigFile</span></span> | <span data-ttu-id="33954-116">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="33954-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="33954-117">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="33954-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="33954-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="33954-118">ForceEnglishOutput</span></span> | <span data-ttu-id="33954-119">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="33954-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="33954-120">Help</span><span class="sxs-lookup"><span data-stu-id="33954-120">Help</span></span> | <span data-ttu-id="33954-121">Yardım komutunun kendisi için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="33954-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="33954-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="33954-122">Markdown</span></span> | <span data-ttu-id="33954-123">İle `-All`kullanıldığında markaşağı biçiminde ayrıntılı yardım yazdırın.</span><span class="sxs-lookup"><span data-stu-id="33954-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="33954-124">Aksi halde yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="33954-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="33954-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="33954-125">NonInteractive</span></span> | <span data-ttu-id="33954-126">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="33954-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="33954-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="33954-127">Verbosity</span></span> | <span data-ttu-id="33954-128">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="33954-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="33954-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="33954-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="33954-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="33954-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
