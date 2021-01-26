---
title: NuGet CLı yardım komutu
description: nuget.exe Help komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779361"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="48a44-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="48a44-103">help or ?</span></span> <span data-ttu-id="48a44-104">komut (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="48a44-104">command (NuGet CLI)</span></span>

<span data-ttu-id="48a44-105">**Uygulama hedefi:** tüm &bullet; **Desteklenen sürümler**: tümü</span><span class="sxs-lookup"><span data-stu-id="48a44-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="48a44-106">Belirli komutlarla ilgili genel yardım bilgilerini ve yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="48a44-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="48a44-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="48a44-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="48a44-108">Burada [komut], yardım görüntülenecek belirli bir komutu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="48a44-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="48a44-109">Bazı komutlarla,  `nuget help install` NuGet.org üzerinde "Help" adlı bir paket olduğu için, ' da olduğu gibi öncelikle yardım 'ı belirtmek için küçük bir değer belirleyin. Komuta sahipseniz `nuget install help` , install komutuyla ilgili yardım almaz, ancak bunun yerine yardım adlı paketi yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="48a44-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="48a44-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="48a44-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="48a44-111">Tüm kullanılabilir komutlar için ayrıntılı yardım Yazdır; belirli bir komut verildiyse yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="48a44-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="48a44-112">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="48a44-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="48a44-113">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="48a44-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="48a44-114">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="48a44-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="48a44-115">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="48a44-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="48a44-116">İle kullanıldığında markaşağı biçiminde ayrıntılı yardım yazdırın `-All` .</span><span class="sxs-lookup"><span data-stu-id="48a44-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="48a44-117">Aksi halde yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="48a44-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="48a44-118">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="48a44-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="48a44-119">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="48a44-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="48a44-120">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="48a44-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="48a44-121">Örnekler</span><span class="sxs-lookup"><span data-stu-id="48a44-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
