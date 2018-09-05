---
title: Yerel NuGet akışlarını ayarlama
description: Yerel bir klasör yerel ağınızda kullanarak NuGet paketleri için akış oluşturma
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 91c072c8895ab4267c64fd04deae010ae5af4d37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545458"
---
# <a name="local-feeds"></a><span data-ttu-id="b2494-103">Yerel akışlar</span><span class="sxs-lookup"><span data-stu-id="b2494-103">Local feeds</span></span>

<span data-ttu-id="b2494-104">Yerel NuGet paketi akışlar, paketleri yerleştireceğiniz yerel ağınızda (veya hatta yalnızca kendi bilgisayar) yalnızca hiyerarşik klasör yapılardır.</span><span class="sxs-lookup"><span data-stu-id="b2494-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="b2494-105">Bu akışları sonra CLI, Paket Yöneticisi UI ve Paket Yöneticisi konsolu kullanarak tüm diğer NuGet işlemleri ile paket kaynağı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2494-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="b2494-106">Kaynak etkinleştirmek için yol ekleyin (gibi `\\myserver\packages`) kullanarak kaynakları listesine [Paket Yöneticisi UI](../tools/package-manager-ui.md#package-sources) veya [ `nuget sources` ](../tools/cli-ref-sources.md) komutu.</span><span class="sxs-lookup"><span data-stu-id="b2494-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="b2494-107">Hiyerarşik klasör yapılarını içinde NuGet 3.3 + desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b2494-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="b2494-108">Yalnızca performans hiyerarşik yapıda çok daha düşük olan paketleri içeren tek bir klasör Nuget'in önceki sürümlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2494-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="b2494-109">Başlatma ve hiyerarşik klasör koruma</span><span class="sxs-lookup"><span data-stu-id="b2494-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="b2494-110">Hiyerarşik tutulan klasörü ağacında, aşağıdaki genel yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b2494-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="b2494-111">Kullanırken NuGet bu yapı otomatik olarak oluşturur. [ `nuget add` ](../tools/cli-ref-add.md) akışa bir paket kopyalamak için komut:</span><span class="sxs-lookup"><span data-stu-id="b2494-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="b2494-112">`nuget add` Komutu ile tek bir pakette birden çok paket ile bir akış ayarlarken bilinmelidir bir zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2494-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="b2494-113">Böyle durumlarda kullanmak [ `nuget init` ](../tools/cli-ref-init.md) çalıştırdıysanız gibi tüm paketleri akışa bir klasöre kopyalamak için komut `nuget add` her birinde tek tek.</span><span class="sxs-lookup"><span data-stu-id="b2494-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="b2494-114">Örneğin, aşağıdaki komutu tüm paketleri kopyalar `c:\packages` hiyerarşik bir için `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="b2494-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="b2494-115">Olduğu gibi `add` komutu `init` olan uygun paket her biri içeren bir sürüm numarası klasörü içinde her paket tanımlayıcı için bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2494-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
