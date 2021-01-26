---
title: NuGet CLı Delete komutu
description: nuget.exe Delete komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775947"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="d5f7c-103">Delete komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="d5f7c-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="d5f7c-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="d5f7c-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d5f7c-105">Paket kaynağından bir paketi siler veya listesini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="d5f7c-106">Nuget.org için, Delete komutu [paketin listesini kaldırır](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d5f7c-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d5f7c-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d5f7c-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="d5f7c-108">`<packageID>` `<packageVersion>` silmek veya listeden kaldırmak için tam paketi burada ve belirler.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="d5f7c-109">Tam davranış kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="d5f7c-110">Örneğin, yerel klasörler için, paket silinir; nuget.org için paket listelenmemiş değildir.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="d5f7c-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d5f7c-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="d5f7c-112">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-112">The API key for the target repository.</span></span> <span data-ttu-id="d5f7c-113">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d5f7c-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d5f7c-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d5f7c-116">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d5f7c-117">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d5f7c-118">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="d5f7c-119">Silme sırasında sorma.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="d5f7c-120">**`-NoServiceEndpoint`** Kaynak URL 'ye "API/v2/paket" eklemez.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="d5f7c-121">Sunucu URL 'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-121">Specifies the server URL.</span></span> <span data-ttu-id="d5f7c-122">Nuget.org URL 'SI `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="d5f7c-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d5f7c-123">Özel akışlar için ana bilgisayar adını (örneğin, *% hostname%/api/v3*) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d5f7c-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d5f7c-124">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d5f7c-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d5f7c-125">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d5f7c-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d5f7c-126">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d5f7c-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
