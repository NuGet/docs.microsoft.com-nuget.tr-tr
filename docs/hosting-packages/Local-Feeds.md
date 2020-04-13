---
title: Yerel NuGet Akışlarının Ayarlanması
description: Yerel abunuzdaki klasörleri kullanarak NuGet paketleri için yerel bir özet akışı oluşturma
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317585"
---
# <a name="local-feeds"></a><span data-ttu-id="4db10-103">Yerel akışlar</span><span class="sxs-lookup"><span data-stu-id="4db10-103">Local feeds</span></span>

<span data-ttu-id="4db10-104">Yerel NuGet paket akışları, paketleri yerleştirdiğiniz yerel ağınızda (hatta yalnızca kendi bilgisayarınızda) yalnızca hiyerarşik klasör yapılarıdır.</span><span class="sxs-lookup"><span data-stu-id="4db10-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="4db10-105">Bu akışlar daha sonra CLI, Package Manager UI ve Package Manager Console kullanarak diğer tüm NuGet işlemleriile paket kaynağı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4db10-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="4db10-106">Kaynağı etkinleştirmek için, yol adını `\\myserver\packages`(örneğin) Paket Yöneticisi [Kullanıcı Arabirimi'ni](../consume-packages/install-use-packages-visual-studio.md#package-sources) veya komutu kullanan kaynaklar listesine [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4db10-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="4db10-107">Hiyerarşik klasör yapıları NuGet 3.3+ ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4db10-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="4db10-108">NuGet'in eski sürümleri, performansın hiyerarşik yapıdan çok daha düşük olduğu paketleri içeren tek bir klasör kullanır.</span><span class="sxs-lookup"><span data-stu-id="4db10-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="4db10-109">Hiyerarşik klasörleri başlatma ve koruma</span><span class="sxs-lookup"><span data-stu-id="4db10-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="4db10-110">Hiyerarşik sürümlü klasör ağacı aşağıdaki genel yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4db10-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="4db10-111">NuGet, bir paketi özet akışına [`nuget add`](../reference/cli-reference/cli-ref-add.md) kopyalamak için komutu kullandığınızda bu yapıyı otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="4db10-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="4db10-112">Komut, `nuget add` birden çok paketle bir besleme ayarlarken rahatsız edici olabilecek tek bir paketle çalışır.</span><span class="sxs-lookup"><span data-stu-id="4db10-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="4db10-113">Bu gibi durumlarda, [`nuget init`](../reference/cli-reference/cli-ref-init.md) bir klasördeki tüm paketleri tek tek çalıştırdığınız `nuget add` gibi özet akışına kopyalamak için komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4db10-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="4db10-114">Örneğin, aşağıdaki komut tüm paketleri `c:\packages` hiyerarşik bir ağaca `\\myserver\packages`kopyalar:</span><span class="sxs-lookup"><span data-stu-id="4db10-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="4db10-115">Komutta `add` olduğu `init` gibi, her paket tanımlayıcısı için bir klasör oluşturur ve bunların her biri içinde uygun paket olan bir sürüm numarası klasörü içerir.</span><span class="sxs-lookup"><span data-stu-id="4db10-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
