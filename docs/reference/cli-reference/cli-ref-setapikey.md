---
title: NuGet CLı setapikey komutu
description: nuget.exe setapikey komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622817"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="22e5b-103">setapikey komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="22e5b-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="22e5b-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="22e5b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="22e5b-105">Belirli bir sunucu URL 'SI için bir API anahtarını `NuGet.Config` , sonraki komutlara girilmesi gerekmemesi için öğesine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="22e5b-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="22e5b-106">Kullanım</span><span class="sxs-lookup"><span data-stu-id="22e5b-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="22e5b-107">Burada `<source>` sunucuyu tanımlar ve `<key>` kaydedilecek anahtardır.</span><span class="sxs-lookup"><span data-stu-id="22e5b-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="22e5b-108">`<source>`Atlanırsa, NuGet.org varsayılır.</span><span class="sxs-lookup"><span data-stu-id="22e5b-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="22e5b-109">API anahtarı özel akışta kimlik doğrulaması için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="22e5b-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="22e5b-110">Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [ `nuget sources` komutuna](../cli-reference/cli-ref-sources.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="22e5b-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="22e5b-111">Tek bir NuGet sunucusundan API anahtarları elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="22e5b-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="22e5b-112">Nuget.org için APIKeys oluşturmak ve yönetmek için- [api-Key alma](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) bölümüne bakın</span><span class="sxs-lookup"><span data-stu-id="22e5b-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="22e5b-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="22e5b-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="22e5b-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="22e5b-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="22e5b-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="22e5b-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="22e5b-116">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="22e5b-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="22e5b-117">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="22e5b-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="22e5b-118">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="22e5b-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="22e5b-119">API anahtarının geçerli olduğu sunucu URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="22e5b-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="22e5b-120">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="22e5b-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="22e5b-121">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="22e5b-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="22e5b-122">Örnekler</span><span class="sxs-lookup"><span data-stu-id="22e5b-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
