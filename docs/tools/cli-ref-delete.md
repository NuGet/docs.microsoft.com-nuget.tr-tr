---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426115"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="8d541-103">Sil komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8d541-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="8d541-104">**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="8d541-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d541-105">Bir paketi paket kaynağından unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="8d541-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="8d541-106">Nuget.org, delete komutu için [paket unlists](../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8d541-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8d541-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8d541-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="8d541-108">Burada `<packageID>` ve `<packageVersion>` silme veya listeden tam paket tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8d541-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="8d541-109">Tam davranış kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8d541-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="8d541-110">Yerel klasörler için paketi örneği için silinir; nuget.org için listelenmemiş bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="8d541-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="8d541-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="8d541-111">Options</span></span>

| <span data-ttu-id="8d541-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="8d541-112">Option</span></span> | <span data-ttu-id="8d541-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8d541-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d541-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8d541-114">ApiKey</span></span> | <span data-ttu-id="8d541-115">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8d541-115">The API key for the target repository.</span></span> <span data-ttu-id="8d541-116">Yoksa, yapılandırma dosyasında belirtilen kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d541-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="8d541-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8d541-117">ConfigFile</span></span> | <span data-ttu-id="8d541-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="8d541-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8d541-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d541-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8d541-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d541-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8d541-121">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="8d541-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d541-122">Help</span><span class="sxs-lookup"><span data-stu-id="8d541-122">Help</span></span> | <span data-ttu-id="8d541-123">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8d541-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d541-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8d541-124">NonInteractive</span></span> | <span data-ttu-id="8d541-125">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="8d541-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8d541-126">Source</span><span class="sxs-lookup"><span data-stu-id="8d541-126">Source</span></span> | <span data-ttu-id="8d541-127">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d541-127">Specifies the server URL.</span></span> <span data-ttu-id="8d541-128">Nuget.org URL'si `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8d541-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8d541-129">Özel akışları için örneğin, ana bilgisayar adı yerine *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="8d541-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="8d541-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="8d541-130">Verbosity</span></span> | <span data-ttu-id="8d541-131">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="8d541-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8d541-132">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d541-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d541-133">Örnekler</span><span class="sxs-lookup"><span data-stu-id="8d541-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
