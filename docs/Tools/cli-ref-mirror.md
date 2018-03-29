---
title: NuGet CLI yansıtma komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe yansıtma komut başvurusu
keywords: nuget yansıtma başvuru, yansıtma komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="ab09e-104">Yansıtma komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab09e-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="ab09e-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="ab09e-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="ab09e-106">Bir paketi ve bağımlılıklarını belirtilen kaynak depoları öğesinden hedef depo yansıtır.</span><span class="sxs-lookup"><span data-stu-id="ab09e-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ab09e-107">3.2 önce NuGet sürümleri için bu komutu etkinleştirmek için şu adrese gidin [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), en yeni kararlı sürüm seçin, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diske ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ab09e-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="ab09e-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ab09e-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="ab09e-109">Burada `<packageID>` yansıtmak üzere paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.</span><span class="sxs-lookup"><span data-stu-id="ab09e-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="ab09e-110">`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depo belirtir.</span><span class="sxs-lookup"><span data-stu-id="ab09e-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="ab09e-111">Hedef depo açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/nuget-server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="ab09e-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="ab09e-112">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ab09e-112">Options</span></span>

| <span data-ttu-id="ab09e-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ab09e-113">Option</span></span> | <span data-ttu-id="ab09e-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab09e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab09e-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="ab09e-115">ApiKey</span></span> | <span data-ttu-id="ab09e-116">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="ab09e-116">The API key for the target repository.</span></span> <span data-ttu-id="ab09e-117">Yoksa, yapılandırma dosyasında belirtilen bir kullanılıp kullanılmadığını (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="ab09e-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="ab09e-118">Yardım</span><span class="sxs-lookup"><span data-stu-id="ab09e-118">Help</span></span> | <span data-ttu-id="ab09e-119">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ab09e-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab09e-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="ab09e-120">NoCache</span></span> | <span data-ttu-id="ab09e-121">NuGet kullanarak önbelleğe alınmış paketleri engeller.</span><span class="sxs-lookup"><span data-stu-id="ab09e-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ab09e-122">Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ab09e-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ab09e-123">Sekmeyi</span><span class="sxs-lookup"><span data-stu-id="ab09e-123">Noop</span></span> | <span data-ttu-id="ab09e-124">Ne uygulanır ancak işlemleri gerçekleştirmez kaydeder; İtme işlemleri için başarı varsayar.</span><span class="sxs-lookup"><span data-stu-id="ab09e-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="ab09e-125">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="ab09e-125">PreRelease</span></span> | <span data-ttu-id="ab09e-126">Ön sürüm paketlerini yansıtma işlemi içerir.</span><span class="sxs-lookup"><span data-stu-id="ab09e-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="ab09e-127">Kaynak</span><span class="sxs-lookup"><span data-stu-id="ab09e-127">Source</span></span> | <span data-ttu-id="ab09e-128">Yansıtmak üzere paket kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="ab09e-128">A list of package sources to mirror.</span></span> <span data-ttu-id="ab09e-129">Dosyalardan herhangi bir kaynağa belirtilirse, tanımlanan yapılandırma dosyası (apikey ile yapılan yukarıdaki bakın) kullanılır, nuget.org için Hiçbiri belirtilmezse, varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="ab09e-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="ab09e-130">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="ab09e-130">Timeout</span></span> | <span data-ttu-id="ab09e-131">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ab09e-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="ab09e-132">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="ab09e-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="ab09e-133">Sürüm</span><span class="sxs-lookup"><span data-stu-id="ab09e-133">Version</span></span> | <span data-ttu-id="ab09e-134">Yüklenecek paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="ab09e-134">The version of the package to install.</span></span> <span data-ttu-id="ab09e-135">Belirtilmezse, en son sürümünü yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="ab09e-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="ab09e-136">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab09e-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab09e-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ab09e-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
