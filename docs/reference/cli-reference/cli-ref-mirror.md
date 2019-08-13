---
title: NuGet CLı yansıtma komutu
description: NuGet. exe yansıtma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959719"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="88a3d-103">Mirror komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="88a3d-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="88a3d-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** 3.2 + ' da kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="88a3d-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="88a3d-105">Bir paketi ve onun bağımlılıklarını, belirtilen kaynak depolarından hedef depoya yansıtır.</span><span class="sxs-lookup"><span data-stu-id="88a3d-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="88a3d-106">NuGet 2. x (NuGet-Signed. exe ' yi NuGet. exe ' ye yeniden adlandırarak) bu komutu daha önce destekleyen NuGet. ServerExtensions. dll ve NuGet-Signed. exe artık indirimıyordu.</span><span class="sxs-lookup"><span data-stu-id="88a3d-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="88a3d-107">Şuna benzer bir komut kullanmak için [Nugetmirror](https://www.nuget.org/packages/NuGetMirror/)komutunu deneyin.</span><span class="sxs-lookup"><span data-stu-id="88a3d-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="88a3d-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="88a3d-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="88a3d-109">, yansıtmanın paketsidir veya `<configFilePath>` yansıtmak üzere paketleri listeleyen `packages.config` dosyayı tanımlar. `<packageID>`</span><span class="sxs-lookup"><span data-stu-id="88a3d-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="88a3d-110">, `<listUrlTarget>` Kaynak depoyu belirtir ve `<publishUrlTarget>` hedef depoyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="88a3d-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="88a3d-111">Hedef deponuz `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)çalıştırıyorsa, liste ve `https://machine/repo/nuget` gönderme URL 'leri sırasıyla ve `https://machine/repo/api/v2/package`olur.</span><span class="sxs-lookup"><span data-stu-id="88a3d-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="88a3d-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="88a3d-112">Options</span></span>

| <span data-ttu-id="88a3d-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="88a3d-113">Option</span></span> | <span data-ttu-id="88a3d-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88a3d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88a3d-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="88a3d-115">ApiKey</span></span> | <span data-ttu-id="88a3d-116">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="88a3d-116">The API key for the target repository.</span></span> <span data-ttu-id="88a3d-117">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="88a3d-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="88a3d-118">Help</span><span class="sxs-lookup"><span data-stu-id="88a3d-118">Help</span></span> | <span data-ttu-id="88a3d-119">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="88a3d-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="88a3d-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="88a3d-120">NoCache</span></span> | <span data-ttu-id="88a3d-121">NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="88a3d-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="88a3d-122">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="88a3d-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="88a3d-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="88a3d-123">Noop</span></span> | <span data-ttu-id="88a3d-124">Ne yapılacağını günlüğe kaydeder ancak eylemleri gerçekleştirmez; gönderme işlemleri için başarıyı varsayar.</span><span class="sxs-lookup"><span data-stu-id="88a3d-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="88a3d-125">Sp1'in</span><span class="sxs-lookup"><span data-stu-id="88a3d-125">PreRelease</span></span> | <span data-ttu-id="88a3d-126">Yansıtma işlemindeki ön sürüm paketlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="88a3d-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="88a3d-127">Source</span><span class="sxs-lookup"><span data-stu-id="88a3d-127">Source</span></span> | <span data-ttu-id="88a3d-128">Yansıtmanın bir paket kaynakları listesi.</span><span class="sxs-lookup"><span data-stu-id="88a3d-128">A list of package sources to mirror.</span></span> <span data-ttu-id="88a3d-129">Hiçbir kaynak belirtilmemişse, yapılandırma dosyasında (yukarıdaki ApiKey 'e bakın) tanımlanmış olanlar kullanılır, yoksa nuget.org varsayılan olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="88a3d-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="88a3d-130">zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="88a3d-130">Timeout</span></span> | <span data-ttu-id="88a3d-131">Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="88a3d-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="88a3d-132">Varsayılan değer 300 saniyedir (5 dakika).</span><span class="sxs-lookup"><span data-stu-id="88a3d-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="88a3d-133">Sürüm</span><span class="sxs-lookup"><span data-stu-id="88a3d-133">Version</span></span> | <span data-ttu-id="88a3d-134">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="88a3d-134">The version of the package to install.</span></span> <span data-ttu-id="88a3d-135">Belirtilmemişse, en son sürüm yansıtıldır.</span><span class="sxs-lookup"><span data-stu-id="88a3d-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="88a3d-136">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="88a3d-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="88a3d-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="88a3d-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
