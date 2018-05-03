---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="4c7f0-103">delete komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4c7f0-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="4c7f0-104">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="4c7f0-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4c7f0-105">Bir paketi paket kaynağında unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="4c7f0-106">Nuget.org, delete komutu için [paket unlists](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4c7f0-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="4c7f0-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="4c7f0-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="4c7f0-108">Burada `<packageID>` ve `<packageVersion>` unlist veya silmek için tam paketi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="4c7f0-109">Tam davranışı kaynağa bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="4c7f0-110">Yerel klasör için örneğin, paket silindi; nuget.org için listelenmeyen paketidir.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="4c7f0-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="4c7f0-111">Options</span></span>

| <span data-ttu-id="4c7f0-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="4c7f0-112">Option</span></span> | <span data-ttu-id="4c7f0-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4c7f0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c7f0-114">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="4c7f0-114">ApiKey</span></span> | <span data-ttu-id="4c7f0-115">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-115">The API key for the target repository.</span></span> <span data-ttu-id="4c7f0-116">Yoksa, yapılandırma dosyasında belirtilen bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="4c7f0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4c7f0-117">ConfigFile</span></span> | <span data-ttu-id="4c7f0-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4c7f0-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4c7f0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4c7f0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="4c7f0-121">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4c7f0-122">Yardım</span><span class="sxs-lookup"><span data-stu-id="4c7f0-122">Help</span></span> | <span data-ttu-id="4c7f0-123">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="4c7f0-124">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="4c7f0-124">NonInteractive</span></span> | <span data-ttu-id="4c7f0-125">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4c7f0-126">Kaynak</span><span class="sxs-lookup"><span data-stu-id="4c7f0-126">Source</span></span> | <span data-ttu-id="4c7f0-127">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-127">Specifies the server URL.</span></span> <span data-ttu-id="4c7f0-128">Nuget.org URL'si `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="4c7f0-129">Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="4c7f0-130">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="4c7f0-130">Verbosity</span></span> | <span data-ttu-id="4c7f0-131">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="4c7f0-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4c7f0-132">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4c7f0-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4c7f0-133">Örnekler</span><span class="sxs-lookup"><span data-stu-id="4c7f0-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
