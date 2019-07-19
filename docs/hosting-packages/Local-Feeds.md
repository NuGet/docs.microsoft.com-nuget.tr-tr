---
title: Yerel NuGet akışlarını ayarlama
description: Yerel ağınızdaki klasörleri kullanarak NuGet paketleri için yerel akış oluşturma
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317585"
---
# <a name="local-feeds"></a>Yerel akışlar

Yerel NuGet paket akışları, paketleri yerleştirdiğiniz yerel ağınızdaki (hatta yalnızca kendi bilgisayarınız) hiyerarşik klasör yapılarıdır. Bu akışlar daha sonra CLı, Paket Yöneticisi Kullanıcı arabirimi ve Paket Yöneticisi konsolu kullanılarak diğer tüm NuGet işlemlerinde paket kaynakları olarak kullanılabilir.

Kaynağı etkinleştirmek için, dizin adını (gibi `\\myserver\packages`) [Paket Yöneticisi](../consume-packages/install-use-packages-visual-studio.md#package-sources) [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) Kullanıcı arabirimini veya komutunu kullanarak kaynak listesine ekleyin.

> [!Note]
> Hiyerarşik klasör yapıları NuGet 3.3 + ' de desteklenir. Daha eski NuGet sürümleri, performansı hiyerarşik yapıdan çok daha düşük olan paketleri içeren tek bir klasör kullanır.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Hiyerarşik klasörleri başlatma ve sürdürme

Hiyerarşik sürümlü klasör ağacı aşağıdaki genel yapıya sahiptir:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Bir paketi akışa kopyalamak için [`nuget add`](../reference/cli-reference/cli-ref-add.md) komutunu kullandığınızda NuGet bu yapıyı otomatik olarak oluşturur:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Komut aynı anda bir paket ile çalışır ve birden çok pakete sahip bir akış ayarlarken bu kullanışlı olabilir.

Bu gibi durumlarda, bir klasördeki [`nuget init`](../reference/cli-reference/cli-ref-init.md) tüm paketleri tek tek çalıştırdığınız `nuget add` gibi akışa kopyalamak için komutunu kullanın. Örneğin, aşağıdaki komut, tüm paketleri içinden `c:\packages` hiyerarşik bir `\\myserver\packages`ağaca kopyalar:

```cli
nuget init c:\packages \\myserver\packages
```

Komutunda olduğu gibi, `init` her biri bir sürüm numarası klasörü içeren her bir paket tanımlayıcısı için bir klasör oluşturur, bu da uygun bir pakettir. `add`
