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
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="a0774-104">delete komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0774-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="a0774-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="a0774-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a0774-106">Bir paketi paket kaynağında unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="a0774-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="a0774-107">Nuget.org, delete komutu için [paket unlists](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="a0774-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a0774-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a0774-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="a0774-109">Burada `<packageID>` ve `<packageVersion>` unlist veya silmek için tam paketi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="a0774-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="a0774-110">Tam davranışı kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a0774-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="a0774-111">Yerel klasör için örneğin, paket silindi; nuget.org için listelenmeyen paketidir.</span><span class="sxs-lookup"><span data-stu-id="a0774-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="a0774-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a0774-112">Options</span></span>

| <span data-ttu-id="a0774-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="a0774-113">Option</span></span> | <span data-ttu-id="a0774-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a0774-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0774-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="a0774-115">ApiKey</span></span> | <span data-ttu-id="a0774-116">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="a0774-116">The API key for the target repository.</span></span> <span data-ttu-id="a0774-117">Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0774-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a0774-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0774-118">ConfigFile</span></span> | <span data-ttu-id="a0774-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a0774-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a0774-120">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0774-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a0774-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0774-121">ForceEnglishOutput</span></span> | <span data-ttu-id="a0774-122">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="a0774-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0774-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="a0774-123">Help</span></span> | <span data-ttu-id="a0774-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a0774-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="a0774-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="a0774-125">NonInteractive</span></span> | <span data-ttu-id="a0774-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="a0774-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0774-127">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a0774-127">Source</span></span> | <span data-ttu-id="a0774-128">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a0774-128">Specifies the server URL.</span></span> <span data-ttu-id="a0774-129">Nuget.org URL'si `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a0774-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="a0774-130">Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="a0774-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="a0774-131">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="a0774-131">Verbosity</span></span> | <span data-ttu-id="a0774-132">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="a0774-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a0774-133">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a0774-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a0774-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a0774-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
