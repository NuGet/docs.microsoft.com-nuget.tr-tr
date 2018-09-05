---
title: NuGet CLI setapikey komutunu
description: Nuget.exe setapikey komutunu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549226"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="bcd30-103">setapikey komutunu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bcd30-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="bcd30-104">**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="bcd30-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="bcd30-105">İçinde belirtilen sunucu URL'si için bir API anahtarı kaydeder `NuGet.Config` böylece sonraki komutlarda kullanılmak girilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bcd30-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="bcd30-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcd30-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="bcd30-107">Burada `<source>` sunucuyu tanımlar ve `<key>` anahtarı veya kaydetmek için parola.</span><span class="sxs-lookup"><span data-stu-id="bcd30-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="bcd30-108">Varsa `<source>` olan atlanırsa nuget.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="bcd30-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="bcd30-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="bcd30-109">Options</span></span>

| <span data-ttu-id="bcd30-110">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bcd30-110">Option</span></span> | <span data-ttu-id="bcd30-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcd30-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcd30-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bcd30-112">ConfigFile</span></span> | <span data-ttu-id="bcd30-113">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bcd30-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bcd30-114">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bcd30-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bcd30-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bcd30-115">ForceEnglishOutput</span></span> | <span data-ttu-id="bcd30-116">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="bcd30-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bcd30-117">Yardım</span><span class="sxs-lookup"><span data-stu-id="bcd30-117">Help</span></span> | <span data-ttu-id="bcd30-118">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bcd30-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="bcd30-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bcd30-119">NonInteractive</span></span> | <span data-ttu-id="bcd30-120">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="bcd30-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bcd30-121">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="bcd30-121">Verbosity</span></span> | <span data-ttu-id="bcd30-122">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="bcd30-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bcd30-123">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bcd30-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bcd30-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bcd30-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
