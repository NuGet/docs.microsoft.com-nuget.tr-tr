---
title: NuGet CLı setapikey komutu
description: NuGet. exe setapikey komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383975"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2671f-103">setapikey komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="2671f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2671f-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="2671f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2671f-105">Belirli bir sunucu URL 'SI için bir API anahtarını, sonraki komutlara girilmesi gerekmiyorsa, `NuGet.Config` ' a kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2671f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2671f-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="2671f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2671f-107">`<source>` sunucuyu tanımladığı ve `<key>`, kaydedilecek anahtar veya paroladır.</span><span class="sxs-lookup"><span data-stu-id="2671f-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2671f-108">`<source>` atlanırsa, nuget.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="2671f-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="2671f-109">API anahtarı özel akışta kimlik doğrulaması için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="2671f-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="2671f-110">Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [`nuget sources` komutuna](../cli-reference/cli-ref-sources.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="2671f-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="2671f-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="2671f-111">Options</span></span>

| <span data-ttu-id="2671f-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="2671f-112">Option</span></span> | <span data-ttu-id="2671f-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2671f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2671f-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2671f-114">ConfigFile</span></span> | <span data-ttu-id="2671f-115">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="2671f-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2671f-116">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2671f-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2671f-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2671f-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2671f-118">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="2671f-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2671f-119">Yardım</span><span class="sxs-lookup"><span data-stu-id="2671f-119">Help</span></span> | <span data-ttu-id="2671f-120">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2671f-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="2671f-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2671f-121">NonInteractive</span></span> | <span data-ttu-id="2671f-122">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="2671f-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2671f-123">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="2671f-123">Verbosity</span></span> | <span data-ttu-id="2671f-124">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="2671f-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2671f-125">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2671f-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2671f-126">Örnekler</span><span class="sxs-lookup"><span data-stu-id="2671f-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
