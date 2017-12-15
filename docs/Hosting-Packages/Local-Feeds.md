---
title: "NuGet yerel akışları ayarlama | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Yerel ağınızda klasörleri'ni kullanarak NuGet paketleri için akış yerel oluşturma"
keywords: "NuGet akış, NuGet galerisinde, yerel paket akışı"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a><span data-ttu-id="d685c-104">Yerel akışları</span><span class="sxs-lookup"><span data-stu-id="d685c-104">Local feeds</span></span>

<span data-ttu-id="d685c-105">Yerel NuGet paketi akışları yalnızca hiyerarşik klasör yapılarınızı paketleri yerleştirin, yerel ağınızda (veya hatta yalnızca kendi bilgisayarınızı) var.</span><span class="sxs-lookup"><span data-stu-id="d685c-105">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="d685c-106">Bu Özet akışlarını CLI, Paket Yöneticisi kullanıcı Arabirimi ve Paket Yöneticisi konsolu kullanılarak tüm diğer NuGet işlemleriyle sonra paket kaynağı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d685c-106">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="d685c-107">Kaynak sağlamak için kendi pathname ekleyin (gibi `\\myserver\packages`) kullanarak kaynaklarının listesi için [Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md#package-sources) veya [ `nuget sources` ](../tools/cli-ref-sources.md) komutu.</span><span class="sxs-lookup"><span data-stu-id="d685c-107">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="d685c-108">Hiyerarşik klasör yapılarınızı NuGet içinde 3.3 + desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d685c-108">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="d685c-109">NuGet eski sürümleri yalnızca performans hiyerarşik yapıda çok daha az paketleri içeren tek bir klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="d685c-109">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="d685c-110">Başlatma ve hiyerarşik klasörleri koruma</span><span class="sxs-lookup"><span data-stu-id="d685c-110">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="d685c-111">Hiyerarşik sürümlü klasör ağacında aşağıdaki genel yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d685c-111">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="d685c-112">Kullandığınızda NuGet bu yapı otomatik olarak oluşturur. [ `nuget add` ](../tools/cli-ref-add.md) bir paket akışa kopyalamak için komut:</span><span class="sxs-lookup"><span data-stu-id="d685c-112">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="d685c-113">`nuget add` Komutu, bir seferde birden çok paket ile bir akış ayarlarken bilinmelidir bir paketi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="d685c-113">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="d685c-114">Bu gibi durumlarda kullanmak [ `nuget init` ](../tools/cli-ref-init.md) çalıştırdıysanız gibi tüm paketler akışa bir klasöre kopyalamak için komut `nuget add` her birinde tek tek.</span><span class="sxs-lookup"><span data-stu-id="d685c-114">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="d685c-115">Örneğin, aşağıdaki komut tüm paketleri kopyalar `c:\packages` hiyerarşik bir için `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="d685c-115">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="d685c-116">İle `add` komutu, `init` uygun paketi olan her biri içeren bir sürüm numarası klasör içinde her paket tanımlayıcısı için bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d685c-116">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
