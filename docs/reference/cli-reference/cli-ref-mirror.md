---
title: NuGet CLı yansıtma komutu
description: nuget.exe yansıtma komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779168"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="b5874-103">Mirror komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="b5874-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="b5874-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** 3.2 + ' da kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="b5874-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="b5874-105">Bir paketi ve onun bağımlılıklarını, belirtilen kaynak depolarından hedef depoya yansıtır.</span><span class="sxs-lookup"><span data-stu-id="b5874-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b5874-106">Bu komutu daha önce NuGet 2. x içinde (NuGet-Signed.exe nuget.exe olarak yeniden adlandırarak) NuGet.ServerExtensions.dll ve NuGet-Signed.exe artık indirimıyordu.</span><span class="sxs-lookup"><span data-stu-id="b5874-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="b5874-107">Şuna benzer bir komut kullanmak için [Nugetmirror](https://www.nuget.org/packages/NuGetMirror/)komutunu deneyin.</span><span class="sxs-lookup"><span data-stu-id="b5874-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="b5874-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="b5874-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="b5874-109">, `<packageID>` yansıtmanın paketsidir veya `<configFilePath>` `packages.config` yansıtmak üzere paketleri listeleyen dosyayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b5874-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="b5874-110">, `<listUrlTarget>` Kaynak depoyu belirtir ve `<publishUrlTarget>` Hedef depoyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b5874-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="b5874-111">Hedef deponuz `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)çalıştırıyorsa, liste ve gönderme URL 'leri `https://machine/repo/nuget` sırasıyla ve olur `https://machine/repo/api/v2/package` .</span><span class="sxs-lookup"><span data-stu-id="b5874-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="b5874-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="b5874-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="b5874-113">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b5874-113">The API key for the target repository.</span></span> <span data-ttu-id="b5874-114">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır ( `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="b5874-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="b5874-115">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b5874-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="b5874-116">NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="b5874-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b5874-117">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b5874-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="b5874-118">Ne yapılacağını günlüğe kaydeder ancak eylemleri gerçekleştirmez; gönderme işlemleri için başarıyı varsayar.</span><span class="sxs-lookup"><span data-stu-id="b5874-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="b5874-119">Yansıtma işlemindeki ön sürüm paketlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b5874-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="b5874-120">Yansıtmanın bir paket kaynakları listesi.</span><span class="sxs-lookup"><span data-stu-id="b5874-120">A list of package sources to mirror.</span></span> <span data-ttu-id="b5874-121">Hiçbir kaynak belirtilmemişse, yapılandırma dosyasında (yukarıdaki ApiKey 'e bakın) tanımlanmış olanlar kullanılır, yoksa nuget.org varsayılan olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="b5874-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="b5874-122">Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b5874-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="b5874-123">Varsayılan değer 300 saniyedir (5 dakika).</span><span class="sxs-lookup"><span data-stu-id="b5874-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="b5874-124">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="b5874-124">The version of the package to install.</span></span> <span data-ttu-id="b5874-125">Belirtilmemişse, en son sürüm yansıtıldır.</span><span class="sxs-lookup"><span data-stu-id="b5874-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="b5874-126">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b5874-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b5874-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b5874-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
