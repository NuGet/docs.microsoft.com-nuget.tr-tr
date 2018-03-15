---
title: NuGet CLI Sil komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Reference for the nuget.exe delete command
keywords: nuget delete reference, delete package command
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="d6f45-104">delete komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d6f45-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="d6f45-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="d6f45-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d6f45-106">Bir paketi paket kaynağında unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="d6f45-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="d6f45-107">Nuget.org, delete komutu için [paket unlists](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d6f45-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d6f45-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d6f45-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="d6f45-109">Burada `<packageID>` ve `<packageVersion>` unlist veya silmek için tam paketi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d6f45-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="d6f45-110">Tam davranışı kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d6f45-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="d6f45-111">Yerel klasör için örneğin, paket silindi; nuget.org için listelenmeyen paketidir.</span><span class="sxs-lookup"><span data-stu-id="d6f45-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="d6f45-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d6f45-112">Options</span></span>

| <span data-ttu-id="d6f45-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="d6f45-113">Option</span></span> | <span data-ttu-id="d6f45-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d6f45-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6f45-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d6f45-115">ApiKey</span></span> | <span data-ttu-id="d6f45-116">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d6f45-116">The API key for the target repository.</span></span> <span data-ttu-id="d6f45-117">Yoksa, yapılandırma dosyasında belirtilen bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6f45-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="d6f45-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d6f45-118">ConfigFile</span></span> | <span data-ttu-id="d6f45-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d6f45-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d6f45-120">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6f45-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d6f45-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d6f45-121">ForceEnglishOutput</span></span> | <span data-ttu-id="d6f45-122">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="d6f45-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d6f45-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="d6f45-123">Help</span></span> | <span data-ttu-id="d6f45-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d6f45-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="d6f45-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="d6f45-125">NonInteractive</span></span> | <span data-ttu-id="d6f45-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="d6f45-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d6f45-127">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d6f45-127">Source</span></span> | <span data-ttu-id="d6f45-128">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d6f45-128">Specifies the server URL.</span></span> <span data-ttu-id="d6f45-129">Nuget.org URL'si `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d6f45-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d6f45-130">Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="d6f45-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="d6f45-131">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="d6f45-131">Verbosity</span></span> | <span data-ttu-id="d6f45-132">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="d6f45-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d6f45-133">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d6f45-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d6f45-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d6f45-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
