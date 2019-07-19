---
title: NuGet CLı Delete komutu
description: NuGet. exe delete komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328356"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="8d288-103">Delete komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="8d288-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="8d288-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="8d288-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d288-105">Paket kaynağından bir paketi siler veya listesini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8d288-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="8d288-106">Nuget.org için, Delete komutu [paketin listesini kaldırır](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8d288-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8d288-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8d288-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="8d288-108">silmek `<packageID>` veya `<packageVersion>` listeden kaldırmak için tam paketi burada ve belirler.</span><span class="sxs-lookup"><span data-stu-id="8d288-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="8d288-109">Tam davranış kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8d288-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="8d288-110">Örneğin, yerel klasörler için, paket silinir; nuget.org için paket listelenmemiş değildir.</span><span class="sxs-lookup"><span data-stu-id="8d288-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="8d288-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="8d288-111">Options</span></span>

| <span data-ttu-id="8d288-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="8d288-112">Option</span></span> | <span data-ttu-id="8d288-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8d288-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d288-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8d288-114">ApiKey</span></span> | <span data-ttu-id="8d288-115">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8d288-115">The API key for the target repository.</span></span> <span data-ttu-id="8d288-116">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d288-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="8d288-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8d288-117">ConfigFile</span></span> | <span data-ttu-id="8d288-118">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="8d288-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8d288-119">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d288-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8d288-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d288-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8d288-121">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="8d288-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d288-122">Help</span><span class="sxs-lookup"><span data-stu-id="8d288-122">Help</span></span> | <span data-ttu-id="8d288-123">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8d288-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d288-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8d288-124">NonInteractive</span></span> | <span data-ttu-id="8d288-125">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="8d288-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8d288-126">Source</span><span class="sxs-lookup"><span data-stu-id="8d288-126">Source</span></span> | <span data-ttu-id="8d288-127">Sunucu URL 'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d288-127">Specifies the server URL.</span></span> <span data-ttu-id="8d288-128">Nuget.org URL 'SI `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8d288-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8d288-129">Özel akışlar için ana bilgisayar adını (örneğin, *% hostname%/api/v3*) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8d288-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="8d288-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8d288-130">Verbosity</span></span> | <span data-ttu-id="8d288-131">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="8d288-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8d288-132">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d288-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d288-133">Örnekler</span><span class="sxs-lookup"><span data-stu-id="8d288-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
