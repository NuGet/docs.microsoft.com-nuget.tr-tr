---
title: NuGet CLI setapikey komutu
description: Nuget.exe setapikey komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 968e22f32e51659590a6fe1e881bf5a9792a1331
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="a96a2-103">setapikey komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a96a2-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="a96a2-104">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="a96a2-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a96a2-105">Verilen sunucu URL'si bir API anahtarı kaydeder `NuGet.Config` böylece sonraki komutlarında girilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a96a2-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a96a2-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a96a2-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="a96a2-107">Burada `<source>` sunucuyu tanımlar ve `<key>` anahtar ya da kaydetmek için parola.</span><span class="sxs-lookup"><span data-stu-id="a96a2-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="a96a2-108">Varsa `<source>` olan atlandığında nuget.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="a96a2-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="a96a2-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a96a2-109">Options</span></span>

| <span data-ttu-id="a96a2-110">Seçenek</span><span class="sxs-lookup"><span data-stu-id="a96a2-110">Option</span></span> | <span data-ttu-id="a96a2-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a96a2-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a96a2-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a96a2-112">ConfigFile</span></span> | <span data-ttu-id="a96a2-113">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a96a2-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a96a2-114">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a96a2-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a96a2-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a96a2-115">ForceEnglishOutput</span></span> | <span data-ttu-id="a96a2-116">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="a96a2-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a96a2-117">Yardım</span><span class="sxs-lookup"><span data-stu-id="a96a2-117">Help</span></span> | <span data-ttu-id="a96a2-118">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a96a2-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="a96a2-119">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="a96a2-119">NonInteractive</span></span> | <span data-ttu-id="a96a2-120">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="a96a2-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a96a2-121">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="a96a2-121">Verbosity</span></span> | <span data-ttu-id="a96a2-122">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="a96a2-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a96a2-123">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a96a2-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a96a2-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a96a2-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
