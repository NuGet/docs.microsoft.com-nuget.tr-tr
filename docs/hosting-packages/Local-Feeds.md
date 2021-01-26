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
# <a name="local-feeds"></a>Yerel akışlar

Yerel NuGet paket akışları, paketleri yerleştirdiğiniz yerel ağınızdaki (hatta yalnızca kendi bilgisayarınız) hiyerarşik klasör yapılarıdır. Bu akışlar daha sonra CLı, Paket Yöneticisi Kullanıcı arabirimi ve Paket Yöneticisi konsolu kullanılarak diğer tüm NuGet işlemlerinde paket kaynakları olarak kullanılabilir.

Kaynağı etkinleştirmek için, dizin adını (gibi `\\myserver\packages` ) [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md#package-sources) veya komutunu kullanarak kaynak listesine ekleyin [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) .

> [!Note]
> Hiyerarşik klasör yapıları NuGet 3.3 + ' de desteklenir. Daha eski NuGet sürümleri, performansı hiyerarşik yapıdan çok daha düşük olan paketleri içeren tek bir klasör kullanır.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Hiyerarşik klasörleri başlatma ve sürdürme

Hiyerarşik sürümlü klasör ağacı aşağıdaki genel yapıya sahiptir:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      └─<other files>
```

[`nuget add`](../reference/cli-reference/cli-ref-add.md)Bir paketi akışa kopyalamak için komutunu kullandığınızda NuGet bu yapıyı otomatik olarak oluşturur:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add`Komut aynı anda bir paket ile çalışır ve birden çok pakete sahip bir akış ayarlarken bu kullanışlı olabilir.

Bu gibi durumlarda, [`nuget init`](../reference/cli-reference/cli-ref-init.md) bir klasördeki tüm paketleri tek tek çalıştırdığınız gibi akışa kopyalamak için komutunu kullanın `nuget add` . Örneğin, aşağıdaki komut, tüm paketleri içinden `c:\packages` hiyerarşik bir ağaca kopyalar `\\myserver\packages` :

```cli
nuget init c:\packages \\myserver\packages
```

Komutunda olduğu gibi `add` , her `init` biri bir sürüm numarası klasörü içeren her bir paket tanımlayıcısı için bir klasör oluşturur, bu da uygun bir pakettir.
