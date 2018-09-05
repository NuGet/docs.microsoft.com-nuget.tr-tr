---
title: NuGet CLI yansıtma komutu
description: Nuget.exe yansıtma komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550212"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="cdf6f-103">Yansıtma komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cdf6f-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="cdf6f-104">**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="cdf6f-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="cdf6f-105">Bir paketi ve bağımlılıkları belirtilen kaynak depolardan hedef depoda yansıtır.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf6f-106">Bu komut için NuGet sürümü 3.2 önce etkinleştirmek için Git [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), en yeni kararlı bir sürüm seçmek, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diskinize ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="cdf6f-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cdf6f-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="cdf6f-108">Burada `<packageID>` yansıtmak için paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="cdf6f-109">`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depoyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="cdf6f-110">Hedef depoyu açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/nuget-server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="cdf6f-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="cdf6f-111">Options</span></span>

| <span data-ttu-id="cdf6f-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="cdf6f-112">Option</span></span> | <span data-ttu-id="cdf6f-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cdf6f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cdf6f-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="cdf6f-114">ApiKey</span></span> | <span data-ttu-id="cdf6f-115">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-115">The API key for the target repository.</span></span> <span data-ttu-id="cdf6f-116">Mevcut yapılandırma dosyasında belirtilen kullanılıp kullanılmadığını (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="cdf6f-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="cdf6f-117">Yardım</span><span class="sxs-lookup"><span data-stu-id="cdf6f-117">Help</span></span> | <span data-ttu-id="cdf6f-118">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="cdf6f-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="cdf6f-119">NoCache</span></span> | <span data-ttu-id="cdf6f-120">NuGet, önbelleğe eklenen paketler kullanmasını önler.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="cdf6f-121">Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cdf6f-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="cdf6f-122">Noop</span><span class="sxs-lookup"><span data-stu-id="cdf6f-122">Noop</span></span> | <span data-ttu-id="cdf6f-123">Ne olduğu, ancak işlemleri gerçekleştirmez günlüğe kaydeder; Gönderme işlemleri için başarı varsayar.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="cdf6f-124">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="cdf6f-124">PreRelease</span></span> | <span data-ttu-id="cdf6f-125">Yayın öncesi paketleri yansıtma işlemi içerir.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="cdf6f-126">Kaynak</span><span class="sxs-lookup"><span data-stu-id="cdf6f-126">Source</span></span> | <span data-ttu-id="cdf6f-127">Yansıtmak için paket kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-127">A list of package sources to mirror.</span></span> <span data-ttu-id="cdf6f-128">Olanlara kaynak belirtilirse, tanımlanan yapılandırma dosyası (bkz. Yukarıdaki ApiKey) kullanılır, nuget.org için hiçbir şey belirtilmezse varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="cdf6f-129">zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cdf6f-129">Timeout</span></span> | <span data-ttu-id="cdf6f-130">Bir sunucuya göndermek için saniye cinsinden zaman aşımı belirtir.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cdf6f-131">300 saniyedir (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="cdf6f-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="cdf6f-132">Version</span></span> | <span data-ttu-id="cdf6f-133">Yüklemek için Paket sürümü.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-133">The version of the package to install.</span></span> <span data-ttu-id="cdf6f-134">Belirtilmezse, en son sürüme yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="cdf6f-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="cdf6f-135">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cdf6f-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cdf6f-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="cdf6f-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
