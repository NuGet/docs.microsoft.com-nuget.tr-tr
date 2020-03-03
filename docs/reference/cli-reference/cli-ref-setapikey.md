---
title: NuGet CLı setapikey komutu
description: NuGet. exe setapikey komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231233"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="bb90a-103">setapikey komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="bb90a-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="bb90a-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="bb90a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="bb90a-105">Belirli bir sunucu URL 'SI için bir API anahtarını, sonraki komutlara girilmesi gerekmiyorsa, `NuGet.Config` ' a kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bb90a-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="bb90a-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bb90a-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="bb90a-107">Burada `<source>` sunucuyu tanımlar ve `<key>` kaydedilecek anahtardır.</span><span class="sxs-lookup"><span data-stu-id="bb90a-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="bb90a-108">`<source>` atlanırsa, nuget.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="bb90a-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="bb90a-109">API anahtarı özel akışta kimlik doğrulaması için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="bb90a-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="bb90a-110">Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [`nuget sources` komutuna](../cli-reference/cli-ref-sources.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="bb90a-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="bb90a-111">Tek bir NuGet sunucusundan API anahtarları elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="bb90a-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="bb90a-112">Nuget.org için APIKeys oluşturmak ve yönetmek için bkz. [Yayımla-api-Key](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="bb90a-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="bb90a-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="bb90a-113">Options</span></span>

| <span data-ttu-id="bb90a-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bb90a-114">Option</span></span> | <span data-ttu-id="bb90a-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb90a-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bb90a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bb90a-116">ConfigFile</span></span> | <span data-ttu-id="bb90a-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bb90a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bb90a-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb90a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bb90a-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bb90a-119">ForceEnglishOutput</span></span> | <span data-ttu-id="bb90a-120">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="bb90a-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bb90a-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="bb90a-121">Help</span></span> | <span data-ttu-id="bb90a-122">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bb90a-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="bb90a-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bb90a-123">NonInteractive</span></span> | <span data-ttu-id="bb90a-124">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="bb90a-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bb90a-125">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="bb90a-125">Verbosity</span></span> | <span data-ttu-id="bb90a-126">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="bb90a-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bb90a-127">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bb90a-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bb90a-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bb90a-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
