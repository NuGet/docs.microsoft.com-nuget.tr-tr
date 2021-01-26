---
title: Yerel NuGet akışlarını ayarlama
description: Yerel ağınızdaki klasörleri kullanarak NuGet paketleri için yerel akış oluşturma
author: JonDouglas
ms.author: jodou
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 1eb194c9ddaee05281749c7a0420cbaf77044fe3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774039"
---
# <a name="local-feeds"></a><span data-ttu-id="2724f-103">Yerel akışlar</span><span class="sxs-lookup"><span data-stu-id="2724f-103">Local feeds</span></span>

<span data-ttu-id="2724f-104">Yerel NuGet paket akışları, paketleri yerleştirdiğiniz yerel ağınızdaki (hatta yalnızca kendi bilgisayarınız) hiyerarşik klasör yapılarıdır.</span><span class="sxs-lookup"><span data-stu-id="2724f-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="2724f-105">Bu akışlar daha sonra CLı, Paket Yöneticisi Kullanıcı arabirimi ve Paket Yöneticisi konsolu kullanılarak diğer tüm NuGet işlemlerinde paket kaynakları olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2724f-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="2724f-106">Kaynağı etkinleştirmek için, dizin adını (gibi `\\myserver\packages` ) [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md#package-sources) veya komutunu kullanarak kaynak listesine ekleyin [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="2724f-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="2724f-107">Hiyerarşik klasör yapıları NuGet 3.3 + ' de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2724f-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="2724f-108">Daha eski NuGet sürümleri, performansı hiyerarşik yapıdan çok daha düşük olan paketleri içeren tek bir klasör kullanır.</span><span class="sxs-lookup"><span data-stu-id="2724f-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="2724f-109">Hiyerarşik klasörleri başlatma ve sürdürme</span><span class="sxs-lookup"><span data-stu-id="2724f-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="2724f-110">Hiyerarşik sürümlü klasör ağacı aşağıdaki genel yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2724f-110">The hierarchical versioned folder tree has the following general structure:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      └─<other files>
```

<span data-ttu-id="2724f-111">[`nuget add`](../reference/cli-reference/cli-ref-add.md)Bir paketi akışa kopyalamak için komutunu kullandığınızda NuGet bu yapıyı otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2724f-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="2724f-112">`nuget add`Komut aynı anda bir paket ile çalışır ve birden çok pakete sahip bir akış ayarlarken bu kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2724f-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="2724f-113">Bu gibi durumlarda, [`nuget init`](../reference/cli-reference/cli-ref-init.md) bir klasördeki tüm paketleri tek tek çalıştırdığınız gibi akışa kopyalamak için komutunu kullanın `nuget add` .</span><span class="sxs-lookup"><span data-stu-id="2724f-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="2724f-114">Örneğin, aşağıdaki komut, tüm paketleri içinden `c:\packages` hiyerarşik bir ağaca kopyalar `\\myserver\packages` :</span><span class="sxs-lookup"><span data-stu-id="2724f-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="2724f-115">Komutunda olduğu gibi `add` , her `init` biri bir sürüm numarası klasörü içeren her bir paket tanımlayıcısı için bir klasör oluşturur, bu da uygun bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="2724f-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
