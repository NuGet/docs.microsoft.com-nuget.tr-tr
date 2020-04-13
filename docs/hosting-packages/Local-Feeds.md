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
# <a name="local-feeds"></a>Yerel akışlar

Yerel NuGet paket akışları, paketleri yerleştirdiğiniz yerel ağınızda (hatta yalnızca kendi bilgisayarınızda) yalnızca hiyerarşik klasör yapılarıdır. Bu akışlar daha sonra CLI, Package Manager UI ve Package Manager Console kullanarak diğer tüm NuGet işlemleriile paket kaynağı olarak kullanılabilir.

Kaynağı etkinleştirmek için, yol adını `\\myserver\packages`(örneğin) Paket Yöneticisi [Kullanıcı Arabirimi'ni](../consume-packages/install-use-packages-visual-studio.md#package-sources) veya komutu kullanan kaynaklar listesine [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) ekleyin.

> [!Note]
> Hiyerarşik klasör yapıları NuGet 3.3+ ile desteklenir. NuGet'in eski sürümleri, performansın hiyerarşik yapıdan çok daha düşük olduğu paketleri içeren tek bir klasör kullanır.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Hiyerarşik klasörleri başlatma ve koruma

Hiyerarşik sürümlü klasör ağacı aşağıdaki genel yapıya sahiptir:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet, bir paketi özet akışına [`nuget add`](../reference/cli-reference/cli-ref-add.md) kopyalamak için komutu kullandığınızda bu yapıyı otomatik olarak oluşturur:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Komut, `nuget add` birden çok paketle bir besleme ayarlarken rahatsız edici olabilecek tek bir paketle çalışır.

Bu gibi durumlarda, [`nuget init`](../reference/cli-reference/cli-ref-init.md) bir klasördeki tüm paketleri tek tek çalıştırdığınız `nuget add` gibi özet akışına kopyalamak için komutu kullanın. Örneğin, aşağıdaki komut tüm paketleri `c:\packages` hiyerarşik bir ağaca `\\myserver\packages`kopyalar:

```cli
nuget init c:\packages \\myserver\packages
```

Komutta `add` olduğu `init` gibi, her paket tanımlayıcısı için bir klasör oluşturur ve bunların her biri içinde uygun paket olan bir sürüm numarası klasörü içerir.
