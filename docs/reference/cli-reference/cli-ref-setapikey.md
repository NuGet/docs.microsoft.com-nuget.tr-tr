---
title: NuGet CLı setapikey komutu
description: NuGet. exe setapikey komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328287"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="0c2f4-103">setapikey komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="0c2f4-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="0c2f4-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="0c2f4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0c2f4-105">Belirli bir sunucu URL 'si için bir API anahtarını, `NuGet.Config` sonraki komutlara girilmesi gerekmemesi için öğesine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="0c2f4-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="0c2f4-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="0c2f4-107">Burada `<source>` sunucuyu tanımlar ve `<key>` kaydedilecek anahtar veya paroladır.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="0c2f4-108">`<source>` Atlanırsa, NuGet.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="0c2f4-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="0c2f4-109">Options</span></span>

| <span data-ttu-id="0c2f4-110">Seçenek</span><span class="sxs-lookup"><span data-stu-id="0c2f4-110">Option</span></span> | <span data-ttu-id="0c2f4-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0c2f4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c2f4-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0c2f4-112">ConfigFile</span></span> | <span data-ttu-id="0c2f4-113">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0c2f4-114">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0c2f4-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0c2f4-115">ForceEnglishOutput</span></span> | <span data-ttu-id="0c2f4-116">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0c2f4-117">Help</span><span class="sxs-lookup"><span data-stu-id="0c2f4-117">Help</span></span> | <span data-ttu-id="0c2f4-118">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="0c2f4-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0c2f4-119">NonInteractive</span></span> | <span data-ttu-id="0c2f4-120">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0c2f4-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="0c2f4-121">Verbosity</span></span> | <span data-ttu-id="0c2f4-122">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="0c2f4-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0c2f4-123">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0c2f4-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0c2f4-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0c2f4-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
