---
title: NuGet CLI setapikey komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe setapikey komut başvurusu"
keywords: "nuget setapikey başvuru, setapikey komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="be8bf-104">setapikey komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="be8bf-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="be8bf-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="be8bf-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="be8bf-106">Verilen sunucu URL'si bir API anahtarı kaydeder `NuGet.Config` böylece sonraki komutlarında girilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="be8bf-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="be8bf-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="be8bf-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="be8bf-108">Burada `<source>` sunucuyu tanımlar ve `<key>` anahtar ya da kaydetmek için parola.</span><span class="sxs-lookup"><span data-stu-id="be8bf-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="be8bf-109">Varsa `<source>` olan atlandığında nuget.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="be8bf-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="be8bf-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="be8bf-110">Options</span></span>

| <span data-ttu-id="be8bf-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="be8bf-111">Option</span></span> | <span data-ttu-id="be8bf-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be8bf-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="be8bf-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="be8bf-113">ConfigFile</span></span> | <span data-ttu-id="be8bf-114">Değiştirmek için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="be8bf-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="be8bf-115">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be8bf-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="be8bf-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="be8bf-116">ForceEnglishOutput</span></span> | <span data-ttu-id="be8bf-117">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="be8bf-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="be8bf-118">Yardım</span><span class="sxs-lookup"><span data-stu-id="be8bf-118">Help</span></span> | <span data-ttu-id="be8bf-119">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="be8bf-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="be8bf-120">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="be8bf-120">NonInteractive</span></span> | <span data-ttu-id="be8bf-121">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="be8bf-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="be8bf-122">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="be8bf-122">Verbosity</span></span> | <span data-ttu-id="be8bf-123">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="be8bf-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="be8bf-124">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="be8bf-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="be8bf-125">Örnekler</span><span class="sxs-lookup"><span data-stu-id="be8bf-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```