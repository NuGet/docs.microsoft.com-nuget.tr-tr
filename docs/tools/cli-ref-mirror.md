---
title: NuGet CLI yansıtma komutu
description: Nuget.exe yansıtma komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818158"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="e5740-103">Yansıtma komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e5740-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="e5740-104">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="e5740-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="e5740-105">Bir paketi ve bağımlılıklarını belirtilen kaynak depoları öğesinden hedef depo yansıtır.</span><span class="sxs-lookup"><span data-stu-id="e5740-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="e5740-106">3.2 önce NuGet sürümleri için bu komutu etkinleştirmek için şu adrese gidin [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), en yeni kararlı sürüm seçin, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diske ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="e5740-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="e5740-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="e5740-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="e5740-108">Burada `<packageID>` yansıtmak üzere paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.</span><span class="sxs-lookup"><span data-stu-id="e5740-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="e5740-109">`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depo belirtir.</span><span class="sxs-lookup"><span data-stu-id="e5740-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="e5740-110">Hedef depo açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/nuget-server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="e5740-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="e5740-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="e5740-111">Options</span></span>

| <span data-ttu-id="e5740-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="e5740-112">Option</span></span> | <span data-ttu-id="e5740-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e5740-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e5740-114">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="e5740-114">ApiKey</span></span> | <span data-ttu-id="e5740-115">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e5740-115">The API key for the target repository.</span></span> <span data-ttu-id="e5740-116">Yoksa, yapılandırma dosyasında belirtilen bir kullanılıp kullanılmadığını (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="e5740-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="e5740-117">Yardım</span><span class="sxs-lookup"><span data-stu-id="e5740-117">Help</span></span> | <span data-ttu-id="e5740-118">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e5740-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="e5740-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="e5740-119">NoCache</span></span> | <span data-ttu-id="e5740-120">NuGet kullanarak önbelleğe alınmış paketleri engeller.</span><span class="sxs-lookup"><span data-stu-id="e5740-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="e5740-121">Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="e5740-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="e5740-122">Sekmeyi</span><span class="sxs-lookup"><span data-stu-id="e5740-122">Noop</span></span> | <span data-ttu-id="e5740-123">Ne uygulanır ancak işlemleri gerçekleştirmez kaydeder; İtme işlemleri için başarı varsayar.</span><span class="sxs-lookup"><span data-stu-id="e5740-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="e5740-124">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="e5740-124">PreRelease</span></span> | <span data-ttu-id="e5740-125">Ön sürüm paketlerini yansıtma işlemi içerir.</span><span class="sxs-lookup"><span data-stu-id="e5740-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="e5740-126">Kaynak</span><span class="sxs-lookup"><span data-stu-id="e5740-126">Source</span></span> | <span data-ttu-id="e5740-127">Yansıtmak üzere paket kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="e5740-127">A list of package sources to mirror.</span></span> <span data-ttu-id="e5740-128">Dosyalardan herhangi bir kaynağa belirtilirse, tanımlanan yapılandırma dosyası (apikey ile yapılan yukarıdaki bakın) kullanılır, nuget.org için Hiçbiri belirtilmezse, varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="e5740-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="e5740-129">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="e5740-129">Timeout</span></span> | <span data-ttu-id="e5740-130">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e5740-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="e5740-131">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="e5740-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="e5740-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="e5740-132">Version</span></span> | <span data-ttu-id="e5740-133">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="e5740-133">The version of the package to install.</span></span> <span data-ttu-id="e5740-134">Belirtilmezse, en son sürümünü yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="e5740-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="e5740-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e5740-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e5740-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e5740-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
