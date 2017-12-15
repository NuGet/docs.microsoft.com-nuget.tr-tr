---
title: "NuGet CLI yansıtma komutu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe yansıtma komut başvurusu"
keywords: "nuget yansıtma başvuru, yansıtma komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="5410f-104">Yansıtma komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5410f-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="5410f-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="5410f-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="5410f-106">Bir paketi ve bağımlılıklarını belirtilen kaynak depoları öğesinden hedef depo yansıtır.</span><span class="sxs-lookup"><span data-stu-id="5410f-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="5410f-107">3.2 önce NuGet sürümleri için bu komutu etkinleştirmek için şu adrese gidin [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), en yeni kararlı sürüm seçin, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diske ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="5410f-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="5410f-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="5410f-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="5410f-109">Burada `<packageID>` yansıtmak üzere paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.</span><span class="sxs-lookup"><span data-stu-id="5410f-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="5410f-110">`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depo belirtir.</span><span class="sxs-lookup"><span data-stu-id="5410f-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="5410f-111">Hedef depo açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/NuGet-Server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="5410f-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="5410f-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="5410f-112">Options</span></span>

| <span data-ttu-id="5410f-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5410f-113">Option</span></span> | <span data-ttu-id="5410f-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5410f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5410f-115">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="5410f-115">ApiKey</span></span> | <span data-ttu-id="5410f-116">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5410f-116">The API key for the target repository.</span></span> <span data-ttu-id="5410f-117">Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5410f-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5410f-118">Yardım</span><span class="sxs-lookup"><span data-stu-id="5410f-118">Help</span></span> | <span data-ttu-id="5410f-119">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5410f-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="5410f-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="5410f-120">NoCache</span></span> | <span data-ttu-id="5410f-121">NuGet paketleri yerel makine önbellekleri kullanmalarını engeller.</span><span class="sxs-lookup"><span data-stu-id="5410f-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="5410f-122">Sekmeyi</span><span class="sxs-lookup"><span data-stu-id="5410f-122">Noop</span></span> | <span data-ttu-id="5410f-123">Ne uygulanır ancak işlemleri gerçekleştirmez kaydeder; İtme işlemleri için başarı varsayar.</span><span class="sxs-lookup"><span data-stu-id="5410f-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="5410f-124">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="5410f-124">PreRelease</span></span> | <span data-ttu-id="5410f-125">Ön sürüm paketlerini yansıtma işlemi içerir.</span><span class="sxs-lookup"><span data-stu-id="5410f-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="5410f-126">Kaynak</span><span class="sxs-lookup"><span data-stu-id="5410f-126">Source</span></span> | <span data-ttu-id="5410f-127">Yansıtmak üzere paket kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="5410f-127">A list of package sources to mirror.</span></span> <span data-ttu-id="5410f-128">Dosyalardan herhangi bir kaynağa belirtilirse, tanımlanan *%AppData%\NuGet\NuGet.Config* , Hiçbiri belirtilmezse, nuget.org için varsayılan değer olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5410f-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="5410f-129">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="5410f-129">Timeout</span></span> | <span data-ttu-id="5410f-130">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5410f-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="5410f-131">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="5410f-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="5410f-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="5410f-132">Version</span></span> | <span data-ttu-id="5410f-133">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="5410f-133">The version of the package to install.</span></span> <span data-ttu-id="5410f-134">Belirtilmezse, en son sürümünü yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="5410f-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="5410f-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5410f-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5410f-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="5410f-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
