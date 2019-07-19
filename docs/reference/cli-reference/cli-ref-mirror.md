---
title: NuGet CLı yansıtma komutu
description: NuGet. exe yansıtma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328305"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="05a69-103">Mirror komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="05a69-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="05a69-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** 3.2 + ' da kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="05a69-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="05a69-105">Bir paketi ve onun bağımlılıklarını, belirtilen kaynak depolarından hedef depoya yansıtır.</span><span class="sxs-lookup"><span data-stu-id="05a69-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="05a69-106">Bu komutu 3,2 ' dan önce NuGet sürümleri için etkinleştirmek üzere bölümüne [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)gidin, en yeni kararlı yayını seçin, `NuGet.ServerExtensions.dll` yerel `Nuget-Signed.exe` diskinize indirin ve olarak `nuget.exe` yeniden adlandırın `Nuget-Signed.exe` .</span><span class="sxs-lookup"><span data-stu-id="05a69-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="05a69-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="05a69-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="05a69-108">, yansıtmanın paketsidir veya `<configFilePath>` yansıtmak üzere paketleri listeleyen `packages.config` dosyayı tanımlar. `<packageID>`</span><span class="sxs-lookup"><span data-stu-id="05a69-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="05a69-109">, `<listUrlTarget>` Kaynak depoyu belirtir ve `<publishUrlTarget>` hedef depoyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="05a69-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="05a69-110">Hedef deponuz `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)çalıştırıyorsa, liste ve `https://machine/repo/nuget` gönderme URL 'leri sırasıyla ve `https://machine/repo/api/v2/package`olur.</span><span class="sxs-lookup"><span data-stu-id="05a69-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="05a69-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="05a69-111">Options</span></span>

| <span data-ttu-id="05a69-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="05a69-112">Option</span></span> | <span data-ttu-id="05a69-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="05a69-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05a69-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="05a69-114">ApiKey</span></span> | <span data-ttu-id="05a69-115">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="05a69-115">The API key for the target repository.</span></span> <span data-ttu-id="05a69-116">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="05a69-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="05a69-117">Help</span><span class="sxs-lookup"><span data-stu-id="05a69-117">Help</span></span> | <span data-ttu-id="05a69-118">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="05a69-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="05a69-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="05a69-119">NoCache</span></span> | <span data-ttu-id="05a69-120">NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="05a69-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="05a69-121">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="05a69-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="05a69-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="05a69-122">Noop</span></span> | <span data-ttu-id="05a69-123">Ne yapılacağını günlüğe kaydeder ancak eylemleri gerçekleştirmez; gönderme işlemleri için başarıyı varsayar.</span><span class="sxs-lookup"><span data-stu-id="05a69-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="05a69-124">Sp1'in</span><span class="sxs-lookup"><span data-stu-id="05a69-124">PreRelease</span></span> | <span data-ttu-id="05a69-125">Yansıtma işlemindeki ön sürüm paketlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="05a69-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="05a69-126">Source</span><span class="sxs-lookup"><span data-stu-id="05a69-126">Source</span></span> | <span data-ttu-id="05a69-127">Yansıtmanın bir paket kaynakları listesi.</span><span class="sxs-lookup"><span data-stu-id="05a69-127">A list of package sources to mirror.</span></span> <span data-ttu-id="05a69-128">Hiçbir kaynak belirtilmemişse, yapılandırma dosyasında (yukarıdaki ApiKey 'e bakın) tanımlanmış olanlar kullanılır, yoksa nuget.org varsayılan olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="05a69-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="05a69-129">zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="05a69-129">Timeout</span></span> | <span data-ttu-id="05a69-130">Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="05a69-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="05a69-131">Varsayılan değer 300 saniyedir (5 dakika).</span><span class="sxs-lookup"><span data-stu-id="05a69-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="05a69-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="05a69-132">Version</span></span> | <span data-ttu-id="05a69-133">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="05a69-133">The version of the package to install.</span></span> <span data-ttu-id="05a69-134">Belirtilmemişse, en son sürüm yansıtıldır.</span><span class="sxs-lookup"><span data-stu-id="05a69-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="05a69-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="05a69-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="05a69-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="05a69-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
